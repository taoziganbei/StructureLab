# 结构力学实验室（StructureLab）
This software can calculate the planar structure. For the use of simple structure designers and students academic.

# 摘要
结构力学在工程中的应用十分广泛，合理的结构力学求解方法可以有效地提高计算效率。同时，大学生在学习《结构力学》时，许多问题计算之后不知道是否正确，无法发现漏洞和提高水平。在结构力学问题中，若手算则会出现以下的问题：1、结构复杂时，计算每个单元的内力繁琐耗时；2、当结构属于高次超静定结构时，会产生巨大矩阵，几乎无法手算。而市面上一些大型的工业软件安装使用复杂，需要更加高等的力学知识，对新手很不友好。  
基于此，研发一款操作简便的结构力学求解程序，供大学生学习使用，以及能够进行基本的平面结构设计。

# 使用简介
![image1](https://github.com/taoziganbei/StructureLab/blob/main/StructureLabImage/StuctureLab1.jpg)  
无需安装，双击“StructureLab.exe”即可运行，但必须要和 “LinearAlgebra.dll”文件放在同一个文件之下。  
打开界面如上图所示，菜单栏中，单击“文件”，可以选择打开或保存为文件；单击“清空”，可以清空绘制区域；单击“求解”，可以求解结构内力；单击“打印”，可以打印结构图、弯矩图、剪力图或轴力图。  
从左到右的图标依次为“添加结点”、“添加单元”、“添加支座”、“添加荷载”、“添加截面信息”，根据结构力学原理依次添加，节点、单元、支座的标识严格按照《结构力学》(朱慈勉、张伟平)中的图标，初学者也可以轻易明白建模流程。图标点击之后的窗体依次如下所示，还可以直接在子窗体预览图标。  
![image2](https://github.com/taoziganbei/StructureLab/blob/main/StructureLabImage/StuctureLab7Combine.jpg)  

# 举例说明
![image3](https://github.com/taoziganbei/StructureLab/blob/main/StructureLabImage/StuctureLab8.jpg)
选取《结构力学·上》(朱慈勉、张伟平)中例6-4，是一道非常复杂难以求解的题目，题目如上图所示。  
在界面中按照题目要求建立好模型，如下图所示，左边是按照编码规则自动生成的文本格式，右边是绘制的图形样式。  
![image4](https://github.com/taoziganbei/StructureLab/blob/main/StructureLabImage/StuctureLab17.jpg)  
点击菜单栏中的“求解”按钮即可计算出内力（弯矩、剪力、轴力）。求解的结果与教科书相比完全一致！
![image5](https://github.com/taoziganbei/StructureLab/blob/main/StructureLabImage/StuctureLab16combine.jpg)  
![image6](https://github.com/taoziganbei/StructureLab/blob/main/StructureLabImage/StuctureLab15combine.jpg)  
求解完毕之后
