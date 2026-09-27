# 🎷 Polish Jazz Scene Analysis: Classics vs. The New Wave

An exploratory data analysis (EDA) project examining listener reach and fan loyalty across generations of Polish jazz artists using the **Last.fm REST API**.

![Project Visualization](charts/polish_jazz_comparison.png)

---

## 📌 Motivation & Research Questions

Polish jazz has a rich heritage—from the internationally acclaimed *Polish Film School* soundtracks of the 1960s to today's vibrant fusion and hip-hop-influenced scene.

This project investigates two core questions:
1. **Reach:** Do legendary figures (*Polish Jazz School*) continue to dominate the global listener base over contemporary outfits?
2. **Engagement:** Does the contemporary "New Wave" scene demonstrate higher listener loyalty (scrobbles per listener) despite a smaller overall audience?

---

## 📊 Key Findings

* **Reach Advantage:** Heritage artists (e.g., Krzysztof Komeda, Tomasz Stańko) lead in raw listener counts, driven largely by editorial playlists, film scoring, and historic international recognition.
* **The "Cult Following" Effect:** Modern bands (such as Błoto, Niechęć, and EABS) demonstrate a notably higher **loyalty ratio** ($\frac{\text{Playcount}}{\text{Listeners}}$). While their listener base is smaller, fans listen through entire discographies repeatedly.

---

## 🛠️ Tech Stack & Methods

* **Language:** Python 3.10+
* **Data Ingestion:** REST API requests via `requests`
* **Data Processing:** `pandas`
* **Data Visualization:** `seaborn`, `matplotlib`
* **Core Metrics:**
  * **Reach:** Total unique listeners ($N_{listeners}$)
  * **Engagement / Loyalty Index:** $\text{Loyalty} = \frac{\text{Total Scrobbles}}{\text{Total Listeners}}$

---

## 📁 Project Structure

```text
├── charts/
│   └── polish_jazz_comparison.png   # Generated visualization plot
├── data/
│   └── jazz_stats.csv               # Exported dataset snapshot (optional)
├── main.py                          # Data fetching and plotting script
├── requirements.txt                 # Project dependencies
└── README.md                        # Documentation
