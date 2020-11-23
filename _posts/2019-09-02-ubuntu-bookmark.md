---
layout: post
title:  "Shortcut to Website in Ubuntu 18.04 Dock"
categories: ubuntu linux
tags: ubuntu linux dock website shortcut
---

Create and populate the following file to add a dock shortcut to a website in Ubuntu using Ars Technica as an example. This will also enable the shortcut in the Gnome Shell search.

**~/.local/share/applications/MyWebsite.desktop**:
```
[Desktop Entry]
Comment=Ars Technica
Terminal=false
Name=Ars Technica
Exec=firefox https://arstechnica.com/
Type=Application
Icon=applications-internet
NoDisplay=false
```

To use Google Chrome instead, replace `firefox` with `google-chrome` if it is installed.
```
[Desktop Entry]
Comment=Ars Technica
Terminal=false
Name=Ars Technica
Exec=google-chrome https://arstechnica.com/
Type=Application
Icon=applications-internet
NoDisplay=false
```
