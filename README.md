# Xianyu Second-Hand Price & Decision Engine

# It's a half-finished software, I use it to practice, and by 2027 I will integrate AI for automatic analysis to make it more powerful

A pure Windows + Python + FastAPI + SQLite project for analyzing second-hand goods on Xianyu.

## Current Capabilities

- Structured parsing of Xianyu search results: item ID, title, price, images, region, seller, tags, links, etc.
- Automatic matching of CPU / GPU / phone / SoC models
- Automatic storage of search results into the database with model match scoring
- P10 / P25 / median / P75 / P90 price statistics
- Intelligent product analysis, price, match score, and risk ranking
- Four hardware reference databases: CPU / GPU / Phone / SoC
- Product detail pages, decision assistant, favorites / historical price fields
- Resale / bargain-hunting analysis endpoints
- Structured support for seller information, positive feedback rate, repair / condition, and other risk fields
- Pure Windows + FastAPI + SQLite, no Docker dependency

## Windows Startup

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
$env:XIANYU_COOKIE="your Xianyu cookie"
python -m uvicorn app.main:app --host 127.0.0.1 --port 8000 --reload
```

Open `http://127.0.0.1:8000/`, or run `run.bat` directly.

## API

```text
GET /api/health
GET /api/search?keyword=iPhone%2015&page=1
GET /api/product/{item_id}
GET /api/recommendations
GET /api/market/stats
GET /api/market/listings
GET /api/reseller/deals
```

## Decision Logic

Price, model match, performance reference, seller information, and product risk are all treated as explainable fields.

Risk signals may include: insufficient model match, price deviation from the sample, missing seller information, abnormal positive feedback rate / review sample, screen replacement / non-original screen / screen issues, rental / leasing descriptions, as well as hardware risks such as ES/QS, platform compatibility, power consumption, and cooling.

These signals are used for ranking and alerts, and do not constitute a factual determination about the product or seller.

## Database

- `cpu.db`: CPU specs, performance, second-hand price reference, risk
- `gpu.db`: GPU specs, performance, second-hand price reference, risk
- `phone.db`: Phone specs, performance, risk
- `soc.db`: SoC specs, performance, risk
- `xianyu_market.db`: searched products, price history, favorites, and statistics

Market prices are reference data and do not equal real-time transaction prices.

## Cookie and Risk Control

Do not commit cookies, tokens, signs, or other session credentials to Git.

The project does not aim to bypass access controls. When using data collection features, please comply with the relevant platform terms, applicable laws, and data usage restrictions, and do not publicly disclose other people's private information.

## GitHub

https://github.com/mynameisz-max/xianyu-price-decision-engine
