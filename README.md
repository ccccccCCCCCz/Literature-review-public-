# Literature-review(public)
# 最终目的:让自动驾驶电动卡车在存在电气化公路（ERS）的环境中，自主决定“何时走ERS路段 / 何时编队 / 何时独行 / 何时充电”，以最小化能耗 + 行程时间 + 充电次数。(宏观+微观)

# 混合动力RL指导
## 1.Deep reinforcement learning enabled self-learning control for energy efficient driving(2019)--->https://www.sciencedirect.com/science/article/pii/S0968090X18318862
(1)这篇论文提出了一种基于深度强化学习（DQN 与 DDQN）的自学习能量管理方法，使插电式混合动力车辆（PHEV）能够在无需预定义驾驶循环的情况下实现实时能效最优控制。<br>
(2)这项工作是将深度强化学习（DQN 和 DDQN）应用于 PHEV EMS 最优控制的先驱之一，也就是把DRL融入到混合动力车辆的先驱。<br>
(3)无模型:不需要传统控制方法（例如 MPC）通常需要的车辆动力学模型。<br>
## 2.Automated eco-driving in urban scenarios using deep reinforcement learning(2021)--->https://www.sciencedirect.com/science/article/pii/S0968090X2100005X
(1)结构:1.introduction 减少碳排+自动辅助驾驶技术--->生态驾驶+具体算法(MPC、DPP、RL)--->具体场景(前方有车+V2X覆盖率低)TD3 <br>
        2.模拟环境:1)车辆建模:扭矩 T 和转速 n 进行建模(实际后续高层RL用不到)  2)流量建模:前车+红绿灯，使用IDM模型，过滤车速低的，获取车速分布取中值，车辆的驶入与驶出  3)参考策略:控制目标速度，不超过最高不低于最低<br>
        3.RL agent:1)具体智能体构造(TD3):一个动作网络两个评判网络 2)设置奖励值:R=r(通过红绿灯奖励)-ropt(速度惩罚)-ra(加速度惩罚)-rmon(安全监视器)<br>
        4.结果:训练+测评(自己对比+与GLOSA 策略对比+对惩罚单独测评)<br>
        5.结论<br>

# 从单车到车队(使用RL)
## 1.Research on Reinforcement-Learning-Based Truck Platooning Control Strategies in Highway On-Ramp Regions(2023)--->https://www.mdpi.com/2032-6653/14/10/273
(1)<br>
(2)提供了MAPPO可以作为未来的baseline；<br>
   局部稳定性:每一辆车都能根据自己的控制系统，稳定地跟踪目标速度和位置。(就是每辆车都能控制好自己)；<br>
   string stability:整个车队在行驶过程中，误差不会沿着队列放大传播。(就是前面车减速1，后面都是1，不会2、3累加)<br>

# GVRP(宏观，暂时先不看)
## 1.A Green Vehicle Routing Problem(2012)
(1)提出两种方法the Modified Clarke and Wright Savings heuristic and the Density-Based Clustering Algorithm(MCWS和DBCA)<br>
(2)其中MCWS继承C-W算法(C-W算法就是计算两点之间节约值进行合并，类似最小生成树)，DBCA继承DBSCAN(DBSCAN就是聚类的分类方式)
(3)图扩展技巧(补能站多次访问):建立虚拟顶点<br>
(4)路径内优化和跨路径(外)优化
(4)1.一类车辆路径问题的概念化，涉及加油能力有限和加油站可用性有限的车辆；<br>
   2. 开发和测试用于解决大型现实世界问题实例的有效启发法，包括在燃料消耗和补充时跟踪燃料水平的具体步骤，以及通过在途中选择性地访问非唯一加油站来延长车辆的距离限制；
   3.深入了解站点和客户的地理分布对运营可行性的影响；<br>
   4.鉴于当前可用的车辆技术和有限的支持基础设施部署，支持机构减少碳足迹的工具。
(5)个人评价:使用了两种新方法与最优解对比，没差太多。也算是电车充电站的相关VRP的开端了。
# 电动卡车
## 1. Is electric truck a viable alternative to diesel truck in long-haul operation?(2024)
### 提出电动卡车在物流运输方面与原来汽油重卡的对比:
(1)提出具有协调充电计划的电动卡车路线和驾驶员调度问题(eTRDSP-CS)<br>
(2)缺少政策支持、缺乏高速公路的充电设施、前期成本高、充电慢影响效率<br>
(3)结果表明，虽然在州际高速公路上促进长途电动卡车运营在技术上是可行的，但即使在同步和最佳的时间表下，由于充电而导致的行程时间延长（16％至32％之间）以及高昂的初始采用成本仍然阻碍着运营商采用。另一方面，长途电动卡车比柴油卡车节能 43% 以上，这对环境可持续发展具有重大影响。
## 2.Advances in EV wireless charging technology – A systematic review and future trends(2024)
(1)提出WPT(无线充电)<br>
(2)对比传统插入式更方便
# 电气化道路
## 1. Electric road system technologies in Sweden Gaining experience from research and demo facilities(2020)
(1)是对截止2020年的瑞典购买的4个ERS技术试点的综述 <br>
(2)一共三种方式，架空线路、公路电轨、感应发电。其中架空线路最成熟 <br>
(3)我认为公路电轨过于复杂不太可能，架空线路现在还不错，感应的话技术可能还需要进一步优化。
## 2. Route optimization of battery electric vehicles using dynamic charging on electrified roads(2024)
(1)货物的安全是大多数运营商可能不喜欢在公共充电站为其车队充电的个原因，安装私人充电站在经济上并不是一个可行的选择。此外，绕道前往充电站和充电时间长会降低车辆和驾驶员的利用率并增加成本。<br>
(2)电动汽车可以行驶超过 2000 公里的距离而无需充电。我们的实验还表明，在大约 30% 至 40% 的道路上建立基础设施足以确保电动汽车的可靠通行。
(3)可以证明与电动汽车与ERS道路结合的可行性
