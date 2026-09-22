# 📊 Arknights Sheet (TTRPG Data & System Design)

**System & Data Design**: ออกแบบและพัฒนาระบบคำนวณสถิติตัวละครอัตโนมัติผ่าน Google Sheets เพื่ออำนวยความสะดวกและลดข้อผิดพลาดในการประมวลผลข้อมูลของผู้เล่น รองรับการแปลงค่า Modifier, Ability, Saving Throws, Armor Class (AC), Hit Dice และระบบ Dynamic Background ตาม Nationality 

> 🔗 **เอกสารและแหล่งอ้างอิง:**
> - **Google Sheet ตัวเต็ม:** [AK5e Character Sheet v2.1 (Editable)](https://docs.google.com/spreadsheets/d/1Ol_KeIameLlpm_bOtab7GSYVnmM5bgL3HnwGv5CCGVE/edit?usp=sharing)
> - **เอกสารอ้างอิงระบบเดิม:** [GSheet v2.1 Template](https://docs.google.com/spreadsheets/d/1ApmbXHTln99fPTUpanyQRTXNzXbQ8UBTt3Uq8xInQKw/edit?gid=359784640#gid=359784640) | [AK5e Rulebook Reference](https://homebrewery.naturalcrit.com/share/mt8mcG6iRDbv#p503)

---

## 📑 โครงสร้างของ Sheet
แผ่นงาน Arknights Sheet แบ่งออกเป็น **4 หน้าหลัก** เพื่อให้จัดการข้อมูลตัวละครได้อย่างเป็นหมวดหมู่:
1. **Stat:** หน้าคำนวณค่าสถานะ ตัวเลือกสายอาชีพ และการต่อสู้หลัก
2. **Character:** ข้อมูลประวัติตัวละคร และรายละเอียดสกิลเชิงลึก
3. **Inventory:** ช่องเก็บไอเทม อุปกรณ์ และติดตามค่าเงิน
4. **Art:** ระบบเวทมนตร์และคาถา (Originium Arts)

---

## ⚔️ 1. หน้า Stat (Core Stats & Mechanics)

<img width="704" alt="Stat Overview" src="https://github.com/user-attachments/assets/30141620-74c3-4c8b-8c16-89fe7bca2ca9" />

โครงสร้างหน้า **Stat** แบ่งออกเป็น 3 ส่วนหลัก ได้แก่:
1. **Header Zone:** ข้อมูลพื้นฐาน สภาพแวดล้อม และระดับเลเวลตัวละคร
2. **Combat & Core Stats Zone:** ค่าสถานะหลัก ค่าพลังชีวิต และการคำนวณสำหรับการต่อสู้
3. **Details & Inventory Zone:** ข้อมูลทักษะเฉพาะและการเชื่อมโยงกับช่องเก็บของ

---

### 📌 ส่วนที่ 1: Header Zone (การปรับแต่งและเงื่อนไขตัวละคร)

<img width="704" alt="Header Overview" src="https://github.com/user-attachments/assets/0c59e4eb-f315-418c-83cb-1d1fd6722503" />

โซน Header ประกอบด้วย 8 ช่องข้อมูลหลักพร้อมระบบคำนวณอัตโนมัติแบบไดนามิก:

<img width="100%" alt="Header Details" src="https://github.com/user-attachments/assets/bfe92a59-0ac1-4798-8e49-ac48661a07ba" />

* **1. Character Name:** สำหรับใส่ชื่อตัวละคร
* **2. Player Name:** สำหรับใส่ชื่อผู้เล่น
* **3. Class & 3.1 Subclass (Dynamic Class Filtering):** 
  * ในระบบ AK5e Homebrew ประกอบด้วย **8 อาชีพหลัก** และมีอาชีพย่อยรวมกันถึง **54 อาชีพ** (`Caster: 6`, `Defender: 7`, `Guard: 11`, `Marksman: 8`, `Medic: 5`, `Specialist: 7`, `Supporter: 5`, `Vanguard: 5`)
  * **Automated Logic:** เมื่อผู้เล่นเลือกอาชีพหลัก ตัวเลือกในช่อง `Subclass` จะทำการกรอง แสดงเฉพาะอาชีพย่อยที่เกี่ยวข้องเท่านั้น รวมถึงส่งค่าไปยังช่อง `Hit Dice` ในส่วน Combat Stats อัตโนมัติ

  <p float="left">
    <img width="48%" alt="Class Filter 1" src="https://github.com/user-attachments/assets/013ac5e1-c05e-4d69-b0db-f1002de46fcf" />
    <img width="48%" alt="Class Filter 2" src="https://github.com/user-attachments/assets/4d317dc3-51d5-4f19-b150-539384b74d86" />
  </p>

* **4. LMD (Currency Sync):** ช่องแสดงจำนวนเงินในเกม โดยเชื่อมโยงข้อมูล แบบเรียลไทม์กับช่อง LMD ในหน้า `Inventory`
* **5. Nationality:** ถิ่นกำเนิดของตัวละคร (ปัจจุบันมี 20 สัญชาติ) ซึ่งส่งผลต่อสกิล ภาษา และ Background พิเศษ
* **6. Species:** เผ่าพันธุ์ของตัวละคร มีทั้งหมด 20 เผ่าพันธุ์หลัก และ 6 เผ่าพันธุ์พิเศษ โดยแต่ละเผ่าพันธุ์จะมอบความสามารถเฉพาะตัว
* **7. Background (Dynamic Unlocks):** 
  * โดยปกติมี Background พื้นฐานให้เลือก 10 แบบ
  * **Conditional Logic:** หากผู้เล่นเลือก `Nationality` เฉพาะ ระบบจะปลดล็อก Background พิเศษเพิ่มขึ้นมา เช่น เลือก *Siracusa* ระบบจะเปิดตัวเลือก *Unique Background - Famiglia Member (สมาชิกตระกูล)* ให้เลือกล่าสุดทันที

  <p float="left">
    <img width="48%" alt="Background 1" src="https://github.com/user-attachments/assets/db8cf3ce-4b81-40ed-8263-439f0ed31fe9" />
    <img width="48%" alt="Background 2" src="https://github.com/user-attachments/assets/e02bdd5f-6947-430d-bbdf-43cc1d80d6a5" />
  </p>

* **8. Level (Proficiency & Stat Link):** 
  * เมื่อปรับเปลี่ยนระดับเลเวล ค่า **Prof. Bonus (Proficiency Bonus)** และค่า **Total Hit Dice** ในส่วน Combat & Core Stats จะถูกคำนวณและอัปเดตโดยอัตโนมัติทันที

  <p float="left">
    <img width="48%" alt="Level Sync 1" src="https://github.com/user-attachments/assets/7ec2f4d2-9df2-46b3-9b81-0f97c3a87ba0" />
    <img width="48%" alt="Level Sync 2" src="https://github.com/user-attachments/assets/41aedfe6-1778-4e8e-91bc-df43b166ce8e" />
  </p>
---

### 📌 ส่วนที่ 2: Combat & Core Stats Zone 

<img width="1063" height="562" alt="image" src="https://github.com/user-attachments/assets/25474f67-9576-4df0-94d5-9749b21ca51e" />

โซน Combat & Core Stats Zone  ประกอบด้วย 12 ส่วน

- 1.Prof. Bonus และ INSPIRATION : โดย Prof. Bonus จะขึ้นตาม Level ที่เพิ่มขึ้น เช่น 1-4 Prof. Bonus คือ 2 5-8 คือ 3 โดน Prof. Bonus มีส่วนลิ้งสำคัญได้แก่ Saving Throws กับ Skill ส่วน INSPIRATION เป็นช่วงสำหรับใส่จำนวน INSPIRATION ที่ได้รับมาจากการทำเงื่อนไขอะไรบางอย่างสำหรับใช้ในการทอยซ้ำ
- 2.Armor Class : คือช่องแสดงค่า Armor Class ที่ได้จากการใส่ชุกเกราะหรือโล่และปัจจัยภายนอก โดยจะนำค่าจากช่อง Armor ช่อง DEX Modifier ช่อง Shield ช่อง Misc เอามารวมผลกันและแสดงที่ช่อง Armor Class รวมถึง Arts DR Physical DR คือช่องความต้านทานต่อดาเมจประเถทนั้นๆ ยกตัวอย่าง ตัวละครใส่ Light Combat Gear ที่มีค่า AC 13 +  Dexterity Modifier ของตัวละครซึ้งมีอยู่ 3 และชุดมี 2 (Physical) รวมถึง ใส่ Small Shield ที่มี 2 AC
<img width="448" height="167" alt="image" src="https://github.com/user-attachments/assets/58691f4a-dedd-4d98-a82f-bf94c039e160" />





  
