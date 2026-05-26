## **Density setting**

With different display resolutions, the suitable density value will be set to make display shows properly. Now density is set based on display resolution automatically. But if your display is still not correct (navigation bar may be displayed wrongly). Please adjust “Density value” by executing below commands:

```bash
# On Board's console, execute command:
$ su
$ wm density reset
$ wm density <Density value>
```

<div class="table-no-sort" markdown="1">
| Display Resolution | Density value (*) | Note |
| :--- | :---: | :--- |
| 640 x 480 (VGA) | 90 | |
| 800 x 600 (SVGA) | 110 | |
| 1024 x 600 | 120 | |
| 1024 x 768 (XGA) | 145 | |
| 1280 x 720 (HD) | 150 | |
| 1280 x 1024 (SXGA) | 200 | |
| 1920 x 1080 (Full-HD) | 200 | Max display resolution of RZ/V2H |
</div>

(\*) These density values are based on user experiment.

