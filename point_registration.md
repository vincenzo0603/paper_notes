# 点云配准目前可以分为两种：
## 一：局部配准
局部配准最典型的算法为ICP及其部分变体（还有部分变体为全局配准）
其特点：
1. 一般使用场景为精配准，用于两个或多个点云欧式距离已经非常接近
2. 易陷入局部最优，当点云间欧式距离较远时，迭代次数较多，计算开销大（每次迭代点云对齐需要最小邻近搜索，计算代价高）




## 二：全局配准
- 全局配准可以进一步分为无需对应的全局配准和需要对应的全局配准
### 无需对应的全局配准：
- PHASER: a Robust and Correspondence-free Global Pointcloud Registration


### 需要对应的全局配准：
需要对应的全局配准一般流程为提取特征点云作为关键点，然后关键点之间对应进行点云配准
- TEASER: Fast and Certifiable Point Cloud Registration(2020)
- - 基本2020年以后的点云配准论文都会提到他，A Single Correspondence Is Enough这篇论文也是在此基础上提出的，很经典，需要再读

- A Single Correspondence Is Enough: Robust Global Registration to Avoid Degeneracy in Urban Environments(2022)

## 全局配准对比
- TEASER中有开发一个TEASER++: A FAST C++ IMPLEMENTATION适合用于移动机器人的全局配准，但是也使用了开源线程库openMP
- A Single Correspondence Is Enough:防退化


# 目前2d激光slam
## 关于帧间匹配
- pi-icp
- CSM(correlation scan match)
- 梯度优化(Hector-SLAM Non-linear Least Squares)
- state of art: CSM + 梯度优化

## 关于回环检测
- scan to map
- map to map
- branch and bound & lazy decision









# 其他
想法一：一般配准程序其中一项退出程序的条件为我们设置的可接受的残差阈值sigam，那在设计点云配准或者slam中scan to scan/scan to map中我们可以把配准
的迭代阈值alpha降低一点，然后选取两种点云陪准方法（局部和全局）。伪代码如下：

输入原始的点云A，点云B;
设置迭代阈值alpha，残差阈值sigam;

``` 
全局配准(原始的点云A，点云B)
{
    配准算法(迭代阈值alpha)
    {
        配准算法体

        if(配准后的残差值 < sigma)
        {
            return R,t;
            break;
        }
        return R,t;
    }

    if(配准后的残差值 > sigma)
    {
        局部配准(全局配准后的点云A，点云B)
        {
            配准算法(重新设置一个稍微大一点的阈值beta)
            {
                配准算法体

                if()
                {与上同}
            }
            return R,t;
        }
    }
    
}
```

想法二：