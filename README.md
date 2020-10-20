# b460m-pro4 OC0.62
HTTP://5438.XYZ
交流群:156235723

镜像:黑果小兵10.15.6（尽管可以使用gibMacOS制作在线安装版U盘，但是因为在线安装太慢了。完整的原版镜像又得在MAC下制作，所以推荐使用小兵的镜像,省事。还是双EFI带OC和优启动双引导）

EFI文件说明

使用opencore6.2制作

ACPI补丁：

1.10代主板都原生支持NVRAM所以无需SSDT-PMC.aml

2.此主板无需SSDT-EC.aml补丁(使用ssdtime提取并编译,查找关键字PNP0C09)

3.增加操作系统补丁SSDT-OC-XOSI.dsl(opencore是全局引导,在这主板上如果使用opencore引导WINDOWS会导致,win系统下设备管理器出现一个不能识别的USB通用设备) 参考资料:https://github.com/daliansky/OC-little/tree/master/04-%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F%E8%A1%A5%E4%B8%81

4.增加SSDT-AWAC.aml(不打此补丁 安装会卡住 来自SSTD GITHUB仓库 具体地址可以见我一个文章)   SSDT-PLUG.aml(使用ssdtime提取)

5.增加引导主题：

复制Resources到OC目录,Misc-Boot-PickerMode值设置为External（GUI模式）    默认是Builtin(文本模式)



config配置部分

1.在windows下使用ProperTree，参考opencore官方说明 根据CPU平台 调整Booter-Quirks下参数(每代CPU配置都有点不一样,这里配置不对会导致安装卡住)

2.Misc-Security-Vault 值设置为Optional（此操作必须，不然不这是安装还是启动都会卡）

3.声卡驱动

声音驱动比较简单,根据自己的声卡芯片型号查看ID，
layout-id 03000000

4.核显驱动 使用HD630仿冒ID,设置显存为2048M
AAPL,ig-platform-id 07009B3E
device-id 9B3E0000
framebuffer-patch-enable  01000000
framebuffer-unifiedmem  00000080
​
5.usb驱动

直接使用USBInjectAll.kext即可，也可以自己定制(可以参考司波图的视频教程,最早看黑果小兵的看的人好累。。)

6.关于网卡

每次写黑苹果的都会唠叨两句，

正常人推荐：M2网卡第一选择就是94360CS2(网卡120以内可以买 正向转接卡20  反向转接卡30)

PCI网卡选择94360CD,94360CD价格在150内可以买，相比300块的943602CDP使用无区别

勤俭持家推荐：如果100块钱也觉的贵就买35块钱的943224PCIEBT2,这张网卡我自己买来测过。10.14前据说是免驱动 10.14后WIFI部分需要加入驱动。

土豪推荐:你觉的转接麻烦 M2空间也不够  那么DW1560 DW1830也是可以的  这两款我没用过 因为太贵了

不推荐 使用下来也比1820A 这是一块神奇的网卡 尽管有小部人表示用的挺好，但我能力有限 折腾结果就是不中用还贵
