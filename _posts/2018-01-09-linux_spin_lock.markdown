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
When k cores are either using or queued on, the lock, corresponding arrival rate is: <img src="https://yymath.github.io/img/spinlock_f1.PNG" alt="Linux Spin Lock Limitation f1"> for 0 <= k <= n-1
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

### Step 5

<p id="end"></p>