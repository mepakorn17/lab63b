# การทดลองที่ 6 เรื่อง การเขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์ (Wifi AP)

## วัตถุประสงค์ 
เพื่อสามารถสร้าง wifi AP ขึ้นมาเองได้

## อุปกรณ์ที่ใช้
1. Microcontroller ESP01

2. คอมพิวเตอร์ หรือ โน้ตบุ๊ค

3. สาย USB เพื่อต่อไปยังอุปกรณ์ Serial

4. ตัวสร้างไวไฟแอคเซสพอยต์ 

## ศึกษาข้อมูลเบื้องต้น
06 run wifi AP https://youtu.be/T26DVHePlTs

code 06_Wifi-AP-Web-Server : https://github.com/choompol-boonmee/lab63b/blob/master/examples/06_Wifi-AP-Web-Server/src/main.cpp

## วิธีการทำการทดลอง
1. เปิด cmd แล้วป้อนคำสั่ง cd pattani RUN จากนั้นป้อนคำสั่ง cd 06_Wifi-AP-Web-Server

2. ป้อนคำสั่ง vi src/main.cpp จะขึ้นโค้ดดังนี้

```
#include <ESP8266WiFi.h>
//#include <WiFiClient.h>
#include <ESP8266WebServer.h>
const char* ssid = "MY-ESP8266";
const char* password = "choompol";
IPAddress local_ip(192, 168, 1, 1);
IPAddress gateway(192, 168, 1, 1);
IPAddress subnet(255, 255, 255, 0);
ESP8266WebServer server(80);
int cnt = 0;
void setup(void){
	Serial.begin(115200);
	WiFi.softAP(ssid, password);
	WiFi.softAPConfig(local_ip, gateway, subnet);
	delay(100);
	server.onNotFound([]() {
		server.send(404, "text/plain", "Path Not Found");
	});
	server.on("/", []() {
		cnt++;
		String msg = "Hello cnt: ";
		msg += cnt;
		server.send(200, "text/plain", msg);
	});
	server.begin();
	Serial.println("HTTP server started");
}
void loop(void){
  server.handleClient();
}
```

3. โดยทำการตั้งชื่อ wifi และ password

4. ทำการกำหนด IPAddress local gateway และ subnet 

![image](https://user-images.githubusercontent.com/80879791/112335580-f1b1d280-8cee-11eb-9c76-23c41c39eafe.png)

5. ป้อนคำสั่งการอัพโหลดโปรแกรมเข้า Microcontoller ด้วยคำสั่ง pio run -t upload

6. ทำการกดปุ่มดำเพื่ออัพโหลด และกดปุ่มข้างๆเพื่อทำการ reset

7. สามารถดุูผลการอัพโหลดได้จากคำสั่ง pio device monitor

8. สามารถทดสอบได้จากการใช้โทรศัพท์มือถือหรือคอมพิวเตอร์ในการค้นหา wifi 

![image](https://user-images.githubusercontent.com/80879791/112336619-d0051b00-8cef-11eb-9d7d-0f23287c7e0c.png)

## การบันทึกผลการทดลอง
เราสามารถสร้างไวไฟได้จากการ RUN โปรแกรม cd 06_Wifi-AP-Web-Server เมื่อหน้าจอที่สั่งคำสั่งpio device monitorแสดงผลลัพธ์ server started เราจะสามารถตรวจสอบผลลัพธ์ การสร้างไวไฟด้วยการค้นหาชื่อไวไฟด้วย โทรศัพท์มือถือหรือคอมพิวเตอร์ ซึ่งจากการค้นหาด้วยโทรศัพท์มือถือก็ได้พบกับไวไฟที่ได้สร้างจากการเขียนโปรแกรมมี user name และ password ตรงกับที่สร้างไว้ในการ Run โปรแกรม

## อภิปรายผลการทดลอง
จากการทดลองโปรแกรมสามารถสรุปได้ว่า เราสามารถสร้างไวไฟแอคแซสพอยต์ขึ้นมาเองได้

## คำถามหลังจากการทดลอง
-
