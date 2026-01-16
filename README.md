<div align="center">

# 📚 GA-Project-BlogData

### *Blog Data Collection API + Data Structures & Algorithms Library*

[![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://mongodb.com)
[![Google API](https://img.shields.io/badge/Google_API-4285F4?style=for-the-badge&logo=google&logoColor=white)](https://developers.google.com)
[![DiffBot](https://img.shields.io/badge/DiffBot-FF6B35?style=for-the-badge&logo=data:image/svg+xml;base64,PHN...&logoColor=white)](https://diffbot.com)

---

**A dual-purpose repository containing a FastAPI-powered Blog Data Collection service and a comprehensive Data Structures & Algorithms (DSA) learning library.**

[Blog API](#-blog-data-collection) •
[DSA Library](#-dsa-library) •
[Quick Start](#-quick-start) •
[API Reference](#-api-reference)

</div>

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Blog Data Collection](#-blog-data-collection)
- [DSA Library](#-dsa-library)
- [Quick Start](#-quick-start)
- [API Reference](#-api-reference)
- [Project Structure](#-project-structure)
- [Configuration](#-configuration)
- [Contributing](#-contributing)

---

## 🎯 Overview

This repository contains two main components:

<table>
<tr>
<th width="50%">📰 Blog Data Collection</th>
<th width="50%">📐 DSA Library</th>
</tr>
<tr>
<td>

**FastAPI microservice for automated blog content extraction**

- 🔍 Search blogs via Google Custom Search
- 📄 Extract content using DiffBot API
- 💾 Store data in MongoDB
- 📊 Track API usage & billing
- ⚡ Async background processing

</td>
<td>

**Comprehensive DSA implementations in Python**

- 🔢 Sorting algorithms
- 🔎 Searching algorithms
- 📊 Data structures
- ➕ Mathematical algorithms
- 🔄 Recursion patterns

</td>
</tr>
</table>

---

## 📰 Blog Data Collection

### Architecture

```
┌─────────────────────────────────────────────────────────────────────────────────────────────┐
│                              BLOG DATA COLLECTION PIPELINE                                   │
├─────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                              │
│   ┌──────────────┐      ┌──────────────────┐      ┌──────────────┐      ┌──────────────┐    │
│   │              │      │                  │      │              │      │              │    │
│   │   Client     │ ───► │   FastAPI        │ ───► │   Google     │ ───► │   DiffBot    │    │
│   │   Request    │      │   Server         │      │   Custom     │      │   Article    │    │
│   │              │      │                  │      │   Search     │      │   API        │    │
│   └──────────────┘      └────────┬─────────┘      └──────────────┘      └──────┬───────┘    │
│                                  │                                             │            │
│                                  │                                             │            │
│                                  ▼                                             ▼            │
│                         ┌──────────────────┐                          ┌──────────────────┐  │
│                         │                  │                          │                  │  │
│                         │   Background     │ ◄────────────────────────│   Blog Content   │  │
│                         │   Task Queue     │                          │   Extraction     │  │
│                         │                  │                          │                  │  │
│                         └────────┬─────────┘                          └──────────────────┘  │
│                                  │                                                          │
│                                  ▼                                                          │
│                         ┌──────────────────┐                                                │
│                         │                  │                                                │
│                         │    MongoDB       │                                                │
│                         │    Database      │                                                │
│                         │                  │                                                │
│                         │  ┌────────────┐  │                                                │
│                         │  │  metadata  │  │  ← Task status & extracted URLs               │
│                         │  └────────────┘  │                                                │
│                         │  ┌────────────┐  │                                                │
│                         │  │  records   │  │  ← Blog content & sentiment data              │
│                         │  └────────────┘  │                                                │
│                         │                  │                                                │
│                         └──────────────────┘                                                │
│                                                                                              │
└─────────────────────────────────────────────────────────────────────────────────────────────┘
```

### Features

| Feature | Description |
|:--------|:------------|
| 🔍 **Keyword Search** | Search for blogs using keywords via Google Custom Search API |
| 📄 **Content Extraction** | Extract blog content, metadata, and sentiment using DiffBot |
| ⚡ **Async Processing** | Background task processing for non-blocking operations |
| 📊 **Task Tracking** | Track data collection progress through multiple phases |
| 💾 **MongoDB Storage** | Persistent storage for metadata and blog records |
| 📈 **Usage Monitoring** | Monitor DiffBot API credit usage and billing cycles |

### Data Collection Phases

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           TASK STATUS PROGRESSION                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐ │
│   │             │    │             │    │             │    │             │ │
│   │   Started   │ ─► │   Running   │ ─► │  Phase 1    │ ─► │  Phase 2    │ │
│   │             │    │   (URLs)    │    │  (Complete) │    │  (Extract)  │ │
│   │             │    │             │    │             │    │             │ │
│   └─────────────┘    └─────────────┘    └─────────────┘    └──────┬──────┘ │
│                                                                    │        │
│                                                                    ▼        │
│                                         ┌─────────────┐    ┌─────────────┐ │
│                                         │             │    │             │ │
│                                         │  Completed  │ ◄─ │  Phase 3    │ │
│                                         │      ✓      │    │  (Process)  │ │
│                                         │             │    │             │ │
│                                         └─────────────┘    └─────────────┘ │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Extracted Data Fields

| Category | Fields |
|:---------|:-------|
| **Content** | `text`, `type`, `humanLanguage` |
| **Metadata** | `siteName`, `pageUrl`, `icon`, `diffbotUri` |
| **Author** | `author`, `authorUrl`, `authors` |
| **Date** | `date`, `estimatedDate` |
| **Location** | `publisherRegion`, `publisherCountry` |
| **Classification** | `tags`, `categories` |
| **Media** | `images` |
| **Analysis** | `sentiment` (computed) |

---

## 📐 DSA Library

### Algorithm Categories

```
┌─────────────────────────────────────────────────────────────────────────────────────────────┐
│                        DATA STRUCTURES & ALGORITHMS LIBRARY                                  │
├─────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────────────────────┐   │
│   │                               📊 DATA STRUCTURES                                     │   │
│   ├─────────────────────────────────────────────────────────────────────────────────────┤   │
│   │                                                                                      │   │
│   │   ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐           │   │
│   │   │              │  │              │  │              │  │              │           │   │
│   │   │  Linked List │  │    Stack     │  │    Deque     │  │     Set      │           │   │
│   │   │              │  │  (LIFO)      │  │ (Double-end) │  │              │           │   │
│   │   └──────────────┘  └──────────────┘  └──────────────┘  └──────────────┘           │   │
│   │                                                                                      │   │
│   │   ┌──────────────┐  ┌──────────────┐                                                │   │
│   │   │              │  │              │                                                │   │
│   │   │     List     │  │  Dictionary  │                                                │   │
│   │   │              │  │              │                                                │   │
│   │   └──────────────┘  └──────────────┘                                                │   │
│   │                                                                                      │   │
│   └─────────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────────────────────┐   │
│   │                                 🔢 ALGORITHMS                                        │   │
│   ├─────────────────────────────────────────────────────────────────────────────────────┤   │
│   │                                                                                      │   │
│   │   ┌──────────────────────────────────┐  ┌──────────────────────────────────┐        │   │
│   │   │         SORTING                  │  │          SEARCHING               │        │   │
│   │   │                                  │  │                                  │        │   │
│   │   │   • Bubble Sort      O(n²)       │  │   • Linear Search    O(n)        │        │   │
│   │   │   • Selection Sort   O(n²)       │  │   • Binary Search    O(log n)    │        │   │
│   │   │   • Insertion Sort   O(n²)       │  │   • First Occurrence O(log n)    │        │   │
│   │   │   • Merge Sort       O(n log n)  │  │   • Last Occurrence  O(log n)    │        │   │
│   │   │                                  │  │   • Count Occurrence O(log n)    │        │   │
│   │   └──────────────────────────────────┘  └──────────────────────────────────┘        │   │
│   │                                                                                      │   │
│   │   ┌──────────────────────────────────┐  ┌──────────────────────────────────┐        │   │
│   │   │         MATHEMATICS              │  │         RECURSION                │        │   │
│   │   │                                  │  │                                  │        │   │
│   │   │   • Factorial                    │  │   • Basic Patterns               │        │   │
│   │   │   • GCD / LCM                    │  │   • Tail Recursion               │        │   │
│   │   │   • Prime Check                  │  │   • Tree Traversal               │        │   │
│   │   │   • Prime Factorization          │  │                                  │        │   │
│   │   │   • Sieve of Eratosthenes        │  │                                  │        │   │
│   │   │   • Trailing Zeros               │  │                                  │        │   │
│   │   │   • Palindrome Check             │  │                                  │        │   │
│   │   │   • Power Calculation            │  │                                  │        │   │
│   │   │   • Divisors Finding             │  │                                  │        │   │
│   │   │   • Digit Operations             │  │                                  │        │   │
│   │   │                                  │  │                                  │        │   │
│   │   └──────────────────────────────────┘  └──────────────────────────────────┘        │   │
│   │                                                                                      │   │
│   └─────────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                              │
└─────────────────────────────────────────────────────────────────────────────────────────────┘
```

### Algorithm Complexity Reference

#### Sorting Algorithms

| Algorithm | Best | Average | Worst | Space | Stable |
|:----------|:-----|:--------|:------|:------|:-------|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | ❌ |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | ✅ |

#### Searching Algorithms

| Algorithm | Best | Average | Worst | Space |
|:----------|:-----|:--------|:------|:------|
| Linear Search | O(1) | O(n) | O(n) | O(1) |
| Binary Search | O(1) | O(log n) | O(log n) | O(1) |
| Binary (Recursive) | O(1) | O(log n) | O(log n) | O(log n) |

### DSA Topics Covered

<details>
<summary><b>📂 Linked List</b></summary>

- Node class implementation
- Print list traversal
- Search element
- Insert at beginning O(1)
- Insert at end O(n)
- Insert at position
- Delete from beginning O(1)
- Delete from end O(n)

</details>

<details>
<summary><b>📂 Stack</b></summary>

- Stack implementation
- Balanced parenthesis checker
- Push/Pop operations

</details>

<details>
<summary><b>📂 Deque</b></summary>

- List-based implementation
- Double-linked list implementation
- Standard deque operations

</details>

<details>
<summary><b>📂 Mathematical Algorithms</b></summary>

- Factorial (iterative & recursive)
- GCD (Greatest Common Divisor)
- LCM (Least Common Multiple)
- Prime number check
- Prime factorization
- Sieve of Eratosthenes
- Trailing zeros in factorial
- Palindrome check
- Power calculation
- All divisors of a number
- Digit manipulation

</details>

<details>
<summary><b>📂 Sorting</b></summary>

- Bubble Sort with optimization
- Selection Sort
- Insertion Sort
- Merge Sort (divide & conquer)
- Union of sorted arrays
- Intersection of sorted arrays

</details>

<details>
<summary><b>📂 Searching</b></summary>

- Binary search (iterative)
- Binary search (recursive)
- First occurrence
- Last occurrence
- Count occurrences
- Count 1s in binary sorted array

</details>

---

## 🚀 Quick Start

### Prerequisites

- Python 3.9+
- MongoDB running locally
- Google Custom Search API key
- DiffBot API token

### Installation

```bash
# Clone the repository
git clone <repository-url>
cd GA-Project-BlogData

# Navigate to Blog Data Collection
cd Blog_Data_Collection

# Install dependencies
pip install -r requirments.txt
```

### Configuration

Create a `.env` file in `Blog_Data_Collection/`:

```env
GOOGLE_DEVELOPER_KEY=your_google_api_key
GOOGLE_CX_ID=your_custom_search_engine_id
DIFF_BOT_TOKEN=your_diffbot_token
```

### Running the API

```bash
# Start the FastAPI server
uvicorn main:app --reload

# Server runs at http://localhost:8000
# Swagger docs at http://localhost:8000/docs
```

### Running DSA Examples

```bash
# Navigate to DSA folder
cd DSA

# Run any algorithm file
python sorting/merge_sort.py
python searching/binary_search.py
python maths/prime.py
```

---

## 📡 API Reference

### Endpoints

| Method | Endpoint | Description |
|:-------|:---------|:------------|
| `GET` | `/api/v1/ping` | Health check |
| `POST` | `/api/v1/blog/task` | Create blog collection task |
| `GET` | `/api/v1/task/{task_id}` | Get task status |
| `GET` | `/api/v1/diffbot/monitor` | Monitor DiffBot usage |

### Create Blog Collection Task

**Request:**

```bash
curl -X POST "http://localhost:8000/api/v1/blog/task" \
  -H "Content-Type: application/json" \
  -d '{
    "search_term": ["python programming", "machine learning"],
    "message": "Collect ML blog posts",
    "start": 1
  }'
```

**Response:**

```json
{
  "data": {
    "task_id": "Ab3cD4e",
    "search_term": ["python programming", "machine learning"],
    "message": "Collect ML blog posts",
    "status": "Started",
    "_id": "507f1f77bcf86cd799439011"
  }
}
```

### Get Task Status

**Request:**

```bash
curl -X GET "http://localhost:8000/api/v1/task/Ab3cD4e"
```

**Response:**

```json
{
  "task_id": "Ab3cD4e",
  "search_term": ["python programming", "machine learning"],
  "message": "Collect ML blog posts",
  "status": "Blog data collection Completed",
  "extracted_URLs": [
    {"python programming": ["https://example1.com", "https://example2.com"]},
    {"machine learning": ["https://example3.com", "https://example4.com"]}
  ]
}
```

### Monitor DiffBot Usage

**Request:**

```bash
curl -X GET "http://localhost:8000/api/v1/diffbot/monitor"
```

**Response:**

```json
{
  "total_usage": 1500,
  "percentage": 15
}
```

---

## 📁 Project Structure

```
GA-Project-BlogData/
│
├── 📁 Blog_Data_Collection/            # FastAPI Blog Collection Service
│   │
│   ├── 📄 main.py                      # FastAPI application entry point
│   ├── 📄 requirments.txt              # Python dependencies
│   ├── 📄 run-command                  # Uvicorn run command
│   ├── 📄 README.md                    # Blog collection docs
│   │
│   └── 📁 src/
│       ├── 📁 controllers/             # API endpoints
│       │   ├── 📄 ping_controller.py           # Health check
│       │   ├── 📄 blog_data_controller.py      # Create collection task
│       │   ├── 📄 get_blog_data_controller.py  # Get task status
│       │   └── 📄 monitor_diffbot_controller.py # DiffBot usage
│       │
│       ├── 📁 models/
│       │   └── 📄 model.py             # Pydantic models & enums
│       │
│       └── 📁 service/
│           ├── 📄 blog_data_collection_service.py  # Core collection logic
│           ├── 📄 mongo_service.py                 # MongoDB operations
│           ├── 📄 data_object_converter.py         # Data transformation
│           └── 📄 logger_config.py                 # Logging configuration
│
├── 📁 DSA/                             # Data Structures & Algorithms
│   │
│   ├── 📄 main.py                      # Entry point
│   │
│   ├── 📁 sorting/                     # Sorting algorithms
│   │   ├── 📄 bubble_sort.py
│   │   ├── 📄 selection_sort.py
│   │   ├── 📄 insertion_sort.py
│   │   ├── 📄 merge_sort.py
│   │   └── 📄 sort.py
│   │
│   ├── 📁 searching/                   # Searching algorithms
│   │   ├── 📄 binary_search.py
│   │   └── 📄 search.py
│   │
│   ├── 📁 linked_list/
│   │   └── 📄 linked_list.py           # Singly linked list
│   │
│   ├── 📁 stack/
│   │   ├── 📄 stack.py
│   │   └── 📄 Balanced_parenthasis.py
│   │
│   ├── 📁 deque/
│   │   ├── 📄 deque.py
│   │   ├── 📄 list-imp-of-deque.py
│   │   └── 📄 Double-linked-list-of-deque.py
│   │
│   ├── 📁 list/
│   │   ├── 📄 list.py
│   │   └── 📄 max_min_sort.py
│   │
│   ├── 📁 dict/
│   │   └── 📄 dict.py
│   │
│   ├── 📁 set/
│   │   └── 📄 set.py
│   │
│   ├── 📁 strings/
│   │   └── 📄 strings.py
│   │
│   ├── 📁 recursion/
│   │   └── 📄 recursion.py
│   │
│   └── 📁 maths/                       # Mathematical algorithms
│       ├── 📄 factorial.py
│       ├── 📄 gcd.py
│       ├── 📄 lcm.py
│       ├── 📄 prime.py
│       ├── 📄 primefactorization.py
│       ├── 📄 sieve of eratosthenes.py
│       ├── 📄 palindrome.py
│       ├── 📄 power.py
│       ├── 📄 alldivisorofnumber.py
│       ├── 📄 digits.py
│       ├── 📄 TrailingZeros.py
│       └── 📄 sum.py
│
└── 📄 README.md                        # This file
```

---

## ⚙️ Configuration

### Environment Variables

| Variable | Description | Required |
|:---------|:------------|:---------|
| `GOOGLE_DEVELOPER_KEY` | Google Custom Search API key | ✅ |
| `GOOGLE_CX_ID` | Custom Search Engine ID | ✅ |
| `DIFF_BOT_TOKEN` | DiffBot API token | ✅ |

### MongoDB Configuration

Default connection: `mongodb://localhost:27017/`

**Collections:**
- `blogs.metadata` - Task metadata and status
- `blogs.records` - Extracted blog content

### Getting API Keys

1. **Google Custom Search API:**
   - Go to [Google Cloud Console](https://console.cloud.google.com/)
   - Enable Custom Search API
   - Create credentials (API Key)
   - Create Custom Search Engine at [cse.google.com](https://cse.google.com/)

2. **DiffBot API:**
   - Sign up at [diffbot.com](https://www.diffbot.com/)
   - Get your API token from dashboard

---

## 🛡️ Error Handling

| Error | Status Code | Description |
|:------|:------------|:------------|
| Missing API Keys | `500` | Server not configured with API keys |
| Task Not Found | `404` | No blog data found for task ID |
| DiffBot Limit Exceeded | `400` | API credit limit reached |
| Request Failed | `500` | External API request failed |

---

## 📊 Usage Monitoring

The DiffBot monitor endpoint tracks:
- **Total Usage**: Credits used in current billing cycle
- **Percentage**: Percentage of plan credits used
- **Billing Cycle**: Resets on the 8th of each month

```bash
# Check current usage
curl http://localhost:8000/api/v1/diffbot/monitor

# Response: {"total_usage": 1500, "percentage": 15}
```

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

---

<div align="center">

## 🔗 Quick Links

| Resource | Link |
|:---------|:-----|
| 📚 **FastAPI Docs** | [fastapi.tiangolo.com](https://fastapi.tiangolo.com) |
| 🔍 **Google Custom Search** | [developers.google.com](https://developers.google.com/custom-search) |
| 📰 **DiffBot API** | [diffbot.com](https://www.diffbot.com/dev/docs/) |
| 🍃 **MongoDB** | [mongodb.com](https://www.mongodb.com/docs/) |

---

**Built with ❤️ using FastAPI, MongoDB, and Python**

⭐ Star this repo if you find it useful!

</div>
