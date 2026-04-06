# University Event Management System


## ภาพรวมโครงการ

University Event Management System เป็นแพลตฟอร์มเว็บสำหรับบริหารกิจกรรมภายในมหาวิทยาลัย โดยครอบคลุมกระบวนการหลักตั้งแต่การสร้างกิจกรรม การอนุมัติกิจกรรม การลงทะเบียนเข้าร่วม และการยกเลิกลงทะเบียน



## ฟีเจอร์หลัก

### 1. ระบบบัญชีผู้ใช้และสิทธิ์การเข้าถึง
- สมัครสมาชิกและเข้าสู่ระบบด้วยอีเมล/รหัสผ่าน
- ใช้ JWT สำหรับการยืนยันตัวตน
- ควบคุมสิทธิ์ตามบทบาทผู้ใช้

### 2. ระบบจัดการกิจกรรม
- ผู้สอนหรือผู้ดูแลสร้างกิจกรรมใหม่
- กิจกรรมใหม่เข้าสถานะรออนุมัติ
- แสดงรายการกิจกรรมที่ผ่านการอนุมัติแล้วสำหรับผู้ใช้ทั่วไป

### 3. ระบบอนุมัติและลงทะเบียน
- ผู้มีสิทธิ์ตรวจสอบคิวกิจกรรมที่รออนุมัติ
- อนุมัติหรือปฏิเสธกิจกรรมพร้อมบันทึกผล
- นิสิตลงทะเบียนเข้าร่วมกิจกรรมและยกเลิกการลงทะเบียนได้

### 4. ระบบตรวจสอบคุณภาพ
- Unit และ Integration tests ด้วย Jest + Supertest
- วัด coverage อัตโนมัติ
- ตรวจคุณภาพโค้ดด้วย ESLint

## บทบาทผู้ใช้งาน

| บทบาท | หน้าที่หลัก |
|---|---|
| STUDENT | ดูกิจกรรมที่อนุมัติแล้ว ลงทะเบียน และยกเลิกการลงทะเบียน |
| LECTURER | สร้างกิจกรรมและอนุมัติกิจกรรมตามสิทธิ์ |

## เทคโนโลยีที่ใช้

- Frontend: React + Vite
- Backend: Node.js + Express
- Database: MySQL
- Validation: Zod
- Authentication: JWT + bcryptjs
- Testing: Jest + Supertest
- Quality: ESLint
- Environment: Docker Compose (สำหรับ MySQL/phpMyAdmin)

## โครงสร้างโปรเจกต์

```text
.
├── backend
│   ├── database
│   ├── src
│   │   ├── config
│   │   ├── controllers
│   │   ├── middlewares
│   │   ├── models
│   │   ├── routes
│   │   ├── utils
│   │   └── validators
│   └── tests
│       ├── integration
│       └── unit
├── frontend
│   ├── public
│   └── src
│       ├── api
│       ├── components
│       ├── context
│       └── pages
├── docs
├── coverage
└── docker-compose.yml
```

## การติดตั้งและเริ่มใช้งาน

### ทางเลือก A: ใช้ Docker Compose สำหรับฐานข้อมูล

1. เริ่มบริการฐานข้อมูล

```bash
docker compose up -d
```

2. เปิด phpMyAdmin
- URL: http://localhost:8080
- Server: mysql
- Username: root
- Password: 11111111

3. ตั้งค่าไฟล์ของ backend

```env
DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=11111111
DB_NAME=university_events_db
PORT=5001
```

### ทางเลือก B: ใช้ MySQL ในเครื่อง

1. คัดลอก backend/.env.example เป็น backend/.env
2. สร้าง schema ด้วยไฟล์ backend/database/schema.sql
3. ติดตั้ง dependencies

```bash
cd backend
npm install

cd ../frontend
npm install
```

4. รัน backend

```bash
cd backend
npm run dev
```

5. รัน frontend

```bash
cd frontend
npm run dev
```

ค่า API พื้นฐานของ frontend คือ http://localhost:5001/api

## API หลักที่รองรับ

- POST /api/auth/register
- POST /api/auth/login
- GET /api/auth/me
- GET /api/events
- POST /api/events
- GET /api/events/registrations/me
- POST /api/events/:eventId/register
- PATCH /api/events/:eventId/cancel-registration
- GET /api/approvals/pending
- PATCH /api/approvals/:eventId

## การทดสอบ

รันจาก root โปรเจกต์

```bash
npm --prefix backend test
npm --prefix backend run test:unit
npm --prefix backend run test:integration
npm --prefix backend run test:coverage
```

รายงาน coverage ถูกสร้างในโฟลเดอร์ coverage

## สถานะโครงการ

สถานะปัจจุบัน: พัฒนาและทดสอบฟีเจอร์หลักเสร็จในระดับใช้งานได้

แนวทางพัฒนาต่อ:
- เพิ่ม branch coverage สำหรับจุดที่ยังต่ำ
- เพิ่ม rate limiting และ security logging
- ทำ load test อย่างเป็นทางการสำหรับ production readiness

## คณะผู้จัดทำ

| ชื่อ-นามสกุล | บทบาท |
|---|---|
| นางสาวกมลชนก เรืองแสน | Product Owner |
| พชรพล เชิดชู | Scrum Master |
| นายทิษณุ กลิ่นกำธรกุล | Developer |
| นายรพีพัฒน์ ทับทอง | QA / DevOps |
| นายเทพเมธี ศรีพล | QA / DevOps |

จัดทำสำหรับรายวิชา 88744065 Software Development
