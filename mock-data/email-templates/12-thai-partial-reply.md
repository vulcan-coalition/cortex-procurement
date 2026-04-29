# Scenario: Thai Partial Reply (ตอบกลับบางส่วน)

## Context
Vendor was asked for: pricing, certifications, delivery terms, after-sales, company profile, bank account.
Thai vendor replies with pricing and basic company info only. Informal but polite Thai tone.

## Email

From: sale@commart-supply.co.th
To: procurement@abc.co.th
Subject: Re: ABC Co., Ltd. — ขอข้อมูลผู้ขาย: อุปกรณ์ IT

สวัสดีครับ ฝ่ายจัดซื้อ ABC

ขอบคุณที่ติดต่อมาครับ ผมขอส่งราคาเบื้องต้นให้ก่อนนะครับ

**ราคาสินค้า (ยังไม่รวม VAT 7%):**
- โน้ตบุ๊ค i7/16GB/512GB — 70,000 บาท/เครื่อง (ยี่ห้อ Lenovo ThinkPad E16)
- จอ 27 นิ้ว 4K — 14,800 บาท/จอ
- หูฟังบลูทูธ ANC — 4,700 บาท/ชุด
- Docking Station USB-C — 4,200 บาท/ตัว

ราคานี้เป็นราคาสำหรับหน่วยงานครับ ถ้าสั่งเยอะคุยลดได้อีกครับ

**ข้อมูลบริษัทคร่าวๆ:**
- ชื่อ: บริษัท คอมมาร์ทซัพพลาย จำกัด
- เปิดมาประมาณ 8 ปี
- ออฟฟิศอยู่แถวพันธุ์ทิพย์ ประตูน้ำ
- ลูกค้าหลักๆ เป็นบริษัทเอกชนและโรงเรียนครับ

ส่วนเรื่องใบรับรอง ISO กับรายละเอียดการจัดส่ง ขอเวลาเตรียมข้อมูลสัก 2-3 วันนะครับ

ขอบคุณครับ
ธนกร วงศ์สุวรรณ
ฝ่ายขาย คอมมาร์ทซัพพลาย
โทร: 085-999-1234
Line: @commart-supply

## Attachments
None

## Expected Behavior
- Extract: pricing (4 items, informal format), company name, approximate years in business (8 years), location (Pantip/Pratunam area), client types (private companies, schools), contact (phone + Line ID)
- Note: informal Thai — "คุยลดได้อีก" means negotiable pricing, "คร่าวๆ" means rough/approximate
- Still missing: certifications, delivery terms, after-sales/warranty, bank account, formal address, tax ID
- Action: draft follow-up in Thai requesting remaining fields
- outreachStatus: "in_progress"
- dataCompleteness: ~35%
- Flag: vendor uses Line for communication — note for contact preference
