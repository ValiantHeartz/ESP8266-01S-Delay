# ESP8266-01S-Delay
## 一、软件和库 
1、arduino安装
附加开发板管理地址：http://arduino.esp8266.com/stable/package_esp8266com_index.json 通过改地址更新获得8266 by community开发板信息，选择正确的com口即可 
2、blink点灯科技介入小爱同学 
代码示例 
```c 
#define BLINKER_WIFI
#define BLINKER_MIOT_LIGHT

#include <Blinker.h>
#define DELAY 0
char auth[] = "7fb0b5b567ab";
char ssid[] = "Xiaomi_FA52";
char pswd[] = "13696773255";

//// 新建组件对象
//BlinkerButton Button1("btn-abc");
//
//// 按下按键即会执行该函数
//void button1_callback(const String & state) {
//  BLINKER_LOG("get button state: ", state);
//  digitalWrite(DELAY, !digitalRead(LED_BUILTIN));
//  Blinker.vibrate();
//}

void miotPowerState(const String & state)
{
    BLINKER_LOG("need set power state: ", state);

    if (state == BLINKER_CMD_ON) {
        digitalWrite(DELAY, LOW);

        BlinkerMIOT.powerState("on");
        BlinkerMIOT.print();
    }
    else if (state == BLINKER_CMD_OFF) {
        digitalWrite(DELAY, HIGH);

        BlinkerMIOT.powerState("off");
        BlinkerMIOT.print();
    }
}

void setup() {
  // 初始化串口，并开启调试信息
  Serial.begin(115200);
  BLINKER_DEBUG.stream(Serial);
  // 初始化有LED的IO
  pinMode(DELAY, OUTPUT);
  digitalWrite(DELAY, HIGH);
  // 初始化blinker
  Blinker.begin(auth, ssid, pswd);
  //Button1.attach(button1_callback);
  // 注册回调函数
  BlinkerMIOT.attachPowerState(miotPowerState);
}

void loop() {
  Blinker.run();
}
```` 


