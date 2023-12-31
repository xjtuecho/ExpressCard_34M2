# ExpressCard_34M2

EC2M2: ExpressCard 34mm or 54mm to M.2 NVMe 2230 or 2242 SSD adapter card.

## 简介

ExpressCard详细介绍请参考[WikiPedia](https://en.wikipedia.org/wiki/ExpressCard)，这个接口提供了一条PCIe通道和一个USB2.0接口，以及3.3V电源。Sandy Bridge时代的笔记本普遍不具备USB3.0接口，所以ExpressCard接口的PCIe通道经常用来扩展USB3.0接口，由于ExpressCard接口只提供了3.3V电源，功率也不大，升压到5V以后功率进一步损失，这些ExpressCard的USB3.0扩展卡供电普遍不佳，不加外部供电的情况下，对外输出电流不超过1A，很难带动移动硬盘这样的大功率负载。

Ivy Bridge时代USB3.0接口成为笔记本标配，ExpressCard转USB3.0也逐渐失去了价值，这个接口逐渐被闲置。那个时代，硬盘的主流协议还是SATA，无论传统2.5寸还是小型化的mSATA，M.2接口那时候还叫作NGFF，协议也是SATA。随着时间的推移，NVMe逐渐成为主流，当前硬盘的主流已经是M.2接口2280外形NVMe协议，也有很多2230和2242外形的短硬盘，这些短硬盘可以完美放入34mm和54mm的ExpressCard卡，布局如下：

![正面背面实际图](image/230623-正面背面实际图.jpg "正面背面实际图")

![安装2230固态硬盘](image/230623-安装2230固态硬盘.jpg "安装2230固态硬盘")

![安装以后待固定](image/230623-安装以后待固定.jpg "安装以后待固定")

## 主要特征

- 支持2230和2242外形NVMe协议短硬盘
- 支持34mm和54mm两种ExpressCard外壳
- PCIe协议直连，无性能损失，不发热（SSD自身还是会发热的）
- 大板设计，强度高散热好
- 创新的M.2固定方式，不使用螺丝，降低总高度
- 带SSD工作指示灯，工作电流不足1mA，省电不刺眼
- 通过焊盘引出ExpressCard的USB 2.0接口

## 安装方法

安装步骤如下：

1. 揭开EC2M2卡2230或者2242位置的固定胶带，将SSD水平插入，然后使用胶带固定SSD尾部
2. 将EC2M2卡放入金属底壳，注意SSD那一面朝下放置
3. 盖上EC2M2卡金属上盖，保证两侧卡口完全咬合
4. 将安装完成的EC2M2卡推入笔记本的ExpressCard插槽，34mm版本注意不要插反

Win10系统无需驱动，Win7需要安装[KB2990941](driver/Win7_NVMe_Driver/x64/Windows6.1-KB2990941-v3-x64.msu)和[KB3087873](driver/Win7_NVMe_Driver/x64/Windows6.1-KB3087873-v2-x64.msu)两个补丁才能识别NVMe硬盘。由于微软的NVMe驱动限制，Win7下无法查看硬盘的SMART信息，Win8/8.1也有类似问题，Win10下一切正常，推荐使用Win10。

如果你的电脑比较老安装Win10有困难，或者对Win7情有独钟，想体验完整的NVMe固态硬盘也有办法，思路是使用第三方厂家比如三星或者Intel的NVMe驱动，安装这个[Intel NVMe驱动修改版](driver/Intel_Win7_NVMe_Driver_Mod)即可。该修改版驱动来自网友文章[关于Win7\8\8.1上NVMe固态读不到smart信息的解决方案参考](https://tieba.baidu.com/p/6365965925)，向作者表示感谢。如果Win7已经安装微软的NVMe驱动，这个驱动是无法安装的，需要先卸载`KB2990941`和`KB3087873`两个补丁，控制面板->卸载程序->查看已安装的更新，搜索两个补丁卸载后重启即可，无需按照原贴方法直接删改文件。

![SN520在X230上CDI信息](image/230620-SN520在X230上CDI信息.png "230620-SN520在X230上CDI信息")

安装好以后可以在CrystalDiskInfo中查看硬盘信息，SN520硬盘支持`PCIe 3.0x4`，但是X230的ExpressCard接口只支持`PCIe 2.0x1`，低速带来了更低的温度，同时对4K读写性能影响并不大。

## 性能测试

ExpressCard到NVMe协议SSD之间不存在协议转换，无性能损失。连续读写性能受PCIe协议版本本身限制，对用户体验影响更大的4K性能影响不大。以下为SN520在X230上使用EC2M2转接卡速度测试。
![SN520在X230上使用EC2M2转接卡速度测试](image/230620-SN520在X230上使用EC2M2转接卡速度测试.png "SN520在X230上使用EC2M2转接卡速度测试")

## 具备ExpressCard接口的笔记本

Intel三代CPU及之前的ThinkPad很多具备ExpressCard接口，大部分都是PCIe2.0x1协议，速度接近SATA3，可用性良好。Ivy Bridge后续机型大多数取消了ExpressCard接口，只有ThinkPad的P系列等少数机型保留了34mm的ExpressCard接口，得益于SkyLake架构升级，ExpressCard接口的PCIe协议也升级到了3.0x1，速度1GB/s，已经将SATA3远远甩在身后。

以下是具备ExpressCard接口的ThinkPad型号，欢迎补充。

- X200/X201，54mm
- X220(i)/X230(i)，54mm，PCIe 2.0x1
- T60(p)/T400，54mm，PCIe 1.0x1
- T420/T430(s)，34mm，PCIe 2.0x1
- W520/W530/W541，34mm，PCIe 2.0x1
- P50/P51/P70/P71，34mm，PCIe3.0x1

## 支持的SSD型号

理论上支持所有2230和2242外形的NVMe协议SSD，注意不支持SATA协议SSD(通常叫做NGFF)。相比2280外形的长硬盘，2230和2242外形的短硬盘型号要少的多，往往只有存储大厂以OEM形式提供，常见的型号如下，欢迎补充。

- 西数：SN520/SN530/SN740
- 东芝/铠侠：BG3/BG4/BG5/BG6
- 三星：PM971/PM971a/PM991/PM991a/PM9B1/PM9C1a
- SK海力士：BC501/BC511/BC711/BC901

这些短硬盘都是单面颗粒布局，容量分布在128GB/256GB/512GB/1TB/2TB之间，截至目前SN740有最大的2TB容量版本。

## 进阶玩法

### 裸PCBA直接安装

EC2M2转接卡使用USB转接卡外壳，尾部还留有USB的开口，不是十分美观，时间长了也容易有异物进入。笔记本的ExpressCard插槽有一个挡板，没有ExpressCard设备插入时这个挡板会盖住插槽的洞口。在不安装34mm或者54mm外壳的情况下，EC2M2转接卡也是可以直接安装的。使用一把镊子将挡板按下，将转接卡放入正确的位置，再使用另外一把镊子或者一字螺丝刀将转接卡压入即可，按压时能感觉到弹簧的弹力，按压到位以后听到"哒"的一声表明安装到位，将镊子松开以后挡板会自动复位封闭ExpressCard插槽的洞口。实测不安装金属外壳时，取出转接卡只能用镊子拔出，继续按压不会复位卡扣。想复位的话，只能压入另外一张带外壳的ExpressCard卡，然后按压以后取出。

安装要点：

- 关机断电操作，避免带电操作
- 使用高温胶带保护转接卡和SSD上的裸露金属，防止它们与ExpressCard插槽外壳接触短路。避免使用普通透明胶带和电工绝缘胶带，不耐高温，并且容易有残胶，非常难清理
- 取出转接卡只能用镊子拔出，继续按压不会复位ExpressCard插槽卡扣
- 复位ExpressCard插槽卡扣，只能压入另外一张带外壳的ExpressCard卡，然后按压以后取出
- 按压转接卡时使用一字螺丝刀按压PCB边沿，不要按压M.2插槽，避免损坏M.2插槽

### 扩展Logitech罗技鼠标接收器

除了PCIe，ExpressCard还提供了一个USB2.0接口，由于缺少5V供电，3.3V电压功率也不充裕，这个USB2.0接口不太适合外接使用，只能连接一些小功率的USB设备，比如罗技的优联接收器。EC2M2转接卡通过焊盘形式引出了USB接口，54mm宽度外壳也有足够的空间容纳优联接收器。

罗技鼠标接收器分为优联和非优联两种版本，优联可以支持六个设备，非优联可以支持一个设备，笔记本使用的接收器大多只是用来外接鼠标，因此无论是否优联接收器实际使用体验差别不大，通常非优联接收器价格更便宜。优联版本使用SetPoint软件配对，非优联版本使用ConnectUtility软件配对。配对以后使用无差别。

内置鼠标接收器的第一步是将接收器外壳拆掉，注意选择6mm宽度接收器，这种接收器使用PCB天线，PCB更薄。不要选择3mm的优联接收器，这种不是PCB天线，更厚，而且价格更高。拆掉以后在USB焊盘上焊接4条铜丝，铜丝推荐网线中的单股铜丝，它的强度适中，便于结构固定，也不会将PCB焊盘弄坏。

![焊接金属丝](image/230712-01-罗技接收器焊接金属丝.jpg "焊接金属丝")

将接收器焊接到EC2M2转接卡的USB焊盘上，焊盘距离是按照标准USB-A接口设计，注意方向，不要焊反。

![焊到USB焊盘](image/230712-02-焊到USB焊盘.jpg "焊到USB焊盘")
![焊到USB焊盘](image/230712-03-焊到USB焊盘.jpg "焊到USB焊盘")

放到54mm外壳中测试一下，尺寸刚刚好。

![放到54mm外壳](image/230712-04-放到54mm外壳.jpg "放到54mm外壳")

不过还是推荐裸PCB安装，下图是X230的ExpressCard插槽，可以看到插槽上是有开孔的，不会影响接收器的2.4G无线信号传输。

![插座孔不影响信号](image/230712-07-插座孔不影响信号.jpg "插座孔不影响信号")

裸PCB安装需要做好绝缘，使用高温胶带覆盖SSD和鼠标接收器上裸露的金属。图中SSD上的散热贴主要目的是增加转接卡厚度，让转接卡和顶壳更接近，避免阻挡ExpressCard接口挡板。

![高温胶带绝缘](image/230712-05-高温胶带绝缘.jpg "高温胶带绝缘")
![高温胶带绝缘](image/230712-06-高温胶带绝缘.jpg "高温胶带绝缘")

安装以后使用ConnectUtility软件配对接收器和鼠标，实测工作良好。对于X230这种具备3个USB-A接口的机型来说，节约一个USB-A口貌似意义不大，但是不用插USB接收器，机身少了一个高于6mm的突起，放在鼠标中携带时不容易被勾到，从这个角度来看内置接收器也是有意义的。

