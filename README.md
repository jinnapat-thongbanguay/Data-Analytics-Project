# Problem 2: High Distribution Costs (Channel Profitability)

## Background
Azure Stay Hotel พบว่ารายรับรวม (Gross Revenue) มีแนวโน้มเติบโต แต่กำไรสุทธิกลับไม่เพิ่มขึ้นในสัดส่วนเดียวกัน สาเหตุหลักคือโรงแรมพึ่งพาช่องทาง OTA (Online Travel Agents) เช่น Expedia และ Booking.com เป็นสัดส่วนสูง ซึ่งเรียกเก็บค่า commission สูงถึง 15–20% ต่อ booking ทำให้รายรับสุทธิต่อห้องลดลงอย่างมีนัยสำคัญ

## Pain Points
- OTA commission สูง

### สาเหตุ  

1.การพึ่งพา OTA มากเกินไป: ยอดจองส่วนใหญ่มาจากบุคคลที่สาม (Expedia, Booking.com) ซึ่งแม้จะสร้าง Volume ได้สูง แต่ต้องแลกมาด้วยค่า commission ที่สูงถึง 15-25% ทำให้รายได้สุทธิที่โรงแรมได้รับจริง (Net Revenue) ต่ำกว่าที่ควรจะเป็น

2.ความไม่ชัดเจนของต้นทุนแฝง: โรงแรมไม่เคยเปรียบเทียบอย่างจริงจังว่า ระหว่างการจ่ายค่า commission ให้ OTA กับการทุ่มงบการตลาด (Marketing Spend) เพื่อให้ลูกค้าจองตรง (Direct Web) แบบไหนมีความคุ้มค่ามากกว่ากัน (COA% เปรียบเทียบ)

## SMART Objectives
**S(Specific):** เพิ่ม Net RevPAR โดยลดสัดส่วน booking จาก OTA และเพิ่มสัดส่วน Direct Web แทน 

**M(Measurable):** เพิ่ม Net RevPAR ขึ้น 10% และลดสัดส่วน OTA ลง 15 percentage points

**A(Achievable):** ทำได้โดยเพิ่ม budget  สำหรับ Ads (e.g. Google Ads, Facebook) ของ Direct Web

**R(Relevant):** ตรงเป้าหมายหลักของโรงแรมคือ maximize profitability ไม่ใช่แค่ volume

**T(Time-bound):** ภายใน 3 เดือน โดยตรวจสอบสัดส่วน OTA และ Net RevPAR ทุกสิ้นเดือน 

## Hypothesis & Method
**Hypothesis 1:** ช่องทาง Direct มีประสิทธิภาพในการสร้างรายได้สูงสุด โดยให้ค่า Net ADR สูงกว่า OTA อย่างน้อย 15% และสูงกว่า Wholesale อย่างน้อย 25% แม้จะมีสัดส่วนยอดจอง (Volume) น้อยที่สุดใน 3 กลุ่ม
- Method: เปรียบเทียบค่าเฉลี่ยของ Net ADR ระหว่าง Channel_type = 'Direct', Channel_type = 'OTA' และ Channel_type = 'Wholesale'
- Goal: เพื่อใช้เป็นข้อมูลพื้นฐานในการปรับเปลี่ยนสัดส่วน Channel Mix Optimization (ช่องทางการขาย) โดยมุ่งเน้นการเพิ่ม สัดส่วนการจองตรง (Direct Booking) เพื่อยกระดับ Net Revenue (รายได้สุทธิ) ให้สูงขึ้น แทนการเพิ่มยอดจองรวมจากช่องทางที่มีต้นทุนการจองสูงแต่กำไรต่ำ

**Hypothesis 2:** ช่องทาง OTA มีอัตราการยกเลิกการจอง (Cancellation Rate) สูงที่สุด ซึ่งส่งผลกระทบโดยตรงต่อต้นทุนค่าเสียโอกาส (Opportunity Cost) และลดทอนความสามารถในการทำกำไรสุทธิ (Net Profitability) เมื่อเทียบกับช่องทาง Direct และ Wholesale"
- Method (วิธีการ): คำนวณอัตราส่วนการยกเลิก (Cancellation Rate) โดยเปรียบเทียบสัดส่วนระหว่างการจองที่ยกเลิก (Cancelled) กับยอดจองทั้งหมด (Volume) และนำมาวิเคราะห์เปรียบเทียบร่วมกับค่ารายได้สุทธิเฉลี่ย (Net ADR) แยกตามรายช่องทาง (Channel Type)
- Goal (เป้าหมาย): เพื่อพิสูจน์ว่ายอดจองจำนวนมาก (High Volume) จาก OTA เป็นยอดจองที่มีความไม่แน่นอนสูง การปรับ Channel Mix Optimization โดยลดการพึ่งพา OTA และเพิ่มสัดส่วนการจองช่องทาง Direct จะช่วยลดความเสี่ยงจากการถูกยกเลิก และส่งผลให้รายได้สุทธิ (Net Revenue) มีความเสถียรมากยิ่งขึ้น

**Hypothesis 3:** ในช่วง Weekend (วันหยุดสุดสัปดาห์) มีความต้องการเข้าพัก (Demand) สูงกว่า Weekday(วันธรรมดา) อย่างมีนัยสำคัญ
- Method: สร้างตัวแปร Is Weekend เพื่อแบ่งกลุ่มข้อมูลตามวันเข้าพัก (Mon-Fri vs Sat-Sun) จากนั้นคำนวณ Average Daily Booking Volume และ Average Gross ADR เพื่อเปรียบเทียบประสิทธิภาพรายวัน โดยใช้ค่าเฉลี่ยในการขจัดความเหลื่อมล้ำของจำนวนวันในแต่ละกลุ่มข้อมูล
- Goal: เพื่อยืนยันว่า Weekend คือช่วงเวลาที่โรงแรมมีอำนาจต่อรองสูงสุด (Peak Demand) ซึ่งวัดจาก Average Daily Volume และ Gross ADR ที่สูงกว่าปกติ เพื่อใช้เป็นฐานในการตัดสินใจดึง Inventory กลับมาขายเองในช่องทาง Direct

**Hypothesis 4:** ในช่วง Weekend (วันหยุดสุดสัปดาห์)โรงแรมจ่าย Commission OTA โดยไม่จำเป็นในวันที่ Demand สูงอยู่แล้ว
- Method: วิเคราะห์สัดส่วน Channel Mix (100% Stacked Bar) เพื่อดูการเปลี่ยนแปลงของพฤติกรรมการจองในวันหยุด และเปรียบเทียบ Average Commission Amount ต่อการจองหนึ่งครั้ง ระหว่างช่วง Weekday และ Weekend เพื่อพิสูจน์ภาวะ 'Commission Leakage' หรือต้นทุนแฝงที่พุ่งสูงขึ้นตามราคาห้องพักที่เพิ่มขึ้นในวันหยุด"
- Goal: ตรวจสอบว่าโรงแรมสูญเสีย Net Revenue ให้กับ OTA Commission ในช่วงที่ Demand สูงโดยไม่จำเป็น และพิจารณากลยุทธ์ Close-out หรือจำกัดจำนวนห้องบน OTA ในวันเสาร์–อาทิตย์เพื่อลด

**Hypothesis 5:** การจองผ่าน Rate Code ประเภท Promotion บนช่องทาง OTA มีค่า Net ADR ต่ำที่สุด และอาจส่งผลให้ขาดทุน เมื่อเทียบกับต้นทุนการดำเนินงานของโรงแรม
- Method: วิเคราะห์ Net ADR โดยใช้ Rate Code ร่วมกับ Booking Channel เพื่อดูว่าเมื่อรวม discount กับค่า commission แล้ว รายได้ที่เหลือจริงเป็นอย่างไร
- Goal: เพื่อระบุความเสียหายจาก Commission Leakage (สภาวะกำไรสุทธิรั่วไหลจากการจ่ายค่าคอมมิชชันในวันที่โรงแรมมี Demand สูงจนสามารถขายเองได้) ที่พุ่งสูงขึ้นตามราคาห้องพักในวันหยุด และเสนอแนวทาง OTA Close-out (จำกัดการขายบน OTA ช่วง Peak Dates) เพื่อเปลี่ยนต้นทุนค่าคอมมิชชันเฉลี่ยที่สูงถึง 18 หน่วยต่อบุกกิ้ง ให้กลับมาเป็นกำไรสุทธิ (Net Revenue) ของโรงแรมโดยตรง

## Dataset & Features
- จำนวนแถวข้อมูล: 28,689 แถว
- จำนวนตัวแปรทั้งหมด: 21 ตัวแปร (รวม 4 ตาราง)

### Data Generation Prompt
```
ช่วยสร้างข้อมูล Synthetic Data ของโรงแรม "The Azure Stay" ในรูปแบบของไฟล์ .xlxs จำนวน 4 ตาราง เพื่อนำไปวิเคราะห์ปัญหา High Distribution Costs (Channel Profitability) และให้ข้อมูลมีความสอดคล้องเพื่อพิสูจน์ 3 สมมติฐาน ขอ Synthetic Data ที่สะอาดเรียบร้อย พร้อมสำหรับการนำมาทำ EDA และให้สามารถนำไปทำ EDA เพื่อพิสูจน์ทั้ง 3 สมมติฐานนี้

Hypothesis 1: ช่องทาง Direct Web ให้ค่า Net ADR สูงกว่าช่องทาง OTA อย่างน้อย 15% แม้จะมียอดจอง (Volume) น้อยกว่าก็ตาม
 Method: เปรียบเทียบค่าเฉลี่ยของ Net ADR ระหว่าง Channeltype = 'Direct' และ Channeltype = 'OTA'
 Goal: เพื่อใช้เป็นข้อมูลพื้นฐานในการปรับสัดส่วน Channel Mix Optimization (ช่องทางการขาย) โดยมุ่งเน้นการเพิ่ม Net Revenue (รายได้สุทธิ) แทนการเพิ่มยอดจองรวมแต่กำไรต่ำ

Hypothesis 2: ในช่วง Weekend ซึ่งเป็นช่วงที่มีความต้องการสูง ช่องทาง OTA มีค่า COA% สูงกว่าช่องทาง Direct Web อย่างมีนัยสำคัญ ส่งผลให้ Net RevPAR ต่ำกว่าที่ควรจะเป็น
 Method: เปรียบเทียบ COA% และ Net RevPAR ระหว่างช่วง Weekday (จันทร์-ศุกร์) และ Weekend (เสาร์-อาทิตย์) โดยแยกตามกลุ่ม Channel
 Goal: วางแผนเลือกช่องทางขายให้เหมาะสมในช่วง Peak เพื่อลดรายจ่ายค่า commission และเปลี่ยนยอดจองมาเป็นกำไรสุทธิ (Net Revenue) ให้ได้มากที่สุด
 
Hypothesis 3: การจองผ่าน Rate Code ประเภท Promotion บนช่องทาง OTA มีค่า Net ADR ต่ำที่สุด และอาจส่งผลให้ขาดทุน เมื่อเทียบกับต้นทุนการดำเนินงานของโรงแรม
 Method: วิเคราะห์ Net ADR โดยใช้ Rate Code ร่วมกับ Booking Channel เพื่อดูว่าเมื่อรวม discount กับค่า commission แล้ว รายได้ที่เหลือจริงเป็นอย่างไร
 Goal: เพื่อตรวจสอบว่าการตั้งราคาแบบโปรโมชัน ช่วยสร้างกำไรหรือสร้างรายได้ไม่คุ้มทุนให้กับโรงแรม และพิจารณาจำกัดสิทธิ์การใช้ Rate Code ประเภท Promotion เฉพาะในช่องทาง Direct Web เท่านั้น  

โดยแต่ละตารางมีตัวแปร และรายละเอียดตามนี้ 
Measure	Definition	Calculation Formula
ADR (Average Daily Rate)	The average rental income per paid occupied room in a given time period.	Gross Room Revenue / Rooms Sold ( $0 - Rack Rate )
OCC (Occupancy)	The percentage of available rooms that were sold during a specific period.	(Rooms Sold / Total Rooms)  100 ( 0% - 100% )
Net ADR	Average revenue per room after deducting commissions.	(Gross Revenue - Commission Cost) / Rooms Sold
Commission Cost	The actual dollar amount paid to the 3rd party.	Gross Revenue  Com
mission Rate (or flat fee)
Cost of Acquisition (COA) %	The efficiency of the channel (lower is better).	(Total Commission + Marketing Spend) / Total Revenue
Net RevPAR	Revenue per available room, adjusted for distribution costs.	(Gross Revenue - Commission Cost) / Total Rooms Available
Dimension	Definition	Set of Possible Values
Booking Channel	The source where the reservation originated (high cost vs. low cost channels).	Direct Website, OTA (Expedia, Booking.com), Walk-in, Corporate Agent, GDS
Channel Type	Categorization for cost analysis.	OTA (High Commission), Direct (Low Commission), Wholesale (Net Rate)
Commission Model	How the channel gets paid.	Percentage (e.g., 15%), Flat Fee (e.g., $5/booking), Merchant (Net Rate)
Day of Week	The specific day the room is occupied (critical for weekend vs. weekday analysis).	Mon, Tue, Wed, Thu, Fri, Sat, Sun
Rate Code	The specific price package or discount applied to the reservation.	Rack Rate, AAA Discount, Corporate Negotiated, Non-Refundable, Seasonal Promo

Table 1: factbookings (The Transaction Data)
 bookingid (PK): Unique ID for the reservation.
 bookingdate: Date the booking was made.
 checkindate: Date of arrival.
 channelid (FK): Links to dimchannels.
 ratecodeid (FK): Links to dimratecodes.
 grossroomrevenue: Total revenue paid by the guest (before commission).
 commissionamount: (New) The calculated cost paid to the channel for this specific booking.
 netroomrevenue: (New) grossroomrevenue - commissionamount.
 status: Confirmed, Cancelled, Checked-Out.
 
Table 2: dimchannels (The Cost Definitions)
 channelid (PK): Unique ID (e.g., CH01).
 channelname: Name (e.g., "Booking.com").
 channeltype: Category (e.g., "OTA").
 commissionmodel: Type of cost (e.g., Percentage, Flat Fee, Net Rate).
 defaultcommissionrate: The standard % fee (e.g., 0.15 for 15%).
 contractowner: The internal sales manager responsible for this relationship.
 
Table 3: dimratecodes
 ratecodeid (PK): Unique ID (e.g., RTCORP).
 ratename: Name of the rate.
 iscommissionable: Boolean (True/False). If False, the channel usually takes their cut before sending you the money.
 
Table 4: factmarketingspend (Optional but Advanced)
 spendid (PK): Unique ID.
 spenddate: The date the money was spent.
 channelid (FK): Links to dimchannels (specifically the Direct Website channel).
 platform: Where the ad ran (e.g., Google Ads, Facebook).
 costamount: The amount spent (e.g., $500).
 clicks: Number of clicks generated.
```

### Data Dictionary
1.	Table: fact_bookings (Transaction Data)
   
| Field Name         | Data Type | Constraints | Description                                  | Example                           |
| ------------------ | --------- | ----------- | -------------------------------------------- | --------------------------------- |
| booking_id         | VARCHAR   | PK          | รหัสการจองที่ไม่ซ้ำกัน                       | RES-10001, RES-10002              |
| booking_date       | DATE      | -           | วันที่ลูกค้าทำการจอง                         | 26/12/2023                        |
| check_in_date      | DATE      | -           | วันที่ลูกค้าเข้าพัก                          | 1/1/2024                          |
| channel_id         | VARCHAR   | FK          | เชื่อมกับ dim_channels                       | CH_01, CH_02                      |
| rate_code_id       | VARCHAR   | FK          | เชื่อมกับ dim_rate_codes                     | RT_AAA, RT_RACK                   |
| gross_room_revenue | DECIMAL   | -           | รายได้รวมที่ลูกค้าจ่าย (ก่อนหักค่าคอมมิชชัน) | 154.15, 110.02                    |
| commission_amount  | DECIMAL   | -           | ค่าคอมมิชชันที่ต้องจ่ายให้ช่องทางนั้นๆ       | 0, 27.75                          |
| net_room_revenue   | DECIMAL   | -           | รายได้สุทธิหลังจากหักค่าคอมมิชชันแล้ว        | 126.4, 110.02                     |
| status             | VARCHAR   | -           | สถานะการจอง                                  | Confirmed, Cancelled, Checked-Out |


2. Table: dim_channels

| Field Name              | Data Type | Constraints | Description                        | Example                                                              |
| ----------------------- | --------- | ----------- | ---------------------------------- | -------------------------------------------------------------------- |
| channel_id              | VARCHAR   | PK          | รหัสช่องทาง                        | CH_01, CH_02                                                         |
| channel_name            | VARCHAR   | -           | ชื่อช่องทาง                        | Booking.com, Direct Website                                          |
| channel_type            | VARCHAR   | -           | ประเภทช่องทาง                      | OTA (High Commission), Direct (Low Commission), Wholesale (Net Rate) |
| commission_model        | VARCHAR   | -           | รูปแบบการคิดเงิน                   | Percentage, Flat Fee, Net Rate                                       |
| default_commission_rate | DECIMAL   | -           | อัตราค่าธรรมเนียมมาตรฐาน           | 0, 0.1, 0.12, 0.15, 0.18                                             |
| contract_owner          | VARCHAR   | -           | ผู้จัดการที่ดูแลสัญญาของช่องทางนี้ | Sarah Chen                                                           |

3.	Table: dim_rate_codes
   
| Field Name        | Data Type | Constraints | Description                                                       | Example                 |
| ----------------- | --------- | ----------- | ----------------------------------------------------------------- | ----------------------- |
| rate_code_id      | VARCHAR   | PK          | รหัสเรทราคา (เช่น RT_CORP)                                        | RT_AAA, RT_RACK         |
| rate_name         | VARCHAR   | -           | ชื่อประเภทราคา                                                    | Rack Rate, AAA Discount |
| is_commissionable | BOOLEAN   | -           | True: ต้องจ่ายคอมมิชชันเพิ่ม / False: ราคาที่หักมาแล้ว (Net Rate) | TRUE, FALSE             |

4.	Table: fact_marketing_spend ตารางบันทึกต้นทุนแฝง (เช่น ค่าโฆษณา)
   
| Field Name  | Data Type          | Constraints | Description                        | Example              |
| ----------- | ------------------ | ----------- | ---------------------------------- | -------------------- |
| spend_id    | VARCHAR            | PK          | รหัสรายการค่าใช้จ่าย               | SP-00001, SP-00002   |
| spend_date  | DATE               | -           | วันที่จ่ายเงินค่าโฆษณา             | 1/1/2024             |
| channel_id  | VARCHAR            | FK          | มักเชื่อมกับช่องทาง Direct Website | CH_01, CH_02         |
| platform    | VARCHAR            | -           | แพลตฟอร์มที่ใช้                    | Google Ads, Facebook |
| cost_amount | DECIMAL            | -           | จำนวนเงินที่จ่ายไป                 | 75.48, 129.77        |
| clicks      | INT (Whole Number) | -           | จำนวนคลิกที่ได้รับจากยอดเงินนี้    | 934, 2515            |


## Insight
**Insight Hypothesis 1**
-	จากการวิเคราะห์พบว่าช่องทาง Direct มีประสิทธิภาพในการสร้างรายได้สุทธิสูงที่สุด โดยให้ค่า Net ADR สูงกว่า OTA อยู่ 18.29% และสูงกว่า Wholesale ถึง 28.98% เมื่อพิจารณาควบคู่กับด้านปริมาณ (Volume) จะเห็นความขัดแย้งที่สำคัญ (Inversion): แม้ช่องทาง OTA จะเป็นแหล่งสร้างยอดจองหลัก (มียอด Volume สูงที่สุด) แต่กลับมีประสิทธิภาพการสร้างรายได้ต่อห้องต่ำกว่าช่องทาง Direct ซึ่งมียอดจองน้อยกว่า OTA ถึง 53.78% หรือน้อยกว่า 2 เท่า อย่างมีนัยสำคัญ แสดงให้เห็นว่าปริมาณการจองที่สูงจาก OTA ต้องแลกมาด้วยต้นทุนค่า commission ที่ทำให้กำไรสุทธิลดลง

**Insight Hypothesis 2**
- จากการวิเคราะห์พบว่าแม้ช่องทาง OTA จะสร้างปริมาณยอดจองได้สูงสุดเป็นอันดับหนึ่ง (16,293 รายการ) แต่กลับมีอัตราการยกเลิกสูงที่สุดถึง 8.19% ซึ่งสะท้อนให้เห็นว่ายอดจองจำนวนมากจาก OTA มีความผันผวนสูง และสร้างความเสี่ยงต่อการบริหารจัดการห้องพัก (Inventory Management) รวมถึงเกิดต้นทุนแฝงจากค่าเสียโอกาส (Opportunity Cost) เมื่อมีการยกเลิกในนาทีสุดท้าย  
- เมื่อเปรียบเทียบกับช่องทาง Direct ซึ่งให้รายได้เฉลี่ยต่อห้องสุทธิ (Net ADR) สูงที่สุดถึง 146.24 และมีอัตราการยกเลิกเพียง 7.81% ซึ่งต่ำกว่าช่องทาง OTA แสดงให้เห็นว่าช่องทาง Direct มีประสิทธิภาพในการสร้างรายได้ที่มั่นคง และมีคุณภาพมากกว่าอย่างมีนัยสำคัญ  
- ในขณะที่ช่องทาง Wholesale แม้จะมีอัตราการยกเลิกต่ำที่สุด (7.45%) แต่ความสามารถในการสร้างรายได้ต่อหน่วยยังคงต่ำกว่าทั้งช่องทาง Direct และ OTA ส่งผลให้ช่องทาง Direct เป็นช่องทางที่ตอบโจทย์การเพิ่มกำไรสุทธิได้ดีที่สุด

**Insight Hypothesis 3**
-  จากการวิเคราะห์พบว่า Seasonal Promotion บนช่องทาง OTA มีค่า Net ADR ต่ำที่สุดที่ ~111 ต่ำกว่า Benchmark 123.88 ถึง 10.4% เมื่อรวมค่า Commission 15–20% รายได้สุทธิมีความเสี่ยงสูงที่จะไม่คุ้มทุน แม้แต่บนช่องทาง Direct (~117) ก็ยังต่ำกว่า Benchmark สะท้อนภาวะ Over-discounting ในทุกช่องทาง โรงแรมจึงควรจำกัด Promotion Rate เฉพาะช่องทาง Direct และกำหนด Price Floor ใหม่ให้สูงกว่า Benchmark เพื่อปกป้อง Net Revenue
