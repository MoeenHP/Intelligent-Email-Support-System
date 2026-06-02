# Intelligent Email Support System | سیستم هوشمند پشتیبانی ایمیل

**Description | توضیحات پروژه:**  
This project is an end-to-end **Intelligent Email Support System** that automatically processes customer emails, detects requests, and generates coherent multi-department responses in Persian.  
این پروژه یک **سیستم هوشمند پشتیبانی ایمیل** است که ایمیل‌های مشتریان را پردازش کرده، درخواست‌ها را تشخیص داده و پاسخ‌های منسجم چند‌بخشی به زبان فارسی تولید می‌کند.

---

## Table of Contents | فهرست مطالب

1. [Overview | معرفی](#overview--معرفی)  
2. [Features | ویژگی‌ها](#features--ویژگی‌ها)  
3. [Architecture & Layers | معماری و لایه‌ها](#architecture--layers--معماری-و-لایه‌ها)  
4. [Installation | نصب](#installation--نصب)  
5. [Usage | نحوه استفاده](#usage--نحوه-استفاده)  
6. [File Structure | ساختار فایل‌ها](#file-structure--ساختار-فایل‌ها)  
7. [Testing | تست پروژه](#testing--تست-پروژه)  
8. [Example | مثال](#example--مثال)  
9. [Future Improvements | بهبودهای آینده](#future-improvements--بهبودهای-آینده)

---

## Overview | معرفی

**English:**  
The system automates customer support by:

- Preprocessing emails (normalization, tokenization).  
- Extracting entities like order IDs and product names.  
- Routing requests to the relevant department(s) using TF-IDF and cosine similarity.  
- Orchestrating tasks by calling internal tools (mock APIs for Sales, Technical, Finance).  
- Generating a unified, readable Persian email response.  
- Saving structured JSON output for logging and analytics.  

**فارسی:**  
این سیستم به صورت خودکار پشتیبانی مشتری را انجام می‌دهد:

- پیش‌پردازش ایمیل‌ها (نرمال‌سازی و توکن‌بندی).  
- استخراج موجودیت‌هایی مانند شماره سفارش و نام محصول.  
- هدایت درخواست‌ها به بخش‌های مرتبط با استفاده از TF-IDF و شباهت کسینوسی.  
- هماهنگی وظایف با فراخوانی ابزارهای داخلی (API شبیه‌سازی‌شده برای فروش، فنی و مالی).  
- تولید یک پاسخ منسجم و قابل خواندن به زبان فارسی.  
- ذخیره خروجی JSON ساختار یافته برای تحلیل و ثبت سوابق.  

---

## Features | ویژگی‌ها

- Multi-department support | پشتیبانی چندبخشی (فروش، فنی، مالی)  
- Entity recognition | شناسایی موجودیت‌ها (سفارش، محصول، نوع درخواست)  
- Intelligent routing | هدایت هوشمند درخواست‌ها  
- Mock API integration | شبیه‌سازی ابزارهای داخلی شرکت  
- Unified response generation | تولید پاسخ یکپارچه  
- JSON output | ذخیره خروجی به صورت JSON  
- CLI support | دریافت ایمیل از خط فرمان  
- Verbose debugging | نمایش مراحل پردازش و جزئیات  

---

## Architecture & Layers | معماری و لایه‌ها

The system is organized into **6 layers | سیستم شامل ۶ لایه می‌باشد**:

1. **Preprocessor | پیش‌پردازش:** Normalize, tokenize, remove stopwords | نرمال‌سازی، توکن‌بندی، حذف کلمات اضافه.  
2. **Router | هدایت:** TF-IDF + cosine similarity to determine relevant departments | هدایت به بخش‌های مرتبط.  
3. **Entity Extractor | استخراج موجودیت‌ها:** Regex for order numbers, products | استخراج شماره سفارش و نام محصول.  
4. **Orchestrator | هماهنگ‌کننده:** Build task plan and call tools | ساخت برنامه کاری و فراخوانی ابزارها.  
5. **Tools | ابزارها:** Mock APIs for Sales, Technical, Finance | API شبیه‌سازی‌شده برای بخش‌ها.  
6. **Response Generator | تولید پاسخ:** Combine results into a unified email and JSON output | ترکیب نتایج و تولید ایمیل و خروجی JSON.  

---

## Installation | نصب

1. Clone the repository | کلون کردن پروژه:

```bash
git clone https://github.com/yourusername/intelligent-email-support.git
cd intelligent-email-support
```

2. Install Python 3.10+ | نصب پایتون ۳.۱۰ یا بالاتر.

3. Run the system | اجرای پروژه:

```bash
python main.py
```

---

## Usage | نحوه استفاده

### Default sample email | اجرای ایمیل نمونه پیش‌فرض

```bash
python main.py
```

The system will process the built-in sample email and generate a response involving Sales, Technical Support, and Finance departments.

سیستم ایمیل نمونه داخلی را پردازش کرده و پاسخی شامل بخش‌های فروش، پشتیبانی فنی و مالی تولید می‌کند.

### Custom email via CLI | اجرای پروژه با ایمیل سفارشی

```bash
python main.py "Hello, my order 12345 has not arrived yet."
```

Example (Persian):

```bash
python main.py "سلام، سفارش شماره 12345 هنوز به دستم نرسیده است."
```

---

## Output | خروجی

After execution, the system produces:

پس از اجرا، سیستم موارد زیر را تولید می‌کند:

### 1. Final Email Response

Displayed in the terminal.

در ترمینال نمایش داده می‌شود.

### 2. JSON Output File

Saved automatically with a timestamp:

```text
output_YYYYMMDD_HHMMSS.json
```

Example:

```text
output_20260531_142530.json
```

---

## File Structure | ساختار فایل‌ها

```text
.
├── main.py
├── preprocessor.py
├── router.py
├── entity_extractor.py
├── orchestrator.py
├── tools.py
├── response_generator.py
├── README.md
└── output_*.json
```

### File Descriptions | توضیح فایل‌ها

| File | Description |
|--------|-------------|
| `main.py` | Entry point of the system |
| `preprocessor.py` | Text normalization, tokenization, stopword removal |
| `router.py` | TF-IDF and Cosine Similarity routing engine |
| `entity_extractor.py` | Entity extraction using regex and rule-based methods |
| `orchestrator.py` | Task planning and execution |
| `tools.py` | Mock APIs for Sales, Technical Support, and Finance |
| `response_generator.py` | Final response and JSON generation |

---

## Testing | تست پروژه

### Test 1 — Sales Department

```bash
python main.py "سلام، سفارش شماره 12345 هنوز به دستم نرسیده است."
```

Expected behavior:

- Detect order ID `12345`
- Route to Sales
- Call `get_order_status()`
- Generate order tracking response

---

### Test 2 — Technical Department

```bash
python main.py "لپتاپ X200 من روشن نمی‌شود."
```

Expected behavior:

- Detect product `X200`
- Route to Technical Support
- Call `get_product_info()`
- Generate technical information response

---

### Test 3 — Finance Department

```bash
python main.py "میخواهم درخواست استرداد وجه ثبت کنم."
```

Expected behavior:

- Detect refund request
- Route to Finance
- Call `get_refund_policy()`
- Generate refund policy response

---

### Test 4 — Multi-Department Email

```bash
python main.py "سفارش 78432 هنوز نرسیده، لپتاپ X200 مشکل دارد و میخواهم شرایط بازگشت وجه را بدانم."
```

Expected behavior:

- Route to Sales
- Route to Technical
- Route to Finance
- Execute all three tools
- Generate a unified response containing all three sections

---

### Test 5 — English Email

```bash
python main.py "My order 12345 has not arrived yet. I also need refund information."
```

Expected behavior:

- Detect order tracking request
- Detect refund request
- Route to Sales and Finance
- Generate combined response

---

## Processing Pipeline | جریان پردازش سیستم

```text
Customer Email
       │
       ▼
┌────────────────────┐
│ Layer 1            │
│ Preprocessor       │
└────────────────────┘
       │
       ▼
┌────────────────────┐
│ Layer 3            │
│ Entity Extractor   │
└────────────────────┘
       │
       ▼
┌────────────────────┐
│ Layer 2            │
│ Router             │
│ TF-IDF + Cosine    │
└────────────────────┘
       │
       ▼
┌────────────────────┐
│ Layer 4            │
│ Orchestrator       │
└────────────────────┘
       │
       ▼
┌────────────────────┐
│ Layer 5            │
│ Tools (Mock APIs)  │
└────────────────────┘
       │
       ▼
┌────────────────────┐
│ Layer 6            │
│ Response Generator │
└────────────────────┘
       │
       ▼
 Final JSON Output
```

---

## Example | مثال

### Input Email

```text
سلام،

سفارش شماره 78432 هنوز به دستم نرسیده است.
همچنین لپتاپ X200 من روشن نمی‌شود.
لطفاً شرایط بازگشت وجه را نیز توضیح دهید.
```

### Detected Entities

```json
{
  "order_ids": ["78432"],
  "product_names": ["لپتاپ X200", "X200"],
  "has_sales": true,
  "has_technical": true,
  "has_refund": true
}
```

### Routed Departments

```json
[
  "sales",
  "technical",
  "finance"
]
```

### Final Output

```json
{
  "original_text": "...",
  "processing_steps": [...],
  "final_response": "..."
}
```

---

## Future Improvements | توسعه‌های آینده

### Technical Improvements

- Add stemming and lemmatization
- Improve Persian NLP support
- Better product recognition
- More advanced intent detection
- Dynamic department configuration

### Infrastructure Improvements

- Replace mock APIs with real APIs
- Connect to SQL/NoSQL databases
- Add REST API endpoints
- Docker deployment
- Web dashboard for support agents

### Machine Learning Improvements

- Train a classifier for routing
- Named Entity Recognition (NER)
- Intent classification models
- Customer sentiment analysis

---

## Project Highlights | نکات برجسته پروژه

✅ Pure Python implementation (No external NLP libraries)

✅ TF-IDF implemented from scratch

✅ Cosine Similarity implemented from scratch

✅ Rule-based entity extraction

✅ Multi-department routing

✅ Task orchestration layer

✅ Structured JSON output

✅ Modular 6-layer architecture

✅ Persian and English language support

✅ Easy to extend and maintain

---

## Author

Developed as an educational project demonstrating:

- Natural Language Processing (NLP)
- Information Retrieval (TF-IDF)
- Cosine Similarity
- Rule-Based Entity Extraction
- Multi-Agent Task Orchestration
- Software Architecture Design

---

**Intelligent Email Support System**  
*An educational end-to-end customer support automation pipeline built entirely in Python.*
