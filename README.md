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
+ @SQ 行的 “SN”标签是参考序列说明，它的值主要是用于 Alignments section 的第三列
“RNAME”和第七列“MRNM”比对的记录
+ @PG 行是使用的程序说明；该行“ID”为程序记录标识符，“PN”为程序名字，“CL”为命令行
+ @CO 行是任意的说明信息

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
| 3 | RNAME | String | \\\*\| \[:rname:<sup>∧</sup>*=]\[:rname:]* | Reference sequence NAME<br>1‑based leftmost mapping |
| 4 | POS | Int | \[0,2<sup>31</sup>−1] | POSition |
| 5 | MAPQ | Int | \[0,2<sup>8</sup>−1] | MAPping Quality |
| 6 | CIGAR | String |  \\\*\|\(\[0‑9]+\[MIDNSHPX=])+ | CIGAR string |
| 7 | RNEXT | String | \\\*\| \[:rname:<sup>∧</sup>*=]\[:rname:]* | Reference name of the<br>mate/next read |
| 8 | PNEXT | Int |  \[0,2<sup>31</sup>−1] | Position of the mate/next<br>read |
| 9 | TLEN | Int | \[−2<sup>31</sup>+1,2<sup>31</sup>−1] | observed Template LENgth |
| 10 | SEQ | String | \\\*\|\[A‑Za‑z=.]+ | segment SEQuence |
| 11 | QUAL | String | \[!-~]+ | ASCII of Phred-scaled base QUALity+33 |
+ QNAME: 序列的名字，也就是Read的名字
+ FLAG: 是一个标记的数字，是有需要转换成二进制才能知道代表的意思，各个数字分别代表
  - 每一个 read 的比对情况可以用十进制数字（或者十六进制数字）表示，如果比对情况有多
个，将多个比对情况所代表的十进制数字加和就是这一行的 FLAG
      - 比如，图 1 中 r001 的 FLAG 是 99（1+2+32+64），则表示了“该 read 是 pair read 中的一
个”，“pair read 中每个都能够正确比对上”，“该 read 的 mate read 的反向互补可以比对
上”，“该 read 是 pari read 中的 read1”
