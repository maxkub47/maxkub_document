---
sidebar_position: 10
title: (Infra) Software Architecture Design
---
Software Architecture Design
ในการออกแบบซอฟต์แวร์ขนาดใหญ่ในองค์กร มักจะมีการทำงานร่วมกันโดยคนจำนวนมาก หากเราต่างคนต่างเขียนซอฟต์แวร์ไปในทางที่ตัวเองเห็นว่าดี ซอฟต์แวร์ที่แต่ละคนทำก็อาจจะทำงานร่วมกันไม่ได้หรือมีปัญหาตอนที่ Integrate เป็น Solution ใหญ่

ดังนั้น การทำซอฟต์แวร์ในระดับนั้นจึงจำเป็นต้องมีการแบ่งสันปันส่วน และมีการออกแบบโครงสร้างเพื่อให้ทำงานร่วมกันได้ดีและมองเห็นภาพรวมไปในทางเดียวกัน ทั้งระหว่างนักพัฒนาในทีมพัฒนากันเอง และระหว่างทีมพัฒนาและทีมธุรกิจ รวมไปถึงทีมอื่นๆที่เกี่ยวข้อง นอกจากนี้หลังพัฒนาเสร็จยังต้องสามารถดูแลต่อได้ทั้งงานซัพพอร์ต แก้ไขปัญหาบั๊ก และการพัฒนาต่อยอดเพิ่มเติมได้ในอนาคต

ในคอร์สนี้เราจะพูดถึง Software Architecture Pattern พื้นฐานที่นิยมใช้ในการออกแบบซอฟต์แวร์ขนาดใหญ่ โดยเน้นไปที่เรื่องของรูปแบบการร่วมมือ (Collaboration Pattern) ต่างๆ ตั้งแต่

- Specialist Collaboration การออกแบบโครงสร้างทำงานร่วมกันของทีม Software Developer หลากหลายส่วน เช่น Frontend, Backend, Database และส่วนอื่นๆ เป็นต้น
- Business Collaboration การออกแบบโครงสร้างล้อไปตาม Business model ขององค์กร
- Organization Collaboration การออกแบบโครงสร้างสำหรับองค์กรขนาดใหญ่ที่มีหลายทีมทำงานร่วมกันโดยไม่ขัดแย้งกัน

โดยพูดถึง ข้อดี-ข้อเสีย ประโยชน์และจุดประสงค์ของแต่ละ Pattern เพื่อให้ผู้เรียนเข้าใจหลักการของแต่ละแบบ และสามารถนำไปเลือกใช้ได้ตรงกับงานและโมเดลขององค์กรได้ ประกอบการสอนด้วยวิดีโอการจำลองสถานการณ์ที่เกิดขึ้นในการทำงานจริง และ Case Study ต่างๆ แทรกประกอบตลอดบทเรียน

### Introduction

| ตอนที่  | หัวข้อ                               | วีดีโอ                           |
|:---:  |------------------------------------ |:-----------------------------: |
| 1     | Welcome to Class                    | [https://youtu.be/Dn7qxv_AZUw] |
| 2     | Introduction to Organize a Codebase | [https://youtu.be/yx0PZzDe8m0] |

**Download Doc** : [Material](./Document/Infra_software-architecture-design/Material.pdf)

### Specialist Collaboration

| ตอนที่  | หัวข้อ                               | วีดีโอ                           |
|:---:  |------------------------------------ |:-----------------------------: |
| 1     | N-Tier Architecture                 |  [https://youtu.be/70r7J1nTlhk]|
| 2     | Demystify N-Tier Benefits           |  [https://youtu.be/rpFCFn23F9k]|
| 3     | Security                 |  [https://youtu.be/Az9IdkM3ZeY]|
| 4     | Easy to Manage                 |  [https://youtu.be/-BMXlaVnVAY]|
| 5     | Scalability                 |  [https://youtu.be/EXHF4dXXPMw]|
| 6     | Recap                 |  []|
| 7     | Requirements                 |  []|
| 8     | What is MVC ?                 |  []|
| 9     | Applying MVC                 |  []|
| 10    | Requirements                 |  []|
| 11    | What is Clean Architecture ?                 |  []|
| 12    | Applying Clean Architecture                 |  []|
| 13    | When We Go Clean ?                 |  []|
| 14    | Recap                 |  []|

### Business Collaboration

| ตอนที่  | หัวข้อ                               | วีดีโอ                           |
|:---:  |------------------------------------ |:-----------------------------: |
| 1     | Introduction|[]|
| 2     | What is Domain Driven Design|[]|
| 3     | Three level of Domain Driven Design|[]|
| 4     | Bounded Context and Ubiquitous Language|[]|
| 5     | Drawing Bounded Context|[]|
| 6     | Tactical DDD: Entity and Value Object (1)|[]|
| 7     | Tactical DDD: Entity and Value Object (2)|[]|
| 8     | Tactical DDD: Aggregate|[]|
| 9     | Tactical DDD: Service|[]|
| 10    | Tactical DDD: Domain Event|[]|
| 11    | Recap|[]|
| 12    | [Bonus] Connecting the Specialist to the Business|[]|

### Organization Collaboration

| ตอนที่  | หัวข้อ                               | วีดีโอ                           |
|:---:  |------------------------------------ |:-----------------------------: |
| 1     | Introduction |[]|
| 2     | Conway's Law |[]|
| 3     | Cross-Functional Team |[]|
| 4     | Monolith |[]|
| 5     | SoA and Microservices|[]|
| 6     | Differences between SOA and Microservices|[]|
| 7     | Design Service Boundary|[]|
| 8     | Recap|[]|
