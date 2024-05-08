#  蛋白准备
Protein Preparation Wizard
+ 将 PDB 晶体结构库中的蛋白配体复合物结构导入 import
+ 定位需要保留的水分子，删掉其他水分子 remove waters
+ 简化多聚复合物 restrained minimization
+ 调整蛋白、金属离/原子和辅因子 propcess
+ 调整配体的键序和形式电荷 modify
+ 精炼结构，能量最小化 minimize

# 对接盒子生成
Receptor Grid Generation
+ 设置用于生成盒子的受体参数 receptor
  识别出配体、缩放受体原子的范德华半径...
+ 选择对接盒子中心并设置盒子尺寸 site
  使对接时配体坐标和质心不会超出盒子、对配体构象约束...

# 配体准备
LigPrep
+ 产生离子化状态、产生正确手性结构...

# 分子对接
Ligand Docking
+ 加载配体
+ 对接设置
  对接精度、增强采样...
+ 设置输出

# 结果分析
