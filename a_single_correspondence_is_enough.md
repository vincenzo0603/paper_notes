- 论文借助截断最小二乘那篇论文的代码库实现了防止退化（即inlier的点云少于三个）的点云全局配准算法。

1.假设点云集A，B的xy-plane已经对齐（利用Atlanta world assumption：论文 The Manhattan frame model—Manhattan world inference in the space of
surface normals）

2简化了截断最小二乘的配准模型建立，一：去除尺度和判断是否在inlier的向量；二：假设噪声项是服从高斯分布的

3.解耦旋转和平移估计
解耦论文：
（Closed-form solution of absolute orientation using unit quaternions）
（Least-squares fitting of two 3-D point sets）

4.Quasi-so(3):
几乎可以是纯yaw旋转（论文GP-ICP: Ground plane ICP for mobile robots提出的假设）

5.作者认为即使假设的xy-plane在不平面区域/视点不共面区域，也会有目前大多数建图/导航系统（惯性导航系统：inertial navigation system）给出观测的roll和pitch，通过从重力向量估计的水平平面。

6.使用渐变非凸性（Graduated Non-Convexity ）来估计Quasi-so(3)：
这里对GNC不懂，所以公式没看懂（Black-Rangarajan）

7.截断最小二乘和本文都用到了max clique inlier selection
理论来源于：Parallel maximum clique algorithms with applications to network analysis and storage


总结：本论文适用于源和目标点云视点较远  和  对防退化要求高的场景 （在数据集中 state of art）

作者在测试算法的回环检测时借助lego-loam框架，比较适合回环检测
