Markdown
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
🚀 Getting Started
1. Clone the repository
Bash
git clone [https://github.com/YOUR_USERNAME/polish-jazz-data-analysis.git](https://github.com/YOUR_USERNAME/polish-jazz-data-analysis.git)
cd polish-jazz-data-analysis
2. Set up virtual environment & install dependencies
Bash
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate
pip install -r requirements.txt
(Create a requirements.txt containing: requests, pandas, matplotlib, seaborn)

3. Configure API Credentials
Get a free API key at Last.fm API and replace the placeholder in main.py:

Python
API_KEY = "YOUR_LASTFM_API_KEY"
4. Run the script
Bash
python main.py
The script will fetch live statistics from Last.fm, output a formatted summary to the console, and generate the comparative visualization.

🔮 Future Improvements
[ ] Fetch and parse specific track attributes (tempo, valence, acousticness) via the Spotify Web API.

[ ] Implement automated caching to reduce API overhead.

[ ] Build an interactive dashboard using Streamlit.
