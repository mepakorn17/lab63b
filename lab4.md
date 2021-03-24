# การทดลองที่ 4 เรื่อง การเขียนโปรแกรมอินพุทสัญญาณดิจิทัล
## วัตถุประสงค์
1. เพื่อเป็นการ input สัญญาณภายนอกเข้า Microcontroller 

2. เพื่อศึกษาการนำ Microcontroller ที่มีการเขียนโปรแกรมอยู่แล้วไปประยุกต์ใช้

## อุปกรณ์ที่ใช้ 
1. Microcontroller ESP01

2. คอมพิวเตอร์ หรือ โน้ตบุ๊ค

3. สาย USB เพื่อต่อไปยังอุปกรณ์ Serial

4. adepter สำหรับเสียบผ่านพอท 0,1

5. CPU

6. หลอดไฟ LED

7. ตัวโปรแกรม output สัญญาณ

8. ตัว senser แสง

## ศึกษาข้อมูลเบื้องต้น

04 run example 4 https://youtu.be/nFqoZT26U5k

code 04 Input-Port : https://github.com/choompol-boonmee/lab63b/blob/master/examples/04_Input-Port/src/main.cpp

## วิธีทำการทดลอง
1. เชื่อมต่อ usb to Serial กับสาย adapter พอท 0,1 และต่อ Micorcontroller เข้าไปด้านบนดังรูป

![image](https://user-images.githubusercontent.com/80879791/112323675-967ae280-8ce4-11eb-8546-d49725e42249.png)

2. เปิด cmd แล้วป้อนคำสั่ง cd pattani RUN จากนั้นป้อนคำสั่ง cd 04_Input-Port

3. ป้อนคำสั่ง vi src/main.cpp จะขึ้นโค้ดดังนี้

```
#include <Arduino.h>
#include <ESP8266WiFi.h>
int cnt = 0;
void setup()
{
	Serial.begin(115200);
	pinMode(0, INPUT);
	pinMode(2, OUTPUT);
	Serial.println("\n\n\n");
}
void loop()
{
	int val = digitalRead(0);
	Serial.printf("======= read %d\n", val);
	if(val==1) {
		digitalWrite(2, LOW);
	} else {
		digitalWrite(2, HIGH);
	}
	delay(100);
}
```

4. ทำการกดปุ่มดำเพื่ออัพโหลด และกดปุ่มข้างๆเพื่อทำการ reset

5. สามารถดุูผลการอัพโหลดได้จากคำสั่ง pio device monitor

![image](https://user-images.githubusercontent.com/80879791/112324782-b959c680-8ce5-11eb-9f9c-dac8223fb648.png)

เห็นได้ว่าค่าที่อ่านได้ คือ 1 ไฟ LED จึงติดตลอดเวลา

โดยจะเช็คจากพอท 0 ว่ามีการทำงานหรือไม่ ถ้า input คือ 0 ไฟ LED จะติดที่พอท 2 ถ้า input คือ 1 LED จะไม่ติด 

6. นำสายไฟเส้นสีขาว คือ พอท 0 จิ้มไปที่ 0 V เพื่อให้สัญญาณ output เป็น 0 ทำให้ไฟติดดังภาพ 

![image](https://user-images.githubusercontent.com/80879791/112325427-40a73a00-8ce6-11eb-82bb-aa1a3c7effa3.png)

7. เมื่อกดปุ่มสีดำข้างๆปุ่ม Reset ไฟ LED จะติดดังภาพ 

![image](https://user-images.githubusercontent.com/80879791/112325859-9ed41d00-8ce6-11eb-85c6-54805b0247b2.png)

8. นำ senser แสงที่ต่อกับตัวต้านทานกับไฟเลี่ยง 3 V เส้นสีแดง แล้วต่อเข้าพอท 0 ดังรูป

![image](https://user-images.githubusercontent.com/80879791/112326463-1efa8280-8ce7-11eb-8fe9-c10fa4bb526f.png)
 
 ต่อสายสีขาวกับ senser ขากลาง
 
9. หน้า senser เมื่อไม่ถูกปิดจะอ่านค่า = 0 แล้วไฟ LED จะส่องสว่าง ดังภาพ 

![image](https://user-images.githubusercontent.com/80879791/112326913-89abbe00-8ce7-11eb-8fe3-ae2117f6d1bb.png)

10. หน้า senser เมื่อถูกปิดจะอ่านค่า = 1 แล้วไฟ LED จะไม่สว่าง ดังภาพ 

![image](https://user-images.githubusercontent.com/80879791/112327092-b65fd580-8ce7-11eb-9d94-647cf27d948d.png)

## การบันทึกผลการทดลอง
1. อัพโหลด Microcontroller ด้วยโปรแกรม 04_Input-Port

เห็นได้ว่าจากคำสั่ง pio device monitor ได้ผลว่า read 1 input คือ 1 ทำให้เป็นไฟดับใน ที่พอร์ท 2

นำสายไฟเส้นสีขาว คือ พอท 0 จิ้มไปที่ 0 V ทำให้เป็น  ไฟติด นำสายไฟเส้นสีขาว คือ พอท 0 จิ้มไปที่ 0 V 1 ทำให้เป็น  ไฟดับ

กดปุ่มสีดำ ข้างปุ่ม reset แสดงผลลัพธ์ 0 ทำให้เป็น  ไฟติด ปล่อยปุ่ม ข้างปุ่ม reset แสดงผลลัพธ์ 1 ทำให้เป็น  ไฟดับ

2.การนำตัว Microcontroller ที่ลงโปรแกรมแล้ว มาประยุกต์ใช้ต่อกับตัวเซนเซอร์แสง จะเห็นว่าเมื่อ หน้า senser เมื่อไม่ถูกปิดจะอ่านค่า = 0 แล้วไฟ LED จะส่องสว่าง และเมื่อหน้า senser เมื่อถูกปิดจะอ่านค่า = 1 แล้วไฟ LED จะไม่สว่าง

## อภิปรายผลการทดลอง 
จากการทดลองการRUNโปรแกรม สามารถสรุปได้ว่า สัญญาณอินพุทจากพอร์ท 0 คือตัวควบคุมให้ไฟเปิดหรือปิด ถ้าแสดงผลลัพธ์ 1 ไฟดับ ถ้าแสดงผลลัพธ์ 0 ไฟติด โดยจะดูไฟที่พอท 2

และอีกการทดลองที่นำเซนเซอร์แสงมาต่อเข้ากับ Microcontroller ที่เขียนโปรแกรทแล้ว โดยเมื่อบังแสง จะเห็นว่าเมื่อ หน้า senser เมื่อไม่ถูกปิดจะอ่านค่า = 0 แล้วไฟ LED จะส่องสว่าง และเมื่อหน้า senser เมื่อถูกปิดจะอ่านค่า = 1 แล้วไฟ LED จะไม่สว่าง

## คำถามหลังการทดลอง 
-
