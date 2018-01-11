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

### Step 1
This is a simple proof to some limitations to Linux Spin Lock mechanism:

When k cores are either using or queued on, the lock, corresponding arrival rate is: <img src="https://yymath.github.io/img/spinlock_f1.PNG" alt="Linux Spin Lock Limitation f1"> for 0 <= k <= n-1
Average cache-update time is proportional to the half of the total number of cores queued on the lock. Then we have the completion rate (output rate): <img src="https://yymath.github.io/img/spinlock_f2.PNG" alt="Linux Spin Lock Limitation f2"> for 1 <= k <= n

### Step 2
Transition from state k is equal to the transition into the state k when the system is at the equilibrium. Then the general relationship (closed-form) between state k and state k+1 is: <img src="https://yymath.github.io/img/spinlock_f3.PNG" alt="Linux Spin Lock Limitation f3"> Therefore: <img src="https://yymath.github.io/img/spinlock_f4.PNG" alt="Linux Spin Lock Limitation f4">
which gives the general solution for state k in terms of probability of state 0. Since the total probability of all states is 1, where: 
<img src="https://yymath.github.io/img/spinlock_f5.PNG" alt="Linux Spin Lock Limitation f5">

Total population N (the mean number of cores either using or waiting for the lock) is:

### Step 3

### Step 4

### Step 5

<img src="https://yymath.github.io/img/linux_spin_lock_1.pdf" alt="Linux Spin Lock Limitation"  width="4200" height="42000">
<img src="https://yymath.github.io/img/linux_spin_lock_2.pdf" alt="Linux Spin Lock Limitation"  width="4200" height="42000">
<p id="end"></p>