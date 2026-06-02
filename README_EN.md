# Intelligent Email Support System

🌐 Language: English | [فارسی](README.md)

---

## Project Description

This project is an intelligent email support system that automatically processes customer emails, extracts important information, routes requests to the appropriate departments, and generates a unified response.

The system follows a modular 6-layer architecture consisting of:

- Text preprocessing
- Entity extraction
- Intelligent routing
- Task orchestration
- Mock APIs
- Response generation

---

## Features

- Multi-department support (Sales, Technical, Finance)
- Order ID extraction
- Product recognition
- TF-IDF implementation from scratch
- Cosine Similarity implementation from scratch
- Unified response generation
- JSON output generation
- Pure Python implementation (no external dependencies)

---

## System Architecture

The system consists of six layers:

### Layer 1 — Preprocessor

- Persian text normalization
- Tokenization
- Stopword removal

### Layer 2 — Router

- TF-IDF implementation from scratch
- Cosine Similarity implementation from scratch
- Department selection

### Layer 3 — Entity Extractor

Extracts:

- Order IDs
- Product names
- Refund requests
- Technical requests
- Sales/tracking requests

### Layer 4 — Orchestrator

- Task planning
- Tool execution management

### Layer 5 — Tools

Mock APIs:

- Order status lookup
- Product information lookup
- Refund policy lookup

### Layer 6 — Response Generator

- Unified response generation
- JSON output generation

---

## Installation

Clone the repository:

```bash
git clone https://github.com/USERNAME/intelligent-email-support-system.git
cd intelligent-email-support-system
```

Run the project:

```bash
python main.py
```

---

## Usage

### Run the default sample

```bash
python main.py
```

### Run with a custom email

```bash
python main.py "My order 12345 has not arrived yet."
```

---

## Testing

### Sales Department Test

```bash
python main.py "Order 12345 has not arrived yet."
```

### Technical Department Test

```bash
python main.py "My X200 laptop does not turn on."
```

### Finance Department Test

```bash
python main.py "I would like to request a refund."
```

### Multi-Department Test

```bash
python main.py "Order 78432 has not arrived, my X200 laptop has issues, and I need refund information."
```

---

## File Structure

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
└── README_EN.md
```

---

## Output

The system generates a JSON file with the following structure:

```json
{
  "original_text": "...",
  "processing_steps": [...],
  "final_response": "..."
}
```

---

## Future Improvements

- Real database integration
- Multi-language support
- Customer sentiment analysis
- Machine-learning-based routing

---

## Author

Educational project demonstrating:

- Natural Language Processing (NLP)
- TF-IDF
- Cosine Similarity
- Entity Extraction
- Task Orchestration
- Software Architecture Design
