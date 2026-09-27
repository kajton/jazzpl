import time
import matplotlib.pyplot as plt
import pandas as pd
import requests
import seaborn as sns

API_KEY = "01e3fea7e1bc7478cdfce453f314683b"
URL = "https://ws.audioscrobbler.com/2.0/"

# Zdefiniowana kohorta polskich artystów jazzowych z podziałem na ery
ARTISTS_DATA = {
    # Klasyczna Polska Szkoła Jazzu
    "Krzysztof Komeda": "Polska Szkoła Jazzu",
    "Tomasz Stańko": "Polska Szkoła Jazzu",
    "Michał Urbaniak": "Polska Szkoła Jazzu",
    "Zbigniew Namysłowski": "Polska Szkoła Jazzu",
    "Andrzej Kurylewicz": "Polska Szkoła Jazzu",
    "Jan Ptaszyn Wróblewski": "Polska Szkoła Jazzu",
    # Nowa Fala / Współczesny Jazz
    "Leszek Możdżer": "Współczesny / Nowa Fala",
    "Wojtek Mazolewski Quintet": "Współczesny / Nowa Fala",
    "EABS": "Współczesny / Nowa Fala",
    "Błoto": "Współczesny / Nowa Fala",
    "Niechęć": "Współczesny / Nowa Fala",
    "Immortal Onion": "Współczesny / Nowa Fala",
}

records = []
print("Pobieram dane o polskich artystach jazzowych...")

for artist, era in ARTISTS_DATA.items():
    params = {
        "method": "artist.getinfo",
        "artist": artist,
        "api_key": API_KEY,
        "format": "json",
    }

    res = requests.get(URL, params=params).json()
    stats = res.get("artist", {}).get("stats", {})

    listeners = int(stats.get("listeners", 0))
    playcount = int(stats.get("playcount", 0))

    # Obliczenie metryki zaangażowania: średnia liczba odtworzeń na słuchacza
    scrobbles_per_listener = (
        round(playcount / listeners, 2) if listeners > 0 else 0
    )

    records.append(
        {
            "Artysta": artist,
            "Era": era,
            "Sluchacze_tys": listeners / 1_000,
            "Odtworzenia_tys": playcount / 1_000,
            "Lojalnosc": scrobbles_per_listener,
        }
    )
    print(
        f"✓ {artist} ({era}): {listeners:,} słuchaczy | wierność: {scrobbles_per_listener}x"
    )
    time.sleep(0.15)

df = pd.DataFrame(records)

# ==========================================
# WIZUALIZACJA: 2 Wykresy (Zasięg vs Zaangażowanie)
# ==========================================
sns.set_theme(style="whitegrid")
fig, axes = plt.subplots(1, 2, figsize=(14, 6), sharey=True)

# 1. Wykres: Ogólna liczba słuchaczy
sns.barplot(
    data=df,
    x="Sluchacze_tys",
    y="Artysta",
    hue="Era",
    palette={"Polska Szkoła Jazzu": "#1f77b4", "Współczesny / Nowa Fala": "#ff7f0e"},
    ax=axes[0],
    dodge=False,
)
axes[0].set_title("Zasięg: Liczba słuchaczy (w tysiącach)", weight="bold", pad=12)
axes[0].set_xlabel("Liczba słuchaczy (K)")
axes[0].set_ylabel("")

# 2. Wykres: Wskaźnik wierności fanów
sns.barplot(
    data=df,
    x="Lojalnosc",
    y="Artysta",
    hue="Era",
    palette={"Polska Szkoła Jazzu": "#1f77b4", "Współczesny / Nowa Fala": "#ff7f0e"},
    ax=axes[1],
    dodge=False,
)
axes[1].set_title(
    "Zaangażowanie: Średnia liczba odtworzeń na 1 słuchacza",
    weight="bold",
    pad=12,
)
axes[1].set_xlabel("Odtworzenia / słuchacz")
axes[1].set_ylabel("")

# Dodanie pionowej linii średniej dla zaangażowania
srednia_lojalnosc = df["Lojalnosc"].mean()
axes[1].axvline(
    srednia_lojalnosc,
    color="gray",
    linestyle="--",
    alpha=0.7,
    label=f"Średnia ({srednia_lojalnosc:.1f}x)",
)
axes[1].legend(loc="lower right")

plt.tight_layout()
plt.show()
