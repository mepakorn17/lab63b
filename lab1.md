# การทดลองที่ 1 เรื่อง การเขียนโปรแกรมเพื่อรันบนไมโครคอนโทรเลอร์
## วัตถุประสงค์
1. เพื่อศึกษาวิธีการทำงานเบื้องต้นของ Microcontroller

2. เพื่อศึกษาการเขียนโปรแกรม Microcontroller ด้วย Platform IO

3. เขียนโปรแกรมเพื่อทดสอบ Microcontroller
## อุปกรณ์ที่ใช้
1. Microcontroller ESP01

2. คอมพิวเตอร์ หรือ โน้ตบุ๊ค
 
3. สาย USB เพื่อต่อไปยังอุปกรณ์ Serial
## ศึกษาข้อมูลเบื้องต้น
01 run example 1 https://www.youtube.com/watch?v=NLIUsWLEpmg

code 01_Serial-Monitor https://github.com/choompol-boonmee/lab63b/blob/master/examples/01_Serial-Monitor/src/main.cpp
## วิธีการทำการทดลอง
1. ทำการเชื่อมต่อ Microcontroller เข้ากับ Serial

![image](https://user-images.githubusercontent.com/80879791/112302406-a2a77580-8ccd-11eb-9e05-37f03113dd6b.png)


2. ดูตัวอย่างโปรแกรมได้ที่โฟลเดอร์ pattani โดยใช้คำสั่ง CD เมื่อทำการรันโปรแกรมจะเห็นได้ว่ามีตัวอย่างอยู่ทั้งหมด 9 ตัวอย่าง

![image](https://user-images.githubusercontent.com/80879791/112302886-2eb99d00-8cce-11eb-894e-1e7c9633a405.png)

3. ใช้คำสั่ง cd 01_Serial-Monitor แล้วตามด้วย vi src/main.cpp จะแสดงโค้ดตัวอย่างโปรแกรมที่ใช้ในการทดสอบ Microcontroller

```
#include <Arduino.h>
int cnt = 0;
void setup()
{
	Serial.begin(115200);
}
void loop()
{
	cnt++;
	Serial.printf("PATTANI :%d\n",cnt);
	delay(1000);
}
```

4. ใช้คำสั่ง vi platformio.ini เพื่อจะบอกว่า Microcontroller นี้ บอกว่าเป็น Platform หรือ ผลิตภัณฑ์ของที่ใด Bord ชื่ออะไร เขียนโปรแกรมโดยวิธีการใด

5. ทำการอัปโหลดโปรแกรม 01 Serail moniter ได้จากคำสั่ง pio run -t upload

6. เพื่อให้ Microcontroller รับโปรแกรมใหม่เข้าไปให้กดที่ปุ่มสีดำ และกด set ที่ปุ่มด้านข้าง

![image](https://user-images.githubusercontent.com/80879791/112304149-bb188f80-8ccf-11eb-9f2f-eba04ba76a73.png)

7. หากโปรแกรมขึ้นแสดงผล SUCCESS หมายถึงโปรแกรมพร้อมในการ RUN โดยเราสามารถใช้คำสั่ง pio device moniter เพื่อดูผลลัพธ์ที่แสดงผลออกมาจากมอนิเตอร์

![image](https://user-images.githubusercontent.com/80879791/112304524-2c584280-8cd0-11eb-8e70-d216be7eb889.png)


## การบันทึกผลการทดลอง
จากการ RUN โดยใช้คำสั่ง vi platformio.ini ทำให้เราทราบข้อมูลดังนี้

![image](https://user-images.githubusercontent.com/80879791/112304922-a8eb2100-8cd0-11eb-9eea-f29676964df9.png)

1. Platform ชนิดนี้เป็นของบริษัท espressif8266

2. bord ชนิดนี้ชื่อว่า esp01_1m

3. framework วิธีที่ใช้เขียนโปรแกรมคือวิธี ardino

## อภิปรายผลการทดลอง
จากการใช้คำสั่ง vi src/main.cpp เป็นโปรแกรมเพื่อทดสอบ ทำให้เราทราบว่าโปรแกรม 01_Serial-Monitor สามารถ RUN ได้ 2 ส่วนดังนี้

1. ส่วนการ set up โปรแกรม

2. ส่วน loop ที่เพิ่มจะเพิ่มตัวแปร count ในแต่ละครั้งเพื่อแสดงผลของตัวแปรโดยมีการหน่วงเวลา 1 วินาที โดยการทดลองเมื่อใช้คำสั่ง pio device moniter โดยหน้าจอจะขึ้นว่ามีนับ count หรือนับขึ้นทุกๆ 1 วินาทีตามโปรแกรม

## คำถามหลังการทดลอง 

-

