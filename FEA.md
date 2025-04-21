# Finite Element Analysis

## 目录

- [1. 静力学](#静力学分析)
    - [1.1 单零件分析](#单个零件的静力学分析)
- [2. 刚体动力学](#刚体动力学)
    - [2.1 回转体分析](#回转体分析)

<a name="静力学分析"></a>
### 1 静力学

<a name="单个零件的静力学分析"></a>
##### 1.1 单个零件分析

###### 1.1.1 模块选择：静力学

<img src="./Images/For-FEA/Static/FEA-JLX-1.jpg" width="460">

###### 1.1.2 进入分析页面：
<img src="./Images/For-FEA/Static/FEA-JLX-2.jpg" width="460">

###### 1.1.3 材料选择：

<img src="./Images/For-FEA/Static/FEA-JLX-3.jpg" width="460">

###### 1.1.4 网格划分（右键生成）：

<img src="./Images/For-FEA/Static/FEA-JLX-4.jpg" width="460">

###### 1.1.5 选择固定支撑处：
固定支持选择：

<img src="./Images/For-FEA/Static/FEA-JLX-5.jpg" width="460">

固定位置选择（Ctrl可多选）：

<img src="./Images/For-FEA/Static/FEA-JLX-6.jpg" width="460">

###### 1.1.5 选择力：

选择基本力（需要点击应用）：

<img src="./Images/For-FEA/Static/FEA-JLX-7.jpg" width="460">

选择力作用对象（Ctrl可多选）：

<img src="./Images/For-FEA/Static/FEA-JLX-8.jpg" width="460">


###### 1.1.6 选择力分量：

<img src="./Images/For-FEA/Static/FEA-JLX-9.jpg" width="460">

###### 1.1.7 选择分析类型：

<img src="./Images/For-FEA/Static/FEA-JLX-10.jpg" width="460">

###### 1.1.8 查看静力学分析结果：

<img src="./Images/For-FEA/Static/FEA-JLX-11.jpg" width="460">


<a name="刚体动力学"></a>
### 2 刚体动力学

<a name="回转体分析"></a>
##### 2.1 回转体分析

###### 2.1.1 选择刚体动力学模块

<img src="./Images/For-FEA/Rigid Body Dynamics/FEA-GTDLX-1.jpg" width="460">

###### 2.1.2 选择材料、导入装配体后进入分析页面：

<img src="./Images/For-FEA/Rigid Body Dynamics/FEA-GTDLX-2.jpg" width="460">

###### 2.1.3 材料选择：

<img src="./Images/For-FEA/Rigid Body Dynamics/FEA-GTDLX-3.jpg" width="460">

###### 2.1.4 连接配置：

删除软件自动配合的连接：

<img src="./Images/For-FEA/Rigid Body Dynamics/FEA-GTDLX-4.jpg" width="460">

添加固定副：

<img src="./Images/For-FEA/Rigid Body Dynamics/FEA-GTDLX-5.jpg" width="460">

选择固定面（不可多选，每个固定面要设置独立的固定副）：

<img src="./Images/For-FEA/Rigid Body Dynamics/FEA-GTDLX-6.jpg" width="460">

添加回转副：

<img src="./Images/For-FEA/Rigid Body Dynamics/FEA-GTDLX-7.jpg" width="460">

选择相对回转对象（从固定点副回转点出发，第一个为参考，第二个为移动，以此重复）：

<img src="./Images/For-FEA/Rigid Body Dynamics/FEA-GTDLX-8.jpg" width="460">

...，重复选择，直到完成

###### 2.1.5 划分网格，插入标准重力

插入地球标准重力：

<img src="./Images/For-FEA/Rigid Body Dynamics/FEA-GTDLX-9.jpg" width="460">

设置重力方向：

<img src="./Images/For-FEA/Rigid Body Dynamics/FEA-GTDLX-10.jpg" width="460">

###### 2.1.6 设置分析时间：

<img src="./Images/For-FEA/Rigid Body Dynamics/FEA-GTDLX-11.jpg" width="460">

###### 2.1.7 设置随机扰动与惯性参考系：

<img src="./Images/For-FEA/Rigid Body Dynamics/FEA-GTDLX-12.jpg" width="460">

###### 2.1.8 设置求解内容

<img src="./Images/For-FEA/Rigid Body Dynamics/FEA-GTDLX-13.jpg" width="460">

###### 2.1.9 执行求解分析

<img src="./Images/For-FEA/Rigid Body Dynamics/FEA-GTDLX-14.jpg" width="460">