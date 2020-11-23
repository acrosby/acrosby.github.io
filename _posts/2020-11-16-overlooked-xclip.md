---
layout: post
title:  "Overlooked Tools: xclip"
categories: ubuntu linux overlooked
tags: ubuntu linux xclip command clipboard
---

If you have ever had a need to move the output of a Linux console command to your clipboard, `xclip` is the solution!

To copy a file's contents to the standard "ctl+c/v" clipboard buffer issue you can following this command:

```bash
xclip -sel clip your-file-path
```

The most useful feature is reading from a stdin pipe:

```bash
head my-file-path | xclip -sel clip
```

...and then your ready to paste into an email or Slack chat.

This functionality is especially useful for programatically providing 2-factor authentication tokens to command-line or browser based logins!
