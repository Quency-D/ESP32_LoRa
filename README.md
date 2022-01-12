# DIY电子工牌
## 开发环境搭建
1. [搭建Arduino开发环境。](https://heltec-automation.readthedocs.io/zh_CN/latest/general/how_to_install_git_and_arduino.html)   
2. [安装开发框架。](https://heltec-automation.readthedocs.io/zh_CN/latest/esp32/quick_start.html#git)   
3. 用 [boards.txt](./data_decode/boards.txt) 替换**Arduino\hardware\heltec\esp32** 文件夹下的 boards.txt。
## 使用演示
### 开发板基本使用
1. 打开 **LoRaWan_CLASS_A_wakeOverTheAir.ino** 示例，并按照图片进行配置。![配置示例图](./img/配置图片.png)
2. 连接上串口之后，点击下载，把需要运行的程序下载进去。
3. 如果提示需要license，打开对应[网址](http://resource.heltec.cn/search),查询并输入即可。
4. 正常运行之后，串口会打印 **Within 10 seconds, send any data to the serial port and enter the configuration mode.** 在10S内向串口发送任何数据，都可以进入配置模式。如果不发送，等10S之后，就会进入正常运行。（程序只有在复位之后的第一次运行才会等待10S，后面不会再次等待。）
5. 进入配置模式之后，可以按照一下格式，对下面三项参数进行配置。
>- dev_eui=2232330000888801
>- app_key=88888888888888888888888888886601
>- qrcode_info={"DeviceName":"e_link","ProductId":"WR00ATPGRU","Signature":"a83aaa9708a54790ae020dfa809ca998"}
6. 配置完成之后，复位即可正常进行使用。
### 使用腾讯连连进行远程控制
1. 参看 [LoRaWAN开发文档](https://cloud.tencent.com/document/product/1081/52426) 在腾讯云服务器上面添加网关和节点信息。
2. 将[物模型json文件](./decode/decode.json)，导入物模型。如图![导入物模型](./img/导入物模型.png)
3. 将[数据解析文件](./data_decode/decode.js)内容，复制到下行数据解析栏。如图：![下行数据解析](./img/下行数据解析.png)
4. 在小程序面板配置界面，选择H5自定义面板，并把[JS文件](./data_decode/SummitInfo_panel-default.c1a671ab6c.js)和[CSS文件](./data_decode/1_SummitInfo_panel-default.8a85310b27.css)导入到相对应的位置。
5. 在微信里面打开腾讯连连小程序，扫描腾讯云网页上面的二维码![二维码](./img/扫描二维码.png)进入腾讯连连小程序的下发界面。![腾讯连连小程序界面](./img/腾讯连连小程序界面.jpg)在连接lora 入网之后，就可以进行下发，并显示到墨水屏上面了。   
注：也可以把上面的二维码解析出来，然后通过串口配置，显示到墨水屏上面。然后再使用腾讯连连小程序进行扫描。