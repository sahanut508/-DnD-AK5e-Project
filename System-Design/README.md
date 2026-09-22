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

โดยเริ่มจาก ส่วน Header
