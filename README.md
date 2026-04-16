# Problem 2: High Distribution Costs (Channel Profitability)

## Background
Azure Stay Hotel พบว่ารายรับรวม (Gross Revenue) มีแนวโน้มเติบโต แต่กำไรสุทธิกลับไม่เพิ่มขึ้นในสัดส่วนเดียวกัน สาเหตุหลักคือโรงแรมพึ่งพาช่องทาง OTA (Online Travel Agents) เช่น Expedia และ Booking.com เป็นสัดส่วนสูง ซึ่งเรียกเก็บค่า commission สูงถึง 15–20% ต่อ booking ทำให้รายรับสุทธิต่อห้องลดลงอย่างมีนัยสำคัญ

## Pain Points
- OTA commission สูง

## สาเหตุ  

1.การพึ่งพา OTA มากเกินไป: ยอดจองส่วนใหญ่มาจากบุคคลที่สาม (Expedia, Booking.com) ซึ่งแม้จะสร้าง Volume ได้สูง แต่ต้องแลกมาด้วยค่า commission ที่สูงถึง 15-25% ทำให้รายได้สุทธิที่โรงแรมได้รับจริง (Net Revenue) ต่ำกว่าที่ควรจะเป็น

2.ความไม่ชัดเจนของต้นทุนแฝง: โรงแรมไม่เคยเปรียบเทียบอย่างจริงจังว่า ระหว่างการจ่ายค่า commission ให้ OTA กับการทุ่มงบการตลาด (Marketing Spend) เพื่อให้ลูกค้าจองตรง (Direct Web) แบบไหนมีความคุ้มค่ามากกว่ากัน (COA% เปรียบเทียบ)

## SMART Objectives
**S(Specific):** เพิ่ม Net RevPAR โดยลดสัดส่วน booking จาก OTA และเพิ่มสัดส่วน Direct Web แทน 

**M(Measurable):** เพิ่ม Net RevPAR ขึ้น 10% และลดสัดส่วน OTA ลง 15 percentage points

**A(Achievable):** ทำได้โดยเพิ่ม budget  สำหรับ Ads (e.g. Google Ads, Facebook) ของ Direct Web

**R(Relevant):** ตรงเป้าหมายหลักของโรงแรมคือ maximize profitability ไม่ใช่แค่ volume

**T(Time-bound):** ภายใน 3 เดือน โดยตรวจสอบสัดส่วน OTA และ Net RevPAR ทุกสิ้นเดือน 

## Hypothesis & Method
**Hypothesis 1:** ช่องทาง Direct Web ให้ค่า Net ADR สูงกว่าช่องทาง OTA อย่างน้อย 15% แม้จะมียอดจอง (Volume) น้อยกว่าก็ตาม
- Method: เปรียบเทียบค่าเฉลี่ยของ Net ADR ระหว่าง Channel_type = 'Direct' และ Channel_type = 'OTA'
- Goal: เพื่อใช้เป็นข้อมูลพื้นฐานในการปรับสัดส่วน Channel Mix Optimization (ช่องทางการขาย) โดยมุ่งเน้นการเพิ่ม Net Revenue (รายได้สุทธิ) แทนการเพิ่มยอดจองรวมแต่กำไรต่ำ

**Hypothesis 2:** ในช่วง Weekend ซึ่งเป็นช่วงที่มีความต้องการสูง ช่องทาง OTA มีค่า COA% สูงกว่าช่องทาง Direct Web อย่างมีนัยสำคัญ ส่งผลให้ Net RevPAR ต่ำกว่าที่ควรจะเป็น
- Method: เปรียบเทียบ COA% และ Net RevPAR ระหว่างช่วง Weekday (จันทร์-ศุกร์) และ Weekend (เสาร์-อาทิตย์) โดยแยกตามกลุ่ม Channel
- Goal: เพื่อระบุโอกาสในการใช้กลยุทธ์ Channel Pinching หรือการปิดรับจองจากช่องทางที่คอมมิชชันแพงในช่วงที่โรงแรมสามารถขายห้องเองได้อยู่แล้ว เพื่อรักษาผลกำไรสูงสุดในช่วง Peak Demand

