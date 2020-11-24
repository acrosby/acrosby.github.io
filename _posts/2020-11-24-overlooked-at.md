---
layout: post
title:  "Overlooked Tools: 'at'"
categories: ubuntu linux overlooked
tags: ubuntu linux at command batch schedule gnu
---

If you find you are using commands like `sleep` to run a one-off task at a specific time, then meet the GNU `at` command.

`at` will allow you to specify a time to run a specific command, and accepts a wide range of different formats including "now + 4 hours", "noon", and "next tuesday". The command will read commands from stdin or using the `-f` to specifiy a file to be executed using the default `/bin/sh`.

One can find a great summary of the command's use and available formats for time specification at the link [here](https://www.computerhope.com/unix/uat.htm).

Once a job has been scheduled, the list of pending jobs can be listed with `atq`, and a job can be removed with `atrm` followed by a job ID.