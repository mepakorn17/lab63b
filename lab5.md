# การทดลองที่ 5 เรื่อง การเขียนโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์
## วัตถุประสงค์
1. เพื่อศึกษาการสร้างเว็บเซอร์เวอร์ผ่านไวไฟ

2. เพื่อศึกษาการนำ Microcontroller ที่มีการเขียนโปรแกรมอยู่แล้วไปประยุกต์ใช้

## อุปกรณ์ที่ใช้
1. Microcontroller ESP01

2. คอมพิวเตอร์ หรือ โน้ตบุ๊ค

3. สาย USB เพื่อต่อไปยังอุปกรณ์ Serial

4. ตัวโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์

## ศึกษาข้อมูลเบื้องต้น
05 run wifi https://youtu.be/VX-QNQcO-b4

code 05 run_wifi https://github.com/choompol-boonmee/lab63b/blob/master/examples/05_Wifi-Web-Server/src/main.cpp

## วิธีการทำการทดลอง
1. เปิด cmd แล้วป้อนคำสั่ง cd pattani RUN จากนั้นป้อนคำสั่ง cd 05_Wifi-web-Server

2. ป้อนคำสั่ง vi src/main.cpp จะขึ้นโค้ดดังนี้

```
#include <ESP8266WiFi.h>
//#include <WiFiClient.h>
#include <ESP8266WebServer.h>
const char* ssid = "HI_BMFWIFI_2.4G";
const char* password = "0819110933";
ESP8266WebServer server(80);
int cnt = 0;
void setup(void){
	Serial.begin(115200);
	WiFi.mode(WIFI_STA);
	WiFi.begin(ssid, password);
	while (WiFi.status() != WL_CONNECTED) {
		delay(500);
		Serial.print(".");
	}
	Serial.print("\n\nIP address: ");
	Serial.println(WiFi.localIP());
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

3. เนื่องจากโปรแกรมเชื่อมต่อกับไวไฟดังนั้นต้องใส่ชื่อ wifi ที่เรียกว่า ssid และ password ก่อน ตัวโปรแกรมจะแบ่งออกเป็น 2 ส่วนได้แก่

set up จะเป็นการเชื่อมต่อกับไวไฟที่เราทำการป้อนลงไป และหลังจากนั้นจะ set up ตัวเน็ตเซิร์ฟเวอร์ จะส่งผลลัพธ์ออกมาเป็น Hello แล้วจะนับ count +1 ขึ้นเรื่อยๆ

loop

4. นำ Microcontoller เสียบไปที่  usb to serial

ทำการกดปุ่มดำเพื่ออัพโหลด และกดปุ่มข้างๆเพื่อทำการ reset

![image](https://user-images.githubusercontent.com/80879791/112331837-dbeede00-8ceb-11eb-844d-ba958e6cccd9.png)

5. ใช้เว็บ browser ในการแสดงผลลัพธ์

6. โดยการให้ copy ip address ไป browser ในการทดสอบแล้วบันทึกผล

## การบันทึกผลการทดลอง

จะเห็นว่าจากคำสั่ง pio device monitor เพื่อดูผลลัพธ์ของการ RUN โปรแกรมใน Microcontroller จะได้ตัว ip address เป็นตัวเดิม และเมื่อ copy ip address ไปที่บราวเซอร์ก็จะป็น Hello 1 โดย count ก็จะเปลี่ยนตัวแปรไปเรื่อย ๆ

## อภิปรายผลการทดลอง

จากการทดลอง RUN โปรแกรมด้วย Microcontroller สามารถสรุปได้ว่า สามารถนำ  Microcontroller เชื่อมต่อไวไฟและเว็บเซิร์ฟเวอร์ ซึ่งจะสามารถทำงานได้เหมือนเว็บเซิร์ฟเวอร์ปกติทั่วไป

## คำถามหลังการทดลอง
-

