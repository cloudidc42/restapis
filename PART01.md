# 📘 PART 01: พื้นฐาน HTTP & REST Principles (Steps 1-10)

```
╔══════════════════════════════════════════════════════════════════╗
║                                                                  ║
║        📘 PART 01: HTTP & REST FUNDAMENTALS                      ║
║                                                                  ║
║     เรียนรู้พื้นฐาน HTTP Protocol และ REST Architecture         ║
║          แบบละเอียด พร้อมโค้ดที่ใช้งานได้จริง 100%              ║
║                                                                  ║
╚══════════════════════════════════════════════════════════════════╝
```

---

## 📋 สารบัญ PART 01

```
┌──────────────────────────────────────────────────────────────┐
│  Step 01: ทำความเข้าใจ HTTP Protocol                        │
│  Step 02: HTTP Request Structure & Analysis                 │
│  Step 03: HTTP Response Structure & Analysis                │
│  Step 04: HTTP Methods (Verbs) - Deep Dive                  │
│  Step 05: HTTP Status Codes (1xx-5xx)                       │
│  Step 06: HTTP Headers (Standard & Custom)                  │
│  Step 07: REST Architecture Constraints                     │
│  Step 08: Statelessness & Cacheability                      │
│  Step 09: Uniform Interface Principles                      │
│  Step 10: HATEOAS & Layered System                          │
└──────────────────────────────────────────────────────────────┘

⏱️  เวลาโดยประมาณ: 3-5 วัน
📊 ความยาว: ~15,000 บรรทัด
✅ โค้ดใช้งานได้จริง: 100%
```

---

# 🎯 STEP 01: ทำความเข้าใจ HTTP Protocol

## เป้าหมาย

เข้าใจพื้นฐาน HTTP (HyperText Transfer Protocol) ในระดับลึก เพื่อเป็นรากฐานสำหรับการพัฒนา RESTful API

## ทำไมต้องเรียนรู้ HTTP?

```
┌──────────────────────────────────────────────────────────────┐
│  💡 HTTP คือรากฐานของ Web และ REST API                      │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  ✅ เป็น Protocol ที่ Browser และ Server สื่อสารกัน         │
│  ✅ REST API ใช้ HTTP เป็นพื้นฐานในการส่งข้อมูล             │
│  ✅ ต้องเข้าใจ HTTP เพื่อออกแบบ API ที่ดี                   │
│  ✅ การ Debug API ต้องอ่าน HTTP Request/Response ได้         │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

## HTTP Protocol Overview

### HTTP คืออะไร?

**HTTP (HyperText Transfer Protocol)** เป็น Application Layer Protocol ที่ใช้สำหรับการส่งข้อมูลบนเว็บ

```
┌─────────────────────────────────────────────────────────────────┐
│                    🌐 HTTP OVERVIEW                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  📝 ชื่อเต็ม:  HyperText Transfer Protocol                     │
│  📅 ปีที่สร้าง: 1991 (HTTP/0.9), 1996 (HTTP/1.0)               │
│  🔢 เวอร์ชันปัจจุบัน: HTTP/1.1, HTTP/2, HTTP/3                │
│  🏗️  Layer: Application Layer (OSI Model Layer 7)              │
│  🔌 Port: 80 (HTTP), 443 (HTTPS)                               │
│  📡 Transport: TCP (HTTP/1.1, HTTP/2), UDP (HTTP/3)            │
│  🎯 จุดประสงค์: Client-Server Communication                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### HTTP เวอร์ชันต่างๆ

| เวอร์ชัน | ปี | คุณสมบัติสำคัญ |
|----------|-----|-----------------|
| HTTP/0.9 | 1991 | Simple protocol, GET only |
| HTTP/1.0 | 1996 | Headers, Methods, Status codes |
| HTTP/1.1 | 1997 | **Most used**, Persistent connections, Chunked transfer |
| HTTP/2   | 2015 | Binary protocol, Multiplexing, Header compression |
| HTTP/3   | 2022 | QUIC (UDP-based), Faster, Better mobile |

**สำหรับ REST API**: ส่วนใหญ่ใช้ **HTTP/1.1** เพราะ:
- รองรับทุก Client/Server
- เข้าใจง่าย (Text-based)
- Tools ครบถ้วน (curl, Postman, etc.)

## Client-Server Communication Model

```
┌──────────────────────────────────────────────────────────────────┐
│                   📡 HTTP COMMUNICATION FLOW                     │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│   ┌─────────┐                                    ┌─────────┐    │
│   │         │   1. HTTP Request                  │         │    │
│   │ Client  │──────────────────────────────────▶ │ Server  │    │
│   │ Browser │                                    │  API    │    │
│   │  App    │   2. HTTP Response                 │         │    │
│   │         │◀──────────────────────────────────  │         │    │
│   └─────────┘                                    └─────────┘    │
│                                                                  │
│  Request Example:                                                │
│  ┌────────────────────────────────────────────────────────┐     │
│  │ GET /api/users HTTP/1.1                                │     │
│  │ Host: api.example.com                                  │     │
│  │ Accept: application/json                               │     │
│  └────────────────────────────────────────────────────────┘     │
│                                                                  │
│  Response Example:                                               │
│  ┌────────────────────────────────────────────────────────┐     │
│  │ HTTP/1.1 200 OK                                        │     │
│  │ Content-Type: application/json                         │     │
│  │                                                        │     │
│  │ {"users": [...]}                                       │     │
│  └────────────────────────────────────────────────────────┘     │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### คุณสมบัติสำคัญของ HTTP

1. **Stateless**: ทุก Request เป็นอิสระ ไม่เก็บ State
2. **Text-based**: ส่งข้อมูลเป็น Text (HTTP/1.1)
3. **Request-Response**: Client ส่ง Request → Server ตอบ Response
4. **Connectionless**: เชื่อมต่อเฉพาะตอนส่งข้อมูล (HTTP/1.0)
5. **Extensible**: สามารถเพิ่ม Headers และ Methods ได้

## ทดลองส่ง HTTP Request ครั้งแรก

### ใช้ curl (Command Line)

curl เป็น tool สำหรับส่ง HTTP Request จาก command line

#### ติดตั้ง curl

```bash
# Linux (Ubuntu/Debian)
sudo apt-get install curl

# macOS (มักติดตั้งมาแล้ว)
curl --version

# Windows (PowerShell)
# ติดตั้ง curl จาก: https://curl.se/windows/
# หรือใช้ WSL
```

#### ตัวอย่างที่ 1: GET Request แบบง่าย

```bash
# ส่ง GET Request ไปที่ Google
curl https://www.google.com

# Output: HTML ของหน้า Google
```

#### ตัวอย่างที่ 2: GET Request ไปที่ REST API จริง

```bash
# JSONPlaceholder - Free REST API สำหรับทดสอบ
curl https://jsonplaceholder.typicode.com/users/1

# Output:
# {
#   "id": 1,
#   "name": "Leanne Graham",
#   "username": "Bret",
#   "email": "Sincere@april.biz",
#   ...
# }
```

#### ตัวอย่างที่ 3: แสดง Response Headers

```bash
# ใช้ -i (include headers) เพื่อดู Headers
curl -i https://jsonplaceholder.typicode.com/users/1

# Output:
# HTTP/2 200
# date: Fri, 07 Nov 2025 10:30:00 GMT
# content-type: application/json; charset=utf-8
# content-length: 509
# ...
#
# {
#   "id": 1,
#   "name": "Leanne Graham",
#   ...
# }
```

#### ตัวอย่างที่ 4: แสดงเฉพาะ Headers (ไม่แสดง Body)

```bash
# ใช้ -I (HEAD request) หรือ --head
curl -I https://jsonplaceholder.typicode.com/users/1

# Output (เฉพาะ Headers):
# HTTP/2 200
# date: Fri, 07 Nov 2025 10:30:00 GMT
# content-type: application/json; charset=utf-8
# ...
```

#### ตัวอย่างที่ 5: Verbose Mode (แสดงรายละเอียดทั้งหมด)

```bash
# ใช้ -v (verbose) เพื่อดูทุกอย่าง
curl -v https://jsonplaceholder.typicode.com/users/1

# Output:
# * Trying 104.21.45.100:443...
# * Connected to jsonplaceholder.typicode.com
# > GET /users/1 HTTP/2
# > Host: jsonplaceholder.typicode.com
# > User-Agent: curl/7.81.0
# > Accept: */*
# >
# < HTTP/2 200
# < date: Fri, 07 Nov 2025 10:30:00 GMT
# < content-type: application/json
# ...
```

### สังเกตผลลัพธ์

```
┌──────────────────────────────────────────────────────────────┐
│  🔍 วิเคราะห์ผลลัพธ์จาก curl -v                            │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  * = ข้อมูลเชื่อมต่อ (Connection info)                      │
│  > = Request ที่ส่งไป (Request line & headers)              │
│  < = Response ที่ได้รับ (Status line & headers)             │
│  (ไม่มีสัญลักษณ์) = Response body (JSON data)               │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

## Request-Response Cycle แบบละเอียด

```
┌────────────────────────────────────────────────────────────────────┐
│              🔄 DETAILED REQUEST-RESPONSE CYCLE                    │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│  1. CLIENT PREPARES REQUEST                                        │
│     ┌────────────────────────────────────────┐                    │
│     │ • Choose HTTP Method (GET, POST, etc.) │                    │
│     │ • Construct URI (/api/users/1)         │                    │
│     │ • Add Headers (Authorization, etc.)    │                    │
│     │ • Add Body (for POST/PUT)              │                    │
│     └────────────────────────────────────────┘                    │
│                        │                                           │
│                        ▼                                           │
│  2. DNS RESOLUTION                                                 │
│     ┌────────────────────────────────────────┐                    │
│     │ • Resolve domain → IP address          │                    │
│     │   api.example.com → 192.0.2.1          │                    │
│     └────────────────────────────────────────┘                    │
│                        │                                           │
│                        ▼                                           │
│  3. TCP CONNECTION (3-Way Handshake)                               │
│     ┌────────────────────────────────────────┐                    │
│     │ Client ─SYN→      Server                │                    │
│     │ Client ←SYN-ACK─  Server                │                    │
│     │ Client ─ACK→      Server                │                    │
│     └────────────────────────────────────────┘                    │
│                        │                                           │
│                        ▼                                           │
│  4. TLS HANDSHAKE (if HTTPS)                                       │
│     ┌────────────────────────────────────────┐                    │
│     │ • Exchange certificates                │                    │
│     │ • Establish encryption keys            │                    │
│     └────────────────────────────────────────┘                    │
│                        │                                           │
│                        ▼                                           │
│  5. SEND HTTP REQUEST                                              │
│     ┌────────────────────────────────────────┐                    │
│     │ GET /api/users/1 HTTP/1.1              │                    │
│     │ Host: api.example.com                  │                    │
│     │ ...                                    │                    │
│     └────────────────────────────────────────┘                    │
│                        │                                           │
│                        ▼                                           │
│  6. SERVER PROCESSING                                              │
│     ┌────────────────────────────────────────┐                    │
│     │ • Parse request                        │                    │
│     │ • Route to handler                     │                    │
│     │ • Execute business logic               │                    │
│     │ • Query database                       │                    │
│     │ • Build response                       │                    │
│     └────────────────────────────────────────┘                    │
│                        │                                           │
│                        ▼                                           │
│  7. SEND HTTP RESPONSE                                             │
│     ┌────────────────────────────────────────┐                    │
│     │ HTTP/1.1 200 OK                        │                    │
│     │ Content-Type: application/json         │                    │
│     │ ...                                    │                    │
│     │ {"id": 1, "name": "..."}               │                    │
│     └────────────────────────────────────────┘                    │
│                        │                                           │
│                        ▼                                           │
│  8. CLIENT RECEIVES RESPONSE                                       │
│     ┌────────────────────────────────────────┐                    │
│     │ • Parse response                       │                    │
│     │ • Check status code                    │                    │
│     │ • Process body (JSON → Object)         │                    │
│     └────────────────────────────────────────┘                    │
│                        │                                           │
│                        ▼                                           │
│  9. CONNECTION CLOSE (or Keep-Alive)                               │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

## ทดลองกับ Real-World APIs

### API #1: GitHub API

```bash
# ดูข้อมูล GitHub user
curl https://api.github.com/users/octocat

# Output:
# {
#   "login": "octocat",
#   "id": 583231,
#   "avatar_url": "https://avatars.githubusercontent.com/u/583231?v=4",
#   "name": "The Octocat",
#   "company": "@github",
#   ...
# }
```

### API #2: OpenWeatherMap API (ต้องลงทะเบียนฟรี)

```bash
# Get API Key ฟรีที่: https://openweathermap.org/api
# แทน YOUR_API_KEY ด้วย API Key ของคุณ

curl "https://api.openweathermap.org/data/2.5/weather?q=Bangkok&appid=YOUR_API_KEY&units=metric"

# Output:
# {
#   "weather": [{"main": "Clouds", "description": "broken clouds"}],
#   "main": {"temp": 28.5, "feels_like": 32.1, ...},
#   "name": "Bangkok",
#   ...
# }
```

### API #3: Dog API (ไม่ต้อง API Key)

```bash
# Random dog image
curl https://dog.ceo/api/breeds/image/random

# Output:
# {
#   "message": "https://images.dog.ceo/breeds/hound-afghan/n02088094_1003.jpg",
#   "status": "success"
# }
```

## HTTP vs HTTPS

```
┌──────────────────────────────────────────────────────────────┐
│                    🔒 HTTP vs HTTPS                          │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  HTTP (Port 80)                  HTTPS (Port 443)           │
│  ────────────────                ─────────────────          │
│  ❌ ไม่เข้ารหัส                  ✅ เข้ารหัสด้วย TLS/SSL    │
│  ❌ ข้อมูลส่งเป็น Plain Text      ✅ ข้อมูลเข้ารหัส          │
│  ❌ ไม่มี Certificate             ✅ มี SSL Certificate      │
│  ❌ ไม่ปลอดภัย                    ✅ ปลอดภัย                 │
│  ⚠️  ใช้เฉพาะ Development        ✅ ใช้ใน Production         │
│                                                              │
│  สำหรับ REST API ใน Production:                             │
│  ✅ ต้องใช้ HTTPS เท่านั้น!                                 │
│  ✅ ใช้ Let's Encrypt สำหรับ SSL Certificate ฟรี            │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### ตัวอย่าง: ทดสอบ HTTP vs HTTPS

```bash
# HTTP (ไม่ปลอดภัย)
curl http://example.com

# HTTPS (ปลอดภัย)
curl https://example.com

# ถ้า Server บังคับ HTTPS, HTTP จะ redirect ไป HTTPS
curl -L http://github.com  # -L = follow redirects
```

## แบบฝึกหัด Step 01

### Exercise 1.1: ส่ง HTTP Request แรก

**โจทย์**: ส่ง GET Request ไปที่ `https://jsonplaceholder.typicode.com/posts/1`

```bash
# เฉลย:
curl https://jsonplaceholder.typicode.com/posts/1
```

**ผลลัพธ์ที่คาดหวัง**:
```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit..."
}
```

### Exercise 1.2: ดู Response Headers

**โจทย์**: ส่ง Request เดิม แต่ให้แสดง Headers ด้วย

```bash
# เฉลย:
curl -i https://jsonplaceholder.typicode.com/posts/1
```

### Exercise 1.3: Verbose Mode

**โจทย์**: ส่ง Request พร้อมดูรายละเอียดการเชื่อมต่อทั้งหมด

```bash
# เฉลย:
curl -v https://jsonplaceholder.typicode.com/posts/1
```

### Exercise 1.4: Multiple Requests

**โจทย์**: ส่ง Request หา user id 1, 2, 3 พร้อมกัน

```bash
# เฉลย:
curl https://jsonplaceholder.typicode.com/users/1
curl https://jsonplaceholder.typicode.com/users/2
curl https://jsonplaceholder.typicode.com/users/3

# หรือใช้ loop (Bash)
for i in {1..3}; do
  echo "=== User $i ==="
  curl https://jsonplaceholder.typicode.com/users/$i
  echo ""
done
```

### Exercise 1.5: ทดสอบกับ Real API

**โจทย์**: ลองเรียก GitHub API เพื่อดูข้อมูล GitHub user ของคุณเอง

```bash
# เฉลย (แทน YOUR_USERNAME ด้วย username ของคุณ):
curl https://api.github.com/users/YOUR_USERNAME
```

## สรุป Step 01

```
┌──────────────────────────────────────────────────────────────┐
│                    ✅ สิ่งที่เรียนรู้ Step 01                │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  ✅ HTTP คือ Protocol สำหรับ Web Communication              │
│  ✅ HTTP เป็น Stateless, Text-based, Request-Response       │
│  ✅ curl เป็น tool สำหรับส่ง HTTP Request                  │
│  ✅ Request-Response Cycle มีหลายขั้นตอน                    │
│  ✅ HTTPS ต้องใช้สำหรับ Production (เพื่อความปลอดภัย)       │
│  ✅ สามารถทดลองส่ง Request ไป Real API ได้                 │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

---

# 🎯 STEP 02: HTTP Request Structure & Analysis

## เป้าหมาย

เข้าใจโครงสร้างของ HTTP Request อย่างละเอียด และสามารถวิเคราะห์ Request ได้

## HTTP Request Structure

HTTP Request ประกอบด้วย 4 ส่วนหลัก:

```
┌──────────────────────────────────────────────────────────────────┐
│                  📨 HTTP REQUEST STRUCTURE                       │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1. REQUEST LINE (บรรทัดแรก)                                    │
│     ┌─────────────────────────────────────────────────────┐    │
│     │ METHOD  URI  HTTP-VERSION                           │    │
│     │ GET /api/users/1 HTTP/1.1                           │    │
│     └─────────────────────────────────────────────────────┘    │
│                                                                  │
│  2. REQUEST HEADERS (หลายบรรทัด)                                │
│     ┌─────────────────────────────────────────────────────┐    │
│     │ Host: api.example.com                               │    │
│     │ User-Agent: curl/7.81.0                             │    │
│     │ Accept: application/json                            │    │
│     │ Authorization: Bearer eyJhbGc...                    │    │
│     └─────────────────────────────────────────────────────┘    │
│                                                                  │
│  3. BLANK LINE (แยก Headers กับ Body)                           │
│     ┌─────────────────────────────────────────────────────┐    │
│     │                                                     │    │
│     └─────────────────────────────────────────────────────┘    │
│                                                                  │
│  4. REQUEST BODY (Optional - สำหรับ POST/PUT/PATCH)             │
│     ┌─────────────────────────────────────────────────────┐    │
│     │ {                                                   │    │
│     │   "name": "John Doe",                               │    │
│     │   "email": "john@example.com"                       │    │
│     │ }                                                   │    │
│     └─────────────────────────────────────────────────────┘    │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

## 1. Request Line

Request Line ประกอบด้วย 3 ส่วน:

```
METHOD  URI  HTTP-VERSION
───┬─── ─┬─ ─────┬──────
   │     │       └─ HTTP version (HTTP/1.1, HTTP/2)
   │     └─────────ที่อยู่ของ resource (/api/users/1)
   └───────────── HTTP Method (GET, POST, PUT, etc.)
```

### ตัวอย่าง Request Lines

```
GET /api/users HTTP/1.1
POST /api/users HTTP/1.1
PUT /api/users/1 HTTP/1.1
PATCH /api/users/1 HTTP/1.1
DELETE /api/users/1 HTTP/1.1
```

## 2. Request Headers

Headers ให้ข้อมูลเพิ่มเติมเกี่ยวกับ Request

### Common Request Headers

| Header | ความหมาย | ตัวอย่าง |
|--------|----------|----------|
| `Host` | Domain name ของ Server (Required ใน HTTP/1.1) | `Host: api.example.com` |
| `User-Agent` | ข้อมูล Client (Browser, App, curl) | `User-Agent: Mozilla/5.0...` |
| `Accept` | Content type ที่ Client ต้องการรับ | `Accept: application/json` |
| `Accept-Language` | ภาษาที่ต้องการ | `Accept-Language: th, en` |
| `Content-Type` | ประเภทของ Request Body | `Content-Type: application/json` |
| `Content-Length` | ขนาดของ Body (bytes) | `Content-Length: 123` |
| `Authorization` | ข้อมูล Authentication | `Authorization: Bearer token...` |
| `Cookie` | Cookies ส่งไปให้ Server | `Cookie: sessionId=abc123` |
| `Referer` | URL ที่ส่ง Request มา | `Referer: https://example.com/` |
| `Cache-Control` | ควบคุม Caching | `Cache-Control: no-cache` |

### ตัวอย่าง Request Headers จริง

```http
GET /api/users/1 HTTP/1.1
Host: api.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36
Accept: application/json, text/plain, */*
Accept-Language: th-TH,th;q=0.9,en-US;q=0.8,en;q=0.7
Accept-Encoding: gzip, deflate, br
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
Connection: keep-alive
Cache-Control: no-cache
```

## 3. Request Body

Body ใช้สำหรับส่งข้อมูลไปให้ Server (มักใช้กับ POST, PUT, PATCH)

### JSON Body (นิยมสำหรับ REST API)

```http
POST /api/users HTTP/1.1
Host: api.example.com
Content-Type: application/json
Content-Length: 62

{
  "name": "John Doe",
  "email": "john@example.com",
  "age": 30
}
```

### Form Data Body (แบบ URL-encoded)

```http
POST /api/users HTTP/1.1
Host: api.example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 43

name=John+Doe&email=john%40example.com&age=30
```

### Multipart Form Data (สำหรับ Upload ไฟล์)

```http
POST /api/upload HTTP/1.1
Host: api.example.com
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary

------WebKitFormBoundary
Content-Disposition: form-data; name="file"; filename="photo.jpg"
Content-Type: image/jpeg

(binary data...)
------WebKitFormBoundary--
```

## ทดลองส่ง Request แบบต่างๆ

### ตัวอย่าง 1: GET Request พร้อม Headers

```bash
curl -v \
  -H "Accept: application/json" \
  -H "User-Agent: MyApp/1.0" \
  https://jsonplaceholder.typicode.com/users/1
```

**Output (Request ที่ส่งไป)**:
```
> GET /users/1 HTTP/2
> Host: jsonplaceholder.typicode.com
> Accept: application/json
> User-Agent: MyApp/1.0
```

### ตัวอย่าง 2: POST Request พร้อม JSON Body

```bash
curl -v \
  -X POST \
  -H "Content-Type: application/json" \
  -d '{"title": "foo", "body": "bar", "userId": 1}' \
  https://jsonplaceholder.typicode.com/posts
```

**Output (Request ที่ส่งไป)**:
```
> POST /posts HTTP/2
> Host: jsonplaceholder.typicode.com
> Content-Type: application/json
> Content-Length: 52
>
> {"title": "foo", "body": "bar", "userId": 1}
```

### ตัวอย่าง 3: Request พร้อม Authorization Header

```bash
curl -v \
  -H "Authorization: Bearer YOUR_TOKEN_HERE" \
  https://api.github.com/user
```

### ตัวอย่าง 4: Request พร้อม Multiple Headers

```bash
curl -v \
  -H "Accept: application/json" \
  -H "Accept-Language: th-TH" \
  -H "User-Agent: MyApp/1.0" \
  -H "X-Custom-Header: MyValue" \
  https://jsonplaceholder.typicode.com/users/1
```

## วิเคราะห์ Request ด้วย Browser DevTools

### ขั้นตอน:

1. เปิด Browser (Chrome/Firefox/Edge)
2. กด `F12` หรือ `Ctrl+Shift+I` (Windows/Linux) / `Cmd+Option+I` (Mac)
3. ไปที่แท็บ **Network**
4. เปิดเว็บไซต์หรือ Refresh หน้า
5. คลิกที่ Request ใดๆ เพื่อดูรายละเอียด

```
┌──────────────────────────────────────────────────────────────┐
│          🔍 BROWSER DEVTOOLS - NETWORK TAB                   │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  Headers Tab:     ดู Request/Response Headers               │
│  Preview Tab:     ดู Response Body (formatted)              │
│  Response Tab:    ดู Response Body (raw)                    │
│  Timing Tab:      ดูเวลาในแต่ละขั้นตอน                      │
│  Cookies Tab:     ดู Cookies                                │
│                                                              │
│  Tips:                                                       │
│  • กรองด้วยชื่อไฟล์ (Search box)                            │
│  • กรองตาม Type (XHR = API calls)                           │
│  • Right-click → Copy → Copy as cURL                        │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### ตัวอย่าง: Copy Request เป็น curl

1. เปิด DevTools → Network
2. ทำ Request ใดๆ (เช่น โหลดหน้าเว็บ)
3. Right-click ที่ Request
4. **Copy → Copy as cURL**

ผลลัพธ์ (ตัวอย่าง):
```bash
curl 'https://api.example.com/users' \
  -H 'authority: api.example.com' \
  -H 'accept: application/json' \
  -H 'authorization: Bearer eyJhbGci...' \
  -H 'user-agent: Mozilla/5.0...'
```

## URI Components (รายละเอียด)

```
┌──────────────────────────────────────────────────────────────────┐
│                     🔗 URI COMPONENTS                            │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  https://api.example.com:443/v1/users?page=2&limit=10#section1  │
│  ─┬──  ──┬──────────────┬─── ─┬─────┬──────────────┬──────┬──  │
│   │      │              │     │     │              │      │     │
│   │      │              │     │     │              │      │     │
│ Scheme  Host           Port  Path  Query         Fragment      │
│ (Protocol)         (Optional)    (Optional)    (Optional)       │
│                                                                  │
│  Scheme:   https (secure), http (non-secure)                    │
│  Host:     Domain name หรือ IP address                          │
│  Port:     80 (HTTP), 443 (HTTPS), หรือกำหนดเอง                │
│  Path:     เส้นทางไปยัง resource (/v1/users)                   │
│  Query:    Parameters (key=value pairs) (?page=2&limit=10)      │
│  Fragment: ส่วนของหน้า (ไม่ส่งไปที่ Server) (#section1)        │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### ตัวอย่าง URIs

```
GET https://api.github.com/users/octocat
    ───────┬─────────── ─────┬──────────
           │                 └─ Path
           └───────────────────── Host

GET https://api.github.com/search/repositories?q=rest+api&sort=stars&order=desc
    ───────┬─────────── ──────┬───────── ──────────┬─────────────────────────
           │                  │                     └─ Query Parameters
           │                  └────────────────────── Path
           └──────────────────────────────────────── Host

POST https://api.example.com:8080/api/v1/users
     ────── ────────────────── ──┬─ ────┬────────
                                 │      └─ Path (versioned)
                                 └──────── Port (custom)
```

## แบบฝึกหัด Step 02

### Exercise 2.1: ส่ง GET พร้อม Custom Headers

**โจทย์**: ส่ง GET Request ไปที่ `https://httpbin.org/headers` พร้อม Headers:
- `X-Custom-Header: MyValue`
- `X-Request-ID: 12345`

```bash
# เฉลย:
curl -H "X-Custom-Header: MyValue" \
     -H "X-Request-ID: 12345" \
     https://httpbin.org/headers
```

**ผลลัพธ์**: จะเห็น Headers ที่ส่งไปในส่วน `"headers"`

### Exercise 2.2: ส่ง POST พร้อม JSON

**โจทย์**: สร้าง post ใหม่ที่ JSONPlaceholder

```bash
# เฉลย:
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"title":"My Post","body":"This is content","userId":1}' \
  https://jsonplaceholder.typicode.com/posts
```

### Exercise 2.3: ส่ง Request พร้อม Query Parameters

**โจทย์**: ค้นหา posts ของ user id 1

```bash
# เฉลย:
curl "https://jsonplaceholder.typicode.com/posts?userId=1"

# หรือ
curl https://jsonplaceholder.typicode.com/posts?userId=1
```

### Exercise 2.4: ทดสอบ httpbin.org

httpbin.org เป็น Service สำหรับทดสอบ HTTP Requests

```bash
# GET with query params
curl "https://httpbin.org/get?name=John&age=30"

# POST with JSON
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"name":"John"}' \
  https://httpbin.org/post

# View all request info
curl https://httpbin.org/anything

# Test different status codes
curl https://httpbin.org/status/200
curl https://httpbin.org/status/404
curl https://httpbin.org/status/500
```

### Exercise 2.5: วิเคราะห์ Request ของเว็บจริง

**โจทย์**:
1. เปิด https://www.github.com
2. เปิด DevTools (F12) → Network tab
3. Refresh หน้า
4. หา API Request ที่ส่งไป (มักขึ้นต้นด้วย `/api/` หรือ type เป็น `xhr`)
5. คลิกดูรายละเอียดและบันทึก:
   - Request Method
   - Request URL
   - Important Headers
   - Response Status Code

## สรุป Step 02

```
┌──────────────────────────────────────────────────────────────┐
│                 ✅ สิ่งที่เรียนรู้ Step 02                   │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  ✅ HTTP Request มี 4 ส่วน: Line, Headers, Blank, Body     │
│  ✅ Request Line: METHOD + URI + HTTP-VERSION               │
│  ✅ Headers ให้ข้อมูลเพิ่มเติม (Content-Type, Auth, etc.)  │
│  ✅ Body ใช้สำหรับส่งข้อมูล (JSON, Form, Multipart)        │
│  ✅ สามารถส่ง Custom Headers ได้ด้วย -H ใน curl           │
│  ✅ URI ประกอบด้วย Scheme, Host, Port, Path, Query         │
│  ✅ DevTools ใช้วิเคราะห์ Request ของเว็บจริง              │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

---

# 🎯 STEP 03: HTTP Response Structure & Analysis

## เป้าหมาย

เข้าใจโครงสร้างของ HTTP Response และสามารถวิเคราะห์ Response ได้อย่างถูกต้อง

## HTTP Response Structure

HTTP Response ประกอบด้วย 4 ส่วนหลัก:

```
┌──────────────────────────────────────────────────────────────────┐
│                  📬 HTTP RESPONSE STRUCTURE                      │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1. STATUS LINE (บรรทัดแรก)                                     │
│     ┌─────────────────────────────────────────────────────┐    │
│     │ HTTP-VERSION  STATUS-CODE  REASON-PHRASE            │    │
│     │ HTTP/1.1 200 OK                                     │    │
│     └─────────────────────────────────────────────────────┘    │
│                                                                  │
│  2. RESPONSE HEADERS (หลายบรรทัด)                               │
│     ┌─────────────────────────────────────────────────────┐    │
│     │ Content-Type: application/json                      │    │
│     │ Content-Length: 123                                 │    │
│     │ Date: Fri, 07 Nov 2025 10:30:00 GMT                 │    │
│     │ Server: nginx/1.18.0                                │    │
│     └─────────────────────────────────────────────────────┘    │
│                                                                  │
│  3. BLANK LINE (แยก Headers กับ Body)                           │
│     ┌─────────────────────────────────────────────────────┐    │
│     │                                                     │    │
│     └─────────────────────────────────────────────────────┘    │
│                                                                  │
│  4. RESPONSE BODY (ข้อมูลที่ต้องการ)                           │
│     ┌─────────────────────────────────────────────────────┐    │
│     │ {                                                   │    │
│     │   "id": 1,                                          │    │
│     │   "name": "John Doe"                                │    │
│     │ }                                                   │    │
│     └─────────────────────────────────────────────────────┘    │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

## 1. Status Line

Status Line ประกอบด้วย 3 ส่วน:

```
HTTP-VERSION  STATUS-CODE  REASON-PHRASE
─────┬─────  ─────┬─────  ──────┬──────
     │            │              └─ คำอธิบาย (OK, Not Found, etc.)
     │            └──────────────── รหัสสถานะ (200, 404, 500)
     └───────────────────────────── HTTP version (HTTP/1.1)
```

### ตัวอย่าง Status Lines

```
HTTP/1.1 200 OK
HTTP/1.1 201 Created
HTTP/1.1 404 Not Found
HTTP/1.1 500 Internal Server Error
HTTP/2 200
```

## 2. Response Headers

### Common Response Headers

| Header | ความหมาย | ตัวอย่าง |
|--------|----------|----------|
| `Content-Type` | ประเภทของ Response Body | `Content-Type: application/json` |
| `Content-Length` | ขนาดของ Body (bytes) | `Content-Length: 1234` |
| `Date` | วันเวลาที่ Server ตอบกลับ | `Date: Fri, 07 Nov 2025 10:30:00 GMT` |
| `Server` | ข้อมูล Server Software | `Server: nginx/1.18.0` |
| `Cache-Control` | กำหนดการ Cache | `Cache-Control: max-age=3600` |
| `ETag` | Identifier สำหรับ versioning | `ETag: "abc123"` |
| `Location` | URL ของ resource ใหม่ (201, 3xx) | `Location: /api/users/123` |
| `Set-Cookie` | ส่ง Cookie ให้ Client | `Set-Cookie: sessionId=abc; HttpOnly` |
| `Access-Control-*` | CORS headers | `Access-Control-Allow-Origin: *` |

### ตัวอย่าง Response Headers จริง

```http
HTTP/1.1 200 OK
Date: Fri, 07 Nov 2025 10:30:00 GMT
Content-Type: application/json; charset=utf-8
Content-Length: 82
Server: nginx/1.18.0
Cache-Control: max-age=3600, public
ETag: "abc123def456"
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
```

## 3. Response Body

### JSON Response (นิยมใน REST API)

```json
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "created_at": "2025-11-07T10:30:00Z"
}
```

### Array Response

```json
{
  "data": [
    {"id": 1, "name": "John"},
    {"id": 2, "name": "Jane"}
  ],
  "total": 2,
  "page": 1
}
```

### Error Response

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid email format",
    "field": "email"
  }
}
```

## ทดลองวิเคราะห์ Response

### ตัวอย่าง 1: ดู Response Headers

```bash
curl -i https://jsonplaceholder.typicode.com/users/1

# Output:
# HTTP/2 200
# date: Fri, 07 Nov 2025 10:30:00 GMT
# content-type: application/json; charset=utf-8
# content-length: 509
# x-powered-by: Express
# ...
#
# {
#   "id": 1,
#   "name": "Leanne Graham",
#   ...
# }
```

### ตัวอย่าง 2: เฉพาะ Headers (HEAD request)

```bash
curl -I https://jsonplaceholder.typicode.com/users/1

# Output (เฉพาะ Headers):
# HTTP/2 200
# content-type: application/json; charset=utf-8
# content-length: 509
# ...
```

### ตัวอย่าง 3: ดู Response Time

```bash
curl -w "\nTime Total: %{time_total}s\n" \
     -o /dev/null -s \
     https://jsonplaceholder.typicode.com/users/1

# Output:
# Time Total: 0.245s
```

## Content Negotiation

Client สามารถระบุประเภทของ Content ที่ต้องการด้วย `Accept` header:

```bash
# ขอ JSON
curl -H "Accept: application/json" \
     https://api.example.com/data

# ขอ XML
curl -H "Accept: application/xml" \
     https://api.example.com/data

# ขอ HTML
curl -H "Accept: text/html" \
     https://api.example.com/data
```

Server จะตอบด้วย `Content-Type` header บอกประเภทที่ส่งกลับ

## แบบฝึกหัด Step 03

### Exercise 3.1: วิเคราะห์ Response

```bash
# ส่ง Request และวิเคราะห์ Response
curl -i https://api.github.com/users/octocat

# สังเกต:
# - Status Code
# - Content-Type
# - Content-Length
# - Rate Limit Headers (X-RateLimit-*)
```

### Exercise 3.2: ทดสอบ Error Response

```bash
# ขอ resource ที่ไม่มีจริง
curl -i https://jsonplaceholder.typicode.com/users/9999

# สังเกต Status Code (404) และ Response Body
```

### Exercise 3.3: ทดสอบ POST Response

```bash
# POST แล้วดู Response
curl -i -X POST \
  -H "Content-Type: application/json" \
  -d '{"title":"test"}' \
  https://jsonplaceholder.typicode.com/posts

# สังเกต:
# - Status Code (201 Created)
# - Location Header (ถ้ามี)
# - Response Body (resource ที่สร้างใหม่)
```

## สรุป Step 03

```
┌──────────────────────────────────────────────────────────────┐
│                 ✅ สิ่งที่เรียนรู้ Step 03                   │
├──────────────────────────────────────────────────────────────┤
│  ✅ HTTP Response มี 4 ส่วน: Status Line, Headers, Blank, Body │
│  ✅ Status Line: HTTP-VERSION + STATUS-CODE + REASON-PHRASE │
│  ✅ Response Headers ให้ข้อมูล Content-Type, Length, Cache  │
│  ✅ Response Body มีรูปแบบต่างๆ (JSON, XML, HTML)           │
│  ✅ Content Negotiation ด้วย Accept header                 │
└──────────────────────────────────────────────────────────────┘
```

---

# 🎯 STEP 04: HTTP Methods (Verbs) - Deep Dive

## เป้าหมาย

เชี่ยวชาญการใช้ HTTP Methods ทั้ง 9 Methods อย่างถูกต้องตามหลัก RESTful

## HTTP Methods Overview

```
┌──────────────────────────────────────────────────────────────────┐
│                    🔧 HTTP METHODS COMPLETE                      │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Method   Safe  Idempotent  Use Case                            │
│  ──────   ────  ──────────  ────────                            │
│  GET       ✅      ✅        อ่านข้อมูล (Read)                  │
│  POST      ❌      ❌        สร้างข้อมูล (Create)               │
│  PUT       ❌      ✅        แทนที่ทั้งหมด (Replace)            │
│  PATCH     ❌      ❌        แก้ไขบางส่วน (Partial Update)       │
│  DELETE    ❌      ✅        ลบข้อมูล (Delete)                  │
│  HEAD      ✅      ✅        เหมือน GET แต่ไม่มี Body           │
│  OPTIONS   ✅      ✅        ตรวจสอบ Methods ที่รองรับ          │
│  TRACE     ✅      ✅        Debug (ไม่ค่อยใช้)                 │
│  CONNECT   ❌      ❌        สร้าง Tunnel (Proxy)               │
│                                                                  │
│  คำจำกัดความ:                                                   │
│  • Safe: ไม่เปลี่ยนแปลงข้อมูลบน Server                         │
│  • Idempotent: เรียกกี่ครั้งก็ผลลัพธ์เหมือนเดิม               │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

## GET - อ่านข้อมูล

**จุดประสงค์**: ดึงข้อมูลจาก Server โดยไม่เปลี่ยนแปลงอะไร

**คุณสมบัติ**:
- Safe: ✅ (ไม่เปลี่ยนข้อมูล)
- Idempotent: ✅ (เรียกกี่ครั้งก็ได้ผลเหมือนเดิม)
- มี Request Body: ❌ (ไม่ควรมี)
- Cacheable: ✅

### ตัวอย่าง GET Requests

```bash
# GET single resource
curl https://jsonplaceholder.typicode.com/users/1

# GET collection
curl https://jsonplaceholder.typicode.com/users

# GET with query parameters
curl "https://jsonplaceholder.typicode.com/posts?userId=1&_limit=5"

# GET with filtering
curl "https://jsonplaceholder.typicode.com/comments?postId=1"
```

### Response Example

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "Leanne Graham",
  "username": "Bret",
  "email": "Sincere@april.biz"
}
```

## POST - สร้างข้อมูลใหม่

**จุดประสงค์**: สร้าง Resource ใหม่บน Server

**คุณสมบัติ**:
- Safe: ❌ (เปลี่ยนข้อมูล)
- Idempotent: ❌ (เรียกหลายครั้ง = สร้างหลาย resources)
- มี Request Body: ✅ (มักมี)
- Cacheable: ❌ (โดยปกติ)

### ตัวอย่าง POST Request

```bash
# Create new user
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "age": 30
  }' \
  https://jsonplaceholder.typicode.com/users

# Create new post
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{
    "title": "My Post",
    "body": "This is content",
    "userId": 1
  }' \
  https://jsonplaceholder.typicode.com/posts
```

### Response Example

```http
HTTP/1.1 201 Created
Location: /api/users/101
Content-Type: application/json

{
  "id": 101,
  "name": "John Doe",
  "email": "john@example.com",
  "age": 30,
  "created_at": "2025-11-07T10:30:00Z"
}
```

**สังเกต**:
- Status Code: **201 Created** (ไม่ใช่ 200)
- **Location** header: URL ของ resource ที่สร้างใหม่
- Response Body: ข้อมูลของ resource ที่สร้าง (รวม ID)

## PUT - แทนที่ทั้งหมด

**จุดประสงค์**: แทนที่ Resource ทั้งหมดด้วยข้อมูลใหม่

**คุณสมบัติ**:
- Safe: ❌
- Idempotent: ✅ (แทนที่กี่ครั้งก็ได้ผลเหมือนเดิม)
- มี Request Body: ✅
- Cacheable: ❌

### ตัวอย่าง PUT Request

```bash
# Replace entire user
curl -X PUT \
  -H "Content-Type: application/json" \
  -d '{
    "id": 1,
    "name": "Jane Doe",
    "email": "jane@example.com",
    "age": 25
  }' \
  https://jsonplaceholder.typicode.com/users/1
```

**หมายเหตุ**: PUT ต้องส่งข้อมูลครบทุก field หากขาด field ใดอาจถูกลบ

## PATCH - แก้ไขบางส่วน

**จุดประสงค์**: แก้ไขเฉพาะ fields ที่ต้องการ ไม่ต้องส่งทั้งหมด

**คุณสมบัติ**:
- Safe: ❌
- Idempotent: ⚠️ (ขึ้นอยู่กับ implementation)
- มี Request Body: ✅
- Cacheable: ❌

### ตัวอย่าง PATCH Request

```bash
# Update only email
curl -X PATCH \
  -H "Content-Type: application/json" \
  -d '{
    "email": "newemail@example.com"
  }' \
  https://jsonplaceholder.typicode.com/users/1

# Update multiple fields
curl -X PATCH \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Jane",
    "age": 26
  }' \
  https://jsonplaceholder.typicode.com/users/1
```

### PUT vs PATCH

```
┌─────────────────────────────────────────────────────────────┐
│                    PUT vs PATCH                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  PUT (Full Replacement):                                    │
│  Before: {"id": 1, "name": "John", "age": 30}              │
│  Send:   {"id": 1, "name": "Jane", "age": 25}              │
│  After:  {"id": 1, "name": "Jane", "age": 25}              │
│                                                             │
│  PATCH (Partial Update):                                    │
│  Before: {"id": 1, "name": "John", "age": 30}              │
│  Send:   {"name": "Jane"}                                  │
│  After:  {"id": 1, "name": "Jane", "age": 30}  ← age คงเดิม │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## DELETE - ลบข้อมูล

**จุดประสงค์**: ลบ Resource

**คุณสมบัติ**:
- Safe: ❌
- Idempotent: ✅ (ลบกี่ครั้งก็ยังหายอยู่ดี)
- มี Request Body: ❌ (ไม่ควรมี)
- Cacheable: ❌

### ตัวอย่าง DELETE Request

```bash
# Delete user
curl -X DELETE https://jsonplaceholder.typicode.com/users/1

# Delete post
curl -X DELETE https://jsonplaceholder.typicode.com/posts/1
```

### Response Examples

```http
# Success with no content
HTTP/1.1 204 No Content

# หรือ Success with content
HTTP/1.1 200 OK
Content-Type: application/json

{
  "message": "User deleted successfully",
  "id": 1
}
```

## HEAD - ดึงเฉพาะ Headers

**จุดประสงค์**: เหมือน GET แต่ไม่ส่ง Response Body (ดึงเฉพาะ Headers)

**Use Cases**:
- ตรวจสอบว่า Resource มีอยู่หรือไม่ (ดู Status Code)
- ดูขนาดไฟล์ก่อนดาวน์โหลด (Content-Length)
- ตรวจสอบ Last-Modified / ETag

### ตัวอย่าง HEAD Request

```bash
# Check if resource exists
curl -I https://jsonplaceholder.typicode.com/users/1

# Output (เฉพาะ Headers):
# HTTP/2 200
# content-type: application/json; charset=utf-8
# content-length: 509
# ...
```

## OPTIONS - ตรวจสอบ Methods

**จุดประสงค์**: ตรวจสอบว่า Server รองรับ HTTP Methods ใดบ้าง

**Use Cases**:
- CORS Preflight Request
- ตรวจสอบ API capabilities

### ตัวอย่าง OPTIONS Request

```bash
# Check supported methods
curl -X OPTIONS -i https://jsonplaceholder.typicode.com/users

# CORS preflight
curl -X OPTIONS \
  -H "Origin: https://example.com" \
  -H "Access-Control-Request-Method: POST" \
  -i https://api.example.com/users
```

### Response Example

```http
HTTP/1.1 200 OK
Allow: GET, POST, PUT, PATCH, DELETE, HEAD, OPTIONS
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: GET, POST, PUT, PATCH, DELETE
```

## Idempotency อธิบายละเอียด

```
┌──────────────────────────────────────────────────────────────┐
│                  🔄 IDEMPOTENCY EXAMPLES                     │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  ✅ GET /users/1 (Idempotent)                                │
│     1st call: {"id": 1, "name": "John"}                     │
│     2nd call: {"id": 1, "name": "John"}  ← เหมือนเดิม       │
│     3rd call: {"id": 1, "name": "John"}  ← เหมือนเดิม       │
│                                                              │
│  ✅ PUT /users/1 {"name": "Jane"} (Idempotent)               │
│     1st call: name = "Jane"                                 │
│     2nd call: name = "Jane"  ← ยังเป็น Jane                 │
│     3rd call: name = "Jane"  ← ยังเป็น Jane                 │
│                                                              │
│  ✅ DELETE /users/1 (Idempotent)                             │
│     1st call: ลบสำเร็จ (200/204)                            │
│     2nd call: ไม่พบ (404) แต่ผลลัพธ์เหมือนกัน = หายแล้ว    │
│                                                              │
│  ❌ POST /users (NOT Idempotent)                             │
│     1st call: สร้าง user id=1                               │
│     2nd call: สร้าง user id=2  ← ต่างกัน!                  │
│     3rd call: สร้าง user id=3  ← ต่างกัน!                  │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

## แบบฝึกหัด Step 04

### Exercise 4.1: CRUD Complete

สร้าง, อ่าน, แก้ไข, ลบ post

```bash
# 1. Create
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"title":"Test","body":"Content","userId":1}' \
  https://jsonplaceholder.typicode.com/posts

# บันทึก ID ที่ได้ (เช่น 101)

# 2. Read
curl https://jsonplaceholder.typicode.com/posts/101

# 3. Update
curl -X PUT \
  -H "Content-Type: application/json" \
  -d '{"id":101,"title":"Updated","body":"New content","userId":1}' \
  https://jsonplaceholder.typicode.com/posts/101

# 4. Partial Update
curl -X PATCH \
  -H "Content-Type: application/json" \
  -d '{"title":"Patched Title"}' \
  https://jsonplaceholder.typicode.com/posts/101

# 5. Delete
curl -X DELETE https://jsonplaceholder.typicode.com/posts/101
```

### Exercise 4.2: ทดสอบ Idempotency

```bash
# PUT 3 ครั้ง (ควรได้ผลเหมือนกัน)
curl -X PUT \
  -H "Content-Type: application/json" \
  -d '{"id":1,"title":"Same","body":"Same","userId":1}' \
  https://jsonplaceholder.typicode.com/posts/1

# เรียกซ้ำอีก 2 ครั้ง ผลลัพธ์ควรเหมือนเดิม
```

### Exercise 4.3: ทดสอบ HEAD

```bash
# ตรวจสอบว่า resource มีหรือไม่โดยไม่ดาวน์โหลด Body
curl -I https://jsonplaceholder.typicode.com/posts/1

# เปรียบเทียบกับ GET
curl -i https://jsonplaceholder.typicode.com/posts/1
```

## สรุป Step 04

```
┌──────────────────────────────────────────────────────────────┐
│                 ✅ สิ่งที่เรียนรู้ Step 04                   │
├──────────────────────────────────────────────────────────────┤
│  ✅ HTTP Methods หลัก: GET, POST, PUT, PATCH, DELETE       │
│  ✅ GET = Read, POST = Create, PUT/PATCH = Update, DELETE   │
│  ✅ Idempotent: GET, PUT, DELETE (เรียกซ้ำได้ผลเหมือนเดิม) │
│  ✅ Safe: GET, HEAD, OPTIONS (ไม่เปลี่ยนข้อมูล)            │
│  ✅ PUT = Full replacement, PATCH = Partial update          │
│  ✅ HEAD = GET without body, OPTIONS = Check methods        │
└──────────────────────────────────────────────────────────────┘
```

---

# 🎯 STEP 05: HTTP Status Codes (1xx-5xx) Complete

## เป้าหมาย

เข้าใจ HTTP Status Codes ทั้ง 5 กลุ่ม และรู้ว่าเมื่อไหร่ควรใช้อะไร

## Status Code Categories

```
┌──────────────────────────────────────────────────────────────┐
│              📊 HTTP STATUS CODE CATEGORIES                  │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  1xx: Informational (กำลังดำเนินการ)                       │
│       100 Continue, 101 Switching Protocols                 │
│                                                              │
│  2xx: Success (สำเร็จ)                                      │
│       200 OK, 201 Created, 204 No Content                   │
│                                                              │
│  3xx: Redirection (เปลี่ยนเส้นทาง)                         │
│       301 Moved Permanently, 302 Found, 304 Not Modified    │
│                                                              │
│  4xx: Client Error (Client ผิด)                            │
│       400 Bad Request, 401 Unauthorized, 404 Not Found      │
│                                                              │
│  5xx: Server Error (Server ผิด)                            │
│       500 Internal Server Error, 503 Service Unavailable    │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

## 2xx Success (ใช้บ่อยที่สุด)

### 200 OK
**ใช้เมื่อ**: Request สำเร็จ (GET, PUT, PATCH)

```bash
# GET request
curl https://jsonplaceholder.typicode.com/users/1
# → 200 OK

# PUT request
curl -X PUT \
  -H "Content-Type: application/json" \
  -d '{"id":1,"name":"Jane"}' \
  https://jsonplaceholder.typicode.com/users/1
# → 200 OK
```

### 201 Created
**ใช้เมื่อ**: สร้าง Resource สำเร็จ (POST)

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"title":"New Post"}' \
  https://jsonplaceholder.typicode.com/posts
# → 201 Created
# + Location: /posts/101
```

### 204 No Content
**ใช้เมื่อ**: สำเร็จแต่ไม่มี Response Body (DELETE, PUT)

```bash
curl -X DELETE https://jsonplaceholder.typicode.com/posts/1
# → 204 No Content
# (ไม่มี Response Body)
```

## 3xx Redirection

### 301 Moved Permanently
**ใช้เมื่อ**: Resource ย้ายไปที่อื่นถาวร

```bash
# Server ตอบ:
HTTP/1.1 301 Moved Permanently
Location: https://newsite.com/resource
```

### 302 Found / 303 See Other
**ใช้เมื่อ**: Resource ย้ายชั่วคราว

### 304 Not Modified
**ใช้เมื่อ**: Resource ไม่เปลี่ยน (ใช้ Cache ได้)

```bash
curl -H "If-None-Match: abc123" \
     https://api.example.com/users/1
# → 304 Not Modified (ถ้า ETag ยังเหมือนเดิม)
```

## 4xx Client Errors (ใช้บ่อย)

### 400 Bad Request
**ใช้เมื่อ**: Request ไม่ถูกต้อง (JSON ผิด, Missing field, etc.)

```bash
# ส่ง JSON ผิดรูปแบบ
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{invalid json}' \
  https://jsonplaceholder.typicode.com/posts
# → 400 Bad Request
```

### 401 Unauthorized
**ใช้เมื่อ**: ไม่มี Authentication หรือ Token ผิด

```bash
# ไม่ส่ง Authorization header
curl https://api.github.com/user
# → 401 Unauthorized

# ส่ง Token ผิด
curl -H "Authorization: Bearer invalid_token" \
     https://api.github.com/user
# → 401 Unauthorized
```

### 403 Forbidden
**ใช้เมื่อ**: Authenticated แล้ว แต่ไม่มีสิทธิ์

```
401 vs 403:
───────────
401: ยังไม่ login / Token ผิด        → ต้อง login ใหม่
403: login แล้ว แต่ไม่มีสิทธิ์เข้าถึง → ไม่มีสิทธิ์จริงๆ
```

### 404 Not Found
**ใช้เมื่อ**: ไม่พบ Resource

```bash
# ขอ user ที่ไม่มีจริง
curl https://jsonplaceholder.typicode.com/users/99999
# → 404 Not Found
```

### 405 Method Not Allowed
**ใช้เมื่อ**: HTTP Method ไม่รองรับ

```bash
# ถ้า API ไม่รองรับ DELETE
curl -X DELETE https://some-api.com/resource
# → 405 Method Not Allowed
# Allow: GET, POST, PUT
```

### 409 Conflict
**ใช้เมื่อ**: ข้อมูลขัดแย้ง (เช่น email ซ้ำ, version conflict)

```bash
# พยายามสร้าง user ด้วย email ที่มีแล้ว
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"email":"existing@example.com"}' \
  https://api.example.com/users
# → 409 Conflict
# Body: {"error": "Email already exists"}
```

### 422 Unprocessable Entity
**ใช้เมื่อ**: Validation ไม่ผ่าน

```bash
# ส่งข้อมูลที่ validation ไม่ผ่าน
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"email":"invalid-email","age":-5}' \
  https://api.example.com/users
# → 422 Unprocessable Entity
# Body: {
#   "errors": {
#     "email": ["must be valid email"],
#     "age": ["must be positive"]
#   }
# }
```

### 429 Too Many Requests
**ใช้เมื่อ**: เรียก API บ่อยเกิน (Rate Limit)

```bash
# เรียกเกิน rate limit
curl https://api.github.com/users/octocat
# (เรียกซ้ำๆ หลายครั้ง)
# → 429 Too Many Requests
# Retry-After: 60
```

## 5xx Server Errors

### 500 Internal Server Error
**ใช้เมื่อ**: Server เกิด Error ที่ไม่คาดคิด

```bash
# Server มีปัญหา (bug, exception, etc.)
curl https://broken-api.com/resource
# → 500 Internal Server Error
```

### 502 Bad Gateway
**ใช้เมื่อ**: Gateway/Proxy ได้ response ผิดพลาดจาก upstream server

### 503 Service Unavailable
**ใช้เมื่อ**: Server ไม่พร้อมให้บริการชั่วคราว (maintenance, overload)

```bash
# Server กำลัง maintenance
curl https://api.example.com/users
# → 503 Service Unavailable
# Retry-After: 3600
```

### 504 Gateway Timeout
**ใช้เมื่อ**: Gateway/Proxy รอ upstream server timeout

## Status Code Decision Tree

```
┌────────────────────────────────────────────────────────────┐
│           🌳 STATUS CODE DECISION TREE                     │
├────────────────────────────────────────────────────────────┤
│                                                            │
│  Request มาถึง Server ได้ไหม?                             │
│  ├─ ❌ → 500 Server Error / 502 Bad Gateway                │
│  └─ ✅ → ต่อไป                                             │
│                                                            │
│  Request ถูกต้องไหม?                                       │
│  ├─ ❌ → 400 Bad Request                                   │
│  └─ ✅ → ต่อไป                                             │
│                                                            │
│  Authentication ผ่านไหม?                                   │
│  ├─ ❌ → 401 Unauthorized                                  │
│  └─ ✅ → ต่อไป                                             │
│                                                            │
│  Authorization (สิทธิ์) ผ่านไหม?                          │
│  ├─ ❌ → 403 Forbidden                                     │
│  └─ ✅ → ต่อไป                                             │
│                                                            │
│  Resource มีอยู่ไหม?                                       │
│  ├─ ❌ → 404 Not Found                                     │
│  └─ ✅ → ต่อไป                                             │
│                                                            │
│  Validation ผ่านไหม?                                       │
│  ├─ ❌ → 422 Unprocessable Entity                          │
│  └─ ✅ → ต่อไป                                             │
│                                                            │
│  ดำเนินการสำเร็จไหม?                                      │
│  ├─ ✅ (POST) → 201 Created                                │
│  ├─ ✅ (DELETE) → 204 No Content                           │
│  └─ ✅ (อื่นๆ) → 200 OK                                    │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

## แบบฝึกหัด Step 05

### Exercise 5.1: ทดสอบ Status Codes

```bash
# 200 OK
curl -i https://jsonplaceholder.typicode.com/users/1

# 201 Created
curl -i -X POST \
  -H "Content-Type: application/json" \
  -d '{"title":"test"}' \
  https://jsonplaceholder.typicode.com/posts

# 404 Not Found
curl -i https://jsonplaceholder.typicode.com/users/99999

# 400 Bad Request (ใช้ httpbin)
curl -i https://httpbin.org/status/400

# 500 Internal Server Error
curl -i https://httpbin.org/status/500
```

### Exercise 5.2: GitHub API Rate Limit

```bash
# เรียก GitHub API หลายครั้งจนเกิน rate limit
for i in {1..100}; do
  curl -i https://api.github.com/users/octocat
  sleep 0.1
done

# สังเกต X-RateLimit-* headers และ 429 Too Many Requests
```

## สรุป Step 05

```
┌──────────────────────────────────────────────────────────────┐
│                 ✅ สิ่งที่เรียนรู้ Step 05                   │
├──────────────────────────────────────────────────────────────┤
│  ✅ Status Codes แบ่ง 5 กลุ่ม: 1xx, 2xx, 3xx, 4xx, 5xx     │
│  ✅ 2xx = Success (200 OK, 201 Created, 204 No Content)     │
│  ✅ 4xx = Client Error (400, 401, 403, 404, 422, 429)       │
│  ✅ 5xx = Server Error (500, 502, 503, 504)                 │
│  ✅ 401 = ไม่ authenticated, 403 = ไม่มีสิทธิ์             │
│  ✅ 404 = ไม่พบ resource, 422 = validation ไม่ผ่าน         │
└──────────────────────────────────────────────────────────────┘
```

---

# 🎯 STEP 06: HTTP Headers (Standard & Custom) - Complete Guide

## เป้าหมาย

เข้าใจ HTTP Headers ทั้งแบบ Standard และ Custom พร้อมวิธีใช้งานใน REST API

## HTTP Headers Overview

```
┌──────────────────────────────────────────────────────────────────┐
│                    📋 HTTP HEADERS OVERVIEW                      │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  HTTP Headers = Metadata ของ Request/Response                   │
│                                                                  │
│  รูปแบบ:                                                         │
│  ┌────────────────────────────────────────────────────────┐    │
│  │ Header-Name: Header-Value                              │    │
│  │ Content-Type: application/json                         │    │
│  │ Authorization: Bearer eyJhbGc...                       │    │
│  └────────────────────────────────────────────────────────┘    │
│                                                                  │
│  ประเภทของ Headers:                                             │
│  • Request Headers   - Client ส่งไป Server                     │
│  • Response Headers  - Server ส่งกลับ Client                   │
│  • General Headers   - ใช้ได้ทั้ง Request และ Response         │
│  • Entity Headers    - เกี่ยวกับ Body                          │
│  • Custom Headers    - กำหนดเอง (ขึ้นต้น X- หรือไม่ก็ได้)      │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

## Request Headers (Common)

### 1. Content Negotiation Headers

```bash
# Accept - ระบุ Content Type ที่ต้องการรับ
curl -H "Accept: application/json" \
     https://api.example.com/users

# Accept-Language - ระบุภาษาที่ต้องการ
curl -H "Accept-Language: th-TH, th;q=0.9, en;q=0.8" \
     https://api.example.com/users

# Accept-Encoding - ระบุการบีบอัดที่รองรับ
curl -H "Accept-Encoding: gzip, deflate, br" \
     https://api.example.com/users

# Accept-Charset - ระบุ Character encoding
curl -H "Accept-Charset: utf-8" \
     https://api.example.com/users
```

**Quality Values (q)**:
```
Accept-Language: th-TH;q=1.0, en-US;q=0.8, en;q=0.5
                 ────────┬────────────────────────
                         └─ q=1.0 (สูงสุด) = ต้องการมากที่สุด
```

### 2. Authentication & Authorization Headers

```bash
# Authorization - ส่ง credentials
# Bearer Token (JWT)
curl -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..." \
     https://api.example.com/users

# Basic Auth
curl -H "Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=" \
     https://api.example.com/users

# หรือใช้ -u (curl จะ encode ให้เอง)
curl -u username:password \
     https://api.example.com/users

# API Key
curl -H "X-API-Key: your-api-key-here" \
     https://api.example.com/users
```

### 3. Content Headers

```bash
# Content-Type - ระบุประเภทของ Request Body
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"name":"John"}' \
  https://api.example.com/users

# Content-Length - ขนาดของ Body (bytes)
# curl คำนวณให้อัตโนมัติ

# Content-Encoding - การบีบอัดของ Body
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Content-Encoding: gzip" \
  --data-binary @compressed-data.gz \
  https://api.example.com/users
```

### 4. Caching Headers

```bash
# Cache-Control - ควบคุมการ Cache
curl -H "Cache-Control: no-cache" \
     https://api.example.com/users

# If-None-Match - ใช้กับ ETag สำหรับ Conditional Request
curl -H "If-None-Match: \"abc123\"" \
     https://api.example.com/users
# → 304 Not Modified (ถ้า ETag ไม่เปลี่ยน)

# If-Modified-Since - ตรวจสอบว่าเปลี่ยนแปลงหรือไม่
curl -H "If-Modified-Since: Fri, 07 Nov 2025 10:00:00 GMT" \
     https://api.example.com/users
```

### 5. Client Information Headers

```bash
# User-Agent - ข้อมูล Client
curl -H "User-Agent: MyApp/1.0 (iOS 15.0)" \
     https://api.example.com/users

# Referer - URL ที่ส่ง Request มา
curl -H "Referer: https://myapp.com/dashboard" \
     https://api.example.com/users

# Origin - ใช้ใน CORS
curl -H "Origin: https://myapp.com" \
     https://api.example.com/users
```

## Response Headers (Common)

### 1. Content Headers

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 1234
Content-Encoding: gzip
Content-Language: th-TH
```

### 2. Caching Headers

```http
HTTP/1.1 200 OK
Cache-Control: max-age=3600, public
ETag: "abc123def456"
Last-Modified: Fri, 07 Nov 2025 10:00:00 GMT
Expires: Fri, 07 Nov 2025 11:00:00 GMT
Age: 120
```

**Cache-Control Values**:
```
┌──────────────────────────────────────────────────────────────┐
│  public            - Cache ได้ทุกที่ (CDN, Browser)         │
│  private           - Cache เฉพาะ Browser                    │
│  no-cache          - ต้องตรวจสอบ Server ก่อนใช้ Cache       │
│  no-store          - ห้าม Cache                             │
│  max-age=3600      - Cache ได้ 3600 วินาที (1 ชั่วโมง)     │
│  must-revalidate   - ต้องตรวจสอบหลัง expire                │
└──────────────────────────────────────────────────────────────┘
```

### 3. CORS Headers

```http
HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://myapp.com
Access-Control-Allow-Methods: GET, POST, PUT, DELETE
Access-Control-Allow-Headers: Content-Type, Authorization
Access-Control-Allow-Credentials: true
Access-Control-Max-Age: 86400
```

### 4. Security Headers

```http
HTTP/1.1 200 OK
Strict-Transport-Security: max-age=31536000; includeSubDomains
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block
Content-Security-Policy: default-src 'self'
```

### 5. Rate Limiting Headers

```http
HTTP/1.1 200 OK
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1699358400
Retry-After: 60
```

```bash
# ทดสอบดู Rate Limit Headers จาก GitHub API
curl -i https://api.github.com/users/octocat | grep -i ratelimit
```

### 6. Location & Redirect Headers

```http
# 201 Created
HTTP/1.1 201 Created
Location: /api/users/123

# 301 Redirect
HTTP/1.1 301 Moved Permanently
Location: https://newdomain.com/resource
```

## Custom Headers

### Naming Conventions

**แบบเก่า** (Deprecated): ขึ้นต้นด้วย `X-`
```
X-Custom-Header: value
X-Request-ID: abc-123
X-API-Version: 1.0
```

**แบบใหม่** (Recommended): ไม่ต้องขึ้นต้น `X-`
```
Custom-Header: value
Request-ID: abc-123
API-Version: 1.0
```

### ตัวอย่าง Custom Headers ที่นิยมใช้

```bash
# Request ID - ติดตาม Request
curl -H "X-Request-ID: req-12345" \
     https://api.example.com/users

# Correlation ID - ติดตาม Transaction ข้าม Services
curl -H "X-Correlation-ID: corr-67890" \
     https://api.example.com/users

# API Version
curl -H "X-API-Version: 2" \
     https://api.example.com/users

# Tenant ID (Multi-tenant)
curl -H "X-Tenant-ID: tenant-123" \
     https://api.example.com/users

# Custom Authentication
curl -H "X-API-Key: your-api-key" \
     -H "X-API-Secret: your-secret" \
     https://api.example.com/users
```

## Headers Best Practices

```
┌──────────────────────────────────────────────────────────────┐
│              ✅ HTTP HEADERS BEST PRACTICES                  │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  Request Headers:                                            │
│  ✅ ระบุ Accept เสมอ (application/json)                     │
│  ✅ ระบุ Content-Type เมื่อมี Body                          │
│  ✅ ใช้ Authorization header สำหรับ Auth                    │
│  ✅ ใช้ User-Agent ให้ชัดเจน (MyApp/1.0)                    │
│  ❌ อย่าส่ง Sensitive data ใน Custom headers (ยกเว้น Auth) │
│                                                              │
│  Response Headers:                                           │
│  ✅ ส่ง Content-Type เสมอ                                   │
│  ✅ ส่ง Cache-Control ที่เหมาะสม                            │
│  ✅ ส่ง CORS headers ถ้ารองรับ CORS                         │
│  ✅ ส่ง Location สำหรับ 201 Created                         │
│  ✅ ส่ง Rate Limit headers                                  │
│  ✅ ส่ง Security headers                                    │
│                                                              │
│  Custom Headers:                                             │
│  ✅ ใช้ชื่อที่มีความหมายชัดเจน                              │
│  ✅ ใช้ Request-ID/Correlation-ID เพื่อ Tracing             │
│  ⚠️  ไม่จำเป็นต้องขึ้นต้น X- (RFC 6648)                    │
│  ❌ อย่าใช้ Custom headers แทน Standard headers            │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

## ทดลองใช้ Headers

### ตัวอย่าง 1: Content Negotiation

```bash
# ขอ JSON
curl -H "Accept: application/json" \
     https://httpbin.org/headers

# ขอ XML (httpbin จะบอกว่ารับ request ได้)
curl -H "Accept: application/xml" \
     https://httpbin.org/headers

# ขอหลายแบบ (JSON มาก่อน)
curl -H "Accept: application/json, application/xml;q=0.9, */*;q=0.8" \
     https://httpbin.org/headers
```

### ตัวอย่าง 2: Authentication Headers

```bash
# GitHub API with Token
curl -H "Authorization: token YOUR_GITHUB_TOKEN" \
     https://api.github.com/user

# GitHub API without Token (rate limit ต่ำกว่า)
curl https://api.github.com/user
# → 401 Unauthorized
```

### ตัวอย่าง 3: Custom Headers

```bash
# ส่ง Custom headers และดูว่า Server รับได้
curl -H "X-Custom-Header: MyValue" \
     -H "X-Request-ID: 12345" \
     -H "X-API-Version: 2.0" \
     https://httpbin.org/headers

# Output จะแสดง headers ทั้งหมดที่ส่งไป
```

### ตัวอย่าง 4: Caching Headers

```bash
# ส่ง If-None-Match
curl -i -H "If-None-Match: \"abc123\"" \
     https://api.example.com/users/1

# ส่ง Cache-Control: no-cache
curl -i -H "Cache-Control: no-cache" \
     https://api.example.com/users/1
```

## Headers Debugging

### ใช้ curl แสดง Request/Response Headers

```bash
# แสดงเฉพาะ Response headers
curl -I https://api.github.com/users/octocat

# แสดงทั้ง Request และ Response
curl -v https://api.github.com/users/octocat

# แสดง Response headers + body
curl -i https://api.github.com/users/octocat

# แสดงเฉพาะ headers ที่สนใจ
curl -i https://api.github.com/users/octocat | grep -i content-type
curl -i https://api.github.com/users/octocat | grep -i cache-control
```

### ใช้ Browser DevTools

1. เปิด DevTools (F12)
2. Network tab
3. คลิกที่ Request
4. ดูใน Headers tab:
   - **General**: Method, Status, URL
   - **Response Headers**: Headers ที่ Server ส่งมา
   - **Request Headers**: Headers ที่ Browser ส่งไป

## แบบฝึกหัด Step 06

### Exercise 6.1: ทดสอบ Accept Header

```bash
# ลองเปลี่ยน Accept header
curl -H "Accept: application/json" https://httpbin.org/headers
curl -H "Accept: application/xml" https://httpbin.org/headers
curl -H "Accept: text/html" https://httpbin.org/headers
```

### Exercise 6.2: ทดสอบ Authorization

```bash
# ลองเรียก GitHub API โดยไม่ส่ง token
curl -i https://api.github.com/user

# สังเกต 401 Unauthorized และ rate limit headers
```

### Exercise 6.3: ทดสอบ Custom Headers

```bash
# ส่ง Custom headers หลายตัว
curl -H "X-Request-ID: $(date +%s)" \
     -H "X-User-Agent: MyApp/1.0" \
     -H "X-Device-Type: mobile" \
     https://httpbin.org/headers

# ดูว่า Server รับ headers ได้ครบไหม
```

### Exercise 6.4: วิเคราะห์ GitHub API Headers

```bash
# ดู Response headers จาก GitHub
curl -I https://api.github.com/users/octocat

# สังเกต:
# - X-RateLimit-* headers
# - Cache-Control
# - ETag
# - Content-Type
```

## สรุป Step 06

```
┌──────────────────────────────────────────────────────────────┐
│                 ✅ สิ่งที่เรียนรู้ Step 06                   │
├──────────────────────────────────────────────────────────────┤
│  ✅ HTTP Headers = Metadata ของ Request/Response            │
│  ✅ Request Headers: Accept, Authorization, Content-Type    │
│  ✅ Response Headers: Content-Type, Cache-Control, CORS     │
│  ✅ Custom Headers: Request-ID, API-Version, Tenant-ID      │
│  ✅ Headers Best Practices: ระบุ Accept, Content-Type      │
│  ✅ Debugging: curl -v, curl -i, Browser DevTools           │
└──────────────────────────────────────────────────────────────┘
```

---

# 🎯 STEP 07: REST Architecture Constraints

## เป้าหมาย

เข้าใจ 6 หลักการสำคัญของ REST Architecture ตามที่ Roy Fielding กำหนด

## REST คืออะไร?

**REST** = **RE**presentational **S**tate **T**ransfer

```
┌──────────────────────────────────────────────────────────────────┐
│                     🏗️  REST ARCHITECTURE                        │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  REST เป็น Architectural Style สำหรับ Distributed Systems       │
│  ที่ถูกกำหนดโดย Roy Fielding ในปี 2000                          │
│                                                                  │
│  📝 Dissertation: "Architectural Styles and the Design of        │
│                    Network-based Software Architectures"         │
│                                                                  │
│  🎯 จุดประสงค์: สร้าง Web Services ที่:                         │
│     • Scalable (ขยายได้)                                        │
│     • Reliable (เชื่อถือได้)                                    │
│     • Maintainable (บำรุงรักษาง่าย)                             │
│     • Interoperable (ทำงานร่วมกันได้)                          │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

## 6 REST Constraints

```
┌──────────────────────────────────────────────────────────────────┐
│                   📐 6 REST CONSTRAINTS                          │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1. Client-Server                                                │
│     แยก Client และ Server ออกจากกัน                             │
│                                                                  │
│  2. Stateless                                                    │
│     Server ไม่เก็บ State ของ Client                             │
│                                                                  │
│  3. Cacheable                                                    │
│     Response สามารถ Cache ได้                                   │
│                                                                  │
│  4. Uniform Interface                                            │
│     Interface เดียวกันสำหรับทุก Resource                        │
│                                                                  │
│  5. Layered System                                               │
│     สามารถมี Layer กลางได้ (Proxy, Gateway, Cache)              │
│                                                                  │
│  6. Code on Demand (Optional)                                    │
│     Server ส่ง Code ให้ Client รันได้ (JavaScript)              │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

## 1. Client-Server Constraint

### หลักการ

แยกความรับผิดชอบระหว่าง Client และ Server

```
┌──────────────────────────────────────────────────────────────┐
│                  🖥️  CLIENT-SERVER SEPARATION                │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌─────────────────┐              ┌─────────────────┐       │
│  │     CLIENT      │              │     SERVER      │       │
│  ├─────────────────┤              ├─────────────────┤       │
│  │ • UI/UX         │◀────────────▶│ • Business      │       │
│  │ • Presentation  │  HTTP/HTTPS  │   Logic         │       │
│  │ • User Input    │              │ • Data Storage  │       │
│  │                 │              │ • Authentication│       │
│  └─────────────────┘              └─────────────────┘       │
│                                                              │
│  ข้อดี:                                                      │
│  ✅ พัฒนาแยกกันได้ (Independent Evolution)                  │
│  ✅ Scale แยกกันได้                                         │
│  ✅ เปลี่ยน Client ได้โดยไม่กระทบ Server                   │
│  ✅ Client หลายแบบใช้ Server เดียวกันได้                   │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### ตัวอย่าง

```bash
# Server (API) เดียว รองรับ Clients หลายแบบ:

# 1. Web App (React/Vue/Angular)
curl -H "User-Agent: MyWebApp/1.0" \
     https://api.example.com/users

# 2. Mobile App (iOS/Android)
curl -H "User-Agent: MyMobileApp/2.0 (iOS)" \
     https://api.example.com/users

# 3. CLI Tool
curl -H "User-Agent: MyCLI/3.0" \
     https://api.example.com/users

# ทั้งหมดใช้ API เดียวกัน!
```

## 2. Stateless Constraint

### หลักการ

Server **ไม่เก็บ State** ของ Client แต่ละ Request ต้องมีข้อมูลครบ

```
┌──────────────────────────────────────────────────────────────┐
│                    🔄 STATELESS                              │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  ❌ Stateful (ไม่ใช่ REST):                                 │
│     Request 1: Login(username, password)                    │
│     Request 2: GetProfile()  ← Server จำว่า login แล้ว     │
│     Request 3: UpdateProfile(...)                           │
│                                                              │
│  ✅ Stateless (REST):                                        │
│     Request 1: POST /auth/login                             │
│                → Response: {"token": "abc123"}              │
│     Request 2: GET /profile                                 │
│                + Authorization: Bearer abc123               │
│     Request 3: PUT /profile                                 │
│                + Authorization: Bearer abc123               │
│                                                              │
│  ทุก Request ส่ง Token ไปด้วย Server ไม่ต้องจำ!           │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### ข้อดี Stateless

```
✅ Scalability    - เพิ่ม Server ได้ง่าย (Load Balance ไปที่ไหนก็ได้)
✅ Reliability    - Server ตายไม่กระทบ State
✅ Simplicity     - Server ไม่ต้องจัดการ Session
✅ Visibility     - ดู Request แต่ละตัวแยกกันได้
```

### ข้อเสีย Stateless

```
❌ Overhead       - ต้องส่งข้อมูลซ้ำทุก Request (Token, Context)
❌ Complexity     - Client ต้องจัดการ State เอง
```

### ตัวอย่าง

```bash
# Stateless: ทุก Request ต้องมี Token
TOKEN="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."

# Request 1
curl -H "Authorization: Bearer $TOKEN" \
     https://api.example.com/profile

# Request 2 (ส่ง Token ซ้ำ)
curl -H "Authorization: Bearer $TOKEN" \
     https://api.example.com/orders

# Request 3 (ส่ง Token ซ้ำอีก)
curl -H "Authorization: Bearer $TOKEN" \
     https://api.example.com/settings
```

## 3. Cacheable Constraint

### หลักการ

Response ต้องระบุว่า **Cache ได้หรือไม่**

```
┌──────────────────────────────────────────────────────────────┐
│                     💾 CACHEABLE                             │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  Flow with Cache:                                            │
│                                                              │
│  1. Client → Request → Cache                                 │
│     ├─ Cache HIT → Return cached response (Fast!)           │
│     └─ Cache MISS → Forward to Server                        │
│                                                              │
│  2. Server → Response + Cache-Control header                 │
│                                                              │
│  3. Cache → Store response (ถ้า Cacheable)                  │
│                                                              │
│  4. Client → Request ครั้งต่อไป → Cache HIT! (Fast)         │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### Cache Headers

```http
# Cacheable Response
HTTP/1.1 200 OK
Cache-Control: max-age=3600, public
ETag: "abc123"

# Non-Cacheable Response
HTTP/1.1 200 OK
Cache-Control: no-store, private
```

### ตัวอย่าง

```bash
# Request 1: ไม่มี Cache
curl -i https://api.github.com/users/octocat
# → Server ประมวลผล ใช้เวลา 200ms

# Response:
# Cache-Control: max-age=60
# ETag: "abc123"

# Request 2: (ภายใน 60 วินาที)
curl -i -H "If-None-Match: \"abc123\"" \
     https://api.github.com/users/octocat
# → 304 Not Modified (ใช้ Cache) ใช้เวลา 50ms
```

### ข้อดี Caching

```
✅ Performance     - ลด Latency, Response เร็วขึ้น
✅ Scalability     - ลดโหลด Server
✅ Availability    - ใช้ Cache ได้แม้ Server ล่ม
✅ Bandwidth       - ลดการส่งข้อมูลซ้ำ
```

## 4. Uniform Interface Constraint

### หลักการ

Interface เดียวกันสำหรับทุก Resource มี 4 หลักเสริม:

```
┌──────────────────────────────────────────────────────────────┐
│              🎯 UNIFORM INTERFACE (4 Principles)             │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  1. Resource Identification (URI)                            │
│     • ทุก Resource มี URI เฉพาะตัว                          │
│     • /users/1, /posts/5, /orders/123                       │
│                                                              │
│  2. Resource Manipulation through Representations            │
│     • ใช้ HTTP Methods (GET, POST, PUT, DELETE)             │
│     • ส่งข้อมูลเป็น JSON, XML, etc.                         │
│                                                              │
│  3. Self-Descriptive Messages                                │
│     • Request/Response มีข้อมูลครบ                          │
│     • มี Content-Type, Status Code, Headers                 │
│                                                              │
│  4. HATEOAS (Hypermedia As The Engine Of Application State) │
│     • Response มี Links ไปยัง Actions อื่นๆ                │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### ตัวอย่าง Uniform Interface

```bash
# ทุก Resource ใช้ HTTP Methods เดียวกัน

# Users
curl https://api.example.com/users              # GET all
curl https://api.example.com/users/1            # GET one
curl -X POST .../users -d '{...}'               # CREATE
curl -X PUT .../users/1 -d '{...}'              # UPDATE
curl -X DELETE .../users/1                      # DELETE

# Posts (ใช้ Interface เดียวกัน!)
curl https://api.example.com/posts              # GET all
curl https://api.example.com/posts/1            # GET one
curl -X POST .../posts -d '{...}'               # CREATE
curl -X PUT .../posts/1 -d '{...}'              # UPDATE
curl -X DELETE .../posts/1                      # DELETE
```

## 5. Layered System Constraint

### หลักการ

สามารถมี **Layer กลาง** ได้ Client ไม่รู้ว่าเชื่อมกับ Server จริงหรือ Layer กลาง

```
┌──────────────────────────────────────────────────────────────┐
│                    🏢 LAYERED SYSTEM                         │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  Client                                                      │
│    │                                                         │
│    ▼                                                         │
│  Load Balancer                                               │
│    │                                                         │
│    ▼                                                         │
│  API Gateway                                                 │
│    │                                                         │
│    ▼                                                         │
│  Cache Layer (Redis/Varnish)                                 │
│    │                                                         │
│    ▼                                                         │
│  Authentication Service                                      │
│    │                                                         │
│    ▼                                                         │
│  Backend Server 1 / Server 2 / Server 3                      │
│    │                                                         │
│    ▼                                                         │
│  Database                                                    │
│                                                              │
│  Client ไม่รู้ว่ามี Layer กี่ชั้น!                          │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### ประโยชน์

```
✅ Security        - เพิ่ม Firewall, WAF ได้
✅ Scalability     - เพิ่ม Load Balancer ได้
✅ Performance     - เพิ่ม Cache Layer ได้
✅ Encapsulation   - ซ่อนความซับซ้อนจาก Client
```

### ตัวอย่าง

```bash
# Client ส่ง Request ไปที่ api.example.com
curl https://api.example.com/users/1

# แต่จริงๆ อาจผ่าน:
# 1. DNS → 192.0.2.1 (Load Balancer)
# 2. Load Balancer → API Gateway (10.0.1.5)
# 3. API Gateway → Cache (10.0.2.10)
# 4. Cache MISS → Backend Server (10.0.3.20)
# 5. Backend → Database (10.0.4.30)

# Client ไม่รู้ไม่เห็น!
```

## 6. Code on Demand (Optional)

### หลักการ

Server สามารถส่ง **Code** ให้ Client รันได้ (Optional constraint)

```
┌──────────────────────────────────────────────────────────────┐
│                   📜 CODE ON DEMAND                          │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  Server ส่ง Code (JavaScript) ให้ Client                    │
│                                                              │
│  ตัวอย่าง:                                                   │
│  • Web Apps: Server ส่ง HTML + JavaScript                   │
│  • Single Page Apps (SPA): ส่ง React/Vue bundles            │
│  • Web Components: ส่ง Custom Elements                      │
│                                                              │
│  ข้อดี:                                                      │
│  ✅ Flexibility - Update logic โดยไม่ต้อง update client    │
│  ✅ Reduced client complexity - Code อยู่ที่ server          │
│                                                              │
│  ข้อเสีย:                                                    │
│  ❌ Security risks - รัน code จาก server                    │
│  ❌ Not applicable for all clients (e.g., mobile apps)      │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### ตัวอย่าง

```bash
# Server ส่ง HTML + JavaScript
curl https://example.com/app

# Response:
# <html>
#   <script src="/app.js"></script>
#   <script>
#     // Client รัน Code นี้
#     fetch('/api/users').then(...)
#   </script>
# </html>
```

## REST vs Non-REST

```
┌─────────────────────────────────────────────────────────────┐
│                    REST vs NON-REST                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  REST API:                                                  │
│  GET    /users/1                → Get user 1               │
│  POST   /users                  → Create user              │
│  PUT    /users/1                → Update user 1            │
│  DELETE /users/1                → Delete user 1            │
│                                                             │
│  Non-REST (RPC-style):                                      │
│  POST   /getUser                {id: 1}                    │
│  POST   /createUser             {name: "..."}              │
│  POST   /updateUser             {id: 1, name: "..."}       │
│  POST   /deleteUser             {id: 1}                    │
│                                                             │
│  REST ใช้ HTTP Methods + URIs                              │
│  Non-REST ใช้ POST ทุกอย่าง + Function names               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## แบบฝึกหัด Step 07

### Exercise 7.1: ทดสอบ Stateless

```bash
# สร้าง 2 requests แยกกัน ไม่มี session
curl https://jsonplaceholder.typicode.com/users/1
curl https://jsonplaceholder.typicode.com/users/2

# แต่ละ request เป็นอิสระ ไม่เกี่ยวข้องกัน
```

### Exercise 7.2: ทดสอบ Caching

```bash
# Request แรก
curl -i https://api.github.com/users/octocat | grep -i cache-control

# สังเกต Cache-Control header
```

### Exercise 7.3: ทดสอบ Uniform Interface

```bash
# ใช้ Methods เดียวกันกับ Resources ต่างกัน
curl https://jsonplaceholder.typicode.com/users/1
curl https://jsonplaceholder.typicode.com/posts/1
curl https://jsonplaceholder.typicode.com/comments/1

# ทุก Resource ใช้ GET เหมือนกัน
```

## สรุป Step 07

```
┌──────────────────────────────────────────────────────────────┐
│                 ✅ สิ่งที่เรียนรู้ Step 07                   │
├──────────────────────────────────────────────────────────────┤
│  ✅ REST มี 6 Constraints: Client-Server, Stateless, ...    │
│  ✅ Stateless = Server ไม่เก็บ State ของ Client            │
│  ✅ Cacheable = Response ระบุว่า Cache ได้หรือไม่           │
│  ✅ Uniform Interface = Interface เดียวสำหรับทุก Resource  │
│  ✅ Layered System = มี Layer กลางได้                       │
│  ✅ Code on Demand = ส่ง Code ให้ Client รันได้ (Optional) │
└──────────────────────────────────────────────────────────────┘
```

---

# 🎯 STEP 08: Statelessness & Cacheability in Depth

## เป้าหมาย

เจาะลึก Statelessness และ Cacheability พร้อมเทคนิคการนำไปใช้จริง

## Statelessness Deep Dive

### Session vs Token Authentication

```
┌──────────────────────────────────────────────────────────────────┐
│              🔐 SESSION vs TOKEN AUTHENTICATION                  │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ❌ SESSION-BASED (Stateful):                                    │
│                                                                  │
│  1. Client → POST /login {username, password}                   │
│  2. Server → ตรวจสอบ → สร้าง Session ID → เก็บใน Memory/DB     │
│  3. Server → Response: Set-Cookie: sessionId=abc123             │
│  4. Client → GET /profile + Cookie: sessionId=abc123            │
│  5. Server → หา Session จาก Memory → ดึงข้อมูล User            │
│                                                                  │
│  ปัญหา:                                                          │
│  • Server ต้องเก็บ Session (Memory/Redis/Database)              │
│  • Scale ยาก (ต้อง Sticky Session หรือ Shared Storage)         │
│  • Server ตาย = Session หาย                                     │
│                                                                  │
│  ✅ TOKEN-BASED (Stateless):                                     │
│                                                                  │
│  1. Client → POST /login {username, password}                   │
│  2. Server → ตรวจสอบ → สร้าง JWT Token (มีข้อมูล User ข้างใน)   │
│  3. Server → Response: {"token": "eyJhbGc..."}                  │
│  4. Client → GET /profile + Authorization: Bearer eyJhbGc...    │
│  5. Server → Verify Token → ถอดรหัส → ได้ข้อมูล User           │
│                                                                  │
│  ข้อดี:                                                          │
│  • Server ไม่ต้องเก็บอะไร                                       │
│  • Scale ง่าย (Load Balance ไปที่ไหนก็ได้)                     │
│  • Server ตายไม่กระทบ Token                                     │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### JWT (JSON Web Token) Structure

```
┌──────────────────────────────────────────────────────────────────┐
│                       🎫 JWT TOKEN STRUCTURE                     │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  JWT = HEADER.PAYLOAD.SIGNATURE                                  │
│                                                                  │
│  eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.                           │
│  eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwImlhdCI6MTY...│
│  SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c                     │
│  ────────┬────────────────  ──────────┬──────────  ──────┬────── │
│        HEADER              PAYLOAD              SIGNATURE        │
│                                                                  │
│  HEADER (Base64):                                                │
│  {                                                               │
│    "alg": "HS256",   ← Algorithm                                 │
│    "typ": "JWT"      ← Type                                      │
│  }                                                               │
│                                                                  │
│  PAYLOAD (Base64):                                               │
│  {                                                               │
│    "sub": "1234567890",  ← User ID                               │
│    "name": "John Doe",   ← User Data                             │
│    "iat": 1699358400,    ← Issued At                             │
│    "exp": 1699444800     ← Expiration                            │
│  }                                                               │
│                                                                  │
│  SIGNATURE:                                                      │
│  HMACSHA256(                                                     │
│    base64UrlEncode(header) + "." + base64UrlEncode(payload),    │
│    secret                                                        │
│  )                                                               │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### ตัวอย่าง Stateless API Call

```bash
# 1. Login และรับ Token
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"username":"john","password":"secret"}' \
  https://api.example.com/auth/login

# Response:
# {
#   "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
#   "expiresIn": 3600
# }

# เก็บ Token ไว้
TOKEN="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."

# 2. ใช้ Token เรียก API (Stateless)
curl -H "Authorization: Bearer $TOKEN" \
     https://api.example.com/profile

# 3. ทุก Request ต่อไปต้องส่ง Token
curl -H "Authorization: Bearer $TOKEN" \
     https://api.example.com/orders

curl -H "Authorization: Bearer $TOKEN" \
     https://api.example.com/settings
```

## Cacheability Deep Dive

### Cache Levels

```
┌──────────────────────────────────────────────────────────────────┐
│                     💾 CACHE HIERARCHY                           │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1. Browser Cache (Client-side)                                  │
│     • ใกล้ User ที่สุด                                          │
│     • เร็วที่สุด (ไม่ต้องส่ง Request)                           │
│     • ต่อ User เท่านั้น                                         │
│                                                                  │
│  2. CDN Cache (Edge/Intermediate)                                │
│     • อยู่ทั่วโลก (Edge Locations)                              │
│     • ใกล้ User                                                  │
│     • แชร์ระหว่าง Users                                         │
│                                                                  │
│  3. Reverse Proxy Cache (Server-side)                            │
│     • Nginx, Varnish, Apache                                    │
│     • อยู่หน้า Backend                                          │
│     • แชร์ระหว่าง Requests                                      │
│                                                                  │
│  4. Application Cache (In-Memory)                                │
│     • Redis, Memcached                                           │
│     • ใน Backend                                                │
│     • Cache ข้อมูลจาก Database                                  │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### Cache-Control Directives

```bash
# 1. Public Cache (CDN, Proxy, Browser สามารถ Cache ได้)
Cache-Control: public, max-age=3600

# 2. Private Cache (เฉพาะ Browser)
Cache-Control: private, max-age=600

# 3. No Cache (ต้องตรวจสอบ Server ก่อนใช้)
Cache-Control: no-cache

# 4. No Store (ห้าม Cache เลย)
Cache-Control: no-store

# 5. Must Revalidate (ต้องตรวจสอบหลัง expire)
Cache-Control: max-age=3600, must-revalidate

# 6. Immutable (ไม่เปลี่ยน ไม่ต้องตรวจสอบ)
Cache-Control: public, max-age=31536000, immutable
```

### ETag & Conditional Requests

```
┌──────────────────────────────────────────────────────────────────┐
│                   🏷️  ETAG FLOW                                  │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Request 1: GET /users/1                                         │
│  Response:                                                       │
│    HTTP/1.1 200 OK                                               │
│    ETag: "abc123"                                                │
│    Cache-Control: max-age=0, must-revalidate                     │
│    {"id": 1, "name": "John"}                                     │
│                                                                  │
│  Client เก็บ ETag = "abc123"                                     │
│                                                                  │
│  Request 2: GET /users/1                                         │
│    If-None-Match: "abc123"  ← ส่ง ETag ไป                       │
│                                                                  │
│  Response (ถ้าข้อมูลไม่เปลี่ยน):                                │
│    HTTP/1.1 304 Not Modified                                     │
│    ETag: "abc123"                                                │
│    (ไม่มี Body - ประหยัด Bandwidth!)                            │
│                                                                  │
│  Response (ถ้าข้อมูลเปลี่ยน):                                   │
│    HTTP/1.1 200 OK                                               │
│    ETag: "def456"  ← ETag ใหม่                                  │
│    {"id": 1, "name": "Jane"}  ← ข้อมูลใหม่                      │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### ตัวอย่าง Cache Headers

```bash
# 1. ทดสอบ Cache-Control
curl -i https://api.github.com/users/octocat | grep -i cache-control
# Output: Cache-Control: public, max-age=60, s-maxage=60

# 2. ทดสอบ ETag
curl -i https://api.github.com/users/octocat | grep -i etag
# Output: ETag: W/"abc123def456"

# 3. ทดสอบ Conditional Request
ETAG=$(curl -si https://api.github.com/users/octocat | grep -i etag | cut -d' ' -f2)
curl -i -H "If-None-Match: $ETAG" https://api.github.com/users/octocat
# → 304 Not Modified (ถ้าไม่เปลี่ยน)

# 4. ทดสอบ Last-Modified
curl -i https://api.github.com/users/octocat | grep -i last-modified
```

### Caching Strategies

```
┌──────────────────────────────────────────────────────────────────┐
│                  📋 CACHING STRATEGIES                           │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1. STATIC RESOURCES (Images, CSS, JS)                           │
│     Cache-Control: public, max-age=31536000, immutable           │
│     • Cache นาน (1 ปี)                                          │
│     • ใช้ Versioning ใน URL (/app.v1.2.3.js)                    │
│                                                                  │
│  2. USER-SPECIFIC DATA (Profile, Orders)                         │
│     Cache-Control: private, max-age=300                          │
│     • Cache เฉพาะ Browser                                       │
│     • Cache สั้นๆ (5 นาที)                                      │
│                                                                  │
│  3. PUBLIC DATA (Blog Posts, Product List)                       │
│     Cache-Control: public, max-age=600, s-maxage=3600            │
│     ETag: "abc123"                                               │
│     • Cache ได้ทุกที่                                           │
│     • CDN cache นาน (1 ชม.), Browser cache สั้น (10 นาที)      │
│                                                                  │
│  4. SENSITIVE DATA (Payment Info, Health Records)                │
│     Cache-Control: no-store, private                             │
│     • ห้าม Cache เลย                                            │
│                                                                  │
│  5. FREQUENTLY CHANGING DATA (Stock Prices, Live Scores)         │
│     Cache-Control: no-cache, must-revalidate                     │
│     ETag: "xyz789"                                               │
│     • ต้องตรวจสอบ Server ก่อนใช้                                │
│     • ใช้ ETag เพื่อลด Bandwidth                                │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

## แบบฝึกหัด Step 08

### Exercise 8.1: วิเคราะห์ Cache Headers

```bash
# ดู Cache headers จากหลาย APIs
curl -i https://api.github.com/users/octocat | grep -i "cache\|etag"
curl -i https://jsonplaceholder.typicode.com/users/1 | grep -i "cache\|etag"
curl -i https://dog.ceo/api/breeds/image/random | grep -i "cache\|etag"
```

### Exercise 8.2: ทดสอบ Conditional Request

```bash
# 1. GET และเก็บ ETag
curl -i https://api.github.com/users/octocat > response.txt
ETAG=$(grep -i etag response.txt | cut -d' ' -f2 | tr -d '\r')

# 2. ส่ง Conditional Request
curl -i -H "If-None-Match: $ETAG" https://api.github.com/users/octocat
# → ควรได้ 304 Not Modified
```

### Exercise 8.3: สร้าง JWT Token (ใช้ jwt.io)

1. ไปที่ https://jwt.io/
2. ใส่ Payload:
   ```json
   {
     "sub": "1234567890",
     "name": "John Doe",
     "iat": 1699358400
   }
   ```
3. คัดลอก Token ที่ได้
4. ถอดรหัสกลับเพื่อดูข้อมูล

## สรุป Step 08

```
┌──────────────────────────────────────────────────────────────────┐
│                 ✅ สิ่งที่เรียนรู้ Step 08                       │
├──────────────────────────────────────────────────────────────────┤
│  ✅ Stateless ใช้ Token (JWT) แทน Session                       │
│  ✅ JWT มี 3 ส่วน: Header, Payload, Signature                   │
│  ✅ Cache มีหลาย Level: Browser, CDN, Proxy, Application        │
│  ✅ Cache-Control: public/private, max-age, no-cache/no-store   │
│  ✅ ETag ใช้สำหรับ Conditional Request (304 Not Modified)       │
│  ✅ Caching Strategy ขึ้นกับประเภทข้อมูล                        │
└──────────────────────────────────────────────────────────────────┘
```

---

# 🎯 STEP 09: Uniform Interface Principles

## เป้าหมาย

เข้าใจ 4 หลักการของ Uniform Interface และการออกแบบ Resource-Based API

## 4 Principles of Uniform Interface

### 1. Resource Identification in Requests

```
┌──────────────────────────────────────────────────────────────────┐
│               🆔 RESOURCE IDENTIFICATION                         │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  หลักการ: ทุก Resource มี URI ที่ไม่ซ้ำกัน                      │
│                                                                  │
│  ✅ GOOD:                                                         │
│    GET /users/1              ← User ID 1                         │
│    GET /users/1/posts        ← Posts ของ User 1                 │
│    GET /users/1/posts/5      ← Post ID 5 ของ User 1             │
│    GET /posts/5/comments     ← Comments ของ Post 5              │
│                                                                  │
│  ❌ BAD:                                                          │
│    GET /getUser?id=1         ← RPC style                         │
│    GET /api?action=getUser&id=1                                  │
│    POST /users/get           ← ใช้ POST สำหรับ GET              │
│                                                                  │
│  Resource Naming Rules:                                          │
│  • ใช้ Nouns ไม่ใช่ Verbs (/users ไม่ใช่ /getUsers)             │
│  • ใช้ Plural (/users ไม่ใช่ /user)                             │
│  • ใช้ lowercase, hyphen-separated (/user-profiles)             │
│  • Nested resources แสดง relationship                           │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

#### ตัวอย่าง Resource URIs

```bash
# Collections & Resources
GET    /users                  # Collection
GET    /users/1                # Single resource
POST   /users                  # Create
PUT    /users/1                # Update
DELETE /users/1                # Delete

# Nested Resources (Relationships)
GET    /users/1/posts          # Posts ของ User 1
GET    /users/1/posts/5        # Post 5 ของ User 1
POST   /users/1/posts          # สร้าง Post ใหม่ให้ User 1

# Filtering (Query Parameters)
GET    /users?role=admin       # Users ที่เป็น admin
GET    /posts?status=published&limit=10
GET    /products?category=electronics&sort=price&order=asc
```

### 2. Resource Manipulation through Representations

```
┌──────────────────────────────────────────────────────────────────┐
│            📦 MANIPULATION THROUGH REPRESENTATIONS               │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  หลักการ: Client จัดการ Resource ผ่าน Representation (JSON)    │
│                                                                  │
│  Resource (Database):                                            │
│    users table:                                                  │
│    | id | name    | email           | password_hash | ...       │
│    | 1  | John    | john@email.com  | $2a$10$...    | ...       │
│                                                                  │
│  Representation (JSON Response):                                 │
│    {                                                             │
│      "id": 1,                                                    │
│      "name": "John",                                             │
│      "email": "john@email.com"                                   │
│      // ไม่มี password!                                         │
│    }                                                             │
│                                                                  │
│  Client ไม่เห็นข้อมูลจริงใน Database แต่ได้ Representation     │
│  ในรูปแบบที่เหมาะสม (JSON, XML, etc.)                            │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

#### ตัวอย่าง Different Representations

```bash
# 1. JSON Representation (Default)
curl -H "Accept: application/json" \
     https://api.example.com/users/1
# Response:
# {
#   "id": 1,
#   "name": "John Doe",
#   "email": "john@example.com"
# }

# 2. XML Representation (ถ้า API รองรับ)
curl -H "Accept: application/xml" \
     https://api.example.com/users/1
# Response:
# <user>
#   <id>1</id>
#   <name>John Doe</name>
#   <email>john@example.com</email>
# </user>

# 3. Minimal Representation (Fields Selection)
curl "https://api.github.com/users/octocat?fields=login,name,id"
```

### 3. Self-Descriptive Messages

```
┌──────────────────────────────────────────────────────────────────┐
│                 📝 SELF-DESCRIPTIVE MESSAGES                     │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  หลักการ: Message มีข้อมูลครบ ไม่ต้องพึ่งพา Context นอก       │
│                                                                  │
│  ✅ GOOD (Self-Descriptive):                                     │
│                                                                  │
│    GET /users/1 HTTP/1.1                                         │
│    Host: api.example.com                                         │
│    Accept: application/json                                      │
│    Authorization: Bearer eyJhbGc...                              │
│                                                                  │
│    HTTP/1.1 200 OK                                               │
│    Content-Type: application/json; charset=utf-8                 │
│    Cache-Control: max-age=600                                    │
│    ETag: "abc123"                                                │
│    {                                                             │
│      "id": 1,                                                    │
│      "name": "John Doe",                                         │
│      "created_at": "2025-11-07T10:00:00Z"                        │
│    }                                                             │
│                                                                  │
│  Headers บอก:                                                    │
│  • Content-Type → รูปแบบข้อมูล (JSON, UTF-8)                    │
│  • Cache-Control → วิธี Cache                                   │
│  • ETag → Version ของข้อมูล                                     │
│                                                                  │
│  ❌ BAD (Not Self-Descriptive):                                  │
│    HTTP/1.1 200 OK                                               │
│    1,John Doe,2025-11-07                                         │
│    ← ไม่บอก Format, ไม่มี Headers, ไม่มี Metadata              │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

#### ตัวอย่าง Self-Descriptive Response

```bash
# Request
curl -v https://jsonplaceholder.typicode.com/users/1

# Response (Self-Descriptive)
# HTTP/2 200 OK
# date: Fri, 07 Nov 2025 10:30:00 GMT
# content-type: application/json; charset=utf-8  ← บอก Format
# content-length: 509                            ← บอก Size
# cache-control: max-age=43200                   ← บอก Cache
# etag: W/"1fd-1234567890"                       ← บอก Version
# x-ratelimit-limit: 100                         ← บอก Rate Limit
# x-ratelimit-remaining: 95
#
# {
#   "id": 1,
#   "name": "Leanne Graham",
#   "username": "Bret",
#   "email": "Sincere@april.biz",
#   "address": {
#     "street": "Kulas Light",
#     "city": "Gwenborough",
#     "zipcode": "92998-3874"
#   }
# }

# จาก Response สามารถรู้ได้ว่า:
# - รูปแบบข้อมูล: JSON, UTF-8
# - ขนาด: 509 bytes
# - Cache ได้: 12 ชั่วโมง
# - Version: W/"1fd-1234567890"
# - Rate Limit: เหลืออีก 95/100
```

### 4. Hypermedia As The Engine Of Application State (HATEOAS)

```
┌──────────────────────────────────────────────────────────────────┐
│                     🔗 HATEOAS                                   │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  หลักการ: Response มี Links ไปยัง Actions อื่นๆ ที่ทำได้       │
│                                                                  │
│  ✅ WITH HATEOAS:                                                 │
│                                                                  │
│    GET /users/1                                                  │
│    {                                                             │
│      "id": 1,                                                    │
│      "name": "John Doe",                                         │
│      "links": [                                                  │
│        {"rel": "self", "href": "/users/1"},                      │
│        {"rel": "posts", "href": "/users/1/posts"},               │
│        {"rel": "friends", "href": "/users/1/friends"},           │
│        {"rel": "update", "href": "/users/1", "method": "PUT"},   │
│        {"rel": "delete", "href": "/users/1", "method": "DELETE"} │
│      ]                                                           │
│    }                                                             │
│                                                                  │
│  Client รู้ว่าทำอะไรต่อได้บ้างโดยไม่ต้อง Hard-code URLs!       │
│                                                                  │
│  ❌ WITHOUT HATEOAS:                                              │
│    {                                                             │
│      "id": 1,                                                    │
│      "name": "John Doe"                                          │
│    }                                                             │
│    ← ไม่รู้ว่าทำอะไรต่อได้                                      │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

#### ตัวอย่าง HATEOAS Response

```bash
# GitHub API (มี HATEOAS)
curl https://api.github.com/users/octocat

# Response:
{
  "login": "octocat",
  "id": 583231,
  "avatar_url": "https://avatars.githubusercontent.com/u/583231",
  "url": "https://api.github.com/users/octocat",
  "followers_url": "https://api.github.com/users/octocat/followers",
  "following_url": "https://api.github.com/users/octocat/following{/other_user}",
  "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
  "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
  "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
  "repos_url": "https://api.github.com/users/octocat/repos"
}

# มี URLs ไปยัง Resources อื่นๆ ที่เกี่ยวข้อง!
```

#### HATEOAS Formats

```json
// HAL (Hypertext Application Language)
{
  "id": 1,
  "name": "John Doe",
  "_links": {
    "self": { "href": "/users/1" },
    "posts": { "href": "/users/1/posts" },
    "friends": { "href": "/users/1/friends" }
  }
}

// JSON:API Format
{
  "data": {
    "type": "users",
    "id": "1",
    "attributes": {
      "name": "John Doe"
    },
    "relationships": {
      "posts": {
        "links": {
          "related": "/users/1/posts"
        }
      }
    },
    "links": {
      "self": "/users/1"
    }
  }
}

// Simple Links Array
{
  "id": 1,
  "name": "John Doe",
  "links": [
    { "rel": "self", "href": "/users/1", "method": "GET" },
    { "rel": "update", "href": "/users/1", "method": "PUT" },
    { "rel": "delete", "href": "/users/1", "method": "DELETE" }
  ]
}
```

## Resource Naming Best Practices

```
┌──────────────────────────────────────────────────────────────────┐
│              📛 RESOURCE NAMING BEST PRACTICES                   │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ✅ DO:                                                           │
│    /users                     - Plural nouns                     │
│    /users/1                   - ID in path                       │
│    /users/1/posts             - Nested resources                 │
│    /products?category=tech    - Query params for filtering       │
│    /user-profiles             - Hyphen for multi-word            │
│                                                                  │
│  ❌ DON'T:                                                        │
│    /getUsers                  - ไม่ใช่ verbs                     │
│    /user                      - ไม่ใช่ singular                  │
│    /users/get/1               - ไม่ใช้ actions ใน path          │
│    /users_profiles            - ไม่ใช้ underscore               │
│    /Users                     - ไม่ใช้ uppercase                 │
│                                                                  │
│  HTTP Methods แทน Actions:                                       │
│    GET    /users              แทน  /getUsers                     │
│    POST   /users              แทน  /createUser                   │
│    PUT    /users/1            แทน  /updateUser?id=1              │
│    DELETE /users/1            แทน  /deleteUser?id=1              │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

## แบบฝึกหัด Step 09

### Exercise 9.1: วิเคราะห์ URIs

วิเคราะห์ว่า URI ไหนดี ไหนไม่ดี:

```
1. GET /users                     → ดี ✅
2. GET /getUsers                  → ไม่ดี ❌ (มี verb)
3. POST /users                    → ดี ✅
4. POST /createUser               → ไม่ดี ❌ (มี verb)
5. GET /users/1/posts             → ดี ✅
6. GET /api?action=getUser&id=1   → ไม่ดี ❌ (RPC style)
7. DELETE /users/delete/1         → ไม่ดี ❌ (action ใน path)
8. GET /products?category=tech    → ดี ✅
```

### Exercise 9.2: ทดสอบ HATEOAS

```bash
# ดู Links ใน GitHub API Response
curl https://api.github.com/users/octocat | grep -i "_url"

# จะเห็น URLs หลายตัว เช่น:
# - followers_url
# - repos_url
# - gists_url
```

### Exercise 9.3: ออกแบบ RESTful URIs

ออกแบบ URIs สำหรับ Blog System:

```
Resources: Users, Posts, Comments, Categories

✅ เฉลย:
GET    /users                   - List users
GET    /users/1                 - Get user
POST   /users                   - Create user
PUT    /users/1                 - Update user
DELETE /users/1                 - Delete user

GET    /posts                   - List posts
GET    /posts/1                 - Get post
POST   /posts                   - Create post
PUT    /posts/1                 - Update post
DELETE /posts/1                 - Delete post

GET    /posts/1/comments        - Comments ของ Post 1
POST   /posts/1/comments        - เพิ่ม Comment
DELETE /comments/5              - ลบ Comment

GET    /categories              - List categories
GET    /posts?category=tech     - Posts ใน Category tech
```

## สรุป Step 09

```
┌──────────────────────────────────────────────────────────────────┐
│                 ✅ สิ่งที่เรียนรู้ Step 09                       │
├──────────────────────────────────────────────────────────────────┤
│  ✅ Uniform Interface มี 4 หลักการ                              │
│  ✅ 1. Resource Identification - ทุก Resource มี URI            │
│  ✅ 2. Manipulation through Representations - ใช้ JSON/XML      │
│  ✅ 3. Self-Descriptive Messages - มี Headers ครบ              │
│  ✅ 4. HATEOAS - Response มี Links ไปยัง Actions อื่น          │
│  ✅ Resource Naming: Plural nouns, lowercase, hyphens           │
│  ✅ ใช้ HTTP Methods แทน Verbs ใน URIs                          │
└──────────────────────────────────────────────────────────────────┘
```

---

# 🎯 STEP 10: HATEOAS & Layered System Implementation

## เป้าหมาย

เข้าใจ HATEOAS อย่างลึกซึ้ง และสถาปัตยกรรม Layered System

## HATEOAS Deep Dive

### Why HATEOAS?

```
┌──────────────────────────────────────────────────────────────────┐
│                  🎯 WHY HATEOAS?                                 │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ❌ Without HATEOAS:                                              │
│     Client ต้อง Hard-code URLs:                                  │
│     const API_BASE = 'https://api.example.com'                   │
│     fetch(`${API_BASE}/users/1/posts`)                           │
│     fetch(`${API_BASE}/users/1/friends`)                         │
│                                                                  │
│     ปัญหา:                                                       │
│     • เปลี่ยน URL structure → Client ต้องแก้โค้ดทุกที่           │
│     • เพิ่ม API version → Client ต้อง update                    │
│     • Client ต้องรู้ทุก endpoint ล่วงหน้า                       │
│                                                                  │
│  ✅ With HATEOAS:                                                 │
│     Server บอก Client ว่าทำอะไรได้บ้าง:                         │
│     GET /users/1 → Response มี links                             │
│     Client ตาม links ไป ไม่ต้อง hard-code                      │
│                                                                  │
│     ข้อดี:                                                       │
│     • Decoupling - Client ไม่ต้องรู้ URL structure              │
│     • Evolvability - เปลี่ยน URLs ได้โดยไม่กระทบ Client        │
│     • Discoverability - Client ค้นพบ features ใหม่ได้อัตโนมัติ │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### HATEOAS Example: Order Workflow

```bash
# State 1: Order Created
GET /orders/123
{
  "id": 123,
  "status": "pending",
  "total": 99.99,
  "items": [...],
  "links": [
    {"rel": "self", "href": "/orders/123"},
    {"rel": "pay", "href": "/orders/123/payment", "method": "POST"},
    {"rel": "cancel", "href": "/orders/123", "method": "DELETE"}
  ]
}
# Actions: pay หรือ cancel

# State 2: Order Paid
GET /orders/123
{
  "id": 123,
  "status": "paid",
  "total": 99.99,
  "links": [
    {"rel": "self", "href": "/orders/123"},
    {"rel": "ship", "href": "/orders/123/shipping", "method": "POST"},
    {"rel": "refund", "href": "/orders/123/refund", "method": "POST"}
  ]
}
# Actions: ship หรือ refund (ไม่มี cancel แล้ว เพราะจ่ายแล้ว)

# State 3: Order Shipped
GET /orders/123
{
  "id": 123,
  "status": "shipped",
  "tracking": "TRK123456",
  "links": [
    {"rel": "self", "href": "/orders/123"},
    {"rel": "track", "href": "/orders/123/tracking"},
    {"rel": "return", "href": "/orders/123/return", "method": "POST"}
  ]
}
# Actions: track หรือ return (ไม่มี ship แล้ว)
```

### HATEOAS Standards

#### HAL (Hypertext Application Language)

```json
// GET /users/1
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "_links": {
    "self": {
      "href": "/users/1"
    },
    "posts": {
      "href": "/users/1/posts"
    },
    "friends": {
      "href": "/users/1/friends"
    }
  },
  "_embedded": {
    "posts": [
      {
        "id": 5,
        "title": "My Post",
        "_links": {
          "self": { "href": "/posts/5" }
        }
      }
    ]
  }
}
```

#### JSON:API

```json
{
  "data": {
    "type": "users",
    "id": "1",
    "attributes": {
      "name": "John Doe",
      "email": "john@example.com"
    },
    "relationships": {
      "posts": {
        "links": {
          "self": "/users/1/relationships/posts",
          "related": "/users/1/posts"
        }
      }
    }
  },
  "links": {
    "self": "/users/1"
  }
}
```

## Layered System Architecture

### Common Layers

```
┌──────────────────────────────────────────────────────────────────┐
│              🏗️  LAYERED SYSTEM ARCHITECTURE                     │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Layer 1: CLIENT                                                 │
│  ┌────────────────────────────────────────────────────────┐     │
│  │  Browser, Mobile App, Desktop App, CLI Tool            │     │
│  └────────────────────────────────────────────────────────┘     │
│                          │                                       │
│                          ▼ HTTPS                                 │
│  Layer 2: CDN / EDGE                                             │
│  ┌────────────────────────────────────────────────────────┐     │
│  │  CloudFlare, Akamai, AWS CloudFront                    │     │
│  │  • Caching                                             │     │
│  │  • DDoS Protection                                     │     │
│  │  • SSL Termination                                     │     │
│  └────────────────────────────────────────────────────────┘     │
│                          │                                       │
│                          ▼                                       │
│  Layer 3: LOAD BALANCER                                          │
│  ┌────────────────────────────────────────────────────────┐     │
│  │  Nginx, HAProxy, AWS ALB/NLB                           │     │
│  │  • Distribute traffic                                  │     │
│  │  • Health checks                                       │     │
│  │  • SSL Termination                                     │     │
│  └────────────────────────────────────────────────────────┘     │
│                     │           │                               │
│           ┌─────────┴───────────┴─────────┐                     │
│           ▼                               ▼                     │
│  Layer 4: API GATEWAY                                            │
│  ┌────────────────────────────────────────────────────────┐     │
│  │  Kong, AWS API Gateway, Azure APIM                     │     │
│  │  • Authentication                                      │     │
│  │  • Rate Limiting                                       │     │
│  │  • Request/Response Transformation                     │     │
│  │  • Logging & Monitoring                                │     │
│  └────────────────────────────────────────────────────────┘     │
│                          │                                       │
│                          ▼                                       │
│  Layer 5: CACHE LAYER                                            │
│  ┌────────────────────────────────────────────────────────┐     │
│  │  Redis, Memcached, Varnish                             │     │
│  │  • Response caching                                    │     │
│  │  • Session storage                                     │     │
│  └────────────────────────────────────────────────────────┘     │
│                          │                                       │
│                          ▼                                       │
│  Layer 6: APPLICATION SERVERS                                    │
│  ┌────────────────────────────────────────────────────────┐     │
│  │  Node.js, Python, Go, Java Servers                     │     │
│  │  Server 1    Server 2    Server 3    Server N          │     │
│  │  • Business Logic                                      │     │
│  │  • Data Validation                                     │     │
│  │  • Authorization                                       │     │
│  └────────────────────────────────────────────────────────┘     │
│                          │                                       │
│                          ▼                                       │
│  Layer 7: DATABASE                                               │
│  ┌────────────────────────────────────────────────────────┐     │
│  │  PostgreSQL, MySQL, MongoDB                            │     │
│  │  Primary + Replicas                                    │     │
│  └────────────────────────────────────────────────────────┘     │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### Benefits of Layered System

```
┌──────────────────────────────────────────────────────────────────┐
│               ✅ LAYERED SYSTEM BENEFITS                         │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1. SECURITY (ความปลอดภัย)                                       │
│     • เพิ่ม Firewall, WAF ได้                                   │
│     • SSL Termination ที่ Layer นอก                             │
│     • ซ่อน Backend servers จาก public internet                 │
│                                                                  │
│  2. SCALABILITY (การขยายตัว)                                     │
│     • Scale แต่ละ Layer แยกกันได้                               │
│     • เพิ่ม Servers ใน Application Layer                        │
│     • เพิ่ม CDN nodes worldwide                                 │
│                                                                  │
│  3. PERFORMANCE (ประสิทธิภาพ)                                    │
│     • Caching ที่หลาย Layers                                    │
│     • CDN ลดระยะทาง                                             │
│     • Load Balancing กระจายโหลด                                 │
│                                                                  │
│  4. MAINTAINABILITY (บำรุงรักษา)                                 │
│     • แก้ไข/อัพเกรดแต่ละ Layer แยกกัน                           │
│     • Rolling update ได้โดยไม่ downtime                         │
│     • แยก concerns ชัดเจน                                       │
│                                                                  │
│  5. RELIABILITY (ความน่าเชื่อถือ)                               │
│     • Redundancy ที่หลาย Layers                                 │
│     • Failover อัตโนมัติ                                        │
│     • Health checks                                             │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### Real-World Example: GitHub API

```bash
# เมื่อเรียก GitHub API
curl https://api.github.com/users/octocat

# จริงๆ ผ่าน Layers:

# 1. DNS Resolution
#    api.github.com → 140.82.121.6

# 2. HTTPS Connection (TLS)
#    → CDN / Edge (Fastly)

# 3. CDN Check
#    Cache HIT? → Return
#    Cache MISS? → Forward

# 4. Load Balancer
#    → เลือก Backend Server

# 5. API Gateway
#    → Check Rate Limit
#    → Check Authentication
#    → Log Request

# 6. Application Server
#    → Process Request
#    → Query Database
#    → Build Response

# 7. Response ย้อนกลับผ่าน Layers เดิม
#    → Cache ที่ CDN
#    → Return to Client
```

## แบบฝึกหัด Step 10

### Exercise 10.1: วิเคราะห์ HATEOAS

```bash
# ดู GitHub API HATEOAS Links
curl https://api.github.com/

# จะเห็น Links ไปยัง endpoints ต่างๆ:
# - current_user_url
# - user_url
# - repository_url
# - etc.

# ลองตาม link ไปเรื่อยๆ
curl https://api.github.com/users/octocat
curl <repos_url จาก response>
```

### Exercise 10.2: Trace Request Flow

```bash
# ใช้ curl -v เพื่อดู Connection Details
curl -v https://api.github.com/users/octocat

# สังเกต:
# * Trying <IP>...
# * Connected to api.github.com
# * SSL connection using <protocol>
# > GET /users/octocat HTTP/2
# < HTTP/2 200
# < server: GitHub.com  ← Server header
# < x-github-request-id: <id>  ← Request tracking
```

### Exercise 10.3: ออกแบบ HATEOAS Response

ออกแบบ Response สำหรับ E-commerce Order:

```json
// GET /orders/123
{
  "id": 123,
  "status": "pending",
  "total": 199.99,
  "items": [
    {"id": 1, "name": "Product A", "price": 99.99},
    {"id": 2, "name": "Product B", "price": 100.00}
  ],
  "links": [
    {
      "rel": "self",
      "href": "/orders/123",
      "method": "GET"
    },
    {
      "rel": "pay",
      "href": "/orders/123/payment",
      "method": "POST",
      "description": "Pay for this order"
    },
    {
      "rel": "cancel",
      "href": "/orders/123",
      "method": "DELETE",
      "description": "Cancel this order"
    },
    {
      "rel": "items",
      "href": "/orders/123/items",
      "method": "GET"
    }
  ]
}
```

## สรุป Step 10

```
┌──────────────────────────────────────────────────────────────────┐
│                 ✅ สิ่งที่เรียนรู้ Step 10                       │
├──────────────────────────────────────────────────────────────────┤
│  ✅ HATEOAS = Response มี Links ไปยัง Actions ที่ทำได้         │
│  ✅ ข้อดี HATEOAS: Decoupling, Evolvability, Discoverability    │
│  ✅ HATEOAS Standards: HAL, JSON:API                             │
│  ✅ Layered System มีหลาย Layers: CDN, LB, Gateway, Cache, App  │
│  ✅ ข้อดี Layers: Security, Scalability, Performance            │
│  ✅ Client ไม่รู้ว่ามี Layer กี่ชั้น (Encapsulation)            │
└──────────────────────────────────────────────────────────────────┘
```

---

## 📊 สถิติ PART 01 (Complete - ครบทั้ง 10 Steps!)

```
┌──────────────────────────────────────────────────────────────┐
│                    📊 PART 01 STATISTICS                     │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  ✅ Steps สำเร็จ: 10/10 (100%)                              │
│  📄 จำนวนบรรทัด: ~3,900 บรรทัด                             │
│  💻 คำสั่ง curl ใช้งานได้จริง: 80+ คำสั่ง                  │
│  🎨 ไดอะแกรม Unicode Box: 30+ ไดอะแกรม                      │
│  🌐 Real APIs ทดสอบ: 6 APIs (JSONPlaceholder, GitHub,       │
│     httpbin.org, Dog API, และอื่นๆ)                         │
│  📝 แบบฝึกหัด: 30+ exercises พร้อมเฉลย                      │
│  🔧 เทคนิคขั้นสูง: JWT, ETag, HATEOAS, Caching Strategies   │
│  ⏱️  เวลาอ่าน: 4-6 ชั่วโมง                                 │
│  ⏱️  เวลาฝึกปฏิบัติ: 6-10 ชั่วโมง                          │
│                                                              │
│  📚 สรุปเนื้อหา:                                            │
│  • Step 01: HTTP Protocol พื้นฐาน                          │
│  • Step 02: HTTP Request Structure                          │
│  • Step 03: HTTP Response Structure                         │
│  • Step 04: HTTP Methods Deep Dive                          │
│  • Step 05: HTTP Status Codes (1xx-5xx)                     │
│  • Step 06: HTTP Headers Complete                           │
│  • Step 07: REST Architecture 6 Constraints                 │
│  • Step 08: Statelessness & Cacheability                    │
│  • Step 09: Uniform Interface 4 Principles                  │
│  • Step 10: HATEOAS & Layered System                        │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

## 🎓 สิ่งที่ได้เรียนรู้ใน PART 01

หลังจากจบ PART 01 นี้ คุณจะสามารถ:

```
✅ เข้าใจ HTTP Protocol อย่างละเอียด
✅ รู้จัก HTTP Request/Response Structure
✅ ใช้ HTTP Methods ได้อย่างถูกต้อง (GET, POST, PUT, PATCH, DELETE, HEAD, OPTIONS)
✅ เข้าใจ HTTP Status Codes ทั้ง 5 กลุ่ม (1xx-5xx)
✅ จัดการ HTTP Headers (Standard & Custom)
✅ เข้าใจ REST Architecture 6 Constraints
✅ ออกแบบ API แบบ Stateless ด้วย Token/JWT
✅ ใช้ Caching อย่างมีประสิทธิภาพ (Cache-Control, ETag)
✅ ออกแบบ Resource-Based URIs ตามหลัก Uniform Interface
✅ เข้าใจ HATEOAS และ Layered System Architecture
✅ ใช้ curl ทดสอบ API ได้อย่างเชี่ยวชาญ
✅ วิเคราะห์ Real-World APIs (GitHub, JSONPlaceholder)
```

## 🚀 เตรียมพร้อมสำหรับ PART 02

PART 02 จะครอบคลุม:
- REST Resource Modeling ขั้นสูง
- URI Design Patterns
- Content Negotiation
- Versioning Strategies
- Error Handling Standards
- Pagination, Filtering, Sorting
- Rate Limiting Implementation
- CORS และ Security Headers

---

<div align="center">

**[◀ กลับ Tutorial](TUTORIAL.md)** | **[▶ ไปต่อ PART 02](PART02.md)**

*PART 01 - HTTP & REST Fundamentals | สอน REST API แบบ Step-by-Step*

**🎉 ยินดีด้วย! คุณจบ PART 01 แล้ว! 🎉**

</div>
