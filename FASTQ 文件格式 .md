# FASTQ
是一种基于文本的存储生物序列和对应碱基（或氨基酸）质量的文件格式。最初由桑格研究所（Wellcome Trust Sanger Institute）开发出来，现已成为存储高通量测序数据的事实标准。以Illumina Casava 1.8+ 的fastq格式为例。

~~~
@ST-E00126:128:HJFLHCCXX:2:1101:7405:1133
TTGCAAAAAATTTCTCTCATTCTGTAGGTTGCCTGTTCACTCTGATGATAGTTTGTTTTGG
+
FFKKKFKKFKF<KK<F,AFKKKKK7FFK77<FKK,<F7K,,7AF<FF7FKK7AA,7<FA,,
~~~
每1条reads的信息可分成4行
## 第 1 行
主要储存序列测序时的坐标等信息。
+ @ 为开始的标记符号
+ ST-E00126:128:HJFLHCCXX 为测序仪唯一的设备名称
+ 2 为 lane 的编号
+ 1101 为 tail 的坐标
+ 7405 为在 tail 中的 X 坐标
+ 1133 为在 tail 中的 Y 坐标
## 第 2 行
测序得到的列信息，一般用 ATCGN 来表示，其中 N 表示荧光信号干扰无法判断到底是哪个碱基。
## 第 3 行
以 “+” 开始，可以储存一些附加信息，一般为空。
## 第 4 行
储存质量信息，与第2行的碱基序列一一对应，其中的每一个符号对应的 ASCII 值成为 phred 值，可以简单理解为对应位置碱基的质量值，越大说明测序的质量越好。不同的版本对应的不同。
### FASTQ 质量值计算方法
在测序仪进行测序的时候，会自动根据荧光信号的强弱给出一个参考的测序错误概率（error probility，P）根据定义来说，P 值肯定是越小越好，但以小数形式储存效率不高。Q=-10log<sub>10</sub>P,Q 加上33或者64转成一个新的数值，称为Phred，最后把Phred对应的ASCII字符对应到这个碱基。
如Q=20，Phred = 20 + 33 = 53，对应的符号是”5”这样就可以用1个符号与1个碱基一一对应，
