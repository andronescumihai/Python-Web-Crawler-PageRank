# 🕸️ Web Crawler & PageRank Analyzer

> **Python for Everybody — University of Michigan** | BeautifulSoup, SQLite, PageRank Algorithm, D3.js

---

## 📌 Project Overview

A **4-stage web search engine simulator** that crawls a target domain, builds a directed link graph, computes **PageRank scores** through iterative convergence, and renders the result as an interactive **D3.js force-directed network graph**. The system mirrors the core architecture behind Google's original ranking algorithm — applied to any crawlable website.

Built as part of the *Python for Everybody* specialization (University of Michigan / Coursera).

---

## ✨ Key Features

| Feature | Implementation |
|---|---|
| 🕷️ **Incremental Web Crawler** | `spider.py` — BFS crawl using BeautifulSoup, stores HTML + links in SQLite, resumes from last checkpoint |
| 🔗 **Link Graph Storage** | `Pages(id, url, html, error, old_rank, new_rank)` + `Links(from_id, to_id)` + `Webs(url)` |
| 📐 **PageRank Algorithm** | `sprank.py` — iterative rank propagation over strongly connected component (SCC), evaporation redistribution, convergence tracking |
| 📤 **JSON Export** | `spjason.py` — exports nodes (with normalized rank 0–19) + edges as `spiderJson` for D3 consumption |
| 🌐 **Force-directed Graph** | `force.html` + `spider.js` — interactive D3.js network where node size = PageRank, edges = hyperlinks |
| 🔍 **Diagnostic Tool** | `spdump.py` — ranks pages by inbound link count, shows old vs new rank convergence |

---

## 🛠️ Tech Stack

- **Language:** Python 3.x (`urllib`, `ssl`, `BeautifulSoup`, `sqlite3`)
- **Database:** SQLite3 — 3 tables: `Pages`, `Links`, `Webs`
- **Algorithm:** PageRank with rank evaporation + redistribution (handles dangling nodes)
- **Visualization:** D3.js force-directed graph (`force.html`)
- **Course:** Python for Everybody — University of Michigan (Coursera)

---

## 🗄️ Database Schema

```sql
CREATE TABLE Pages (
    id       INTEGER PRIMARY KEY,
    url      TEXT UNIQUE,
    html     TEXT,
    error    INTEGER,
    old_rank REAL,
    new_rank REAL         -- initialized to 1.0 per page
);

CREATE TABLE Links (
    from_id  INTEGER,
    to_id    INTEGER,
    UNIQUE(from_id, to_id)
);

CREATE TABLE Webs (url TEXT UNIQUE);  -- domain scope filter
```

---

## 📁 Repository Structure

```
├── spider.py       # Stage 1: Crawl domain → Pages + Links tables
├── sprank.py       # Stage 2: Iterative PageRank computation
├── spdump.py       # Stage 3 (optional): Console rank diagnostics
├── spjason.py      # Stage 4: Export to spider.js for visualization
├── force.html      # D3.js force-directed network graph
├── spider.js       # Generated: nodes + links JSON for D3
└── spider.sqlite   # Generated: crawl database
```

---

## ⚙️ How the PageRank Works

```python
# Each iteration:
for node in from_ids:
    amount = old_rank[node] / len(outbound_links[node])
    for target in outbound_links[node]:
        next_ranks[target] += amount

# Evaporation: redistribute rank lost to dangling nodes
evap = (total - newtot) / len(next_ranks)
for node in next_ranks:
    next_ranks[node] += evap

# Convergence check: average absolute rank change per node
avediff = sum(|old - new| for all nodes) / count
```

Convergence is printed at each iteration — run until `avediff` stabilizes near zero.

---

## ▶️ How to Run

```bash
# Stage 1: Crawl a website (enter URL + number of pages when prompted)
python3 spider.py

# Stage 2: Compute PageRank (enter number of iterations, e.g. 10-50)
python3 sprank.py

# Stage 3 (optional): View ranked pages in console
python3 spdump.py

# Stage 4: Export to JSON for visualization
python3 spjason.py

# Open visualization
open force.html   # macOS
# or double-click force.html on Windows/Linux
```

---

## 🧠 What I Learned

- Implementing **BFS web crawling** with domain scoping, error handling, and resumable state via SQLite
- Building and querying a **directed link graph** using relational tables
- Implementing the **PageRank algorithm** from scratch — rank propagation, evaporation for dangling nodes, convergence detection
- **Normalizing scores** to a fixed range (0–19) for visual encoding in D3.js
- Connecting a Python data pipeline to a **D3.js force-directed graph** via file-based JSON export

---

## 📜 Context

Part of the **Python for Everybody** specialization by Dr. Charles Severance (University of Michigan). The PageRank implementation directly mirrors Google's original 1998 algorithm — understanding it from first principles is a core skill for anyone working in data science, information retrieval, or graph analytics.

---

## 👤 Author

**Mihai-Alexandru Andronescu**
Student — Computer Science & Economics, ASE Bucharest

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://www.linkedin.com/in/mihai-alexandru-andronescu-58792b33b/)
[![GitHub](https://img.shields.io/badge/GitHub-Profile-black?logo=github)](https://github.com/andronescumihai)
