# 🕸️ Web Crawler & PageRank Analyzer

### 🎓 Academic Project - Data Mining & Web Exploration
**Developed by Mihai-Alexandru Andronescu**

---

## 🚀 Overview
This project implements a multi-stage web search engine simulator. It starts with a **Web Crawler** that traverses a given domain, mapping out its structure, followed by an implementation of the **PageRank algorithm** to calculate the relative importance of each page based on its inbound and outbound links.

## ✨ Key Features
* **Automated Web Crawling:** Efficiently crawls web pages and stores content/links in a relational database.
* **SQLite Integration:** Uses a robust database schema to manage crawling progress, errors, and link associations.
* **PageRank Computation:** Iterative implementation of the PageRank algorithm to simulate search engine authority scores.
* **Interactive Visualization:** Includes a **D3.js force-directed graph** (`force.html`) to visually explore the connections and hierarchy between crawled web pages.
* **Data Export & Visualization:** Converts complex link databases into JSON/JS formats for web-based graph visualizations.

## 🛠 Tech Stack
* **Language:** Python
* **Database:** SQLite3
* **Libraries:** `urllib`, `ssl`, `BeautifulSoup` (for HTML parsing).
* **Visualization:** JavaScript / JSON.

## 📂 Project Structure
* `spider.py`: The crawler engine that populates the database.
* `sprank.py`: Calculates ranking through multiple iterations.
* `spjason.py`: Exports data for visual representation.
* `spdump.py`: Diagnostic tool for database integrity checks.

## 🚦 How to Run
1. Run `spider.py` to start crawling a website.
2. Run `sprank.py` to compute the PageRank (specify the number of iterations).
3. (Optional) Run `spdump.py` to view current rankings in the console.
4. Run `spjason.py` to generate visualization files.

---
*Developed as part of my advanced Python and Data Science learning path, aiming for a Master's degree at TU Wien.*
