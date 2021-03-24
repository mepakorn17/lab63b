# การทดลองที่ 2 เรื่อง การเขียนโปรแกรมค้นหาไวไฟ

## วัตถุประสงค์
1. เพื่อศึกษาเกี่ยวกับการสแกน wifi รอบๆ Microcontroller

2.เพื่อศึกษาการ RUN โปรแกรมบน Microcontroller 

## อุปกรณ์ที่ใช้
1. คอมพิวเตอร์ หรือ โน้ตบุ๊ค

2. Microcontroller ที่ชื่่อว่า ESP01

3. สาย USB เพื่อต่อไปยังอุปกรณ์ Serial

4. เสา wifi

## ศึกษาข้อมูลเบื้องต้น
02 run example 2 https://youtu.be/yBjab0UNuB8

code 02_scan-wifi https://github.com/choompol-boonmee/lab63b/blob/master/examples/02_Scan-Wifi/platformio.ini

## วิธีการทำการทดลอง
1. ทำการเชื่อมต่อ Microcontroller เข้ากับ Serial

2. เปิด cmd เพื่อสั่งคำสั่ง 1s RUN แล้วตามด้วยคำสั่ง vi src/main.cpp จากนั้นจะขึ้นโปรแกรมมา 2 ส่วน ดังนี้

```
#include <Arduino.h>
#include <ESP8266WiFi.h>
int cnt = 0;
void setup()
{
	Serial.begin(115200);
	WiFi.mode(WIFI_STA);
	WiFi.disconnect();
	delay(100);
	Serial.println("\n\n\n");
}
void loop()
{
	Serial.println("========== เริ่มต้นแสกนหา Wifi ===========");
	int n = WiFi.scanNetworks();
	if(n == 0) {
		Serial.println("NO NETWORK FOUND");
	} else {
		for(int i=0; i<n; i++) {
			Serial.print(i + 1);
			Serial.print(": ");
			Serial.print(WiFi.SSID(i));
			Serial.print(" (");Serial.print(WiFi.RSSI(i));
			Serial.println(")");
			delay(10);
		}
	}
	Serial.println("\n\n");
}
```

3. ใช้คำสั่ง pio run -t upload เพื่อทำการอัพโหลดโปรแกรมเข้าสู่ Microcontroller โดยการกดปุ่มสีดำ แล้วกดปุ่มด้านข้างเพื่อเป็นการ reset 

4. เมื่อโปรแกรมถูกอัพโหลดเสร็จสิ้นให้ใช้คำสั่ง pio device moniter เพื่อเป็นการแสกนค้นหา wifi

![image](https://user-images.githubusercontent.com/80879791/112308546-d76afb00-8cd4-11eb-8d68-ab2c7d34ef35.png)

5. หากกดปุ่ม reset ใหม่อีกครั้งก็จะเป็นการเริ่มค้นหา wifi ใหม่

## การบันทึกผลการทดลอง
จากการใช้คำสั่ง pio device moniter เพื่อเป็นการแสกนค้นหา wifi ทำให้เราเจอ wifi ดังนี้

![image](https://user-images.githubusercontent.com/80879791/112308546-d76afb00-8cd4-11eb-8d68-ab2c7d34ef35.png)

## อภิปรายผลการทดลอง
เห็นได้ว่า จากการทดลองการเขียนโปรแกรมค้นหาไวไฟ เมื่อเราทำการอัพโหลดโปรแกรมลงใน Microcontroller และใช้คำสั่ง pio device monitor เพื่อเป็นการแสกนค้นหา wifi หน้าจอจะแสดงผล จำนวนและชื่อของwifiที่ตรวจพบทั้งหมดโดยอิงจากความแรงของสัญญาณ wifi นั้นๆ
