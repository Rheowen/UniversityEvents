# Sprint 2 Backlog — ระบบจัดการกิจกรรมมหาวิทยาลัย

**Sprint Duration:** ช่วงท้ายโครงการ
**Sprint Goal:** ปิดงานค้างหลักของระบบและเตรียมความพร้อมส่งงานรอบสุดท้าย ได้แก่แก้ไขกิจกรรม, เช็กชื่อหน้างาน, ประวัติการเข้าร่วม, แบบประเมิน, และค้นหา/กรองกิจกรรม

---

## User Stories (Planned)

### US-04 — แก้ไขกิจกรรม (Edit Event)
**As an** ผู้จัดกิจกรรม  
**I want to** แก้ไขรายละเอียดกิจกรรมของตัวเอง  
**So that** ข้อมูลกิจกรรมเป็นปัจจุบันและถูกต้อง

**Story Points:** 5  
**Assigned:** Backend + Frontend  
**Status:** ⏳ Planned  
**Dependencies:** US-04 (create event) from previous sprint

**Tasks:**
| # | Task | Estimate |
|---|------|----------|
| T4.1 | เพิ่ม `PATCH /api/events/:eventId` endpoint | 2h |
| T4.2 | เพิ่ม Zod schema สำหรับการแก้ไขข้อมูล | 1h |
| T4.3 | ตรวจสิทธิ์ให้แก้ได้เฉพาะเจ้าของกิจกรรมหรือ ADMIN | 1h |
| T4.4 | UI หน้าแก้ไขกิจกรรม + prefill ข้อมูลเดิม | 2h |
| T4.5 | เพิ่ม unit/integration tests สำหรับ edit flow | 2h |

---

### US-08 — เช็กชื่อเข้าร่วมกิจกรรม (Check-in Attendance)
**As an** ผู้จัดกิจกรรม  
**I want to** เช็กชื่อผู้เข้าร่วมในวันงาน  
**So that** ระบบบันทึกสถานะเข้าร่วมและเวลาเช็กชื่อได้ถูกต้อง

**Story Points:** 8  
**Assigned:** Backend + Frontend  
**Status:** ⏳ Planned  
**Dependencies:** US-07 register flow

**Tasks:**
| # | Task | Estimate |
|---|------|----------|
| T8.1 | เพิ่ม `PATCH /api/events/:eventId/check-in/:userId` endpoint | 2h |
| T8.2 | ตรวจสิทธิ์ผู้เช็กชื่อ (owner event/ADMIN) | 1h |
| T8.3 | ป้องกัน check-in ซ้ำและบันทึก `check_in_time` | 1.5h |
| T8.4 | UI participant list พร้อมปุ่ม check-in | 2h |
| T8.5 | เพิ่ม integration tests สำหรับ check-in rules | 2h |

---

### US-09 — ประวัติการเข้าร่วมกิจกรรม (Participation History)
**As a** นิสิต  
**I want to** ดูประวัติการเข้าร่วมกิจกรรมทั้งหมดของตัวเอง  
**So that** ฉันติดตามกิจกรรมที่เข้าร่วมได้ครบถ้วน

**Story Points:** 5  
**Assigned:** Backend + Frontend  
**Status:** ⏳ Planned  
**Dependencies:** US-08 check-in

**Tasks:**
| # | Task | Estimate |
|---|------|----------|
| T9.1 | เพิ่ม endpoint ประวัติแบบครบทั้งหมด (รองรับ paging/filter) | 2h |
| T9.2 | แยกสถานะ Registered/Attended/Cancelled ใน response | 1h |
| T9.3 | UI หน้าประวัติการเข้าร่วมแบบเต็มรายการ | 2h |
| T9.4 | เพิ่ม filter ตามช่วงเวลาและสถานะ | 1.5h |
| T9.5 | เพิ่ม unit/integration tests | 1.5h |

---

### US-12 — ประเมินความพึงพอใจ (Feedback)
**As a** นิสิต  
**I want to** ให้คะแนนและแสดงความคิดเห็นหลังเข้าร่วมกิจกรรม  
**So that** ผู้จัดกิจกรรมนำผลไปปรับปรุงงานครั้งถัดไป

**Story Points:** 5  
**Assigned:** Backend + Frontend  
**Status:** ⏳ Planned  
**Dependencies:** US-08 check-in, US-09 participation history

**Tasks:**
| # | Task | Estimate |
|---|------|----------|
| T12.1 | ออกแบบตาราง `feedbacks` และ unique constraint (user_id,event_id) | 1.5h |
| T12.2 | เพิ่ม `POST /api/events/:eventId/feedback` endpoint | 1.5h |
| T12.3 | ตรวจเงื่อนไขส่งได้เฉพาะผู้ที่ attended และส่งได้ครั้งเดียว | 1.5h |
| T12.4 | UI ฟอร์มให้คะแนน 1-5 + comment | 2h |
| T12.5 | เพิ่ม tests สำหรับ one-submission rule | 1.5h |

---

### US-13 — ค้นหาและกรองกิจกรรม (Search & Filter)
**As a** ผู้ใช้  
**I want to** ค้นหาและกรองรายการกิจกรรม  
**So that** หา event ที่ตรงความสนใจได้รวดเร็ว

**Story Points:** 5  
**Assigned:** Backend + Frontend  
**Status:** ⏳ Planned  
**Dependencies:** US-06 event listing

**Tasks:**
| # | Task | Estimate |
|---|------|----------|
| T13.1 | เพิ่ม query params สำหรับ `GET /api/events` (q, date, location, status) | 2h |
| T13.2 | ปรับ SQL ให้รองรับ search/filter อย่างปลอดภัย | 1.5h |
| T13.3 | UI search bar + filter panel | 2h |
| T13.4 | เพิ่ม debounce และ reset filter | 1h |
| T13.5 | เพิ่ม tests ครอบคลุมเงื่อนไขค้นหา/กรอง | 1.5h |

---

## Sprint 2 Summary

| US | Story | Points | Status |
|----|-------|--------|--------|
| US-04 | แก้ไขกิจกรรม | 5 | ⏳ Planned |
| US-08 | เช็กชื่อเข้าร่วมกิจกรรม | 8 | ⏳ Planned |
| US-09 | ประวัติการเข้าร่วมกิจกรรม | 5 | ⏳ Planned |
| US-12 | ประเมินความพึงพอใจ | 5 | ⏳ Planned |
| US-13 | ค้นหาและกรองกิจกรรม | 5 | ⏳ Planned |
| **รวม** |  | **28 pts** |  |

---

## Dependencies Map

```text
US-04 (Edit Event)
US-08 (Check-in) ──► US-09 (Participation History) ──► US-12 (Feedback)
US-13 (Search/Filter) พัฒนาได้คู่ขนานกับ US-04 และ US-08
```

## Definition of Done (Sprint 2)

- API ใหม่ผ่าน unit + integration tests
- Frontend flow หลักทำงานจริงบน role ที่เกี่ยวข้อง
- กฎธุรกิจสำคัญผ่านครบ: owner/admin permission, one feedback per attended event
- เอกสาร API/Backlog อัปเดตตาม implementation จริง
- CI ผ่าน (lint + tests)
