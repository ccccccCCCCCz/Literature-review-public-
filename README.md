# Literature-review(public)
# 最终目的:让自动驾驶电动卡车在存在电气化公路（ERS）的环境中，自主决定“何时走ERS路段 / 何时编队 / 何时独行 / 何时充电”，以最小化能耗 + 行程时间 + 充电次数。(宏观+微观)

# 论文复现
## 1.Combat Urban Congestion via Collaboration: Heterogeneous GNN-Based MARL for Coordinated Platooning and Traffic Signal Control(2025）--->https://ieeexplore.ieee.org/abstract/document/10977660
提出了一种基于异构图神经网络（Heterogeneous GNN）的多智能体强化学习（MARL）方法，用于同时协调“车队编队控制（platooning）”和“交通信号控制”。将车队控制（Platooning）和信号控制（Traffic Signal Control） 视为两类不同的智能体。每类智能体有独立的观测空间、动作空间和奖励函数，使用采用 alternating optimization，让不同类型的智能体交替更新策略。异构图神经网络表达不同类型智能体之间的交互关系。
其实就是siganl 和platooning分别设为不同agent并获取自己的局部观测，然后异构网络的node，而edge则根据是有三种(siganl->platooning,signal->signal,platooning->signal),并通过两者进行信息交互。其中不同agent之间的交互通过GNN进行，GNN进行不同node的信息交互，完成信息的上下文融合后，传递给policy network去进行动作，最后在MARL中更新GNN与policy的参数。

# 车队能耗建模
## 1.Modeling Relationship between Truck Fuel Consumption and Driving Behavior Using Data from Internet of Vehicles(2018)--->https://onlinelibrary.wiley.com/doi/abs/10.1111/mice.12344


# 单车RL控制
## 1.Deep reinforcement learning enabled self-learning control for energy efficient driving(2019)--->https://www.sciencedirect.com/science/article/pii/S0968090X18318862
(1)这篇论文提出了一种基于深度强化学习（DQN 与 DDQN）的自学习能量管理方法，使插电式混合动力车辆（PHEV）能够在无需预定义驾驶循环的情况下实现实时能效最优控制。<br>
(2)这项工作是将深度强化学习（DQN 和 DDQN）应用于 PHEV EMS 最优控制的先驱之一，也就是把DRL融入到混合动力车辆的先驱。<br>
(3)无模型:不需要传统控制方法（例如 MPC）通常需要的车辆动力学模型。<br>
## 2.Automated eco-driving in urban scenarios using deep reinforcement learning(2021)--->https://www.sciencedirect.com/science/article/pii/S0968090X2100005X
(1)这篇论文提出了一种基于深度强化学习（TD3）的生态驾驶策略，用于城市道路环境中，在有红绿灯、前车和交通信号不完全可预测的情况下自动调节速度，实现节能驾驶同时维持交通流畅性。<br>
(2)结构:1.introduction 减少碳排+自动辅助驾驶技术--->生态驾驶+具体算法(MPC、DPP、RL)--->具体场景(前方有车+V2X覆盖率低)TD3 <br>
        2.模拟环境:1)车辆建模:扭矩 T 和转速 n 进行建模(实际后续高层RL用不到)  2)流量建模:前车+红绿灯，使用IDM模型，过滤车速低的，获取车速分布取中值，车辆的驶入与驶出  3)参考策略:控制目标速度，不超过最高不低于最低<br>
        3.RL agent:1)具体智能体构造(TD3):一个动作网络两个评判网络 2)设置奖励值:R=r(通过红绿灯奖励)-ropt(速度惩罚)-ra(加速度惩罚)-rmon(安全监视器)<br>
        4.结果:训练+测评(自己对比+与GLOSA 策略对比+对惩罚单独测评)<br>
        5.结论<br>

# 从单车到车队(使用RL)
## 1.AHS research at the California PATH program and future AHS research needs(2008)--->https://ieeexplore.ieee.org/document/4640915
概述 PATH 计划在自动化高速公路研究中的主要进展，并提出未来研究方向，是该领域早期的指导性研究之一,为后续的ITS研究铺垫基础。PATH研究第一个四车自动排纵向控制实验<br>
## 2.Determination of the Order of Electronically Coupled Trucks on German Motorways(2011)--->https://ieeexplore.ieee.org/abstract/document/5406751
研究了在德国高速公路上电子耦合卡车如何排序与组织编队的策略。其方法基于 GPS-signatures轨迹/路径数据，分析哪些卡车在相近行驶路线与时间上能形成编队以减少燃油消耗与空气阻力。然而，该研究在算法的时变性、动态交通反应能力以及实时性方面已有一定局限，尤其在交通流波动大或车辆进入／退出频繁的场景中表现可能不佳。总体而言，该论文是电子耦合卡车／车队编队研究中的早期工作，为后续关于实时编队优化、车辆排序与混合交通环境下的车队控制提供了借鉴。算是卡车队列的编队的先驱了。
## 3.An automated truck platoon for energy saving(2011)--->https://ieeexplore.ieee.org/document/6094549
实车实验检验了三个重型牵引拖车卡车在不同跟车间距（10 m 到 4 m）及加减速、上坡／下坡、编队加入与退出等动态情形下的纵向控制效果，测量其燃油节省与气动阻力变化，结果显示在较小间距下跟车车节油显著（lead truck 节省约 4-5%，跟随车节省约 10-14%）。这文章是把CCA算法应用到实际车队，而没有提出新算法。(算是传统方法的实际应用了)
## 4.Cooperative Adaptive Cruise Control: A Reinforcement Learning Approach(2011)--->http://ieeexplore.ieee.org/document/5876320/
让联网车辆（CACC系统）在不依赖精确模型的前提下，通过学习实现更安全、更节能的车队跟驰控制。使用了分层算法，算法结合了RL(Q-learning)和博弈论，并提出了RL的分层结构的思想(非常的简单，只是单纯把policy和Q分别分开来而已，严格来说不是现代分层结构)。其中上层管理层使用RL(值函数逼近强化学习以及局部Q-learning(TJA和PJA))，下层引导层使用传统控制器。将RL首次用于CACC系统
## 5.Survey on Platoon-Based Vehicular Cyber-Physical Systems(2016)--->https://ieeexplore.ieee.org/document/7056505
综述性质的文章系统梳理基于车队（platoon） 的联网车辆系统（Vehicular Cyber-Physical Systems, VCPS／也称车联网 + 控制融合系统），车队运动模型、车流模型、车间距／速度关系，车队如何组建、合并／拆分、车队内控制策略、协作驾驶机制以及车队稳定性。介绍混合通信 + 交通仿真平台、典型工具链。总结了队列行驶的关键技术和挑战。
## 6.An Intelligent Path Planning Scheme of Autonomous Vehicles Platoon Using Deep Reinforcement Learning on Network Edge(2020)--->https://ieeexplore.ieee.org/document/9102259
提出了一种基于深度强化学习并部署于网络边缘的自动驾驶车队智能路径规划方法。该研究将车队路径规划建模为一个在任务时限约束下最小化燃油消耗的优化问题，利用强化学习框架在动态交通环境中自适应地学习最优路径策略。同时，引入边缘计算以降低车辆端的计算负担和决策延迟。主要是在路径规划方面(选择耗能最少的)。依靠RL减少能源消耗。
## 7.Decentralized Cooperative Merging of Platoons of Connected and Automated Vehicles at Highway On-Ramps(2021)--->https://ieeexplore.ieee.org/document/9483390
提出了分散式协同控制方法，使高速公路匝道上的自动驾驶车队能够安全、高效地并入主干道车队，将复杂的二维多排协作问题转化为一维排跟随控制问题。先计算通过时间，再计算燃油消耗。
## 8.A Reinforcement Learning-Based Vehicle Platoon Control Strategy for Reducing Energy Consumption in Traffic Oscillations(2021)--->https://ieeexplore.ieee.org/document/9410239
提出了一种通信近端策略优化（CommPPO）算法(主要还是PPO)来控制车队。制定新的奖励以解决虚假奖励和“惰性智能体”问题，采用课程学习方法(从简单环境到难环境)来减少崩溃并加快训练速度，最终实现交通振荡下的能耗优化。后续如果需要学习多智能体的历史可以在这篇文章里看。
## 9.Multi-Agent Reinforcement Learning for Highway Platooning(2023)--->https://www.mdpi.com/2079-9292/12/24/4963
MARL+PPO协作，重点是实现对不同速度条件的自适应响应，并涵盖不同的队列速度。我的评价是这篇文章用的方法是没那么新颖的，主要是为了工程落地的可行性来编写的，用的甚至是即时奖励这种reward，有点抽象了。
## 10.Research on Reinforcement-Learning-Based Truck Platooning Control Strategies in Highway On-Ramp Regions(2023)--->https://www.mdpi.com/2032-6653/14/10/273
(1)提出一种基于 Platoon-MAPPO 的多智能体强化学习策略，用于卡车编队在高速公路匝道（on-ramp）段的纵向控制，从而在面对匝道干扰时保持车队稳定性、提高能效、减少道路占用。<br>
(2)结构:1.introduction:介绍自动卡车队列(具体例子)+好处--->之前研究的不足(传统方法+深度学习)--->RL方法好处+MAPPO-Plooting方法是best<br>
2.related work:传统方法(提供局部稳定性+string stability)--->提出具体的普通RL方法+不足--->具体场景下的应用(匝道)<br>
3.Preliminaries and Methods:Preliminary Knowledge:强化学习基础相关的内容+多智能体RL---->集中训练分散执行方法<br>
Methods:Truck Platoon Communication Topology:说明具体运作交换信息的车辆是前车和后车，避免了计算资源浪费<br>
Crucial Elements:主要介绍PPO的构成(批判者观察全局+参与者只关注自身)--->将state、action、reward(速度、能耗和安全)进行详细描述--->算法伪代码介绍<br>
4.Simulation:仿真平台(SUMO(坡度+IV))+卡车纵向动力学(会受到的不同力+计算不同风阻)+说明神经网络情况+把IDM和CACC作为baseline<br>
5.Result:<br>
(3)提供了MAPPO可以作为未来的baseline；<br>
   局部稳定性:每一辆车都能根据自己的控制系统，稳定地跟踪目标速度和位置。(就是每辆车都能控制好自己)；<br>
   string stability:整个车队在行驶过程中，误差不会沿着队列放大传播。(就是前面车减速1，后面都是1，不会2、3累加)<br>
# 多智能体RL
## 1.Why Does Hierarchy (Sometimes) Work So Well in Reinforcement Learning?(2019)--->http://arxiv.org/abs/1909.10618
层次结构的大多数优势，其实来自于更好的探索（exploration），而不是训练或表示上的简化。奖励稀疏、任务长、需要跨越多个阶段，适用层次结构。
## 2.Hierarchical reinforcement learning based energy management strategy for hybrid electric vehicle(2022)--->https://www.sciencedirect.com/science/article/pii/S0360544221019514
提出了优化能源消耗的分层RL方法(DRL-H)以解决HEV能耗问题，解决了稀疏奖励的问题。上层决定最优油耗率，使每个子条件达到最佳燃料。
## 3.COOR-PLT: A hierarchical control model for coordinating adaptive platoons of connected and autonomous vehicles at signal-free intersections based on deep reinforcement learning(2023)--->http://arxiv.org/abs/2207.07195
提出COOR-PLT双层RL，不过很奇怪的点是双层结构分别处理不同的问题，上层处理编队规模的控制，下层协调控制路口各个车队的交互避免死锁。首次尝试将自适应队列和协调控制进行联和。
## 4.Multi-Agent Deep Reinforcement Learning Cooperative Control Model for Autonomous Vehicle Merging into Platoon in Highway(2025)--->https://www.mdpi.com/2032-6653/16/4/225
提出MAMQPPO，上层（或第一层）利用最大 Q-值方法（DQN 风格）来选择离散动作，下层（或第二层）采用 PPO（近端策略优化）方法处理连续控制动作，同时采用 Actor-Critic 网络结构，在多智能体训练框架中实现协作控制。还是双层Actor-Critic结构分别负责AV agent和Plooting agent。首次将“AV 横纵控制”与“车队纵控＋间隙选择”整合在一个统一 MA-DRL 架构中，用于高速公路合流场景。
## 5.Hierarchical reinforcement learning-based traffic signal control(2025)--->https://www.nature.com/articles/s41598-025-18449-1
提出了一个名为 SHLight的分层强化学习（Hierarchical RL, HRL）方法，用于交通信号控制。主要分为两层，上层为经理层负责全局目标的控制，工人们则负责区域内的控制，采用中央训练、分散执行(CTDE)方法，辅助动作的双Actor-Critic融合机制，每层各一个。后续可以参考他的构建方法，尤其是双Actor-Critic方法。
# 电气化道路(ERS)
## 1. Electric road system technologies in Sweden Gaining experience from research and demo facilities(2020)
主要讲述耶夫勒堡地区用于山特维肯的示范设施和罗瑟斯贝格 Utvecklings AB （eRoadArlanda） 用于阿兰达的示范设施，说明瑞典当时所设计的ERS四个项目，对截止2020年的瑞典购买的4个ERS技术试点的综述。一共三种方式，架空线路、公路电轨、感应发电。其中架空线路最成熟。我认为公路电轨过于复杂不太可能，架空线路现在还不错，感应的话技术可能还需要进一步优化。
## 2.A Fundamental Analysis of the Impact on Traffic Assignment by Toll System of Electric Road System(2024)--->http://arxiv.org/abs/2402.07144
该研究分析了电气化道路系统（ERS）中收费制度（toll system）对交通分配（traffic assignment） 的影响，发现简单的收费模式可能导致总旅行时间、充电量和 ERS 利用率均未达最优化。说明了ERS 在交通流分配／费用体系中的影响。
## 3.A network design perspective on the adoption potential of electric road systems in early development stages(2025)--->https://www.sciencedirect.com/science/article/pii/S0306261924002708
考虑了卡车没有ERS可以行驶的距离、在ERS道路上行驶的最低距离、最大绕行去ERS的距离。双走廊在捕获的总运输流量的百分比方面优于集中网络，走廊捕获的行程连接了相距较远的区域。解释了为什么长途电动重卡要选择长廊类型的ERS。
## 4. Route optimization of battery electric vehicles using dynamic charging on electrified roads(2024)
(1)货物的安全是大多数运营商可能不喜欢在公共充电站为其车队充电的个原因，安装私人充电站在经济上并不是一个可行的选择。此外，绕道前往充电站和充电时间长会降低车辆和驾驶员的利用率并增加成本。<br>
(2)电动汽车可以行驶超过 2000 公里的距离而无需充电。我们的实验还表明，在大约 30% 至 40% 的道路上建立基础设施足以确保电动汽车的可靠通行。
(3)可以证明与电动汽车与ERS道路结合的可行性

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
# 电动卡车(可以不看)
## 1. Is electric truck a viable alternative to diesel truck in long-haul operation?(2024)
### 提出电动卡车在物流运输方面与原来汽油重卡的对比:
(1)提出具有协调充电计划的电动卡车路线和驾驶员调度问题(eTRDSP-CS)<br>
(2)缺少政策支持、缺乏高速公路的充电设施、前期成本高、充电慢影响效率<br>
(3)结果表明，虽然在州际高速公路上促进长途电动卡车运营在技术上是可行的，但即使在同步和最佳的时间表下，由于充电而导致的行程时间延长（16％至32％之间）以及高昂的初始采用成本仍然阻碍着运营商采用。另一方面，长途电动卡车比柴油卡车节能 43% 以上，这对环境可持续发展具有重大影响。
## 2.Advances in EV wireless charging technology – A systematic review and future trends(2024)
(1)提出WPT(无线充电)<br>
(2)对比传统插入式更方便
