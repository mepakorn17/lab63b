# การทดลองที่ 3 เรื่อง การเขียนโปรแกรมเอ้าพุทสัญญาณดิจิทัล
## วัตถุประสงค์
1. เพื่อเป็นการ RUN โปรแกรมบน Microcontroller เกี่ยวกับการ output สัญญาณไปภายนอก

2. เพื่อศึกษาการนำ Microcontroller ที่มีการเขียนโปรแกรมอยู่แล้วไปประยุกต์ใช้

## อุปกรณ์ที่ใช้ 
1. Microcontroller ESP01

2. คอมพิวเตอร์ หรือ โน้ตบุ๊ค

3. สาย USB เพื่อต่อไปยังอุปกรณ์ Serial

4. adepter สำหรับเสียบผ่านพอท 0,1 

5. รีเรย์

6. ขั้วชาร์ต

7. ตัวโปรแกรม output สัญญาณ

## ศึกษาข้อมูลเบื้องต้น
03 run relay https://www.youtube.com/watch?v=6JnhaUILGuw

03 run example https://www.youtube.com/watch?v=CCnN1WJsXQY

code 03 Output-Port https://github.com/choompol-boonmee/lab63b/blob/master/examples/03_Output-Port/src/main.cpp

## วิธีการทำการทดลอง
1. เชื่อมต่อ usb to Serial กับสาย adapter พอท 0,1 และต่อ Micorcontroller เข้าไปด้านบนดังรูป

![image](https://user-images.githubusercontent.com/80879791/112317588-ca530980-8cde-11eb-9aed-4e7f8c37bf7a.png)

2. เปิด cmd ใช้คำสั่งซึ่งจากตัวอย่างอยู่ในโฟล์เดอร์ pattani ใช้คำสั่ง cd แล้วใช้คำสั่ง cd 03_Output-Port

3. ป้อนคำสั่ง vi src/main.cpp จะขึ้นโค้ดดังนี้

```
#include <Arduino.h>
#include <ESP8266WiFi.h>
int cnt = 0;
void setup()
{
	Serial.begin(115200);
	pinMode(0, OUTPUT);
	Serial.println("\n\n\n");
}
void loop()
{
	cnt++;
	if(cnt % 2) {
		Serial.println("========== ON ===========");
		digitalWrite(0, HIGH);
	} else {
		Serial.println("========== OFF ===========");
		digitalWrite(0, LOW);
	}
	delay(500);
}
```

โปรแกรมจะทำหน้าที่ให้ พอท 0 pinmode เป็นพอท output โดยเมื่อ count เป็นเลขคู่โปรแกรมจะส่งค่า off ไปที่พอท 0 ถ้าโปรแกรมเป็นเลขคี่จะส่งค่า on ไปที่พอท 0

4. ทำการอัพโหลดโปรแกรมด้วยคำสั่ง pio run -t upload

5. ทำการกดปุ่มดำเพื่ออัพโหลด และกดปุ่มข้างๆเพื่อทำการ reset

6. สามารถดุูผลการอัพโหลดได้จากคำสั่ง pio device monitor

![image](https://user-images.githubusercontent.com/80879791/112318847-12266080-8ce0-11eb-86f7-16e0decec052.png)

จะเห็นได้ว่าทุกๆครึ่งวินาทีจะขึ้น ON OFF โดยไป LED ส่องสว่างจะเปล่งแสงออกมาตอนเป็น ON 

7. ต่อมานำ รีเรย์ เสียบเข้ากับ Mitrocontroller

8. และนำไปต่อกัยขั้วชาร์ตดพื่อเป็นการจ่ายไฟให้กับ Microcontroller

![image](https://user-images.githubusercontent.com/80879791/112319620-d6d86180-8ce0-11eb-8e46-35270732ae53.png)

จะเป็นการควบคุม รีเรย์ ON OFF ON OFF 

## การบันทึกผลการทดลอง
1. การเขียนโปรแกรมด้วย output พอท โปรแกรมจะทำหน้าที่ให้ พอท 0 pinmode เป็นพอท output โดยเมื่อ count เป็นเลขคู่โปรแกรมจะส่งค่า off ไปที่พอท 0 ถ้าโปรแกรมเป็นเลขคี่จะส่งค่า on ไปที่พอท 0 ในทุกๆครึ่งวินาที

2. เมื่อนำรีเรย์และขั้วชาร์ตมาต่อกับ Microcontroller จะเห็นได้ว่ามีเสีนงสัญญาณส่งออกมาเมื่อไฟ ON OFF เสียงที่ได้ยินเกิดจากหน้าสัมผัสของสวิตช์ไฟฟ้าที่เป็นโลหะ

## อภิปรายผลการทดลอง
จากการทดลองนี้เห็นได้ว่าเมื่อเราทำการอัพโหลดโปรแกรม 03 Output-Port ลงใน Microcontoller และสั่งคำสั่ง pio device monitor เพื่อสังเกตุผลลัพธ์ในการทำงานของ Microcontroller หน้าจอจะปรากฎ on และ off ทุกครึ่งวินาที และไฟจาก LED จะปรากฏตามที่หน้าจอปรากฏ เมื่อสังเกตหลอดไฟ LED ที่พอร์ต 0 จะสว่าง และดับตามคำสั่ง ON OFF ตามโปรแกรมที่เราอัพโหลด เมื่อนำ Microcontroller นี้ไปต่อกับรีเรย์เห็นได้ว่ารีเรย์จะ ON OFF สวิตช์สอดคล้องกับโค้ดที่เราอัพโหลดไว้

## คำถามหลังการทดลอง 
_
