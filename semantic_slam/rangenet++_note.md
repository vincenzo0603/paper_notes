- rangenet++ 是一個lidar語義分割網絡

## 重要摘抄
1. An important tasks in semantic scene understanding is the task of semantic segmentation.
2. The main contribution of this paper is a new method  for accurate, fast, LiDAR-only semantic segmentation.
3. 貢獻一：We  achieve this by operating on a spherical projection of the  input point cloud, i.e., a 2D image representation, similar  to a range image
4. 貢獻二：This yields an efﬁcient  approach but can lead to issues caused by discretization  or blurry CNN outputs. We effectively resolve these issues  via a reconstruction of the original point with semantics  without discarding any points from the original point cloud,  regardless of the used resolution of the image-based CNN.
5. 總結貢獻點：
    - 精確的激光雷达的语义分割
    - 推断出完整的原始点的语义标签，避免丢弃点，無論CNN所使用的离散程度
    - 以帧速率工作在嵌入式计算机上

6. 關於pointNet和pointNet++： Qi等人使用未排序的原始点云作为输入，并应用对称运算符来处理这个排序问题。为此，PointNet[14]使用最大池来组合特征并生成置换不变的特征提取器。然而，这是PointNet的一个限制因素，导致它失去捕获特征之间的空间关系的能力。这限制了它对复杂场景的适用性。PointNet++[15]通过使用多层的特征提取方法解决了这个问题。通过利用本地附近的个别点，PointNet++捕获小范围的特征，然后在层次上应用这个概念来捕获全局特征。
7. 支持检索云中的所有点的标签，即使它们没有直接在范围图像中表示，与使用的分辨率无关。
8. 这四个步骤详细讨论以下部分：
    - （A）一个输入点云转换为range image表示
    - （B） 2d全卷积的语义分割
    - （C）从2d到3d语义迁移点（原始点云恢复所有点），不論使用的range image离散程度
    - （D）基于高效range image的3D后处理，以清除点云中不希望出现的离散化和推理工件。离散化和推理工件，使用一个快速的、基于GPU的 在所有点上进行kNN搜索。

9. for each pi ,its range r, its x, y, and z coordinates, and its remission, and we store them in the image, creating a [5 × h × w] tensor. ? 這裏its remission暫時不知道代表什麼