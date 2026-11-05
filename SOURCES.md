# แหล่งข้อมูลอ้างอิง (Source Reference)

เอกสารนี้สรุปแหล่งข้อมูลและบริการภายนอกที่ระบบ [index.html](index.html) ใช้งาน

## 1. ข้อมูลหลัก — Google Sheets

| รายการ | ค่า |
|---|---|
| ไฟล์ชีต | https://docs.google.com/spreadsheets/d/1P3pBZPPWAGyDoKfdS1WmI4tfgnWk3vjRUNSeqwnJtDU/edit?usp=sharing |
| Sheet ID | `1P3pBZPPWAGyDoKfdS1WmI4tfgnWk3vjRUNSeqwnJtDU` (ตัวแปร `SHEET_ID`) |
| สิทธิ์ที่ต้องตั้ง | แชร์แบบ "ทุกคนที่มีลิงก์ (Anyone with the link) ดูได้" |
| วิธีอ่านข้อมูล | Google Visualization API (gviz) แบบ JSONP ผ่านฟังก์ชัน `loadGvizSheet()` |
| Endpoint | `https://docs.google.com/spreadsheets/d/{SHEET_ID}/gviz/tq?tqx=out:json;responseHandler={callback}&sheet={ชื่อแท็บ}` |

### แท็บที่ใช้ (`SHEET_TABS`)

| key | ชื่อแท็บ | ประเภท |
|---|---|---|
| `contract` | `เลขที่สัญญา` | สัญญา |
| `po` | `เลขที่ใบสั่งซื้อ/จ้าง/เช่า` | ใบสั่งซื้อ/จ้าง/เช่า |
| `agreement` | `เลขที่ข้อตกลง` | ข้อตกลง |

### คอลัมน์ที่ระบบอ่าน

ระบบหาตำแหน่งคอลัมน์จาก**ชื่อหัวตาราง**ของแต่ละแท็บ (`detectColumns()` + `COL_RULES`) ถ้าหาไม่เจอจะใช้ตำแหน่งสำรองใน `COL_MAP`

| ฟิลด์ | คำที่ใช้จับคู่ในหัวตาราง |
|---|---|
| `no` | คอลัมน์แรกเสมอ |
| `date` | วันที่ |
| `party` | คู่สัญญา / คู่ค้า / ผู้ขาย / ผู้รับจ้าง |
| `project` | รายการ / โครงการ |
| `budget` | วงเงินงบประมาณ |
| `medianPrice` | ราคากลาง |
| `offeredPrice` | ราคาที่เสนอ |
| `agreedPrice` | ราคาที่ตกลง |
| `amount` | วงเงินตามสัญญา |
| `startDate` | เริ่มต้น |
| `endDate` | สิ้นสุด |
| `status` | สถานะ |

> แถวที่ไม่มีทั้ง `รายการ/โครงการ` และ `คู่สัญญา` จะถูกข้าม

## 2. การเขียนข้อมูล — Google Apps Script

| รายการ | ค่า |
|---|---|
| ตัวแปร | `WEB_APP_URL` |
| URL ปัจจุบัน | `https://script.google.com/macros/s/AKfycby9H0DgQCCie6XxnvGmokCxCNwNnv16zlSSH0FZqN-d-ff2tIvoICtasD_xxxhxUaeT9Q/exec` |
| หน้าที่ | บันทึก / แก้ไข / ลบข้อมูล จากปุ่มในระบบ |
| โค้ดต้นแบบ | หน้า "Apps Script" ในระบบ (ตัวแปร `SCRIPT_CODE`) |

> ⚠️ โค้ดต้นแบบในระบบตั้ง `SHEET_ID` เป็นชีตใหม่ (`1P3pBZPPWAGyDoKfdS1WmI4tfgnWk3vjRUNSeqwnJtDU`) แล้ว แต่ Web App ที่ deploy อยู่ตาม `WEB_APP_URL` ยังเป็นโค้ดเก่าที่ผูกกับชีตเดิม (`1kGSQKzbaZQ_CW8vw4qBpEmK4g44JzrGPOFGcobCN1hY`) การบันทึก/แก้ไข/ลบจะลงชีตใหม่ได้ต้อง: เปิดชีตใหม่ → Extensions → Apps Script → วางโค้ดจากหน้า "Apps Script" → Deploy → New deployment (Execute as = Me, Access = Anyone) แล้วเปลี่ยน `WEB_APP_URL` เป็น URL ใหม่

## 3. ไลบรารีและฟอนต์ภายนอก (CDN)

| ชื่อ | ใช้ทำอะไร | URL |
|---|---|---|
| ExcelJS 4.4.0 | ส่งออกรายงานเป็นไฟล์ Excel | https://cdnjs.cloudflare.com/ajax/libs/exceljs/4.4.0/exceljs.min.js |
| IBM Plex Sans Thai | ฟอนต์ข้อความ | https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Thai |
| JetBrains Mono | ฟอนต์ตัวเลข/โค้ด | https://fonts.googleapis.com/css2?family=JetBrains+Mono |

ต้องเชื่อมต่ออินเทอร์เน็ตจึงจะแสดงผลได้ครบ

## 4. การเผยแพร่

| รายการ | ค่า |
|---|---|
| Git repository | https://github.com/toonsmith1/htmltest |
| เว็บไซต์ (GitHub Pages) | https://toonsmith1.github.io/htmltest/ |
| Branch | `main` |

หลัง push GitHub Pages ใช้เวลาประมาณ 1–2 นาทีในการอัปเดต และอาจต้องกด `Ctrl+F5` เพื่อล้าง cache
