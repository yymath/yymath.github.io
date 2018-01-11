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

## 3. Linux Spin Lock Limitation proof
This is a simple proof to some limitations to Linux Spin Lock mechanism:

When k cores are either using or queued on, the lock, corresponding arrival rate is: <img src="https://yymath.github.io/img/spinlock_f1.PNG.pdf" alt="Linux Spin Lock Limitation f1">
<img src="https://yymath.github.io/img/linux_spin_lock_1.pdf" alt="Linux Spin Lock Limitation"  width="4200" height="42000">
<img src="https://yymath.github.io/img/linux_spin_lock_2.pdf" alt="Linux Spin Lock Limitation"  width="4200" height="42000">
<p id="end"></p>