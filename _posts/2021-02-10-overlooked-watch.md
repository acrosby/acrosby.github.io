---
layout: post
title:  "Overlooked Tools: 'watch'"
categories: ubuntu linux overlooked
tags: ubuntu linux watch command gnu bash
---

There many GNU/Linux command line tools that provide continuously updated statistics or information like `iotop`, `nload`, and `top`. However, it is often necessary to want to see the output of another simple command or complex chain of tools, updated in real-time.

`watch` is a Linux command that does just that, and by doing so, is incredibly useful for continuously monitoring the output of any Linux terminal command. Usage of the `watch` command is incredibly simple, as the following example monitoring the currently running `tsp` task in the task-spooler queue demonstrates.

```bash
watch "tsp | head"
```

By default, the output is usually updated every 2 seconds, but this can be configured with the `-n`/`--interval` argument (provided in seconds).

```bash
# Here return output every 30 minutes
watch -n 1800 "tsp | head"
```

To highlight any changes in the output, provide the `-d`/`--differences` argument.

```bash
# Highlight if the running task has changed
watch -d  "tsp | head"
```

In addition to providing a terminal based ad-hoc dashboard solution, it can be used control the flow of a command string or shell script if so required. The `-g`/`--chgexit` will exit `watch` when the output of the command changes.

```bash
# Run second command (ls) when task-spooler started the next job.
watch -g "tsp | head" && tsp -t
```
