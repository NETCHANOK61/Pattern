# 📏1. Design Patterns vs Anti-patterns
## A. Design Patterns
คือแนวคิดวิธีการในแก้ปัญหาที่มักจะเจอในการออกแบบซอฟต์แวร์ ประกาศโดย **Gang of Four (GoF)**
design pattern แบ่งออกได้เป็น 3 กลุ่มประกอบด้วยตามวัตถุประสงค์ในการแก้ไขปัญหา
1.**Creational patterns** – เป็นกลุ่มที่ไว้ใช้สร้าง object ในรูปแบบต่างๆ ให้มีความยืดหยุ่น(flexible) และนำโค้ดมาใช้ซ้ำ(reuse)ได้
2.**Structural patterns** – กลุ่มนี้จะเป็นวิธีการนำ object และ class มาใช้งานร่วมกัน สร้างเป็นโครงสร้างที่มีความซับซ้อนยิ่งขึ้น โดยที่ยังมีความยืดหยุ่นและทำงานได้อย่างมีประสิทธิภาพ
3.**Behavioral patterns** – เป็นวิธีการออกแบบการติดต่อกันระกว่าง object ให้มีความยืดหยุ่นและสามารถติดต่อกันกันได้อย่างไม่มีปัญหา
### ✔️ ข้อดี
- ทำให้แก้ปัญหาที่ตรงกับdesign patternอันใดอันหนึ่งได้รวดเร็ว
- เมื่อเกิดปัญหาในการออกแบบซอฟต์แวร์ สามารเอา pattern มาแก้ปัญหาได้เลย
- สามารถแก้ปัญหา requirement ที่มีความซับซ้อนได้
- ลดการเกิด coupling, โค้ดยืดหยุ่นขึ้น, โค้ดนำกลับมาใช้ใหม่ได้
### ❌ ข้อเสีย
- เข้าใจยากสำหรับ developer มือใหม่
- เกิดความซับซ้อนที่เกิดความจำเป็น เมื่อไม่ได้คิดก่อนใช้

## B.Anti-patterns 
คือแนวคิดที่ตรงข้ามกับ design pattern โดยสิ้นเชิง โดย **anti-pattern** จะเน้นการทำงานที่ให้ได้ผลลัพธ์ด้วยการให้ความสำคัญกับปฎิบัติ 
หรือ การ coding เป็นหลัก ด้วยเหตุผลที่ไม่ต้องการเสียเวลาในการปรับ ทำความเข้าใจ หรือ ประยุกต์ใช้ pattern ให้เข้ากับโปรเจ็คที่กำลังพัฒนา
### ✔️ ข้อดีของ anti-patterns
- สามารถทำงานได้เร็วขึ้นแทนการใช้เวลาศึกษาการใช้design pattern ในบางส่วนที่ไม่จำเป็น
- มีความยืดหยุ่น สามารถปรับโปรแกรมให้เหมาะกับการทำงานบางอย่างได้ดี
### ❌ ข้อเสีย
- ขาดการออกแบบที่เป็นระบบ
- Code ขาดมาตรฐานทำให้อาจเกิดความสับสน และ ยากต่อการดูแลรักษา 
- เสียเวลาในการทำความเข้าใจ สำหรับผู้ที่เข้ามาพัฒนาต่อ

## สรุป 
- Anti-pattern เหมาะสำหรับโปรเจ็คที่มีขนาดไม่ใหญ่มาก มีการทำงานบางอย่างที่ไม่จำเป็นต้องใช้ design pattern หรือ ใช้ design pattern แล้วส่งผลให้กระบวนการทำงานบางอย่างติดขัด แต่ในขณะเดียวกัน Design pattern ก็สามารถเอามาปรับใช้ กับปัญหาบางอย่างที่ design นั้นๆตอบโจทย์ และ ช่วยให้การทำงานส่วนนั้นใช้เวลาน้อยลงได้

การใช้ design pattern ในส่วนที่ไม่จำเป็น 
การใช้ singleton ควบคุมการสร้าง object ที่ใช้ทรัพยากรสูง จึงทำให้เกิดปัญหาในการเขียน test แทนเนื่องจากไม่สามารถสร้าง object ตัวนั้นๆขึ้นมา test ได้
แต่ถ้าเรานำ singleton pattern ไปใช้ในการสร้างโปรเจ็คด้าน API ก็จะสามารถช่วยในการสร้าง instant เริ่มต้นได้ // เหมือนเป็นตัวที่ให้ user ใช้ แทนที่จะผล่อยให้ implements ไปใช้เอง

---
# 👻 2. Singleton Pattern
Creational Design Pattern ที่มีคุณสมบัติหลัก คือ
1. จำกัดการสร้าง instance หรือ instantiation ของคลาส เพื่อให้แน่ใจมีเพียง instace เดียวของคลาสที่ถูกสร้างขึ้น
2. ต้องสามารถเข้าถึงได้สาธารณะสำหรับการเอา instance ของคลาส
โดยจุดประสงค์เพื่อลดการสร้าง instance ที่มีการใช้ทรัพยากรโดยไม่จำเป็น
## ควรใช้ singleton pattern ตอนไหน
 - ตอนที่ต้องการควบคุมการสร้าง objectบางตัว ที่ไม่ต้องการให้มีการทำซ้ำ เช่น object ที่มีการใช้งานทีละตัวแต่อาจเกิดการสร้างซ้ำหลายๆตัวโดยยังไม่ได้ทำลายตัวเก่าทิ้ง จะทำให้เกิดการใช้ทรัพยากรเกินความจำเป็น
![sigleton](https://sourcemaking.com/files/v2/content/patterns/singleton1-2x.png)


---
# 🏊  4. Object Pool Pattern
คือ Creational patterns ช่วยในการออกแบบเมื่อจะสร้าง Object ชนิดเดียวกันจำนวนมากๆ 
โดยทั่วไป Object pool คือก็คือที่เก็บ Object เมื่อ Object ถูกนำออกไปใช้ Object นั้นจะไม่สามารถใช้ได้ใน pool จนกว่าจะนำกลับมา
ซึ่ง Object ใน Pool จะมีวงจรชีวิตดังนี้   
- Creation
- Validation
- Destroy
![Ex](https://media.geeksforgeeks.org/wp-content/uploads/uml-pool-design.jpg)
- Clicent : คลาสที่ต้องการใช้ object
- ObjectPool : คลาสที่เก็บ list ของ Object ที่มีอยู่ และพร้อมใช้งาน ซึ่ง Clicent จะสื่อสารกับคลาสนี้เพื่อเช็คว่าตอนนี้ใน Pool มี Object ที่ต้องใช้
- ReusablePool : คลาสที่มีความจำกัดในการสร้าง หรือมีความจำกัดในการพร้อมใช้ ดังนั้นจึงจะต้องจัดเอาไว้ใน object pool

### ✔️ ข้อดี
-มีการเพิ่มประสิทธิภาพ
- จัดการการเชื่อมต่อและจัดหาวิธีการใช้ซ้ำและแบ่งปัน
- รูปแบบนี้จะใช้เมื่ออัตราการเริ่มต้น instance ของคลาสสูง

---
# 🙀 5. Functional Programming 
เป็น paradigm หนึ่งสำหรับการเขียนโปรแกรม โดยพัฒนามาจาก Lambda calculus  ซึ่งหลายเราอาจจะคุ้นเคยกับ paradigm อื่นอย่างเช่น 
object-oriented programming
## “Pure Function” 
การเขียนโปรแกรมแบบ functional นั้น เน้นไปที่การใช้ Pure Function  
### `(1) รับ input  → (2) นำ input มา operate →  (3) return ผลลัพธ์ออกไป`

### 📍ตัวอย่าง
```
function add(x, y) {
   return x + y;
}

```
สิ่งสำคัญที่สุดของ Functional Programming นั้น คือการลด **"side effect"** ที่เกิดจาก function ที่เขียนขึ้นมา  
ดังนั้นจึงต้องหลีกเลี่ยงการใช้ **"Shared state"** และ **"Mutable Data"** เพื่อป้องกันการเปลี่ยนแปลงของข้อมูล จะได้ไม่เกิดปัญหาตามมา

### ✔️ ข้อดี ของ Function Programming
- มีชื่อเสียงในเรื่อง high-level abstractions เพราะมันซ่อนรายละเอียดของ Routine operations อย่างเรื่องของ Iterating ไว้ ทำให้ Code สั้นลง และมี Errors เล็กน้อยที่พอจะสามารถยอมรับได้
- เนื่องจากภาษาและ Structure ที่มีความยืดหยุ่น มันจึงช่วยให้ Functional Programming Developer เข้าใกล้ปัญหาได้มากขึ้น นอกจากนี้มันยังมี Tools ที่ทั้งใหม่และน่าสนใจสำหรับการแก้ปัญหาที่ซับซ้อน ซึ่ง OOP Developers มักจะละเลยไป
- ช่วยให้สามารถเขียน Code ได้อย่างถูกต้อง และรวดเร็ว อีกทั้งการ Test และ Debug ก็ทำได้สะดวกขึ้น

### ❌ ข้อเสีย ของ Function Programming
- ไม่มี Vocabulary ที่มีประสิทธิภาพสำหรับ Functional Languages โดย Purely Functional Vocabularies ทำงานช้ากว่า  Hash tables และมันก็สร้างปัญหาในบาง Applications ได้ สำหรับ Developer ส่วนใหญ่แล้ว ไม่ค่อยมีใครสังเกตเห็นข้อบกพร่องนี้
- ไม่เหมาะสำหรับ Algorithm ในงานเกี่ยวกับ Graph เนื่องจากมันทำงานได้ช้า




