# Scenario: Thai Complete Reply (ตอบกลับครบถ้วน)

## Context
Vendor was asked for: pricing, certifications, delivery terms, after-sales, company profile, bank account.
Thai vendor replies in Thai with ALL requested information. Formal business Thai tone.

## Email

From: sales@siritech.co.th
To: procurement@abc.co.th
Subject: Re: ABC Co., Ltd. — ขอข้อมูลผู้ขาย: อุปกรณ์ IT

เรียน ฝ่ายจัดซื้อ บริษัท ABC จำกัด

ขอบคุณที่ให้ความสนใจในผลิตภัณฑ์ของเรา บริษัท ศิริเทค โซลูชั่นส์ จำกัด ยินดีเสนอข้อมูลตามที่ท่านร้องขอ ดังนี้

**ข้อมูลบริษัท:**
- ชื่อบริษัท: บริษัท ศิริเทค โซลูชั่นส์ จำกัด
- เลขทะเบียนนิติบุคคล: 0105559023456
- เลขประจำตัวผู้เสียภาษี: 0-1057-59023-45-6
- ที่อยู่: 321 ถนนเพชรบุรีตัดใหม่ แขวงบางกะปิ เขตห้วยขวาง กรุงเทพฯ 10310
- ก่อตั้ง: พ.ศ. 2559 (2016)
- จำนวนพนักงาน: 120 คน
- เว็บไซต์: www.siritech.co.th
- โทร: 02-641-5555

**ใบรับรอง:**
- ISO 9001:2015 ระบบบริหารคุณภาพ (หมดอายุ 2570-06-30)
- ISO 14001:2015 ระบบจัดการสิ่งแวดล้อม (หมดอายุ 2570-06-30)
- ตัวแทนจำหน่ายที่ได้รับอนุญาตจาก Dell Technologies ระดับ Titanium
- ตัวแทนจำหน่าย HP Inc. ระดับ Gold Partner

**ราคาเสนอ (ไม่รวม VAT):**

| รายการ | ยี่ห้อ/รุ่น | ราคาต่อหน่วย (บาท) |
|--------|-----------|-------------------|
| Laptop Intel i7/16GB/512GB | Dell Latitude 5540 | 67,500 |
| จอมอนิเตอร์ 27" 4K | Dell U2723QE | 13,500 |
| หูฟังไร้สาย BT ANC | Jabra Evolve2 65 | 4,350 |
| Docking Station USB-C | Dell WD22TB4 | 3,900 |

**หมายเหตุ:** สั่งซื้อรวมเกิน 400,000 บาท ลดเพิ่ม 3%

**เงื่อนไขการจัดส่ง:**
- ระยะเวลาจัดส่ง: 7-10 วันทำการ หลังได้รับ PO
- จัดส่งฟรีในเขตกรุงเทพฯ และปริมณฑล
- จัดส่งต่างจังหวัด คิดค่าขนส่งตามจริง
- จัดส่งพร้อมติดตั้งเบื้องต้น

**การรับประกันและบริการหลังการขาย:**
- Laptop และ จอมอนิเตอร์: รับประกัน 3 ปี On-site บริการถึงที่ ภายในวันทำการถัดไป
- หูฟังและ Docking Station: รับประกัน 1 ปี Carry-in
- สายด่วนบริการ: 02-641-5599 (จันทร์-ศุกร์ 08:30-17:30)
- SLA: ตอบกลับภายใน 2 ชั่วโมง แก้ไขภายใน 24 ชั่วโมง

**เงื่อนไขการชำระเงิน:**
- เครดิต 30 วัน หลังจากส่งมอบสินค้าและได้รับ GRN
- ชำระโดยโอนเงินผ่านธนาคาร

**บัญชีธนาคาร:**
- ธนาคาร: ธนาคารกสิกรไทย
- สาขา: เพชรบุรีตัดใหม่
- เลขที่บัญชี: 098-7-65432-1
- ชื่อบัญชี: บริษัท ศิริเทค โซลูชั่นส์ จำกัด

หากท่านต้องการข้อมูลเพิ่มเติม กรุณาติดต่อได้ตลอดเวลาค่ะ

ขอแสดงความนับถือ
สุภาวดี จันทร์แก้ว
ผู้จัดการฝ่ายขาย
บริษัท ศิริเทค โซลูชั่นส์ จำกัด
โทร: 02-641-5555 ต่อ 101
อีเมล: supawadee@siritech.co.th

## Attachments
- Company_Profile_SiriTech.pdf (see attachments folder)
- ISO_9001_Certificate_SiriTech.pdf (see attachments folder)

## Expected Behavior
- Extract: ALL fields — pricing (4 items + volume discount), certifications (4), delivery terms, after-sales/warranty/SLA, payment terms, bank account, company profile
- Language: Thai — agent must parse Thai text correctly
- Missing fields: none
- Action: mark vendor as dataComplete: true
- outreachStatus: "complete"
- dataCompleteness: 100%
