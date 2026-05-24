---
title: "ชุดข้อมูลสแกน 3 มิติ เมืองขอนแก่น"
track: "Smart City"
domain:
  - "Urban"
  - "Computer Vision"
  - "3D Point Cloud"
source:
  - "Khon Kaen"
total_records: 1274
sampled_records: 12
filetype:
  - "tar.gz"

---

# ชุดข้อมูลสแกน 3 มิติ เมืองขอนแก่น

## คำอธิบาย
ชุดข้อมูลนี้ประกอบด้วยไฟล์ 3D Model และ Point Cloud ที่ได้จากการสแกนพื้นที่เมือง โดยจัดเก็บในรูปแบบ:
- **OBJ files**: ไฟล์แบบจำลอง 3D พร้อม Texture (`.obj`, `.mtl`)
- **3mxb files** (3MX): ไฟล์ Scene แบบละเอียด แบ่งตาม Tile พิกัด เป็นรูปแบบไฟล์ Point Cloud / 3D Mesh ของ **Bentley Systems** (ContextCapture / MicroStation)
- **metadata.xml**: ข้อมูลเมตาของชุดข้อมูล

ข้อมูลถูกแบ่งเป็น Tiles ตามพิกัด (เช่น `Tile_+010_+035`) เพื่อการบริหารจัดการพื้นที่แบบ Grid

## ฟิลด์ข้อมูล
ข้อมูลรูปแบบ 3D Point Cloud / Mesh ไม่มีฟิลด์แบบตาราง (tabular) แต่มีโครงสร้างเป็นไฟล์แบบจำลอง 3D พร้อม texture และ metadata

## โครงสร้างไฟล์
| ไฟล์ | รายละเอียด |
|------|----------|
| [`3D_KKC_sampled.tar.gz`](3D_KKC_sampled.tar.gz) | ไฟล์ข้อมูล 3D Scan (compressed) |

โครงสร้างภายในไฟล์:
```
├── Obj/
│   ├── Data/
│   │   └── Tile_+010_+035/   (และ Tiles อื่นๆ)
│   │       ├── *.obj          # ไฟล์แบบจำลอง 3D
│   │       ├── *.mtl          # Material definition
│   │       └── *.jpg          # Texture
│   └── metadata.xml
└── Production_2/
    └── Scene/
        └── Data/
            └── Tile_p010_p035/   (และ Tiles อื่นๆ)
                ├── *.3mxb         # ไฟล์ Scene แบบละเอียด
                └── metadata.xml
```

## โจทย์ / แนวทางวิเคราะห์
- **การจัดการเมืองและวางผังเมือง**: วิเคราะห์การใช้พื้นที่สาธารณะ โครงสร้างพื้นฐาน
- **Object Detection ใน 3D Space**: ตรวจจับและนับอาคาร ยานพาหนะ ต้นไม้
- **Change Detection**: เปรียบเทียบการเปลี่ยนแปลงของพื้นที่ระหว่างช่วงเวลา
- **City Infrastructure Analysis**: วิเคราะห์โครงสร้างพื้นฐาน เช่น ถนน สะพาน

## หมายเหตุ
- ข้อมูลนี้เป็นตัวอย่างที่ sampled แล้ว
- ไฟล์ถูกจัดเก็บในรูปแบบ `.tar.gz`
- **3MX (3mxb)** เป็นรูปแบบไฟล์ Point Cloud / 3D Mesh ของ **Bentley Systems** ใช้กับ ContextCapture และ MicroStation เป็น binary scene format ที่แบ่งข้อมูลเป็น LOD (Level of Detail) pyramid ตาม spatial tiles
  - อ่านเพิ่มเติม: [Bentley ContextCapture 3MX Format](https://docs.bentley.com/LiveContent/web/ContextCapture%20Help-v18/en/GUID-CED0ABE6-2EE3-458D-9810-D87EC3C521BD.html)
