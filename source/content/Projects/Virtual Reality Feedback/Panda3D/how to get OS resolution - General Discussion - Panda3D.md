---
title: "how to get OS resolution? - General Discussion - Panda3D"
source: "https://discourse.panda3d.org/t/how-to-get-os-resolution/13628"
author:
  - "[[Thaumaturge]]"
published: 2019-03-04
created: 2025-02-26
description: "I’m attempting to implement a simple approach to switching to- and from- fullscreen mode, based on the suggestion given here. Unfortunately, while it appears to work well in the menu, it acts up somewhat once gameplay b&hellip;"
tags:
  - "clippings"
---
How to get the resolution of the OS to set fullscreen properly?

```python
screen_h=base.pipe.getDisplayHeight()
screen_w=base.pipe.getDisplayWidth()
```

Weird situation, I can call loadPrcFileData(’’, ‘win-size 1366 768’) only before creating a ShowBase instance, but I need to know the screen resolution by base.pipe before doing that to set the fullscreen resolution properly. What to do?

==Set window-type to ‘none’ to avoid automatically opening a window, and manually call base.makeDefaultPipe() to open the graphics pipe, after which you can query the resolution. Then you can just open the window using base.openDefaultWindow(size=(123, 456)).==