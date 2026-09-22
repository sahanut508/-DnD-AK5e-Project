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

### 📌 ส่วนที่ 2: Combat & Core Stats Zone (ระบบคำนวณการต่อสู้และสถานะหลัก)

<img width="100%" alt="Combat & Core Stats Overview" src="https://github.com/user-attachments/assets/25474f67-9576-4df0-94d5-9749b21ca51e" />

โซน **Combat & Core Stats** คือส่วนประมวลผลการต่อสู้และคำนวณสถิติอัตโนมัติ ประกอบด้วย 12 ส่วนหลัก:

---

#### 1. Proficiency Bonus & Inspiration (ระบบโบนัสและแต้มพิเศษ)
* **Proficiency Bonus (Prof. Bonus):** คำนวณอัตโนมัติตามระดับ Level ของตัวละคร (เช่น Lv.1-4 = +2, Lv.5-8 = +3) โดยค่านี้จะถูกดึงไปใช้บวกเพิ่มในส่วน `Saving Throws` และ `Skills`
* **Inspiration:** ช่องบันทึกแต้ม Inspiration ที่ได้รับจากการเล่นตามเงื่อนไขพิเศษ สำหรับใช้ทอยสุ่มลูกเต๋าใหม่ (Reroll)

#### 2. Armor Class (AC Calculation & Damage Resistance)
* **AC Automation:** คำนวณค่า Armor Class รวมอัตโนมัติจากการประมวลผลร่วมกันของช่อง `Armor`, `DEX Modifier`, `Shield` และ `Misc`
* **Damage Resistance (DR):** มีช่องสำหรับติดตามค่าความต้านทานความเสียหายแยกประเภท ได้แก่ `Arts DR` (เวทมนตร์) และ `Physical DR` (กายภาพ)
  * *ตัวอย่าง:* ตัวละครสวม Light Combat Gear (Base AC 13) + DEX Modifier (3) + Physical Resistance ชุด (2) + Small Shield (+2 AC) ระบบจะสรุปผลลัพธ์ AC รวมให้อัตโนมัติ

<img width="450" alt="Armor Class Calculation Example" src="https://github.com/user-attachments/assets/58691f4a-dedd-4d98-a82f-bf94c039e160" />

#### 3. Hit Points & Hit Dice Management (พลังชีวิตและการพักผ่อน)
* **Hit Point Maximum & Current HP:** ช่องบันทึกพลังชีวิตสูงสุดและพลังชีวิตปัจจุบัน
* **Hit Dice Sync:** จำนวน `Total Hit Dice` จะอัปเดตตาม Level ของตัวละคร และชนิดเต๋าจะเปลี่ยนตาม `Class` ที่เลือกมา เพื่อใช้ทอยฟื้นฟู HP ช่วง Short/Long Rest

<p float="left">
  <img width="48%" alt="Guard Instructor Hit Dice" src="https://github.com/user-attachments/assets/4160e86a-71ca-4489-be8b-00e06f237017" />
  <img width="48%" alt="Marksman Heavyshot Hit Dice" src="https://github.com/user-attachments/assets/653ff444-d187-468b-b43b-a44322549075" />
</p>

#### 4. Mettle (Death Saving Tracker)
* ช่องบันทึกและติดตามสถานะค่า `METTLE` ที่ได้จากการทอยช่วยเหลือเมื่อตัวละครอยู่ในสภาวะเฉียดตาย (Death Saving Throws)

#### 5. Speed & Initiative (การเคลื่อนที่และลำดับเทิร์น)
* **Speed:** แสดงระยะการเคลื่อนที่ต่อเทิร์น ประมวลผลจากเงื่อนไขเฉพาะของแต่ละเผ่าพันธุ์ (Species) และอาชีพ (Class)
* **Initiative:** คำนวณลำดับการออกแอ็กชันใน lượt ต่อสู้ โดยเชื่อมโยงค่าอัตโนมัติกับ `Dexterity Modifier`

#### 6. Conductive / Oripathy Status (ระบบการติดเชื้อตาม Lore)
* ช่องบันทึกระดับการติดเชื้อ **Oripathy** ซึ่งเป็นกลไกพิเศษประจำเกม (Risk/Reward Mechanics): ยิ่งระดับการติดเชื้อสูง จะยิ่งลดค่า HP สูงสุดของตัวละคร แต่จะได้รับโบนัสความรุนแรงของ Arts (เวทมนตร์) เพิ่มขึ้น

#### 7. Martial DC Automation (คำนวณค่าความยากของท่าต่อสู้)
* ระบบคำนวณค่า **Martial DC** อัตโนมัติ เพื่ออำนวยความสะดวกให้ผู้เล่นไม่ต้องคำนวณด้วยตนเองขณะใช้อบิลิตี้ต่อสู้ พร้อมฟังก์ชันสลับตัวแปรการคำนวณหลักระหว่าง `STR` หรือ `DEX` ได้ตามต้องการ

#### 8. Ability Stat Modifiers & Saving Throws
* **Ability Stat Modifier:** ระบบแปลงค่า Ability Score สุ่มพื้นฐานเป็นค่า Modifier อัตโนมัติ 
  * *Gray Box (Base Stat):* สำหรับใส่ค่าสุ่มดิบ ไม่มีการเปลี่ยนแปลง เพื่อป้องกันความสับสน
  * *White Box (Final Stat):* แสดงค่าสุดท้ายหลังบวกโบนัสจาก เผ่า, อาชีพ, Background และ Nationality
* **Saving Throws Automation:** ดึงค่า Modifier มาแสดงอัตโนมัติ และเมื่อติ๊กเลือกความชำนาญ ระบบจะนำ `Prof. Bonus` มาบวกเพิ่มให้อัตโนมัติ

<img width="500" alt="Ability Stat & Saving Throws Example" src="https://github.com/user-attachments/assets/6546b94c-0d3c-40a6-8287-1bf2140557c5" />

#### 9. Skill Proficiency & Expertise Mechanics (ทักษะเฉพาะด้าน)
* คำนวณค่าทักษะอิงตาม Ability Modifier ของแต่ละสาย โดยมีระบบรองรับการยกระดับความชำนาญ 2 รูปแบบ:
  * พิมพ์ **`p`** (Proficiency): เพิ่มค่า `Prof. Bonus` เข้าไปในทักษะ
  * พิมพ์ **`e`** (Expertise): เพิ่มค่า `Prof. Bonus x 2` เข้าไปในทักษะสำหรับผู้เล่นที่มีความเชี่ยวชาญพิเศษ

<img width="100%" alt="Skill System Example" src="https://github.com/user-attachments/assets/eb1fa26b-e301-48f3-b558-d846aeaf0b89" />

#### 10. Passive Wisdom / Perception
* ช่องคำนวณค่าการรับรู้เชิงรับ (Passive Perception) อัตโนมัติ โดยอิงจากค่าทักษะ `Perception + 10`

#### 11. Operator Skills (ระบบสกิลกดใช้และ SP Management)
* จัดเก็บรายละเอียด Active Skills ของตัวละคร ประกอบด้วย: `Basic Skill Name`, `SP Cost` (รวมถึง Initial SP), `Charging Mode` (รูปแบบการสะสม SP), `Current SP` และ `Maximum SP`

<img width="270" height="309" alt="image" src="https://github.com/user-attachments/assets/1bc5a0b3-ab0f-4a39-9815-ac2a75df9026" />

#### 12. Talents (ระบบความสามารถติดตัว)
* บันทึกความสามารถ Passive Abilities ที่ทำงานตลอดเวลาโดยไม่ต้องบริหารจัดการค่า SP

<img width="466" alt="Talents System" src="https://github.com/user-attachments/assets/100631f3-bdd1-4f50-8267-7b1fbe4b647d" />

---
### 📌 ส่วนที่ 3: Details & Inventory Zone (รายละเอียดความเชี่ยวชาญและทรัพยากรตัวละคร)

<img width="100%" alt="Details & Inventory Overview" src="https://github.com/user-attachments/assets/8d433bf5-09d7-439d-aef2-b9679459ac1b" />

โซน **Details & Inventory** ถูกออกแบบขึ้นเพื่อจัดเก็บข้อมูลคุณสมบัติเสริม และติดตามทรัพยากรการใช้งานของตัวละครอย่างเป็นระบบ โดยแบ่งออกเป็น 3 ส่วนหลัก:


#### 1. Other Proficiencies & Languages (ความชำนาญเฉพาะและภาษา)
* ช่องบันทึกความชำนาญของตัวละครในด้านต่างๆ ได้แก่ **อาวุธ (Weapons), ชุดเกราะ (Armor), เครื่องมืออุปกรณ์ (Tools), ยานพาหนะ (Vehicles)** และ **ภาษา (Languages)** 
* รองรับการบันทึกข้อมูลที่ได้รับมาจากเงื่อนไขหลากหลาย เช่น เผ่าพันธุ์ (Species), อาชีพ (Class), ปูมหลัง (Background), สัญชาติ (Nationality) หรือการฝึกฝนเพิ่มเติมระหว่างการเล่น

<img width="277" alt="Other Proficiencies & Languages" src="https://github.com/user-attachments/assets/2b163c71-470f-4809-abc7-8bdd9b180543" />


#### 2. Features & Traits (คุณลักษณะและความสามารถติดตัว)
* พื้นที่สำหรับจัดเก็บรายละเอียดความสามารถพิเศษ (Traits & Passives) ที่ได้มาจาก เผ่าพันธุ์, ปูมหลัง, สัญชาติ และสายอาชีพ 
* ช่วยให้ผู้เล่นอ่านรายละเอียดเงื่อนไขของสกิลและกิมมิกตัวละครได้อย่างครบถ้วนในที่เดียว

<img width="445" alt="Features & Traits" src="https://github.com/user-attachments/assets/cb2e576f-3c94-4866-aed9-bc1c5901f6f5" />


#### 3. Resources, Charges, & Abilities (ระบบติดตามจำนวนครั้งการใช้งาน)
* ช่องสำหรับบริหารจัดการความสามารถหรือสกิลที่มี **จำนวนครั้งในการใช้งานจำกัด (Limited Uses / Resource Charges)** เช่น สกิลที่ฟื้นฟูหลังจากการพักผ่อน (Short/Long Rest) หรือโควตาการใช้อบิลิตี้พิเศษต่อวัน

<img width="367" alt="Resources & Charges" src="https://github.com/user-attachments/assets/cceb18ea-27fa-4fae-9509-4e7a7991276d" />


💡 **Customizable Workspace (อิสระในการจัดสรรพื้นที่ใช้งาน)**
ระบบถูกออกแบบมาให้ยืดหยุ่นสูง ผู้เล่นสามารถเลือกจัดระเบียบ วางตำแหน่ง หรือแบ่งกลุ่มข้อมูลในทั้ง 3 ส่วนนี้ได้อย่างเป็นอิสระตามความถนัดและการใช้งานจริง เพื่อสร้าง UX (User Experience) ที่สะดวกรวดเร็วที่สุดสำหรับตัวละครนั้นๆ

<img width="100%" alt="Custom Layout Example" src="https://github.com/user-attachments/assets/c1491e81-43e6-4012-b637-1b20ea284992" />









  
