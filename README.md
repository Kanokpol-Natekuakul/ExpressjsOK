# Express SlipOK API

Express.js API สำหรับการประมวลผลไฟล์ผ่าน SlipOK service

## คำอธิบาย

โปรเจกต์นี้เป็น RESTful API ที่สร้างด้วย Express.js เพื่อรับไฟล์จากผู้ใช้และส่งต่อไปยัง SlipOK API สำหรับการประมวลผล เหมาะสำหรับการตรวจสอบสลิปการโอนเงิน

## คุณสมบัติ

- รองรับการอัปโหลดไฟล์ด้วย Multer
- ส่งต่อไฟล์ไปยัง SlipOK API
- CORS Support สำหรับ Cross-Origin requests
- การจัดการ Environment Variables ด้วย dotenv

## การติดตั้ง

1. Clone โปรเจกต์
```bash
git clone <repository-url>
cd express-slipok
```

2. ติดตั้ง dependencies
```bash
npm install
```

3. สร้างไฟล์ `.env` และตั้งค่าตัวแปรสภาพแวดล้อม
```env
API_URL=<SlipOK_API_URL>
API_KEY=<your_api_key>
```

## การใช้งาน

### เริ่มต้นเซิร์ฟเวอร์

```bash
npm start
```

เซิร์ฟเวอร์จะทำงานที่ port 3000

### API Endpoints

#### 1. อัปโหลดไฟล์ SlipOK

**POST** `/slipok`

- **Content-Type**: `multipart/form-data`
- **Body**: ไฟล์ใน field `files`

**ตัวอย่างการใช้งาน:**

```javascript
const formData = new FormData();
formData.append('files', file);

fetch('http://localhost:3000/slipok', {
  method: 'POST',
  body: formData
})
.then(response => response.json())
.then(data => console.log(data));
```

**Response:**
- สำเร็จ: ข้อมูลจาก SlipOK API
- ล้มเหลว: HTTP 500 พร้อมข้อความ error

#### 2. ตรวจสอบสถานะ

**GET** `/`

ส่งคืน API URL ที่กำหนดไว้ในตัวแปรสภาพแวดล้อม

**Response:**
```json
{
  "msg": "API_URL_VALUE"
}
```

## Dependencies

- **express** (^5.1.0) - Web framework สำหรับ Node.js
- **cors** (^2.8.5) - CORS middleware
- **axios** (^1.11.0) - HTTP client สำหรับการเรียก API
- **multer** (^2.0.2) - Middleware สำหรับการจัดการ multipart/form-data
- **form-data** (^4.0.4) - Library สำหรับสร้าง form data
- **dotenv** (^17.2.1) - โหลดตัวแปรสภาพแวดล้อมจากไฟล์ .env

## โครงสร้างโปรเจกต์

```
express-slipok/
├── index.js          # ไฟล์หลักของแอปพลิเคชัน
├── package.json      # ข้อมูลโปรเจกต์และ dependencies
├── package-lock.json # Lock file สำหรับ dependencies
├── .gitignore        # ไฟล์ที่ไม่ต้องการ commit
└── .env             # ตัวแปรสภาพแวดล้อม (ไม่ถูก commit)
```

## การกำหนดค่า Environment Variables

สร้างไฟล์ `.env` ในโฟลเดอร์รูทของโปรเจกต์:

```env
API_URL=https://api.slipok.com/api/line/apikey/
API_KEY=your_slipok_api_key_here
```

## การจัดการข้อผิดพลาด

API จะส่งคืน HTTP status codes ดังนี้:

- **200**: สำเร็จ
- **500**: เกิดข้อผิดพลาดภายในเซิร์ฟเวอร์

กรณีเกิดข้อผิดพลาด จะได้รับข้อความ error จาก response

## ข้อควรระวัง

1. ตรวจสอบให้แน่ใจว่าได้ตั้งค่า API_URL และ API_KEY ถูกต้องในไฟล์ `.env`
2. ไฟล์ `.env` ไม่ควรถูก commit ไปยัง repository
3. ตรวจสอบว่า SlipOK API service พร้อมใช้งาน

## การพัฒนาเพิ่มเติม

สำหรับการพัฒนาเพิ่มเติม แนะนำให้:

1. เพิ่ม validation สำหรับไฟล์ที่อัปโหลด
2. เพิ่ม logging system
3. เพิ่ม rate limiting
4. เพิ่ม authentication/authorization
5. เพิ่ม unit tests

