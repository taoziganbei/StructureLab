# 结构力学实验室（StructureLab）
This software can calculate the planar structure. For the use of simple structure designers and students academic.

# 摘要
结构力学在工程中的应用十分广泛，合理的结构力学求解方法可以有效地提高计算效率。同时，大学生在学习《结构力学》时，许多问题计算之后不知道是否正确，无法发现解题错误和提高知识水平。在结构力学问题中，若手算则会出现以下的问题：1、结构复杂时，计算每个单元的内力繁琐耗时；2、当结构属于高次超静定结构时，会产生巨大矩阵，几乎无法手算。而市面上一些大型的工业软件安装使用复杂，需要更加高等的力学知识，对新手很不友好。  
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

求解完毕之后，可以分别显示“弯矩”、“剪力”、“轴力”，并且能显示每个单元每一点处的内力，如下图所示。  

![image7](https://github.com/taoziganbei/StructureLab/blob/main/StructureLabImage/StuctureLab18.jpg)  

之后点击“文件”可将右边显示的模型编码格式储存为TXT文件，以便下次直接打开。还可以自己按照编码格式自己书写，并读入软件。
下方“删除”行功能可以修改当前模型，但是要注意删除某一行会将与之关联的模型部位删除。  

# 代码说明
首先，依据力学原理，一个模型具有【节点】、【单元】、【支座】、【荷载】、【截面信息】五类基本信息。  
在C#中体现为五个基本“Class”：【Point.cs】、【Element.cs】、【Support.cs】、【Load.cs】、【Section.cs】。  

![image8](https://github.com/taoziganbei/StructureLab/blob/main/StructureLabImage/StuctureLab19.jpg)  

根据力学原理，每一类信息的编码规则如下：  
结点,（结点序号）,（x坐标）,（y坐标）  
单元,（单元序号）,（单元左结点序号）,（单元右结点序号）,（单元左端x约束）, （单元左端y约束）, （单元左端θ约束）,（单元右端x约束）, （单元右端y约束）, （单元右端θ约束）  
支座,（结点序号）,（支座类型）,（x向支座位移）,（y向支座位移）,（支座转角）  
单元荷载,（单元序号）,（荷载类型）,（荷载大小）,（荷载起点位置）,（荷载终点位置），（荷载角度，以左端指向右端为0°，右手旋转逆时针为正）  
单元截面性质,（单元序号）,（抗弯刚度EI）,（抗拉刚度EA）  
本项目创新性地处理了单元两端的连接形式，自由为（0,0,0），铰接为（1,1,0），刚接为（1,1,1），竖向滑动为（1,0,1），横向滑动为（0,1,1）  

该软件由三个模块构成，分别为“主界面”、“matlab”和“interForce”。  
“主界面”起着输入、读取、保存、绘制的功能，同时根据内力信息画出内力图和查看内力也在“主界面”内。  
“matlab”模块对结构的信息进行第一次运算，得到各个单元端部的力  
“interForce”模块进行第二次运算，根据第一次运算结果和结构信息得到所有单元的内力。  

![image9](https://github.com/taoziganbei/StructureLab/blob/main/StructureLabImage/StuctureLab20.jpg)  

【MainForm.cs】：程序主界面，包括绘图区域，菜单栏，控制区  
【PointForm.cs】、【ElementForm.cs】、【LoadForm.cs】、【SupportForm.cs】、【SectionForm.cs】：用于输入结构的文本信息  
【Point.cs】、【Element.cs】、【Load.cs】、【Support.cs】、【Section.cs】：分别储存点、单元、荷载、支座、单元截面等信息的类  
【DrawInterForce.cs】：用于绘制结构的弯矩、剪力、轴力等内力的类  
【GetPointForce.cs】：用于显示某个单元上的某点的内力  
【ScalePoint.cs】：获取当前所有结点坐标信息并实现按图框比例进行动态放缩  
matlab文件夹：对结构信息进行一次矩阵运算，获得各个单元端部的力  
interForce文件夹：对结构信息和各个单元端部的力进行二次运算，获得各个单元所有的内力  

其中主界面中图形绘制由GDI+图形接口完成，避免使用更加复杂的图像绘制。GDI+支持反锯齿，绘制的图形更加平滑、美观。并提供了功能强大的Matrix类来实现矩阵的变换。  
由于图形包括五类基本元素，以及计算之后得到弯矩、剪力、轴力的信息。为了使图像标识显示更加清楚，根据拓扑逻辑以及几何关系，自主研发了一系列有关图像显示的算法。  
比如，图像的动态放缩，使得图形始终充满整个绘图区域，不论图像大还是小都可以清晰显示；以及结点连接建模显示的细部调整，使模型与实际情况严格一致。  

在力学计算方面，根据经典力学原理，将其转化为代码，并且根据实际情况进行了调整。  
比如，在处理已知结点位移（引入位移边界条件）时使用“直接代入法”，而非“对角元素改1法”和“对角元素乘大数法”，保证了计算结果的精度；  
     输入数据中，单元端点的结点类型（连接方式）的u（x方向位移）、v（y方向位移）、θ（转角位移）对应的值以0、1表示；  
     在函数“KetoK0”（将单刚Ke送入总刚K0）中，使用哈希表将单元刚度矩阵Ke的行列下标与总刚度矩阵K0的行列下标一一对应，避免复杂的判断和循环，简洁明了，实现将单刚Ke“对号入座”送入总刚K0的功能；  
     若该结构为可变体系，则K0_two为奇异矩阵，此时将会弹出对话框，终止运算，实现矩阵计算的前处理判断，避免计算结果出错导致程序无法运行。  

# 总结
起初的设想是使用C#与Python混合开发，C#强大的界面功能和GDI+绘图功能对于结构显示很有利，而信息的矩阵运算采用Python，因为Python有强大的矩阵运算功能。但是项目进行到后期发现Python与C#对接会遇到很多不可预测的因素，且降低程序运行速度，带来诸多不便，因此在我们将已经编制完成的Python代码以C#语言改写，运用了现有的“LinearAlgebra.dll”类库和Matrix类进行矩阵的运算，运算方便快捷。
