### V1.0
**1. 本项目是基于[homebridge-creskit](https://github.com/marcusadolfsson/homebridge-creskit)进行二次开发的。**

**2. 修改了event事件中的setValue->updateValue。避免重复发值给快思聪。**

**3. 删除了部分Get事件中的event提交请求（部分有所保留，要更新其状态，因为有的配件获取到的值传不到homebridge）**

**4. 删除set事件中的匹配机制，因为我发现根本没必要了**

# 使用教程
#### 硬件准备
1. 树莓派（最好买一个套件，装过系统的）
2. 一套快思聪系统

#### 软件准备
1. 为树莓派安装系统（已安装的请忽略）。。。。请自行百度
2. 搭建homebridge环境[教程](https://github.com/nfarina/homebridge/wiki/Running-HomeBridge-on-a-Raspberry-Pi),    **本人亲测，可以使用**
3. 打开终端输入    `sudo npm install -g homebridge-creskit2`
4. 配置`config.json` 
  - ` sudo nano /home/pi/.homebridge/config.json`
复制以下内容，然后ctrl+o 回车 ctrl+x
```
{
    "bridge": {
        "name": "Creskit",
        "username": "CC:22:3D:E3:CE:32",
        "port": 51826,
        "pin": "031-45-154"
    },

    "platforms": [
    {
      "platform": "CresKit",
      "name": "CresKit",
      "host": "192.168.5.22", // IP Address of Crestron System
      "port": "50001", // Match Port specified in Modue

      "accessories":[
        {
          "id":1,
          "type":"Lightbulb",
          "name":"Marcus Sidelight"
        },
        {
          "id":2,
          "type":"Lightbulb",
          "name":"Casey Sidelight"
        },
        {
          "id":3,
          "type":"Lightbulb",
          "name":"Bathroom"
        },
        {
          "id":1,
          "type":"Switch",
          "name":"Good Night Scene" 
        }

      ]
    }
  ]
}
```
- 在终端中输入`homebridge`
- 根据错误解决问题
- error conected 查看config.json中的快思聪主机IP和Port对不对，快思聪程序要先上传
- json文件格式有误，[json文件格式验证](https://jsonlint.com/)
- 成功后会出现一个二维码，打开IOS设备，选择家庭-添加配件-扫描二维码-确认添加
- 打开toolbox进行测试
- 成功后，可自行查阅源码，进行自定义修改


#### 其他信息
**QQ Group:** 107927710















# It‘s based on [homebridge-creskit](https://github.com/marcusadolfsson/homebridge-creskit)

### QQ Group 107927710 

CresKit (together with Homebridge) turns Creston controlled devices into HomeKit accessories, enabling you to control many functions using Siri and the iOS 10 Home app. 


It is an early prototype, but functional. It requires you to install a Homebridge on an appropriate server before continuing. I use a $20 RaspberryPi, using this [tutorial](https://github.com/nfarina/homebridge/wiki/Running-HomeBridge-on-a-Raspberry-Pi).
 
HomeKit accessories are supported:

- Lights (dimming is enabled)
- Switches (can also be used to for Creston Scenes)
- Garage Doors
- Alarm
- Thermostat
- Shades
- Various Sensors
- Door Locks
- Airpurifier
- Valve


In Homebridge's config.json file you specify the accessories you want to enable, and link the appropiate Crestron signals via the included SIMPL+ Module (only tested on MC3). You can then use the iOS 10 Home app to tie the accessories to rooms and groups.

On the Crestron side, the SIMPL+ Module acts as a basic TCP Server and communicates using three type of commands:

- Set (Controls Crestron from Homebridge)
- Get (Requests Crestron status from Homebridge)
- Event (Push Crestron status changes to Homebridge)

More to come!

**Crestron Modules is a sample Simple reference，You can customize it according to your needs.**

## Development document

[install-homebridge-RaspberryPi](https://github.com/nfarina/homebridge/wiki/Running-HomeBridge-on-a-Raspberry-Pi).

[homebridge-creskit](https://github.com/marcusadolfsson/homebridge-creskit).

[homebridge](https://github.com/nfarina/homebridge).

[homekit-types](https://github.com/KhaosT/HAP-NodeJS/blob/master/lib/gen/HomeKitTypes.js).

[homekit-Characteristic](https://github.com/KhaosT/HAP-NodeJS/blob/master/lib/Characteristic.js).

[homebridge 多开+自启](https://github.com/nfarina/homebridge/issues/2054) .

