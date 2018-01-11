---
layout:     post
title:      "Linux Spin Lock Limitation"
subtitle:   "Linux Spin Lock Limitation Simple Proof"
date:       2018-01-07 16:15:00
author:     "yymath"
header-img: "img/post-bg-os-metro.jpg"
catalog: true
tags:
    - Linux Spin Lock
---

## Linux Spin Lock Limitation proof
This is a simple proof to some limitations to Linux Spin Lock mechanism:
### Step 1
When k cores are either using or queued on, the lock, corresponding arrival rate is: ![alt text](https://yymath.github.io/img/spinlock_f1.PNG) for 0 <= k <= n-1
Average cache-update time is proportional to the half of the total number of cores queued on the lock. Then we have the completion rate (output rate): <img src="https://yymath.github.io/img/spinlock_f2.PNG" alt="Linux Spin Lock Limitation f2"> for 1 <= k <= n

### Step 2
Transition from state k is equal to the transition into the state k when the system is at the equilibrium. Then the general relationship (closed-form) between state k and state k+1 is: <img src="https://yymath.github.io/img/spinlock_f3.PNG" alt="Linux Spin Lock Limitation f3"> Therefore: <img src="https://yymath.github.io/img/spinlock_f4.PNG" alt="Linux Spin Lock Limitation f4">
which gives the general solution for state k in terms of probability of state 0. Since the total probability of all states is 1, where: <img src="https://yymath.github.io/img/spinlock_f5.PNG" alt="Linux Spin Lock Limitation f5">

Total population N (the mean number of cores either using or waiting for the lock) is: <img src="https://yymath.github.io/img/spinlock_f6.PNG" alt="Linux Spin Lock Limitation f6">

By definition, throughput is the product of completion rate multiplied by the probability of each state, which is also equal to the product of the arrival rate multiplied by corresponding probabilities: <img src="https://yymath.github.io/img/spinlock_f7.PNG" alt="Linux Spin Lock Limitation f7">

According to the Little’s Law: <img src="https://yymath.github.io/img/spinlock_f8.PNG" alt="Linux Spin Lock Limitation f8"> Hence, the queuing time and the service time have the relationship: <img src="https://yymath.github.io/img/spinlock_f9.PNG" alt="Linux Spin Lock Limitation f9">

### Step 3
From the coursework specification, "speed-up" can be expressed by: Speedup = n − N
Figure 1.1 and Figure 1.2 show the queuing time and speed-up against number of cores with different t𝑥.
<img src="https://yymath.github.io/img/spinlock_p1.PNG" alt="Linux Spin Lock Limitation p1">

### Step 4
For an ideal ticket spinlock, completion rate becomes: <img src="https://yymath.github.io/img/spinlock_f10.PNG" alt="Linux Spin Lock Limitation f10"> for 1 <= k <=n
Corresponding speed-up with different number of cores are shown in Figure 1.3 (using the same equation for "speedup" and completion rate). The population is illustrated in Figure 2.2.
completion rate: <img src="https://yymath.github.io/img/spinlock_f11.PNG" alt="Linux Spin Lock Limitation f11">

### Step 5
Collapse in the speed-up was observed in Figures 1.2 due to the average number of either executing or waiting cores (N) has been increasing faster than number of cores (n) itself. The main reason is the cache consistency which is assumed to be the bottle-neck of the spinlock tickets model. This is due to the fact that time to update every locally-cached copy of shared memory takes <img src="https://yymath.github.io/img/spinlock_f12.PNG" alt="Linux Spin Lock Limitation f12"> in average, hence it directly depends on number of cores executing or waiting at the moment. Thus, the more cores are waiting, the more time it takes to acquire the lock and vice versa (the more time it takes to acquire the lock the more cores will be waiting). The vicious cycle leads to the collapse in the speed-up. This means that adding additional cores to the process can result in steep decrease in performance instead of increasing it, as it seen in Figure 1.2.
In Figure 1.1, at t𝑥=300 μs, a small hump can be observed. This hump actually corresponds to the speed-up collapse.
Figure 2.1 demonstrates five throughput plots according to t𝑥 values of 100, 200, 300, 400 and 500μs. It can be clearly seen that the exact number of cores corresponding to the following collapse becomes higher as t𝑥 increases.
As it can be seen in Figure 1.2 and Figure 1.3 whether ideal spinlock gives linear speed-up or not, clearly depends on the number of cores and parameters t𝑥, tc, tu. However, it is not a "perfectly" linear speed-up at any point. As it is demonstrated on the Figure 2.2, the population N is not constant, therefore the speed-up n-N apparently is not "perfectly" linear as n. Obviously, after certain point, increase in average number of cores either waiting or executing (N) becomes equal to increase in number of cores itself (n). At this point previously linear speed up hits the presumably never-ending plateau. According to approximation done as a part of this coursework the plateau occurs after number of
<p id="end"></p>