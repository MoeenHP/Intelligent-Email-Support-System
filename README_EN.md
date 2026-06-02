# Intelligent Email Support System

🌐 Language: English | [Persian](README_EN.md)

An intelligent system for analyzing, routing, and automatically responding to customer support emails.

---

## Table of Contents

* [Project Overview](#project-overview)
* [How to Run](#how-to-run)
* [System Architecture](#system-architecture)
* [Layer Descriptions](#layer-descriptions)
* [Design Patterns](#design-patterns)
* [Output Structure](#output-structure)
* [Technologies Used](#technologies-used)

---

## Project Overview

This system receives a raw customer email and intelligently:

1. Identifies the customer's requests.
2. Determines which departments (Sales, Technical Support, Finance) should respond.
3. Collects the required information from internal services.
4. Generates a unified and professional response email.

### Key Features

* Fully offline — no internet connection or external APIs required.
* TF-IDF and Cosine Similarity implemented completely from scratch.
* Supports both Persian and English text.
* Produces structured JSON output.
* Modular six-layer architecture.
* No external Python libraries required.

---

## How to Run

### Prerequisites

* Python 3.7 or higher
* No third-party libraries required (Standard Library only)

### Installation & Execution

```bash
# Clone the repository
git clone https://github.com/your-username/email-support-system.git

cd email-support-system

# Run with the built-in sample email
python main.py

# Run with a custom email
python main.py "Hello, my order 12345 has not arrived and my X200 laptop has a technical issue."
```

### Testing Individual Layers

Each layer can be tested independently:

```bash
python preprocessor.py
python router.py
python entity_extractor.py
python orchestrator.py
python tools.py
python response_generator.py
```

### Project Structure

```text
email-support-system/
├── main.py
├── preprocessor.py
├── router.py
├── entity_extractor.py
├── orchestrator.py
├── tools.py
├── response_generator.py
└── README.md
```

---

## System Architecture

### High-Level Architecture

```text
Raw Customer Email
        │
        ▼
┌─────────────────────────────┐
│ Layer 1: Preprocessor       │
│ - Normalization             │
│ - Tokenization              │
│ - Stopword Removal          │
└─────────────┬───────────────┘
              │
              ▼
┌─────────────────────────────┐
│ Layer 3: Entity Extractor   │
│ - Order IDs                 │
│ - Product Names             │
│ - Refund Signals            │
└─────────────┬───────────────┘
              │
              ▼
┌─────────────────────────────┐
│ Layer 2: Router             │
│ - TF-IDF                    │
│ - Cosine Similarity         │
│ - Department Matching       │
└─────────────┬───────────────┘
              │
              ▼
┌─────────────────────────────┐
│ Layer 4: Orchestrator       │
│ - Task Planning             │
│ - Tool Invocation           │
│ - Audit Trail Generation    │
└─────────────┬───────────────┘
              │
              ▼
┌─────────────────────────────┐
│ Layer 5: Mock APIs          │
│ - Order Service             │
│ - Product Service           │
│ - Refund Service            │
└─────────────┬───────────────┘
              │
              ▼
┌─────────────────────────────┐
│ Layer 6: Response Generator │
│ - Template Engine           │
│ - Unified Email Builder     │
│ - JSON Output Generator     │
└─────────────┬───────────────┘
              │
              ▼
        Final JSON Output
```

### Data Flow

```text
Email Text
    │
    ▼
preprocessor.preprocess()
    │
    ├── normalized text
    └── clean_tokens
             │
             ├──► entity_extractor.extract_entities()
             │         └── entities
             │
             └──► router.route_email()
                       └── departments
                               │
                               ▼
                    orchestrator.orchestrate()
                               │
                               ▼
                response_generator.build_final_output()
                               │
                               ▼
                          JSON Output
```

---

## Layer Descriptions

### Layer 1 — Preprocessor (`preprocessor.py`)

Prepares raw email text for processing.

| Step             | Description                                    |
| ---------------- | ---------------------------------------------- |
| Normalization    | Standardizes Persian/Arabic character variants |
| Lowercasing      | Converts English characters to lowercase       |
| Tokenization     | Splits text into words                         |
| Stopword Removal | Removes common non-informative words           |

Example:

```text
Input:
"سلام، سفارش X200 دارم."

Output Tokens:
["سفارش", "x200"]
```

---

### Layer 2 — Router (`router.py`)

The intelligent core of the system.

Implements two classic NLP algorithms entirely from scratch:

#### TF-IDF

```text
TF(term, doc)  = term count / total terms
IDF(term)      = log(total docs / docs containing term)
TF-IDF         = TF × IDF
```

#### Cosine Similarity

```text
similarity(A,B) = (A · B) / (|A| × |B|)
```

Each department has a predefined keyword profile. The router compares the email against these profiles and selects departments whose similarity exceeds a threshold.

Departments:

* Sales
* Technical Support
* Finance

---

### Layer 3 — Entity Extractor (`entity_extractor.py`)

Uses regex patterns and rule-based matching to extract structured information.

Extracted entities include:

#### Order IDs

Examples:

```text
Order #12345
Tracking: 987654
```

#### Product Names

Examples:

```text
Laptop X200
Phone S10
```

#### Refund Signals

Examples:

```text
refund
return
cancel order
بازگشت وجه
استرداد
```

#### Technical Signals

Examples:

```text
error
bug
technical issue
خرابی
مشکل فنی
```

---

### Layer 4 — Orchestrator (`orchestrator.py`)

Acts as the decision-making brain of the system.

Responsibilities:

1. Build a task plan.
2. Determine which tools should be called.
3. Execute tasks in the correct order.
4. Generate a complete audit trail.

Example task plan:

```text
Sales      → get_order_status(12345)
Technical  → get_product_info(X200)
Finance    → get_refund_policy()
```

---

### Layer 5 — Tools (`tools.py`)

Simulates internal company services through mock APIs.

| Function            | Input        | Output                   |
| ------------------- | ------------ | ------------------------ |
| get_order_status()  | Order ID     | Status, tracking code    |
| get_product_info()  | Product Name | Technical specifications |
| get_refund_policy() | None         | Refund policy text       |

These APIs are intentionally mocked so the project remains fully offline.

---

### Layer 6 — Response Generator (`response_generator.py`)

Builds the final customer response.

Features:

* Custom template engine.
* Department-specific response sections.
* Unified email assembly.
* JSON output generation.

Example:

```text
Sales Response
+
Technical Response
+
Finance Response
=
Final Customer Email
```

---

## Design Patterns

### 1. Pipeline Pattern

Each layer performs one transformation and passes its output to the next layer.

Benefits:

* Modularity
* Testability
* Maintainability

---

### 2. Strategy Pattern

Used in `response_generator.py`.

Department names are mapped to dedicated section-builder functions:

```python
SECTION_BUILDERS = {
    "sales": build_sales_section,
    "technical": build_technical_section,
    "finance": build_finance_section
}
```

New departments can be added without modifying the core logic.

---

### 3. Dispatcher Pattern

Implemented in:

```python
call_tool()
```

The orchestrator interacts only with the dispatcher instead of calling APIs directly.

---

### 4. Fallback Pattern

Implemented in `router.py`.

If TF-IDF routing fails to identify a department, entity extraction signals are used as a fallback mechanism.

This improves robustness for short or unusual emails.

---

## Output Structure

The final output is a JSON file containing three sections:

```json
{
  "original_text": "...",

  "processing_steps": [
    {
      "step": 1,
      "action": "Entity Extraction"
    },
    {
      "step": 2,
      "action": "Department Routing"
    }
  ],

  "final_response": "Generated email response..."
}
```

### Fields

#### original_text

The customer's original email.

#### processing_steps

Complete audit trail of all system decisions and actions.

#### final_response

The final email sent back to the customer.

---

## Technologies Used

| Technology            | Purpose                                   |
| --------------------- | ----------------------------------------- |
| Python 3              | Core programming language                 |
| re                    | Regex-based entity extraction             |
| math                  | TF-IDF and Cosine Similarity calculations |
| json                  | JSON output generation                    |
| Standard Library Only | No external dependencies                  |

---

## Authors

Student Project
Hamrah First Academy
Artificial Intelligence Track — Group 2
