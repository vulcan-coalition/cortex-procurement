# Scenario: Thai Counter-Question Reply (ถามกลับก่อนเสนอราคา)

## Context
Vendor was asked for: pricing, certifications, delivery terms, after-sales, company profile, bank account.
Thai vendor asks detailed clarifying questions in Thai before providing a quote. Shows strong technical knowledge.

## Email

From: presales@datasphere.co.th
To: procurement@abc.co.th
Subject: Re: ABC Co., Ltd. — ขอข้อมูลผู้ขาย: อุปกรณ์ IT

เรียน ทีมจัดซื้อ บริษัท ABC จำกัด

ขอบคุณที่สนใจสินค้าของ DataSphere ครับ ก่อนที่ผมจะเสนอราคาอย่างเป็นทางการ อยากขอสอบถามรายละเอียดเพิ่มเติมสักเล็กน้อยครับ เพื่อให้ผมเสนอสเปคและราคาที่เหมาะสมที่สุดกับความต้องการของท่าน

**เรื่องโน้ตบุ๊ค:**
1. ต้องการ CPU รุ่น i7-1355U (ประหยัดไฟ) หรือ i7-1370P (ประสิทธิภาพสูง) ครับ? ราคาต่างกันประมาณ 5,000-8,000 บาท
2. ต้องการหน้าจอ 14 นิ้ว หรือ 15.6 นิ้ว ครับ? มีทั้ง FHD และ 2K ให้เลือก
3. ต้องการ Windows 11 Pro พร้อมเครื่อง หรือใช้ License ของทาง ABC เองครับ?
4. มีแผนจะใช้งาน Docking Station ร่วมกับโน้ตบุ๊คด้วยใช่ไหมครับ? ถ้าใช่ ผมจะเสนอโน้ตบุ๊ครุ่นที่มี Thunderbolt 4 เพื่อให้ใช้งานร่วมกันได้ดีที่สุด

**เรื่องจอมอนิเตอร์:**
5. ต้องการ USB-C แบบ Power Delivery กี่วัตต์ครับ? ถ้าต้องชาร์จโน้ตบุ๊คผ่านจอ ต้องใช้อย่างน้อย 65W ครับ
6. ต้องการ Built-in KVM Switch ไหมครับ? สะดวกสำหรับคนที่ใช้โน้ตบุ๊คหลายเครื่อง

**เรื่องจำนวนสั่งซื้อ:**
7. จำนวน 5 ชุด / 10 ชุด ที่แจ้งมา เป็นจำนวนแน่นอนหรือมีแผนจะสั่งเพิ่มภายในปีนี้ครับ? ถ้ามีแผนสั่งเพิ่ม ผมจะเสนอเป็น Framework Agreement ให้ล็อคราคาทั้งปี

**เรื่องงบประมาณ:**
8. งบประมาณ 350,000 บาท รวม VAT หรือยังไม่รวมครับ?

ผมพร้อมเสนอราคาภายใน 2 วันทำการหลังจากได้รับคำตอบครับ

ขอบคุณครับ
วิศรุต เจริญสุข
Pre-sales Consultant
บริษัท เดต้าสเฟียร์ จำกัด
โทร: 02-456-7890
มือถือ: 089-012-3456
อีเมล: wisarut@datasphere.co.th

## Attachments
None

## Expected Behavior
- Extract: contact person (name, phone, mobile, email, role), company name
- Vendor shows strong technical expertise — positive signal for Quality & Spec criterion
- Note: vendor offers Framework Agreement option — relevant for contract negotiation
- NOT extractable: pricing, certifications, delivery terms, after-sales, bank account
- Still missing: all originally requested fields except company name and contact
- Action: draft a reply in Thai that:
  1. Answers all 8 questions using data from the PR (specs, quantities, budget, OS requirement)
  2. Re-requests the missing data (certifications, company profile, bank account)
  3. Mentions interest in Framework Agreement if applicable
- outreachStatus: "in_progress"
- dataCompleteness: ~10%
- Flag: vendor is highly engaged and technically strong — worth pursuing despite no data yet
