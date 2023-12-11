---
title: yuv转png命令
date: 2023-12-12 00:47:43
tags:
category:
---

```
ffmpeg -s 640x480  -i image.yuv  image.png
```

- -s 宽x高、图像实际大小
- -i 输入文件 `yuv` 格式
- 输出文件  `.png` 输出图像格式
