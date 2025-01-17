- hw8_rabbit5024.m
这段代码是用于实现基于QP（二次规划）的MPC（模型预测控制）来追踪一个三轴三次积分器的螺旋锥路径。

以下是代码的主要部分的解释：
1. 初始化条件：定义了初始位置（p_0）、速度（v_0）和加速度（a_0）。
2. 预测和控制时间：定义了预测和控制的时间间隔（dt）和预测的步数（K）。
3. 权重和约束：定义了位置、速度、加速度和急动度的权重（weight），以及在XY平面和Z轴上的速度、加速度和急动度的约束（constraintXY和constraintZ）。
4. 路径生成：生成了一个螺旋锥路径（Path）。首先，物体在水平方向上以1m/s的速度移动8秒。然后，物体开始以0.4rad/s的角速度和-0.5m/s的垂直速度沿着一个螺旋路径移动。
5. MPC求解：调用getMPCresult函数，分别对X、Y、Z轴进行MPC求解，得到每个轴的位置、速度、加速度和急动度的时间序列（logX、logY、logZ）。
6. 结果绘图：绘制了四个图形，分别显示了X、Y、Z轴的位置、速度、加速度和急动度随时间的变化，以及物体在三维空间中的运动轨迹和Z轴的参考与追踪轨迹。

注意：这段代码中的getMPCresult函数没有在代码中定义，可能在其他文件或库中定义。

- getMPCresult.m
这段代码是用于计算模型预测控制（MPC）路径或轨迹的函数。它的主要步骤如下：
1. 初始化一个空的日志（log）和一个计数器（i）。
2. 对于给定的路径（Path）中的每个时间步长（dt），执行以下操作：
- 构建预测矩阵（Tp, Tv, Ta, Bp, Bv, Ba）。
- 获取当前时间步的路径命令（P_cmd）。
- 构建优化问题，包括目标函数的二次项（H）和线性项（F）。
- 定义状态和输出的硬约束（A和b）。
- 使用quadprog函数解决优化问题，得到优化变量J。
- 使用第一个优化变量J(1)更新位置（p_0）、速度（v_0）和加速度（a_0）。
- 将当前时间步的结果添加到日志（log）中。
- 更新计数器（i）。

这段代码中还包含了一些被注释掉的代码，这些代码可能是用于处理软约束的优化问题的。

这个函数的输入参数包括：
- K：预测的时间步数。
- dt：时间步长。
- weight：权重向量，用于构建目标函数。
- constraint：约束向量，用于定义状态和输出的约束。
- p_0, v_0, a_0：初始位置、速度和加速度。
- Path：预定的路径。








