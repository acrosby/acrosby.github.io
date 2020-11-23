---
layout: post
title:  "Overlooked Tools: task-spooler"
categories: ubuntu linux overlooked
tags: ubuntu linux ts tsp command queue
---

Sometimes sophisticated job queue and cluster systems are overkill on office or individual PCs, especially for long lists of batch processing jobs that use comparatively few resources.

Use task-spooler to queue commands on Linux and control the number of simultaneous jobs for an easy way to parallelize a list of batch jobs! This tool is a great complement to some other command line workhorses like `at` and `batch`.

Task-spooler is not usually installed by default on Linux systems. It can be built by scratch after getting the source from [https://vicerveza.homeunix.net/~viric/soft/ts/](https://vicerveza.homeunix.net/~viric/soft/ts/) or on Ubuntu (maybe other Debian based OS's) you can use apt:

```bash
sudo apt-get install task-spooler
```

See the running, queued and completed or errors jobs just by calling `tsp` (on Ubuntu) or `ts` (if built from scratch). Add a command job to the queue by calling with arguments.

```bash
tsp bash myscript1.sh
tsp bash myscript2.sh
```

You can change the number of simultaneous jobs by calling `tsp -S NJOBS`, and there are some basic commands for prioritizing jobs (`ts -u`) and killing/removing jobs (`tsp -r`/`tsp -k`). By default each user has access to their own queue(s), so they are not shared system-wide. Just pile tasks into the queue, and rest assured that your hardware is being used to its full potential.
