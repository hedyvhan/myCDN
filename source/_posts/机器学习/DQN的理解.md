---
title: DQN的理解
date: '2021-06-16 19:58'
tags:
  - RL
  - DQN
categories: 机器学习
abbrlink: 15472
---
<meta name="referrer" content="no-referrer" />

# DQN的流程

[DQN的理解和代码示例1](https://blog.csdn.net/bbbeoy/article/details/79081337?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522162372350016780265495447%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=162372350016780265495447&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_v2~rank_v29-2-79081337.nonecase&utm_term=Deep+Q-Network+%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%EF%BC%88%E4%B8%80%EF%BC%89&spm=1018.2226.3001.4450)

[DQN的理解和代码示例2](https://blog.csdn.net/bbbeoy/article/details/79081130?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522162372299416780269876952%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=162372299416780269876952&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_v2~rank_v29-1-79081130.nonecase&utm_term=Deep+Q-Network+%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%EF%BC%88%E4%B8%80%EF%BC%89&spm=1018.2226.3001.4450)

![](https://raw.githubusercontent.com/hedyvhan/Pictrue/master/img/202310122314159.png)

![](https://raw.githubusercontent.com/hedyvhan/Pictrue/master/img/202310122314120.png)

假设从经验池中随机取出数据：

（s1,a1,r1,s2,False）,

（s7,a7,r7,s8,False），

(s18,a18,r18,s19,Flase)。

- 目标值网络这边：在第一条数据中，把下一状态s2输出到神经网络中，将输出该状态下，各个动作对应的Q值，记作Q1_next。比如Q1_next=（0.5，0.6，0.9，0.2），意思是s2状态下执行a1的Q值为0.5，执行a2的Q值为0.6，执行a3的Q值为0.9，执行a4的Q值为0.2。这对应着第一张图目标值网络对应的输出。
- 当前值网络这边：第一条数据中，把当前状态s1输入当前值网络，也会输出该状态下各个动作对应的Q值，然后通过贪婪策略选择Q值最大的那一个动作作为a1，图一中最大的Q值记为Q(s, a; θ)，图二中记为Q(ai) 。这和  当前网络与环境交互时选择动作  是吻合的。
- DQN误差函数里面：首先计算Q1_target = r1 + gama*Max(Q1_next) ，然后计算loss_1 =(   Q1_target - Q1(s, a; θ)   )^2。进而梯度下降方向传播来更新网络参数 θ。
- 同样，将第二条、第三条的下一状态都输入目标值网络，得到相应的Q7_next, Q18_next。
- ......

