# VCF
Variant Call Format, 用于存储基因组序列中的变异信息，用于描述单核苷酸变异（SNV），小片段插入缺失（INDEL），拷贝数变异（CNV） 和结构变异（SV）结果的文本文件。在 GATK 软件中得到最好的支持，samtools 得到的结果也是 VCF 格式
## 主体结构
+ 注释信息（header）：位于文件开始，每行以 # 开始
  - 基因组的版本 (hg19，hg38)
  - info,filter,format 注释描述
+ 变异信息（body）：没有 # 即为记录的变异信息
```
#CHROM  POS     ID      REF     ALT     QUAL    FILTER  INFO    FORMAT  Sample1
chr1    13116   rs201725126     T       G       267.02  .       AC=2;AF=1.00;AN=2;DB;DP=7;ExcessHet=0.0000;FS=0.000;MLEAC=2;MLEAF=1.00;MQ=25.02;QD=25.36;SOR=4.174;ANNOVAR_DATE=2020-06-08;Func.refGene=ncRNA_intronic;Gene.refGene=DDX11L1\x3bDDX11L17;GeneDetail.refGene=.;Ex
onicFunc.refGene=.;AAChange.refGene=.;cytoBand=1p36.33;ExAC_ALL=.;ExAC_AFR=.;ExAC_AMR=.;ExAC_EAS=.;ExAC_FIN=.;ExAC_NFE=.;ExAC_OTH=.;ExAC_SAS=.;avsnp147=rs62635286;SIFT_score=.;SIFT_pred=.;Polyphen2_HDIV_score=.;Polyphen2_HDIV_pred=.;Polyphen2_HVAR_score=.;Polyphen2_HVAR_
pred=.;LRT_score=.;LRT_pred=.;MutationTaster_score=.;MutationTaster_pred=.;MutationAssessor_score=.;MutationAssessor_pred=.;FATHMM_score=.;FATHMM_pred=.;PROVEAN_score=.;PROVEAN_pred=.;VEST3_score=.;CADD_raw=.;CADD_phred=.;DANN_score=.;fathmm-MKL_coding_score=.;fathmm-MKL
_coding_pred=.;MetaSVM_score=.;MetaSVM_pred=.;MetaLR_score=.;MetaLR_pred=.;integrated_fitCons_score=.;integrated_confidence_value=.;GERP++_RS=.;phyloP7way_vertebrate=.;phyloP20way_mammalian=.;phastCons7way_vertebrate=.;phastCons20way_mammalian=.;SiPhy_29way_logOdds=.;ALL
ELE_END     GT:AD:DP:GQ:PGT:PID:PL:PS       1|1:0,7:7:21:1|1:13116_T_G:281,21,0:13116
chr1    13118   rs200579949     A       G       267.02  .       AC=2;AF=1.00;AN=2;DB;DP=7;ExcessHet=0.0000;FS=0.000;MLEAC=2;MLEAF=1.00;MQ=25.02;QD=28.73;SOR=4.174;ANNOVAR_DATE=2020-06-08;Func.refGene=ncRNA_intronic;Gene.refGene=DDX11L1\x3bDDX11L17;GeneDetail.refGene=.;Ex
onicFunc.refGene=.;AAChange.refGene=.;cytoBand=1p36.33;ExAC_ALL=.;ExAC_AFR=.;ExAC_AMR=.;ExAC_EAS=.;ExAC_FIN=.;ExAC_NFE=.;ExAC_OTH=.;ExAC_SAS=.;avsnp147=rs62028691;SIFT_score=.;SIFT_pred=.;Polyphen2_HDIV_score=.;Polyphen2_HDIV_pred=.;Polyphen2_HVAR_score=.;Polyphen2_HVAR_
pred=.;LRT_score=.;LRT_pred=.;MutationTaster_score=.;MutationTaster_pred=.;MutationAssessor_score=.;MutationAssessor_pred=.;FATHMM_score=.;FATHMM_pred=.;PROVEAN_score=.;PROVEAN_pred=.;VEST3_score=.;CADD_raw=.;CADD_phred=.;DANN_score=.;fathmm-MKL_coding_score=.;fathmm-MKL
_coding_pred=.;MetaSVM_score=.;MetaSVM_pred=.;MetaLR_score=.;MetaLR_pred=.;integrated_fitCons_score=.;integrated_confidence_value=.;GERP++_RS=.;phyloP7way_vertebrate=.;phyloP20way_mammalian=.;phastCons7way_vertebrate=.;phastCons20way_mammalian=.;SiPhy_29way_logOdds=.;ALL
ELE_END     GT:AD:DP:GQ:PGT:PID:PL:PS       1|1:0,7:7:21:1|1:13116_T_G:281,21,0:13116
chr1    13656   .       CAG     C       452.02  .       AC=2;AF=1.00;AN=2;DP=11;ExcessHet=0.0000;FS=0.000;MLEAC=2;MLEAF=1.00;MQ=23.46;QD=30.97;SOR=4.977;ANNOVAR_DATE=2020-06-08;Func.refGene=ncRNA_exonic;Gene.refGene=DDX11L1\x3bDDX11L17;GeneDetail.refGene=.;ExonicFunc.ref
Gene=.;AAChange.refGene=.;cytoBand=1p36.33;ExAC_ALL=.;ExAC_AFR=.;ExAC_AMR=.;ExAC_EAS=.;ExAC_FIN=.;ExAC_NFE=.;ExAC_OTH=.;ExAC_SAS=.;avsnp147=.;SIFT_score=.;SIFT_pred=.;Polyphen2_HDIV_score=.;Polyphen2_HDIV_pred=.;Polyphen2_HVAR_score=.;Polyphen2_HVAR_pred=.;LRT_score=.;LR
T_pred=.;MutationTaster_score=.;MutationTaster_pred=.;MutationAssessor_score=.;MutationAssessor_pred=.;FATHMM_score=.;FATHMM_pred=.;PROVEAN_score=.;PROVEAN_pred=.;VEST3_score=.;CADD_raw=.;CADD_phred=.;DANN_score=.;fathmm-MKL_coding_score=.;fathmm-MKL_coding_pred=.;MetaSV
M_score=.;MetaSVM_pred=.;MetaLR_score=.;MetaLR_pred=.;integrated_fitCons_score=.;integrated_confidence_value=.;GERP++_RS=.;phyloP7way_vertebrate=.;phyloP20way_mammalian=.;phastCons7way_vertebrate=.;phastCons20way_mammalian=.;SiPhy_29way_logOdds=.;ALLELE_END  GT:AD:DP:GQ:
PL  1/1:0,11:11:33:466,33,0
chr1    15040   .       T       A       36.64   .       AC=1;AF=0.500;AN=2;BaseQRankSum=0.050;DP=24;ExcessHet=0.0000;FS=2.205;MLEAC=1;MLEAF=0.500;MQ=31.17;MQRankSum=0.052;QD=1.67;ReadPosRankSum=0.298;SOR=0.255;ANNOVAR_DATE=2020-06-08;Func.refGene=ncRNA_splicing;Gene.refG
ene=WASH7P;GeneDetail.refGene=NR_024540:exon10:c.1233-2A>T;ExonicFunc.refGene=.;AAChange.refGene=.;cytoBand=1p36.33;ExAC_ALL=.;ExAC_AFR=.;ExAC_AMR=.;ExAC_EAS=.;ExAC_FIN=.;ExAC_NFE=.;ExAC_OTH=.;ExAC_SAS=.;avsnp147=.;SIFT_score=.;SIFT_pred=.;Polyphen2_HDIV_score=.;Polyphen
2_HDIV_pred=.;Polyphen2_HVAR_score=.;Polyphen2_HVAR_pred=.;LRT_score=.;LRT_pred=.;MutationTaster_score=.;MutationTaster_pred=.;MutationAssessor_score=.;MutationAssessor_pred=.;FATHMM_score=.;FATHMM_pred=.;PROVEAN_score=.;PROVEAN_pred=.;VEST3_score=.;CADD_raw=.;CADD_phred
=.;DANN_score=.;fathmm-MKL_coding_score=.;fathmm-MKL_coding_pred=.;MetaSVM_score=.;MetaSVM_pred=.;MetaLR_score=.;MetaLR_pred=.;integrated_fitCons_score=.;integrated_confidence_value=.;GERP++_RS=.;phyloP7way_vertebrate=.;phyloP20way_mammalian=.;phastCons7way_vertebrate=.;
phastCons20way_mammalian=.;SiPhy_29way_logOdds=.;ALLELE_END GT:AD:DP:GQ:PL  0/1:18,4:22:44:44,0,425
```

## 主要字段
### CHROM
染色体号，表示变异位点是在哪个 contig 里 call 出来的，人类全基因组是chr1⋯chr22，chrX,Y,M
### POS
变异位点，对于 INDEL 是第一个碱基位点
### ID
dbSNP 的编号，如果 在于 dbSNP 数据库里会显示相应的rs 编号， · 为置空
### REF
参考基因组的碱基，也就是等位基因
### QUAL
Phred 的质量值，表示改位点存在变异的可能性。Q=‑10lgP，Q 表示质量值；P 表示这个位点发生错误的概率。当 Q=20 时，错误率就控制在了 0.01。分数越高则认为越可靠，但同时需要考虑测序深度，覆盖度等因素。· 代表置空，不代表质量值为 0。
### FILTER
过滤标志，理想情况下，QUAL 这个值应该是用所有的错误模型算出来的，这个值就可以代表正确的变异位点了，但是事实是做不到的。因此，还需要对原始变异位点做进一步的过滤。无论你用什么方法对变异位点进行过滤，过滤完了之后，在 FILTER 一栏都会留下过滤记录，如果是通过了过滤标准，那么这些通过标准的好的变异位点的 FILTER 一栏就会注释一个 PASS，如果没有通过过滤，就会在 FILTER 这一栏提示除了 PASS 的其他信息。如果这一栏是一个“.”的话，就说明没有进行过任何过滤。GATK 的 VQSR 可以注释。
### INFO
详细信息
| 字段 | 全程 | 描述 |
| --------- | --------- | --------- |
| AA | Ancestral Allele | 一个群体或物种的共同祖先中存在的该等位基因 |
| AC | Allele Count | 该变异的等位基因（ALT列）在样本集合中出现的次数。如果有多个 ALT，使用 , 分隔 |
| AF | Alternate Allele Frequency | 该变异在样本集合中的频率。对于 1000 Genomes 来说，EAS_AF，AMR_AF，AFR_AF，EUR_AF， SAS_AF 分别表示东亚，美洲，非洲，欧洲，南亚人群的等位基因频率 |
| AN | Allele Number | 该变异的等位基因总数。以二倍体生物为例，如果样本为杂合子（基因型 0/1），AN 值为 1，表示改位点只有一个等位基因发生突变。如果样本为纯合子（基因型 1/1），AN 值为 2 |
| DP | Read Depth | 该变异位点测序深度，也就是改位点 reads 覆盖度 |
| MQ | Mapping Quality | 该变异比对时，reads 的平均质量 |
| QD | Quality by Depth | 该变异质量分数（QUAL）与测序深度（DP）的比值。用于评估改位点的质量 |
| VT | Variant Type | 变异类型，一般包括 SNP，MNP，INDEL，SV 等 |
| MAF | Minor Allele Frequency | 次要等位基因频率，用来粗略地了解给定人群中给定SNP的基因型变异，表示这个SNP有多普遍 |
| EAF | Effect Allele Frequency | 效应等位基因频率，本质上是等位基因，其与疾病的关系正在被研究。因此，效应等位基因总是次要等位基因 |

### FORMAT
在 header 中都有其注解
| 字段 | 全称 | 描述 |
| --------- | --------- | --------- |
| GT | Genotype | 表示基因型。对于二倍体样本，用两个数字中间以 / 或 \| 分隔。0表示 REF 的等位基因，1表示 ALT 的等位基因，2表示有第二个 ALT 的等位基因。 1/1表示纯合子，0/1表示杂合子，有两个基因型 |
| AD | Allele Depth | 样本中等位基因的 reads 覆盖度。对于二倍体，1000,1100用逗号分隔，前者是 REF，后者是 ALT |
| DP | Read Depth | 该位点 reads 覆盖度 |
| GQ | Genotype Quality | 基因型的质量值，表示该基因型的可能性，值越高，可能性越大。计算：Phred 值=-10log10(P)，P 为基因型错误的概率 |
| PL | Provieds the Likelihoods of the given genotypes | 三种基因型的质量值，即0/0，0/1，1/1，三种基因型的概率总和为1。值越小表示是该基因型的概率越大。同样是计算 Phred 值，但是 P 为基因型存在的概率 |
| PGT | Phased Genotype | 只出现在进行过相分离的样本中。表示相分离后的基因型，两个数字间使用 \| 表示二倍体样本的基因型 |
| PID | Phase ID | 描述基因型相位的标识符 |
| PS | Phase Set | 描述同一样本中基因型相位的信息 |
| FS |  FisherStrand | 使用 Fisher’s 精确检验来检测 strand bias 而得到的 Fhred 格式的 p 值，该值越小越好；如果该值较大，表示 strand bias（正负链偏移）越严重，即所检测到的 variants 位点上，reads 比对到正负义链上的比例不均衡。一般进行 filter 的时候，推荐保留 FS<10‑20 的 variants 位点。GATK 可设定 FS 参数 |
| ReadPosRandSum | |  Z‑score from Wilcoxon rank sum test of Alt vs. Ref read position bias. 当 variants 出现在 reads 尾部的时候，其结果可能不准确。该值用于衡量 alternative allele（变异的等位基因）相比于 reference allele（参考基因组等位基因），其 variant 位点是否匹配到 reads 更靠中部的位置。因此只有基因型是杂合且有一个 allele 和参考基因组一致的时候，才能计算该值。若该值为正值，表明和 alternative allele 相当于 reference allele，落来 reads 更靠中部的位置；若该值是负值，则表示 alternative allele 相比于 reference allele 落在 reads 更靠尾部的位置。进行 filter 的之后，推荐保留 ReadPosRankSum>‑1.65 ‑ ‑3.0 的 variant 位点 |
| MQRankSum | | 用于衡量 alternative allele 上 reads 的 mapping quality 与 reference allele上reads的mapping quality的差异。若该值是负数值，则表明alternative allele 比 reference allele 的 reads mapping quality 差。进行 filter 的时候，推荐保留 MQRankSum > ‑1.65 ‑ ‑3.0 的 variant 位点 |
| HaplotypeScore | | 表示该位点与最多两个分离的单倍型的一致性 |
| InbreedingCoef | | 表示基于每个样本的基因型 PL 的近交系数 |
| MLEAC | Maximum Likelihood Expectation (MLE) for the Allele Counts | 不一定与 AC 相同，对于每个 ALT 等位基因，其顺序与所列出的顺序相同 |
| MLEAF | Maximum Likelihood Expectation (MLE) for the Allele Frequency | 不一定与 AF 相同，对于每个 ALT 等位基因，其顺序与所列出的顺序相同 |
| MQ | RMS Mapping Quality | |
| MQ0 | Total Mapping Quality Zero Reads | |
| MQRankSum | Z‑score From Wilcoxon rank sum test of Alt vs. Ref read mapping qualities | |
| QD | Variant Confidence/Quality by Depth | |
| RPA | | 每个等位基因重复序列重复次数（包括参考文献）|
| RU | Tandem repeat unit | |
| ReadPosRankSum | Z‑score from Wilcoxon rank sum test of Alt vs. Ref read position bias | |
| STR | | 变体是一个短的串联重复序列 |
+ 相位化（phasing）是确定某个个体在某个基因位点所携带的等位基因来自哪个亲本的过程
  - GT 字段中的 / 表示基因型未相位化，表示我们不确定哪个等位基因来自父亲或母亲
  - GT 字段中的 | 表示基因型相位化，也就是说可以确定等位基因的来源亲本
