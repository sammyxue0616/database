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
|
