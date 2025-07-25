# 基于 ISO 24758-1 从探针浓度数据计算 ROS 浓度的软件系统

一个基于探针浓度数据和反应速率常数计算活性氧（ROS）浓度的软件系统。

E. Lan, S. Liu,  细气泡技术 — 细气泡分散体中活性氧的测定评价方法 — 第1部分：基于探针的动力学模型 (ROS_Calculate 软件), 1.0版 [在线软件]. GitHub, 2025 [2025‑07‑22 查看].

获取地址:

[https://github.com/ElonLan/ROS_Calculate](https://github.com/ElonLan/ROS_Calculate)

## 项目概述

本软件旨在使用探针分析法定量测定多种活性氧（ROS）的浓度。通过采用多探针联合测量的方法，克服了传统方法无法同时测量多种 ROS 的局限性。该软件具有用户友好的图形界面和强大的计算引擎。

---

## 开发背景

活性氧（ROS）在环境和生物系统中扮演着至关重要的角色。准确测量不同种类 ROS 的浓度对于理解其作用机制和影响至关重要。传统方法通常仅限于测量单一类型的 ROS，而在现实环境中，多种 ROS 往往共存。本软件通过数学模型和多探针法，实现了多种 ROS 的同步测定。

---

##核心功能

- **多种ROS浓度同步测量**：基于线性方程组求解多种ROS浓度。
    
- **灵活的计算方法**：支持标准分析和超定分析两种方法。
    
- **数据管理**：提供数据的导入、编辑和导出功能。
    
- **可视化分析**：支持ROS和探针浓度的图表展示。
    
- **数据库管理**：包含可编辑的ROS种类、探针和反应速率常数数据库。
    

---

## 技术架构

### 系统架构

软件采用 MVC (Model-View-Controller) 架构设计：

**模型层 (Model Layer):**

- 计算引擎：实现ROS浓度计算的核心算法。
    
- 数据库管理：管理探针、ROS种类和反应速率常数的数据。
    

**视图层 (View Layer):**

- 主窗口：提供用户交互界面。
    
- 数据库编辑器：用于编辑和管理数据库内容。
    
- 结果可视化：展示计算结果和图表。
    

**控制层 (Controller Layer):**

- 协调模型层和视图层之间的交互。
    
- 处理用户输入和事件响应。
    

### 系统要求

- Windows 操作系统
    

---

## 用户指南

### 基本工作流程

1. **准备数据文件：**
    
    - 创建一个包含探针浓度百分比的 CSV 或 Excel 文件。
        
    - 文件必须包含一个“Time”列和每个探针的百分比列（格式为“[ProbeID]_percentage”）。
        
2. **配置数据库：**
    
    - 通过“数据库管理”功能查看和编辑 ROS 种类、探针和反应速率常数。
        
3. **计算ROS浓度：**
    
    - 加载数据文件。
        
    - 软件将自动从数据中识别探针类型。
        
    - 选择需要计算的 ROS 种类。
        
    - 选择计算方法（标准分析或超定分析）。
        
    - 点击“计算”按钮执行计算。
        
4. **查看和导出结果：**
    
    - 在结果表格中查看详细的计算结果。
        
    - 在可视化图表中观察 ROS 浓度变化趋势。
        
    - 导出结果数据或图表。
        

---

## 计算方法说明

### 数学模型

软件基于探针与ROS之间的反应动力学方程，建立了探针浓度变化率与ROS浓度之间的线性关系。

**基本反应方程：**

探针与ROS的反应速率方程为：

$-\frac{d[Probe]}{dt} = \sum_i k_i[Probe][ROS_i]$

**积分处理：**

对该方程进行积分，得到：

$\ln\left(\frac{[Probe]_t}{[Probe]_0}\right) = \sum_i k_i \cdot \int_0^t [ROS_i] dt$

其中 $\int_0^t [ROS_i] dt$ 表示 $ROS_i$​ 从时间0到t的累积浓度。

**矩阵表示：**

构建线性方程组：

$A \times x = b$

- A: 反应速率常数矩阵 (n×m)
    
- x: 未知的ROS累积浓度向量 (m×1)
    
- b: 探针浓度变化向量 (n×1)，其中每个元素为 $\ln\left(\frac{[Probe]_t}{[Probe]_0}\right)$
    

### 求解方法

根据探针数量（n）和ROS种类数量（m）的关系，软件提供两种求解方法：

1. 标准分析 (n=m):
    
    当探针数量等于ROS种类数量时，方程组有唯一解，可通过矩阵求逆直接求解：
    
   $x = A^{-1} \times b$
    
2. 超定分析 (n>m):
    
    当探针数量大于ROS种类数量时，采用最小二乘法求解：
   $x = (A^T \times A)^{-1} \times A^T \times b$
    
    此方法可以减少实验误差的影响，提高计算精度。
    

---

## 软件界面

### 主窗口布局

主窗口分为三个主要区域：

**左侧控制面板：**

- 探针选择列表
    
- ROS种类选择列表
    
- 计算方法选择
    
- 计算控制按钮
    

**右侧选项卡窗格：**

- 数据选项卡：显示和管理输入数据。
    
- 结果选项卡：展示计算结果。
    
- 可视化选项卡：显示ROS浓度图表。
    

**工具栏和菜单：**

- 文件操作：打开、保存数据和结果。
    
- 数据库管理：打开数据库编辑器。
    
- 帮助：显示帮助和关于信息。
    

### 数据库编辑器

数据库编辑器包含三个选项卡：

1. **ROS种类管理：**
    
    - ROS种类列表。
        
    - 添加、编辑和删除ROS种类。
        
2. **探针管理：**
    
    - 探针列表。
        
    - 添加、编辑和删除探针。
        
3. **反应速率常数管理：**
    
    - 反应速率常数矩阵表。
        
    - 设置和修改特定探针与ROS之间的反应速率常数。
        

---

## 开发计划

**当前版本 (v1.0)**

- [x] 基本用户界面
    
- [x] 基本计算引擎
    
- [x] 数据库管理系统
    
- [x] 数据可视化
    
- [x] 结果导出功能
    

**未来路线图 (v2.0)**

- [ ] 探针选择优化算法
    
- [ ] 不确定性分析和误差传播
    
- [ ] 高级统计分析功能
    
- [ ] 交互式3D可视化
    
- [ ] 实验设计向导
    

---

## 术语表

- **ROS**: 活性氧 (Reactive Oxygen Species)
    
- **Probe**: 探针，与ROS反应的特定化合物
    
- **Reaction Rate Constant**: 反应速率常数，探针与ROS之间反应的速率常数
    
- **Cumulative Concentration**: 累积浓度，ROS在特定时间段内的积分浓度
    
- **Instantaneous Concentration**: 瞬时浓度，ROS在特定时间点的浓度
    
- **Standard Analysis**: 标准分析，探针数量等于ROS种类数量时的计算方法
    
- **Overdetermined Analysis**: 超定分析，探针数量大于ROS种类数量时的计算方法
    

---

## 如何使用

从 Releases 下载最新的 `ROS_Detection.exe` 程序和CSV格式的示例探针浓度数据表。双击 .exe 文件打开软件程序。您可以直接使用示例CSV数据进行绘图。

---

## 创建者

南京天祺超氧科技有限公司

www.tqcy.top

软件由Elon LAN 和 Shu LIU 创建

### 联系我

- lanqq8@gmail.com
    
- liushu@buaa.edu.cn
    
- lanqq8@tqcy.top
