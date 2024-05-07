# SAM & BAM
Sequence Alignment/Map & 它的二进制格式  [SAM/BAM and related specifications](https://samtools.github.io/hts-specs/)

## Header section
+ 该部分全部以“@”开头，提供基本的软件版本，参考序列信息，排序信息等
+ @HD 行：这一行中有各种不同的标识
+ 标识“VN”用以说明格式版本
+ 标识“SO”用以说明比对排序的情况，有 unknown (default)、unsorted、queryname 和 coordi‑
nate, 对于 coordinate，排序的主键是 Alignments section 的第三列“RNAME”，其顺序由 @SQ
行的“SN”标识的顺序定义，次要排序键是 Alignments section 的第四列“POS”字段。对于
RNAME 和 POS 相等的比对，排列顺序则是任意的
+ @SQ 行的 “SN”标签是参考序列名；LN是参考序列长度，它的值主要是用于 Alignments section 的第三列
“RNAME”和第七列“MRNM”比对的记录
![image](https://github.com/sammyxue0616/database/assets/167417350/b42eda1b-8681-4d1c-992e-2d4d6de8e285)

+ @RG 行是样品基本信息Read Group，1个sample的测序结果为1个Read Group；该sample可以有多个library的测序结果，可以利用bwa mem -R 加上去这些信息 eg：@RG ID:ZX1_ID SM:ZX1 LB:PE400 PU:Illumina PL:Miseq ID：样品号 SM：样品名 LB：文库名 PU：测序以 PL：测序平台
+ @PG 行是使用的程序说明；该行“ID”为程序记录标识符，“PN”为程序名字，“CL”为命令行
+ @CO 行是任意的说明信息
![image](https://github.com/sammyxue0616/database/assets/167417350/53b21d4e-646a-4bd0-8e4f-53512763e3dd)

> [!NOTE]
> 1. mapping: bwa,GATK,bismark,...
> 2. duplication: picard,samblaster,sambamba,...
> 3. reference genome: hg19,hg38

## Alignments section
该部分包含了 11 列必需字段，无效或者没有的字段一般用“0”或者“*”表示
| Col | Field | Type | Regexp/Range | Brief description |
| --------- | --------- | --------- | --------- | --------- |
| 1 | QNAME | String | \[!‑?A‑~]\{1,254} | Query template NAME |
| 2 | FLAG | Int | \[0,2<sup>16</sup>−1] | bitwise FLAG |
| 3 | RNAME | String | \\\*\| \[:rname:<sup>∧</sup>\*=]\[:rname:]* | Reference sequence NAME<br>1‑based leftmost mapping |
| 4 | POS | Int | \[0,2<sup>31</sup>−1] | POSition |
| 5 | MAPQ | Int | \[0,2<sup>8</sup>−1] | MAPping Quality |
| 6 | CIGAR | String |  \\\*\|\(\[0‑9]+\[MIDNSHPX=])+ | CIGAR string |
| 7 | RNEXT | String | \\\*\| \[:rname:<sup>∧</sup>\*=]\[:rname:]* | Reference name of the<br>mate/next read |
| 8 | PNEXT | Int |  \[0,2<sup>31</sup>−1] | Position of the mate/next<br>read |
| 9 | TLEN | Int | \[−2<sup>31</sup>+1,2<sup>31</sup>−1] | observed Template LENgth |
| 10 | SEQ | String | \\\*\|\[A‑Za‑z=.]+ | segment SEQuence |
| 11 | QUAL | String | \[!-~]+ | ASCII of Phred-scaled base QUALity+33 |
+ QNAME: 序列的名字，也就是Read的名字
+ FLAG: 是一个标记的数字，是有需要转换成二进制才能知道代表的意思，各个数字分别代表
  | value 10 | value 16 | description | 99 | 83 | 147 | 163 |
  | --------- | --------- | --------- | --------- | --------- | --------- | --------- |
  | 1 | 0×1 | 该read是成对的paired reads中的一个 | \+ | \+ | \+ | \+ |
  | 2 | 0×2 | paired reads中每个都正确比对到参考序列上 | \+ | \+ | \+ | \+ |
  | 4 | 0×4 | 该read没比对到参考序列上 | | | | |
  | 8 | 0×8 | 与该read成对的matepair read没有比对到参考序列上 | | | | |
  | 16 | 0×10 | 该read其反向互补序列能够比对到参考序列 | | \+ | \+ | |
  | 32 | 0×20 | 与该read成对的matepair read其反向互补序列能够比对到参考序列 | \+ | | | \+ |
  | 64 | 0×40 | 在paired reads中，该read是与参考序列比对的第一条 | \+ | \+ | | |
  | 128 | 0×80 | 在paired reads中，该read是与参考序列比对的第二条 | | | \+ | \+ |
  | 256 | 0×100 | 该read是次优的比对结果 | | | | |
  | 512 | 0×200 | 该read没有通过质量控制 | | | | |
  | 1024 | 0×400 | 由于PCR或测序错误产生的重复reads | | | | |
  | 2048 | 0×800 | 补充匹配的read | | | | |
  - 每一个 read 的比对情况可以用十进制数字（或者十六进制数字）表示，如果比对情况有多
个，将多个比对情况所代表的十进制数字加和就是这一行的 FLAG
    eg: FLAG 是 99（1+2+32+64），则表示了“该 read 是 pair read 中的一
个”，“pair read 中每个都能够正确比对上”，“该 read 的 mate read 的反向互补可以比对
上”，“该 read 是 pari read 中的 read1”
   - 值得注意的是，如果 r001 是 pair read，而且都能比对上，所以 r001 会出现两次，如果 r001 的
read1 比对到参考序列的 2 个地方，r001 的名字则会出现三次；如果 read1 比对上一次，
read2 没有比对上，r001 仍会出现 2 次，不过，其中一个 r001 的第三列为“*”；所以 pair‑end
测序，read1 文件和 read2 文件同时 mapping，相同 reads 的 ID 最少出现 2 次
    - 可以通过网站输入FLAG值得出加和结果 [Decoding SAM flags](https://broadinstitute.github.io/picard/explain‑flags.html)
+ RNAME: 比对上的参考序列的名字，该名字出现在 Header section 的 @SQ 行的 SN 标识中，如果该
read 没有比对上，也就是说该 read 在参考序列上没有坐标，那么这一列则用“\*”表示，那么
这一行的 POS 和 CIGAR 列也会是“*”
+ POS: read 比对到的参考序列“RNAME”最左侧的位置坐标，也是 CIGAR 中第一个比对标识“M”对
应的最左侧碱基在参考序列的位置，未比对上的 read 在参考序列中没有坐标，此列标识为
“0”
+ MAPQ: 比对的质量值，计算方法为比对错误率的‑10*log10 的值，一般是四舍五入的整数值，如果
是 255，说明该比对值无效，unmapped read则MAPQ为0，为60表示mapping率最高
+ CIGAR: 表示 read 中每个碱基的比对情况
  - M: alignment match (can be a sequence match or mismatch) read 上的碱基与参考序列
“RNAME”完全匹配，碱基一一对应，包括了正确匹配与错误匹配
  - I: insertion to the reference read 上的碱基相对于参考序列“RNAME”有插入现象<br>REF: CACGATCA**GACCGATACGTCCGA<br>READ1: CGATCAGAGACCGATA<br>CIGAR：6M2I8M
  - D: deletion from the reference read 上的碱基相对于参考序列“RNAME”有删除现象<br>REF: AGCATCGTGTCGCCCGTCTAGCATACGC<br>READ: TCGCCCGT-TAGCAT<br>CIGAR：8M1D6M
  - N: skipped region from the reference read 上的碱基相对于参考序列“RNAME”存在连续没有比
对上的空缺，这些空缺用 N 来表示，跟“D”相似但远比“D”缺失的更多，这种比对类型也叫
“Spliced alignment”，常见 cDNA 与参考序列比对<br>REF:AGCATCGTGTCGCCCGTCTAGCATACGCATGATCGACTGTCAGCTAGTCAGACTA<br>READ: GTGTAACCC................................TCAGAATA<br>CIGAR：9M32N8M
  - S: soft clipping \(clipped sequences present in SEQ)
  - H: hard clipping \(clipped sequences NOT present in SEQ) read 的开头或者结尾部分没有比对
到参考序列”RNAME”上，但这部分未比对上的连续序列仍保留在 sam 文件的该 read 序列
中，用“S”来表示；如果未保留，则用“H”表示<br>REF: AGCTAGCATCGTGTCGCCCGTCTAGCATACGCAT<br>READ: gggTCGCCCGT-TAGCATgggg<br>CIGAR：3S8M1D6M4S （ 在sam中 存 储 为GGGGTGTAACCGACTAGGGGG）<br>CIGAR：3H8M1D6M4H （ 在sam中 存 储 为GTGTAACCGACTAG）
  - P: padding \(silent deletion from padded reference) 多条 read 比对到参考序列的同一位置时，
如果不同 read 单独同该参考序列比对时，参考序列的情况也不同，比如下方 READ1 同参考
序列比对时，“GA”属于插入（6M2I8M），READ2 同参考序列比对时，“A”属于插入（4M1I9M ），
READ3 同参考序列完全匹配（10M），没有插入，但是三条 read 之前却没有可比性。因此，
当参考序列“比对情况包含完整”且序列唯一时，所有 read 同时进行比对，read3 这种原本
没有插入却默认插入的比对称之为 Padded alignment，这种情况用“P”表示<br>REF: CACGATCA\**GACCGATACGTCCGA<br>READ1: CGATCAGAGACCGATA<br>READ2: ATCA\*AGACCGATAC<br>READ3: GATCA**GACCG<br>The padded CIGAR are different:<br>READ1: 6M2I8M<br>READ2: 4M1P1I9M<br>READ3: 5M2P5M
  - =：sequence match 正确匹配
  - X：sequence mismatch 错误匹配
+ RNEXT: 该 read 的 mate read 比对上的参考序列的名字，该名字出现在 Header section 的 @SQ 行的
SN 标识中
  - 如果和该 read 所在行的第三列“RNAME”一样，则用“=”表示，说明这对 read 比对到了同一条参考序列上
  - 如果 mate read 没有比对上，第七列则用“*”表示
  - 如果这对 read 没有比对到同一条参考序列，那么这一列则是 mate read 所在行第三列的
“RNAME”
+ PNEXT: 该 read 的 mate read 比对到的参考序列“RNAME”最左侧的位置坐标，也是 mate read CIGAR
中第一个比对标识“M”对应的最左侧碱基在参考序列的位置，未比对上的 read 在参考序列
中没有坐标，此列标识为“0”
+ ISIZE: 表示 pair read 完全匹配到同一条参考序列时，两个 read 之间的长度，可简单理解为测序文
库的长度。这个定义有两种情况（虚线表示未比对上的序列，即 soft‑clipped bases）
  - Read1 和 Read2 比对到同一条参考序列，此时 ISIZE 即为 Read2 的
最右侧比对坐标减去 Read1 最左侧比对坐标
  - 此外，由于至今没有明确的定义和共识，因此 ISIZE 可以是 TLEN#1，也
可以是 TLEN#2，视情况而定
+ SEQ: 存储的序列，没有存储，此列则用 “*”标识。该序列的长度一定等于 CIGAR 标识中
“M”，“I”，“S”，“=”，“X”标识的碱基长度之和
+ QUAL: Base quality score
  - 序列的每个碱基对应一个碱基质量字符，每个碱基质量字符对应的 ASCII 码值减去 33
（Sanger Phred‑33 质量值体系），即为该碱基的测序质量得分（Phred Quality Score）。不同
Phred Quality Score 代表不同的碱基测序错误率，如 Phred Quality Score 值为 20 和 30 分别
表示碱基测序错误率为 1% 和 0.1%
  - 假设一个碱基测序错误的概率是 P，那么此时对应的𝑄 = −10𝑙𝑜𝑔<sub>10</sub>\(𝑃)
  - 假设 100 个碱基中有 1 个出现错误，即 P=0.01，根据上式可以计算，此时 Q=20；同理，当
测序错误率为 0.001 时，此时 Q=30。测序结果中的每一个碱基都有这么一个 Phred 评分。
为了便于描述，人们习惯上将 Phred 评分对应一个 ASCII 码，这样每一个碱基的质量都可以
用一个字符来表述
    | P | Q | Sanger Phed | ASCII |
    | --------- | --------- | --------- | --------- |
    | 0.01 | 20 | 53 | 5 |
    | 0.001 | 30 | 63 | ? |
    | 0.0001 | 40 | 73 | I |
    | 0.00001 | 50 | 83 | S |
