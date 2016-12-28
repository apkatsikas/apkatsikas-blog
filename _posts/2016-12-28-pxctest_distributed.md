---
layout: post
title:  "pxctest - distributed, headless runs in Python"
date:   2016-12-28 00:00:00
tags: ['iOS', 'pxctest', 'python', 'xctest', 'parallel', 'simultaneous', 'tests', 'test', 'testing', 'ui', 'simulators', 'swift', 'distributed']
author: "Andrew Katsikas"
---

# pxctest - distributed, headless runs in Python

I wanted to run Swift/xctests in parallel, in a distributed fashion (AKA sharding). Johannes Plunien and Toshihiro Suzuki have provided an amazing start with pxctest - https://github.com/plu/pxctest

However, their frameworks accomodates those who want to run ALL tests against each node (e.g. 10 tests, 10 run on iPad, 10 run on iPhone).

I wanted to run 10 tests, 5 on one iPad, 5 on another iPad to speed up throughput. Additionally, I wanted to be able to run my tests while working in Xcode/the simulator.

The result of this need is a Python script and JSON file. I hope this will help other people who want to do the same.

https://github.com/apkatsikas/xctest_pxctest_distributed

### Instructions
1. install pxctest - ``brew tap plu/pxctest && brew install pxctest --HEAD``
2. clone my repo - ``git clone https://github.com/apkatsikas/xctest_pxctest_distributed ``
3. edit ios_tests.json - see JSON Instructions
4. run the python file ``python ios_parallel.py``
5. see your results at ``./project/sim_devices/{"number of sim device"}/target/iOS version/ios device/junit.xml``

### JSON Instructions
1. modify "number_of_simulators" to your desired count. On my beefy machine, 3 was the max I could pull off.
2. modiy "directory" to your desired directory where the repo will be cloned/simulators build etc.
3. modify "clone_statement" to the URL of your git repo
4. modify "checkout branch" to the branch you want to test against"
5. modify "project string" to your project string
6. modify all occurences of 'name=iPad Air 2,os=iOS 10.2' to your expected device string
7. modify occurences of -scheme 'project' and -workspace 'project.workspace' and -destination 'platform=iOS Simulator,name=iPad Air 2,OS=10.2' to your expected values
8. modify occurence of \"project_iphonesimulator10.2-x86_64.xctestrun\" to your output device name
9. modify occurence of "--only 'uitests%s' to your test target string
