# Sephora Products Analysis

## Project Overview

โปรเจกต์นี้เป็นการวิเคราะห์ข้อมูลผลิตภัณฑ์และรีวิวจาก Sephora โดยศึกษาความสัมพันธ์ระหว่างผลิตภัณฑ์ ราคา คะแนนรีวิว ความนิยม ส่วนผสม และประเภทผิว

โครงการครอบคลุมตั้งแต่การทำความสะอาดและเตรียมข้อมูล การทำ Balanced Sampling การรวมข้อมูล Product และ Review Dataset ไปจนถึงการวิเคราะห์และนำเสนอผลลัพธ์ด้วย Data Visualization

Dataset ประกอบด้วยรีวิวมากกว่า **1 ล้านรายการ** และผลิตภัณฑ์ **8,494 รายการ**


## Objectives

- ทำความสะอาดและเตรียมข้อมูลให้พร้อมสำหรับการวิเคราะห์
- ทดลองทำ Balanced Sampling เพื่อจัดเตรียมข้อมูลรีวิวสำหรับการเปรียบเทียบ
- วิเคราะห์ความสัมพันธ์ระหว่าง Rating, Recommendation, Price, Loves Count และ Skin Type
- วิเคราะห์ข้อมูลส่วนผสมและข้อมูลผลิตภัณฑ์ที่เกี่ยวข้องกับการแพ้และการระคายเคือง
- นำเสนอผลการวิเคราะห์ผ่าน Data Visualization

---

## Dataset

### Product Dataset

ข้อมูลผลิตภัณฑ์ประกอบด้วยข้อมูลสำคัญ เช่น

- `product_id`
- `product_name`
- `brand_name`
- `primary_category`
- `secondary_category`
- `tertiary_category`
- `price_usd`
- `loves_count`
- `rating`
- `reviews`
- `highlights`
- `ingredients_clean`
- สถานะสินค้า เช่น `limited_edition`, `new`, `online_only`, `out_of_stock` และ `sephora_exclusive`

### Review Dataset

ข้อมูลรีวิวประกอบด้วยข้อมูลสำคัญ เช่น

- `author_id`
- `rating`
- `review_text`
- `review_title`
- `is_recommended`
- `skin_type`
- `skin_tone`
- `product_id`
- `product_name`
- `brand_name`
- `price_usd`
- `helpfulness`
- `total_feedback_count`
- `submission_time`


## My Contribution

รับผิดชอบร่วมกับสมาชิกในทีมในส่วน **Data Cleaning and Data Preparation** และรับผิดชอบการวิเคราะห์ **โจทย์ข้อ 3 และข้อ 4**

- **Prepared and cleaned** Product และ Review Dataset โดยจัดการข้อมูลซ้ำ Missing Values Data Types และรูปแบบข้อมูล
- **Performed Balanced Sampling** จากข้อมูลรีวิว 3 กลุ่ม จนได้ชุดข้อมูลสำหรับวิเคราะห์รวม **32,999 รีวิว**
- **Analyzed Question 3** โดย Merge Product และ Review ด้วย `product_id`, ตรวจหา Medical Claim จาก Keywords และแบ่งข้อมูลเป็น `Medical Claim` และ `General`
- **Analyzed Question 4** โดยจัดกลุ่มและเปรียบเทียบผลิตภัณฑ์ตาม `Skin Type`, Rating และ Price พร้อมสร้าง Visualization สำหรับสรุปผล


## Data Preparation

### Data Cleaning

- ลบข้อมูลและคอลัมน์ที่ไม่จำเป็น
- ตรวจสอบและจัดการข้อมูลซ้ำ
- แปลงชนิดข้อมูลให้เหมาะสมกับการวิเคราะห์
- จัดการ Missing Values
- ทำความสะอาดข้อความรีวิวและลบ HTML Tags
- เตรียมข้อมูลส่วนผสมสำหรับการวิเคราะห์

### Balanced Sampling

หลังจากทำความสะอาดข้อมูลรีวิว ได้ทำ Balanced Sampling ดังนี้

| Review Type | Original | Sampled |
|---|---:|---:|
| Positive | 892,214 | 15,000 |
| Negative | 113,726 | 14,999 |
| Neutral | 81,509 | 3,000 |

รวมข้อมูลที่นำมาใช้ในการวิเคราะห์ **32,999 รีวิว**


## Analysis

### Question 3: Medical Claim Analysis

วิเคราะห์ว่าผลิตภัณฑ์ที่มีข้อความเชิงการแพทย์ เช่น `Dermatologist Tested`, `Dermatologist Approved` และ `Medical Grade` มีความแตกต่างจากผลิตภัณฑ์ทั่วไปหรือไม่

กระบวนการหลัก:

- Merge Product และ Review Dataset ด้วย `product_id`
- สร้าง Keyword List สำหรับตรวจหา Medical Claim
- ตรวจสอบข้อมูลใน `highlights`
- สร้างตัวแปร `is_medical` และ `claim_group`
- เปรียบเทียบ Rating, Recommendation และ Loves Count

จากข้อมูล **32,999 รีวิว** พบว่า

- Medical Claim: **409 รีวิว (1.2%)**
- General: **32,590 รีวิว (98.8%)**

### Question 4: Skin Type and Product Analysis

วิเคราะห์ผลิตภัณฑ์ตามประเภทผิว ได้แก่

- Normal
- Dry
- Oily
- Combination

โดยจัดอันดับ **Top 10 Products** ตาม Rating และเปรียบเทียบช่วงราคาในแต่ละ Skin Type

ข้อค้นพบสำคัญ:

- **Normal:** ราคาอยู่ประมาณ **$12–$152** โดยมีผลิตภัณฑ์กลุ่ม Anti-aging และ Serum
- **Dry:** พบ Outlier ที่ **$279** ขณะที่สินค้าส่วนใหญ่อยู่ในช่วง **$12–$98**
- **Oily:** ราคาเฉลี่ยประมาณ **$43** โดยเน้น Sunscreen และ Cleanser
- **Combination:** ราคาเฉลี่ยประมาณ **$60** และมีผลิตภัณฑ์หลากหลาย เช่น Retinol, BHA และ Moisturizer


## Key Findings

- กลุ่ม **Medical Claim คิดเป็น 1.2%** ของรีวิวที่นำมาวิเคราะห์ แต่มีอัตรา Recommended สูงกว่า General ในทุก Skin Type
- Medical Claim ไม่ได้มี `Loves Count` สูงกว่า General อย่างชัดเจน และพบผลิตภัณฑ์กลุ่มนี้น้อยลงเมื่อราคาอยู่ในช่วงสูงกว่า $50
- Medical Claim มีสัดส่วน Rating ระดับ 4–5 ดาวสูงกว่าเล็กน้อยเมื่อเทียบกับ General
- แต่ละ Skin Type มีแนวโน้มด้านผลิตภัณฑ์และช่วงราคาที่แตกต่างกัน


## Data Visualization

ผลการวิเคราะห์ถูกนำเสนอด้วย

- Bar Chart
- Line Chart
- Scatter Plot
- Boxplot
- Correlation Heatmap
- Product Ranking


## Tools and Technologies

### Data Analysis

- Python
- Jupyter Notebook
- Pandas
- NumPy

### Data Visualization

- Matplotlib
- Seaborn

### Methods

- Data Cleaning
- Data Preparation
- Balanced Sampling
- Exploratory Data Analysis
- Keyword-based Classification
- Data Visualization
