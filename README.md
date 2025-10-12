# Literature-review(public)
# 最终目的:让自动驾驶电动卡车在存在电气化公路（ERS）的环境中，自主决定“何时走ERS路段 / 何时编队 / 何时独行 / 何时充电”，以最小化能耗 + 行程时间 + 充电次数。
# GVRP
## 1.A Green Vehicle Routing Problem(2012)
(1)提出两种方法the Modified Clarke and Wright Savings heuristic and the Density-Based Clustering Algorithm<br>
(2)图扩展技巧(补能站多次访问):建立虚拟顶点<br>
(3)1.一类车辆路径问题的概念化，涉及加油能力有限和加油站可用性有限的车辆；<br>
   2. 开发和测试用于解决大型现实世界问题实例的有效启发法，包括在燃料消耗和补充时跟踪燃料水平的具体步骤，以及通过在途中选择性地访问非唯一加油站来延长车辆的距离限制；
   3.深入了解站点和客户的地理分布对运营可行性的影响；<br>
   4.鉴于当前可用的车辆技术和有限的支持基础设施部署，支持机构减少碳足迹的工具。
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
