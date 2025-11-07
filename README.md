# 🚀 คู่มือสอนพัฒนา APIs/RESTful APIs แบบ Step-by-Step (ฉบับสมบูรณ์)

<div align="center">

```
╔═══════════════════════════════════════════════════════════════════════════╗
║                                                                           ║
║   📚 REST API Development Tutorial - From Zero to Production Hero 🚀     ║
║                                                                           ║
║   บทเรียนพัฒนา REST API อย่างครบถ้วน ตั้งแต่พื้นฐานถึงระดับ Production   ║
║                                                                           ║
╚═══════════════════════════════════════════════════════════════════════════╝
```

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Tutorial Steps](https://img.shields.io/badge/steps-100+-green.svg)](#)
[![Language](https://img.shields.io/badge/language-ไทย-red.svg)](#)

</div>

---

## 📋 สารบัญ

```
┌─────────────────────────────────────────────────────────────┐
│                     TABLE OF CONTENTS                       │
├─────────────────────────────────────────────────────────────┤
│  1. ภาพรวมโปรเจค                                            │
│  2. วัตถุประสงค์และเป้าหมายการเรียนรู้                       │
│  3. โครงสร้างบทเรียน (100+ ขั้นตอน)                         │
│  4. เทคโนโลยีและเครื่องมือที่ใช้                             │
│  5. ข้อกำหนดเบื้องต้น                                       │
│  6. วิธีการใช้งานบทเรียน                                     │
│  7. โครงสร้างไฟล์ในโปรเจค                                    │
│  8. แผนการเรียนรู้แบบขั้นตอน                                 │
│  9. การติดตั้งและเตรียมสภาพแวดล้อม                           │
│ 10. แหล่งข้อมูลเพิ่มเติม                                     │
└─────────────────────────────────────────────────────────────┘
```

---

## 🎯 ภาพรวมโปรเจค

บทเรียนนี้เป็นคู่มือการพัฒนา **APIs/RESTful APIs** อย่างละเอียดและครบถ้วน ครอบคลุมทั้ง**ทฤษฎีและภาคปฏิบัติ** ตั้งแต่พื้นฐานจนถึงระดับที่พร้อมใช้งานจริงใน Production

### 🌟 จุดเด่นของบทเรียน

```
┌──────────────────────────────────────────────────────────────────┐
│                     🌟 FEATURES HIGHLIGHTS                       │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ✅ 100+ ขั้นตอนการสอนแบบละเอียด (ขยายได้ถึง 1000+ ขั้นตอน)     │
│  ✅ ไดอะแกรม Unicode Box-Drawing ทุกขั้นตอน                      │
│  ✅ โค้ดตัวอย่างจริงพร้อมใช้งาน (Multi-Stack Support)            │
│  ✅ แบบฝึกหัดและเช็กลิสต์ตรวจสอบทุกบท                           │
│  ✅ ครอบคลุมตั้งแต่ HTTP พื้นฐานถึง Production-Ready             │
│  ✅ รองรับหลายภาษา: Node.js, Python, Go, Java                   │
│  ✅ Best Practices และ Security Guidelines                      │
│  ✅ CI/CD, Docker, Kubernetes Integration                        │
│  ✅ Testing: Unit, Integration, E2E, Contract                    │
│  ✅ Observability: Logs, Metrics, Tracing                        │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

## 🎓 วัตถุประสงค์และเป้าหมายการเรียนรู้

### ผลลัพธ์การเรียนรู้ (Learning Outcomes)

เมื่อเรียนจบหลักสูตรนี้ คุณจะสามารถ:

```
┌─────────────────────────────────────────────────────────────────┐
│                    🎯 LEARNING OUTCOMES                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1️⃣  ออกแบบ API ที่สอดคล้องกับ Domain                          │
│     • Resource-oriented design                                 │
│     • Stable และ evolvable API contracts                      │
│     • Version management strategies                            │
│                                                                 │
│  2️⃣  ใช้ HTTP Protocol อย่างถูกต้อง                            │
│     • HTTP Methods (GET, POST, PUT, PATCH, DELETE)             │
│     • Status Codes (1xx-5xx) และความหมาย                       │
│     • Headers: Content-Type, Authorization, Caching            │
│     • Content Negotiation                                      │
│                                                                 │
│  3️⃣  พัฒนา API ที่ปลอดภัยและตรวจสอบได้                         │
│     • Authentication & Authorization (JWT, OAuth2, mTLS)       │
│     • Input Validation & Sanitization                          │
│     • Rate Limiting & Quota Management                         │
│     • Audit Logging & Compliance                               │
│                                                                 │
│  4️⃣  สร้างเอกสาร API อัตโนมัติ                                 │
│     • OpenAPI Specification (Swagger)                          │
│     • SDK Generation                                           │
│     • Contract Testing                                         │
│     • Interactive Documentation                                │
│                                                                 │
│  5️⃣  ตั้งค่า Observability ครบถ้วน                             │
│     • Structured Logging (JSON logs)                           │
│     • Metrics Collection (Prometheus)                          │
│     • Distributed Tracing (OpenTelemetry)                      │
│     • Dashboards & Alerts                                      │
│                                                                 │
│  6️⃣  ปรับแต่งประสิทธิภาพและ Scalability                        │
│     • Pagination Strategies                                    │
│     • Caching (Redis, CDN)                                     │
│     • Async Processing                                         │
│     • CQRS Pattern                                             │
│                                                                 │
│  7️⃣  Deploy API สู่ Production                                 │
│     • Containerization (Docker)                                │
│     • Orchestration (Kubernetes)                               │
│     • CI/CD Pipelines                                          │
│     • Blue-Green & Canary Deployments                          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📚 โครงสร้างบทเรียน (100+ ขั้นตอน)

บทเรียนแบ่งออกเป็น **10 หมวดหลัก** ครอบคลุม **100+ ขั้นตอน**:

```
┌──────────────────────────────────────────────────────────────────┐
│                   📖 CURRICULUM STRUCTURE                        │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  📘 PART 01 (Steps 01-10): พื้นฐาน HTTP & REST Principles       │
│  │  └─ HTTP Protocol, REST Architecture, Design Principles      │
│  │                                                               │
│  📗 PART 02 (Steps 11-20): HTTP Methods, Status Codes, Headers  │
│  │  └─ GET/POST/PUT/PATCH/DELETE, 2xx/4xx/5xx, Headers          │
│  │                                                               │
│  📙 PART 03 (Steps 21-30): REST Resource Modeling & URI Design  │
│  │  └─ Resources, Collections, Naming, Relationships            │
│  │                                                               │
│  📕 PART 04 (Steps 31-40): API Contract & OpenAPI Specification │
│  │  └─ Contract-First Design, OpenAPI 3.0, Documentation        │
│  │                                                               │
│  📔 PART 05 (Steps 41-50): Project Setup & Structure            │
│  │  └─ Project Scaffolding, Folder Structure, Dependencies      │
│  │                                                               │
│  📓 PART 06 (Steps 51-60): CRUD Operations Implementation       │
│  │  └─ Create, Read, Update, Delete + Advanced Operations       │
│  │                                                               │
│  📒 PART 07 (Steps 61-70): Validation & Error Handling          │
│  │  └─ Schema Validation, Error Formats, Global Handlers        │
│  │                                                               │
│  📖 PART 08 (Steps 71-80): Authentication & Authorization       │
│  │  └─ JWT, OAuth2, RBAC, Scopes, Permissions                   │
│  │                                                               │
│  📘 PART 09 (Steps 81-90): Security Best Practices              │
│  │  └─ OWASP Top 10, Rate Limiting, Security Headers            │
│  │                                                               │
│  📗 PART 10 (Steps 91-100): Database & ORM Integration          │
│     └─ Prisma, TypeORM, Sequelize, Migrations, Seeding          │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘

                            ⋮ (ขยายต่อได้ถึง 1000+ steps)

┌──────────────────────────────────────────────────────────────────┐
│  📙 PART 11-20: Advanced Topics (Steps 101-200)                  │
│  📕 PART 21-30: Testing & QA (Steps 201-300)                     │
│  📔 PART 31-40: Performance & Caching (Steps 301-400)            │
│  📓 PART 41-50: Observability (Steps 401-500)                    │
│  📒 PART 51-60: CI/CD & DevOps (Steps 501-600)                   │
│  📖 PART 61-70: Containerization (Steps 601-700)                 │
│  📘 PART 71-80: Microservices (Steps 701-800)                    │
│  📗 PART 81-90: GraphQL & gRPC (Steps 801-900)                   │
│  📙 PART 91-100: Production Deployment (Steps 901-1000)          │
└──────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ เทคโนโลยีและเครื่องมือที่ใช้

### Stack Options (เลือกได้ตามความถนัด)

```
┌─────────────────────────────────────────────────────────────────┐
│                     🛠️  TECHNOLOGY STACKS                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  🟢 Node.js / TypeScript Stack                                 │
│     ├─ Runtime: Node.js 20+ / Bun 1.0+                         │
│     ├─ Framework: Express, Fastify, Hono, Elysia               │
│     ├─ Validation: Zod, TypeBox, Joi                           │
│     ├─ ORM: Prisma, Drizzle, TypeORM                           │
│     └─ Testing: Jest, Vitest, Supertest                        │
│                                                                 │
│  🔵 Python Stack                                                │
│     ├─ Runtime: Python 3.11+                                   │
│     ├─ Framework: FastAPI, Django REST, Flask                  │
│     ├─ Validation: Pydantic, Marshmallow                       │
│     ├─ ORM: SQLAlchemy, Django ORM, Tortoise                   │
│     └─ Testing: pytest, httpx                                  │
│                                                                 │
│  🔷 Go Stack                                                    │
│     ├─ Runtime: Go 1.21+                                       │
│     ├─ Framework: chi, echo, fiber, gin                        │
│     ├─ Validation: go-playground/validator                     │
│     ├─ ORM: GORM, sqlx, ent                                    │
│     └─ Testing: testing package, testify                       │
│                                                                 │
│  🟠 Java Stack                                                  │
│     ├─ Runtime: Java 17+ / Spring Boot 3+                      │
│     ├─ Framework: Spring WebFlux, Micronaut, Quarkus           │
│     ├─ Validation: Bean Validation (JSR 380)                   │
│     ├─ ORM: Spring Data JPA, Hibernate                         │
│     └─ Testing: JUnit 5, RestAssured, MockMvc                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                   🔧 COMMON TOOLS & SERVICES                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  📝 API Specification                                           │
│     └─ OpenAPI 3.0+, Swagger UI, Redoc, Stoplight              │
│                                                                 │
│  🗄️  Databases                                                  │
│     └─ PostgreSQL, MySQL, MongoDB, Redis                        │
│                                                                 │
│  🔐 Authentication                                              │
│     └─ JWT, OAuth2, Auth0, Keycloak, Firebase Auth             │
│                                                                 │
│  📊 Observability                                               │
│     └─ Prometheus, Grafana, Jaeger, ELK Stack, Datadog         │
│                                                                 │
│  🐳 Containerization                                            │
│     └─ Docker, Docker Compose, Kubernetes, Helm                 │
│                                                                 │
│  🚀 CI/CD                                                       │
│     └─ GitHub Actions, GitLab CI, Jenkins, CircleCI            │
│                                                                 │
│  🧪 Testing                                                     │
│     └─ Postman, Insomnia, k6, Artillery, Locust, JMeter        │
│                                                                 │
│  🌐 API Gateway                                                 │
│     └─ Kong, NGINX, Traefik, AWS API Gateway, Azure APIM       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## ✅ ข้อกำหนดเบื้องต้น

### ความรู้พื้นฐานที่ควรมี

```
┌─────────────────────────────────────────────────────────────────┐
│                    📚 PREREQUISITES                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ความรู้ที่จำเป็น (Required):                                   │
│  ☑️  พื้นฐานการเขียนโปรแกรม (อย่างน้อย 1 ภาษา)                 │
│  ☑️  ความเข้าใจ HTTP/HTTPS                                      │
│  ☑️  Terminal/Command Line พื้นฐาน                              │
│  ☑️  Git พื้นฐาน                                                 │
│                                                                 │
│  ความรู้ที่เป็นประโยชน์ (Recommended):                          │
│  📌 Database พื้นฐาน (SQL)                                      │
│  📌 JSON และ Data Serialization                                │
│  📌 Docker พื้นฐาน                                              │
│  📌 Linux/Unix Commands                                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Software Requirements

```bash
# สำหรับ Node.js Stack
node --version    # v20.0.0 หรือสูงกว่า
npm --version     # v10.0.0 หรือสูงกว่า

# สำหรับ Python Stack
python --version  # 3.11.0 หรือสูงกว่า
pip --version     # 23.0.0 หรือสูงกว่า

# สำหรับ Go Stack
go version        # 1.21.0 หรือสูงกว่า

# สำหรับ Java Stack
java --version    # 17.0.0 หรือสูงกว่า
mvn --version     # 3.9.0 หรือสูงกว่า

# Common Tools
docker --version           # 24.0.0 หรือสูงกว่า
docker-compose --version  # 2.20.0 หรือสูงกว่า
git --version             # 2.40.0 หรือสูงกว่า
curl --version            # 7.0.0 หรือสูงกว่า
```

---

## 🚀 วิธีการใช้งานบทเรียน

### เริ่มต้นอย่างไร?

```
┌─────────────────────────────────────────────────────────────────┐
│                  🎬 GETTING STARTED GUIDE                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  STEP 1: อ่านไฟล์เอกสารภาพรวม                                  │
│  ├─ README.md (ไฟล์นี้) - ภาพรวมและแนวทาง                      │
│  ├─ SUMMARY.md - สรุปเนื้อหาทั้งหมดแบบย่อ                      │
│  └─ TASK.md - รายการงานและแผนการเรียนรู้                       │
│                                                                 │
│  STEP 2: ศึกษาบทเรียนตามลำดับ                                  │
│  ├─ TUTORIAL.md - ดัชนีหลักของบทเรียนทั้งหมด                   │
│  ├─ PART01.md - เริ่มจากพื้นฐาน HTTP & REST                    │
│  ├─ PART02.md - ทำความเข้าใจ Methods และ Status Codes          │
│  └─ ... (ไปตามลำดับ PART03-PART100)                            │
│                                                                 │
│  STEP 3: ทำแบบฝึกหัดและตรวจสอบ                                 │
│  ├─ ทำแบบฝึกหัดในแต่ละ PART                                    │
│  ├─ ใช้ CHECKLIST.md ตรวจสอบความสมบูรณ์                        │
│  └─ บันทึกความคืบหน้าใน TODO.md                                │
│                                                                 │
│  STEP 4: สร้างโปรเจคจริง                                        │
│  ├─ ประยุกต์ความรู้สร้าง API ของตัวเอง                         │
│  ├─ ทดสอบ, Deploy, Monitor                                     │
│  └─ Review และปรับปรุงต่อเนื่อง                                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### แนวทางการเรียนรู้

```
┌──────────────────────────────────────────────────────────────────┐
│                   📖 LEARNING APPROACHES                         │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  🎯 แบบเร่งรัด (Fast Track): 2-4 สัปดาห์                        │
│     ├─ ศึกษาเฉพาะ Core Concepts (PART 01-10)                    │
│     ├─ เน้นทำโปรเจคตัวอย่างควบคู่                              │
│     └─ เหมาะกับผู้มีพื้นฐานอยู่แล้ว                             │
│                                                                  │
│  🎓 แบบมาตรฐาน (Standard): 8-12 สัปดาห์                         │
│     ├─ ศึกษาทุก PART อย่างละเอียด                               │
│     ├─ ทำแบบฝึกหัดครบทุกบท                                      │
│     └─ สร้างโปรเจคตัวอย่างหลายชิ้น                              │
│                                                                  │
│  🏆 แบบเชี่ยวชาญ (Expert): 16-24 สัปดาห์                        │
│     ├─ ศึกษาครบทุก PART รวมถึง Advanced Topics                  │
│     ├─ สร้างโปรเจคขนาดใหญ่พร้อม Production Deployment           │
│     ├─ ศึกษาเพิ่มเติม: Microservices, GraphQL, gRPC             │
│     └─ เตรียมความพร้อมสำหรับ Professional Work                  │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

## 📁 โครงสร้างไฟล์ในโปรเจค

```
restapis/
│
├── 📄 README.md                 # ภาพรวมโปรเจค (ไฟล์นี้)
├── 📄 SUMMARY.md                # สรุปเนื้อหาทั้งหมด
├── 📄 TUTORIAL.md               # ดัชนีบทเรียนหลัก
├── 📄 TASK.md                   # รายการงานและแผนการเรียนรู้
├── 📄 CHECKLIST.md              # เช็กลิสต์ตรวจสอบความสมบูรณ์
├── 📄 TODO.md                   # รายการงานที่ต้องทำ/กำลังทำ
│
├── 📂 docs/                     # เอกสารประกอบ
│   ├── 📄 PART01.md             # บทที่ 1: HTTP & REST Principles
│   ├── 📄 PART02.md             # บทที่ 2: Methods & Status Codes
│   ├── 📄 PART03.md             # บทที่ 3: Resource Modeling
│   ├── 📄 PART04.md             # บทที่ 4: API Contract & OpenAPI
│   ├── 📄 PART05.md             # บทที่ 5: Project Setup
│   ├── 📄 PART06.md             # บทที่ 6: CRUD Operations
│   ├── 📄 PART07.md             # บทที่ 7: Validation & Errors
│   ├── 📄 PART08.md             # บทที่ 8: Authentication
│   ├── 📄 PART09.md             # บทที่ 9: Security
│   ├── 📄 PART10.md             # บทที่ 10: Database & ORM
│   ├── 📄 PART11.md             # บทที่ 11: Advanced Queries
│   ├── 📄 PART12.md             # บทที่ 12: Pagination
│   ├── 📄 PART13.md             # บทที่ 13: Filtering & Sorting
│   ├── 📄 PART14.md             # บทที่ 14: Caching Strategies
│   ├── 📄 PART15.md             # บทที่ 15: Rate Limiting
│   ├── 📄 PART16.md             # บทที่ 16: File Upload
│   ├── 📄 PART17.md             # บทที่ 17: Webhooks
│   ├── 📄 PART18.md             # บทที่ 18: Testing
│   ├── 📄 PART19.md             # บทที่ 19: Logging
│   ├── 📄 PART20.md             # บทที่ 20: Monitoring
│   └── ...                      # (ขยายต่อได้ถึง PART100+)
│
├── 📂 examples/                 # โค้ดตัวอย่าง
│   ├── 📂 nodejs-express/       # ตัวอย่าง Node.js + Express
│   ├── 📂 nodejs-fastify/       # ตัวอย่าง Node.js + Fastify
│   ├── 📂 python-fastapi/       # ตัวอย่าง Python + FastAPI
│   ├── 📂 python-django/        # ตัวอย่าง Python + Django REST
│   ├── 📂 go-chi/               # ตัวอย่าง Go + Chi
│   ├── 📂 java-spring/          # ตัวอย่าง Java + Spring Boot
│   └── 📂 shared/               # Code ที่ใช้ร่วมกัน
│
├── 📂 exercises/                # แบบฝึกหัด
│   ├── 📂 part01-exercises/
│   ├── 📂 part02-exercises/
│   └── ...
│
├── 📂 solutions/                # เฉลยแบบฝึกหัด
│   ├── 📂 part01-solutions/
│   ├── 📂 part02-solutions/
│   └── ...
│
├── 📂 diagrams/                 # ไดอะแกรมและภาพประกอบ
│   ├── 📄 architecture.txt      # ไดอะแกรม Architecture
│   ├── 📄 flow-diagrams.txt     # Flow Diagrams
│   └── 📄 sequence-diagrams.txt # Sequence Diagrams
│
├── 📂 templates/                # เทมเพลตโปรเจค
│   ├── 📂 api-starter-node/
│   ├── 📂 api-starter-python/
│   ├── 📂 api-starter-go/
│   └── 📂 api-starter-java/
│
└── 📂 tools/                    # เครื่องมือและสคริปต์
    ├── 📄 setup.sh              # สคริปต์ติดตั้ง
    ├── 📄 validate.sh           # ตรวจสอบ environment
    └── 📄 test-runner.sh        # รันการทดสอบ

```

---

## 📋 แผนการเรียนรู้แบบขั้นตอน

### Timeline แนะนำ (Standard Track - 12 สัปดาห์)

```
┌──────────────────────────────────────────────────────────────────┐
│                   📅 12-WEEK LEARNING TIMELINE                   │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  🗓️  Week 1-2: Foundation                                        │
│  ├─ PART 01-04: HTTP, REST, Resource Modeling, OpenAPI          │
│  ├─ เรียนรู้พื้นฐาน HTTP และหลักการ REST                        │
│  └─ ฝึกออกแบบ API Contract ด้วย OpenAPI                          │
│                                                                  │
│  🗓️  Week 3-4: Basic Implementation                              │
│  ├─ PART 05-07: Project Setup, CRUD, Validation                 │
│  ├─ ตั้งโปรเจคและสร้าง CRUD API ครบ                             │
│  └─ ทำ Input Validation และ Error Handling                      │
│                                                                  │
│  🗓️  Week 5-6: Security                                          │
│  ├─ PART 08-09: Authentication, Authorization, Security         │
│  ├─ ทำ JWT/OAuth2 Authentication                                │
│  └─ ปรับปรุง Security ตาม OWASP Guidelines                      │
│                                                                  │
│  🗓️  Week 7-8: Data & Persistence                                │
│  ├─ PART 10-14: Database, ORM, Queries, Pagination, Cache       │
│  ├─ เชื่อมต่อฐานข้อมูลและทำ Advanced Queries                    │
│  └─ ทำ Caching และ Performance Optimization                     │
│                                                                  │
│  🗓️  Week 9-10: Quality & Testing                                │
│  ├─ PART 15-20: Rate Limit, Testing, Logging, Monitoring        │
│  ├─ เขียน Unit/Integration/E2E Tests                            │
│  └─ ตั้ง Logging และ Monitoring                                 │
│                                                                  │
│  🗓️  Week 11-12: Deployment                                      │
│  ├─ Advanced Topics: Docker, CI/CD, K8s                          │
│  ├─ Containerize API และตั้ง CI/CD Pipeline                     │
│  └─ Deploy to Production และ Monitor                            │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

## ⚙️ การติดตั้งและเตรียมสภาพแวดล้อม

### Quick Start (5 นาที)

```bash
# 1. Clone โปรเจค (หรือ download ZIP)
git clone https://github.com/yourusername/restapis-tutorial.git
cd restapis-tutorial

# 2. ตรวจสอบ prerequisites
./tools/validate.sh

# 3. เลือก Stack ที่ต้องการ (เช่น Node.js)
cd examples/nodejs-express

# 4. ติดตั้ง dependencies
npm install

# 5. Setup environment
cp .env.example .env

# 6. รัน development server
npm run dev

# 7. ทดสอบ API
curl http://localhost:3000/health
```

### ตั้งค่า Environment Variables

```bash
# .env ตัวอย่าง
NODE_ENV=development
PORT=3000
DATABASE_URL=postgresql://user:password@localhost:5432/apidb
REDIS_URL=redis://localhost:6379
JWT_SECRET=your-super-secret-key-change-in-production
LOG_LEVEL=debug
RATE_LIMIT_MAX=100
RATE_LIMIT_WINDOW_MS=900000
```

### Docker Setup (แนะนำ)

```bash
# รัน API พร้อม Database และ Redis ด้วย Docker Compose
docker-compose up -d

# ตรวจสอบสถานะ
docker-compose ps

# ดู logs
docker-compose logs -f api

# หยุด services
docker-compose down
```

---

## 📖 แหล่งข้อมูลเพิ่มเติม

### เอกสารอ้างอิง

```
┌──────────────────────────────────────────────────────────────────┐
│                      📚 REFERENCES                               │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  📘 HTTP & REST                                                  │
│  ├─ RFC 7230-7235: HTTP/1.1 Specification                       │
│  ├─ RFC 7807: Problem Details for HTTP APIs                     │
│  ├─ Roy Fielding's Dissertation on REST                         │
│  └─ MDN Web Docs: HTTP                                          │
│                                                                  │
│  📗 API Design                                                   │
│  ├─ OpenAPI Specification 3.0+                                  │
│  ├─ Google API Design Guide                                     │
│  ├─ Microsoft REST API Guidelines                               │
│  └─ Zalando RESTful API Guidelines                              │
│                                                                  │
│  📙 Security                                                     │
│  ├─ OWASP API Security Top 10                                   │
│  ├─ OAuth 2.0 RFC 6749                                          │
│  ├─ JWT RFC 7519                                                │
│  └─ NIST Cybersecurity Framework                                │
│                                                                  │
│  📕 Best Practices                                               │
│  ├─ The Twelve-Factor App                                       │
│  ├─ Cloud Native Computing Foundation (CNCF)                    │
│  └─ Site Reliability Engineering (SRE) Books                    │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### เครื่องมือแนะนำ

- **API Testing**: Postman, Insomnia, HTTPie, curl
- **API Documentation**: Swagger UI, Redoc, Stoplight
- **Load Testing**: k6, Artillery, Locust, Apache JMeter
- **Monitoring**: Prometheus + Grafana, Datadog, New Relic
- **Logging**: ELK Stack, Loki, Papertrail
- **Tracing**: Jaeger, Zipkin, OpenTelemetry

---

## 🤝 การสนับสนุนและช่วยเหลือ

### ติดต่อและสอบถาม

```
┌──────────────────────────────────────────────────────────────────┐
│                       💬 SUPPORT                                 │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  📧 Email: support@example.com                                   │
│  💬 Discord: https://discord.gg/xxxxx                            │
│  🐛 Issues: https://github.com/xxx/restapis/issues               │
│  💡 Discussions: https://github.com/xxx/restapis/discussions     │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

## 📜 License

```
MIT License

Copyright (c) 2025 REST API Tutorial Project

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files...
```

---

## 🎉 เริ่มต้นการเรียนรู้

พร้อมแล้วหรือยัง? มาเริ่มต้นสร้าง APIs ที่ยอดเยี่ยมกันเลย!

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│        👉 เริ่มจาก TUTORIAL.md หรือ PART01.md ได้เลย!           │
│                                                                  │
│              🚀 Happy API Development! 🚀                        │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

<div align="center">

**สร้างด้วย ❤️ เพื่อชุมชนนักพัฒนา Thai Developer Community**

⭐ ถ้าชอบบทเรียนนี้ อย่าลืมกด Star ด้วยนะครับ!

[🏠 Home](#-คูมอสอนพฒนา-apisrestful-apis-แบบ-step-by-step-ฉบบสมบรณ) | [📚 Tutorial](TUTORIAL.md) | [📋 Summary](SUMMARY.md) | [✅ Checklist](CHECKLIST.md)

</div>
