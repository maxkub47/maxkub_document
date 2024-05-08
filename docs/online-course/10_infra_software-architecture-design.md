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

| ตอนที่ | หัวข้อ                              |             วีดีโอ             |
| :----: | ----------------------------------- | :----------------------------: |
|   1    | Welcome to Class                    | [https://youtu.be/Dn7qxv_AZUw] |
|   2    | Introduction to Organize a Codebase | [https://youtu.be/yx0PZzDe8m0] |

**Download Doc** : [Material](./Document/Infra_software-architecture-design/Material.pdf)

### Specialist Collaboration

| ตอนที่ | หัวข้อ                       |             วีดีโอ             |
| :----: | ---------------------------- | :----------------------------: |
|   1    | N-Tier Architecture          | [https://youtu.be/70r7J1nTlhk] |
|   2    | Demystify N-Tier Benefits    | [https://youtu.be/rpFCFn23F9k] |
|   3    | Security                     | [https://youtu.be/Az9IdkM3ZeY] |
|   4    | Easy to Manage               | [https://youtu.be/-BMXlaVnVAY] |
|   5    | Scalability                  | [https://youtu.be/EXHF4dXXPMw] |
|   6    | Recap                        | [https://youtu.be/fozkF1ox4jw] |
|   7    | Requirements                 | [https://youtu.be/c0hfqJD7fYY] |
|   8    | What is MVC ?                | [https://youtu.be/PxtuLCiGD_Q] |
|   9    | Applying MVC                 | [https://youtu.be/LRfIUJUeHC0] |
|   10   | Requirements                 | [https://youtu.be/Y1RM9gpIGFs] |
|   11   | What is Clean Architecture ? | [https://youtu.be/z2FcFk4GoWU] |
|   12   | Applying Clean Architecture  | [https://youtu.be/1hfDrD2__jE] |
|   13   | When We Go Clean ?           | [https://youtu.be/wIUBEc-NhtI] |
|   14   | Recap                        | [https://youtu.be/vtRt0CCGE84] |

### Business Collaboration

| ตอนที่ | หัวข้อ                                            |             วีดีโอ             |
| :----: | ------------------------------------------------- | :----------------------------: |
|   1    | Introduction                                      | [https://youtu.be/fXgsPs5Y58Q] |
|   2    | What is Domain Driven Design                      | [https://youtu.be/ggzqgOkxjSM] |
|   3    | Three level of Domain Driven Design               | [https://youtu.be/g3wZICYkFuc] |
|   4    | Bounded Context and Ubiquitous Language           | [https://youtu.be/1qVRLI_yiH8] |
|   5    | Drawing Bounded Context                           | [https://youtu.be/pDyTLsiiaKQ] |
|   6    | Tactical DDD: Entity and Value Object (1)         | [https://youtu.be/d-1D4HLsfMY] |
|   7    | Tactical DDD: Entity and Value Object (2)         | [https://youtu.be/Z0pFck9d_O4] |
|   8    | Tactical DDD: Aggregate                           | [https://youtu.be/39yidE3xgak] |
|   9    | Tactical DDD: Service                             | [https://youtu.be/_k3fiOcOXK8] |
|   10   | Tactical DDD: Domain Event                        | [https://youtu.be/vp-gKOIeRW0] |
|   11   | Recap                                             | [https://youtu.be/dg1TC2Fgl2A] |
|   12   | [Bonus] Connecting the Specialist to the Business |               []               |

### Organization Collaboration

| ตอนที่ | หัวข้อ                                    |             วีดีโอ             |
| :----: | ----------------------------------------- | :----------------------------: |
|   1    | Introduction                              | [https://youtu.be/9e3YLwQr_9E] |
|   2    | Conway's Law                              | [https://youtu.be/wf5wq8c0p10] |
|   3    | Cross-Functional Team                     | [https://youtu.be/0cucVz3nCyA] |
|   4    | Monolith                                  | [https://youtu.be/McW5wTrkwsU] |
|   5    | SoA and Microservices                     | [https://youtu.be/e6BVwE078ZI] |
|   6    | Differences between SOA and Microservices | [https://youtu.be/peN2iWiBf5c] |
|   7    | Design Service Boundary                   | [https://youtu.be/EIkbtcDxvyI] |
|   8    | Recap                                     | [https://youtu.be/3sTGj0YNJ9g] |
