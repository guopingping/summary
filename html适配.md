HTML适配

```
1、dpr
    device pixel ratio 设置像素比
    = 物理像素/设备独立像素

2、获取设备dpr
    js：
        window.devicePixelRatio
    Css:
        -webkit-device-pixel-ratio
        -webkit-min-device-pixel-ratio
        -webkit-max-device-pixel-ratio

3、rem单位
    相对于根标签html的大小

4、屏幕尺寸、屏幕分辨率、屏幕像素密度
    屏幕尺寸：
            屏幕对角线的长度，单位是英寸，1英寸=2.54cm
    屏幕分辨率：
            在横纵向上的像素点数，单位px；
    屏幕像素密度/像素密度/屏幕密度：
            屏幕上每英寸可以显示的像素点的数量，单位是ppi；
    
    物理像素，CSS像素
        设备像素/物理像素
        CSS像素
        。。。

屏幕适配方案：

    简单版：
        屏幕适配（windowWidth/设计稿宽*100）
        font-size：手机deviceWidth与设计稿比值的100倍；
    手淘H5适配库flexible.js：
        淘宝lib-flexible库

    @media
        设置rem
        1rem=100px
        initial-scale：设置缩小效果

        1vw=1/100th viewport width
        1vh=1/100th viewport height

        

```