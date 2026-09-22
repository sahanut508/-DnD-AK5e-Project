# Arknights sheet

**System & Data Design**: ออกแบบและพัฒนาระบบคำนวณสถิติตัวละครผ่าน Excel Sheet อัตโนมัติ โดยระบบรองรับการแปลงค่า Modifier, Ability, Saving Throws, Armor Class (AC), Hit Dice และระบบ Background เฉพาะตาม Nationality เพื่ออำนวยความสะดวกในการจัดเก็บข้อมูลผู้เล่น โดยมีต้นแบบจาก [GSheet v2.1](https://docs.google.com/spreadsheets/d/1ApmbXHTln99fPTUpanyQRTXNzXbQ8UBTt3Uq8xInQKw/edit?gid=359784640#gid=359784640) และ [Character Sheet.pdf](https://imgchest.com/p/qb4zpmejdyj)  จาก https://homebrewery.naturalcrit.com/share/mt8mcG6iRDbv#p503

---
''https://docs.google.com/spreadsheets/d/1Ol_KeIameLlpm_bOtab7GSYVnmM5bgL3HnwGv5CCGVE/edit?usp=sharing''
---
โดย Arknights sheet ฉบับนี้จะมัทั้งหมด 4 สำหรับใส่ข้อมูลของตัวละคร ได้แก่ Stat หน้าสำหรับใส่ค่าตัวละคร CHARACTER ประวัติตัวละครและสกิลแบบละเอียด Inventory ช่องเก็บ Art ช่องเวทมนตร์

# Stat

<img width="704" height="720" alt="image" src="https://github.com/user-attachments/assets/30141620-74c3-4c8b-8c16-89fe7bca2ca9" />

โดยหน้า Stat จะแบ่งได้ 3 ส่วนได้แก่ Header เอาไว้ใส่ข้อมูลเรื่องชื่อผู้เล่น ชื่อตัวละคร อาชีพ บ้านเกิด และ พท้นหลัง รวมถึง เลเวล Combat & Core Stats เอาไว้ใส่ค่า Stats ที่เป็นตัวละคร และ Details & Inventory

<img width="704" height="720" alt="Header" src="https://github.com/user-attachments/assets/0c59e4eb-f315-418c-83cb-1d1fd6722503" />

เริ่มจาก ส่วน Header โดยมีทั้งหมด 8
<img width="1784" height="192" alt="image" src="https://github.com/user-attachments/assets/bfe92a59-0ac1-4798-8e49-ac48661a07ba" />
- 1.CHARACTER NAME สำหรับใส่ชื่อตังละคร
- 2.PLAYER NAME สำหรับใส่ผู้เล่น
- 3.และ 3.1 ใส่ class ซึ้งใน Ak5e Homebrew จะมีอาชีพหลักทั้งหมด 8 อาชีพ และ อาชีพย่อยๆของอาชีพหลักรวมทั้งหมด 54  อาชีพ โดยมี Caster 6 Defender 7 Guard 11 Marksman 8 Medic 5 Specialist 7 Supporter 5 Vanguard 5 โดยใน Arknights sheet อันนี้หากเราเลือกอาชีพหลักได้ ในช่อง SUBCLASS ก็จะมีอาชีพย่อยในคลาสหลักให้เลือก
ภาพตัวอย่าง
<img width="303" height="289" alt="image" src="https://github.com/user-attachments/assets/013ac5e1-c05e-4d69-b0db-f1002de46fcf" />
<img width="297" height="259" alt="image" src="https://github.com/user-attachments/assets/4d317dc3-51d5-4f19-b150-539384b74d86" />
- 4. LMD คือช่องค่าเงินของเกม โดยช่องนี้สามารถลิ้งไปยัง ช่อง LMD ในหน้า Inventory ได้
- 5. 


