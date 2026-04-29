# Scenario: Thai Formal Quotation Reply (ใบเสนอราคาอย่างเป็นทางการ)

## Context
Vendor was asked for: pricing, certifications, delivery terms, after-sales, company profile, bank account.
Thai vendor replies formally with a brief email and attaches an official quotation document and company profile.

## Email

From: quotation@thaicyber.co.th
To: procurement@abc.co.th
Subject: Re: ABC Co., Ltd. — ขอข้อมูลผู้ขาย: อุปกรณ์ IT

เรียน ฝ่ายจัดซื้อ บริษัท ABC จำกัด

ตามที่ท่านได้สอบถามข้อมูลมา บริษัท ไทยไซเบอร์เทค จำกัด ขอนำเสนอรายละเอียดตามเอกสารแนบ ดังนี้

1. ใบเสนอราคา (QT-TC-2026-0456)
2. ข้อมูลบริษัทและใบรับรอง
3. เงื่อนไขการจัดส่งและบริการหลังการขาย

หากท่านมีข้อสงสัยเพิ่มเติม สามารถติดต่อได้ที่เบอร์โทรด้านล่างค่ะ

ขอแสดงความนับถือ
พิมพ์ชนก ศรีสุข
เจ้าหน้าที่ฝ่ายขายอาวุโส
บริษัท ไทยไซเบอร์เทค จำกัด
โทร: 02-888-7777 ต่อ 305
มือถือ: 091-234-5678
อีเมล: pimchanok.s@thaicyber.co.th

## Attachments
- ใบเสนอราคา_QT-TC-2026-0456.pdf (see attachments folder)
- ข้อมูลบริษัท_ThaiCyberTech.pdf (see attachments folder)
- เงื่อนไขการให้บริการ.docx (see attachments folder)

## Expected Behavior
- Email body is brief — all data is in the 3 attachments
- Extract from quotation PDF: pricing (4 items), payment terms, validity
- Extract from company profile PDF: company details, certifications, references, bank account
- Extract from service terms DOCX: delivery terms, warranty, SLA, penalties
- Still missing: possibly nothing — check all attachments thoroughly
- Action: likely dataComplete: true if all attachments contain full data
- outreachStatus: "complete"
- dataCompleteness: ~95-100%
