# order-matching-engine

---

## 🚀 Intraday Trade Matching & Slippage Analysis

A Python application for simulating real-time order matching and slippage analysis in equity trading. Designed for speed, clarity, and robust analytics.

---

## 📦 App Structure

```
order-matching-engine/
├── README.md
├── intraday_trade_matching.md
├── engine/           # Core matching engine logic
│   ├── __init__.py
│   └── matcher.py    # Matching algorithm implementation
├── tests/            # Unit and integration tests
│   └── test_matcher.py
└── scripts/          # CLI and utility scripts
	 └── run_engine.py
```

---

## 🛠️ Features
- Fast in-memory matching of orders and market trades
- FIFO priority for equal prices
- Partial fills supported
- Real-time queries:
  - `get_open_orders(symbol)`
  - `get_filled(order_id)`
  - `get_slippage(order_id)`
- Efficient: O(log N) matching per trade

---

## ⚙️ Deployment

1. **Clone the repository:**
	```sh
	git clone https://github.com/git-abdoul/order-matching-engine.git
	cd order-matching-engine
	```
2. **Set up a Python environment and install dependencies:**
	```sh
	python3 -m venv venv
	source venv/bin/activate
	pip install --upgrade pip
	pip install -r requirements.txt
	```
	This will install all required libraries: numpy, pandas, pytest, flake8, black.
3. **Run the engine:**
	```sh
	python scripts/run_engine.py
	```

---

## 🧑‍💻 Development Setup

1. **Create and activate a virtual environment:**
	```sh
	python3 -m venv venv
	source venv/bin/activate
	```
2. **Install development dependencies:**
	```sh
	pip install -r requirements.txt
	pip install -r dev-requirements.txt  # For testing, linting
	```
3. **Run tests:**
	```sh
	pytest tests/
	```
4. **Lint and format code:**
	```sh
	flake8 engine/
	black engine/
	```

---

## 📚 How to Use

- Place orders and stream market trades using the provided API or CLI.
- Query open orders, filled quantities, and slippage in real time.
- See `intraday_trade_matching.md` for scenario details and requirements.

---

## 💡 Example

- **Order:** BUY 500 AAPL @190.25
- **Tape prints:**
	 - AAPL 190.10 x100 → fills 100 (ok, <= 190.25)
	 - AAPL 190.20 x250 → fills 250 (ok, <= 190.25)
	 - AAPL 190.40 x200 → ignored (price too high)

**Open qty** = 150 left.  
**Filled qty** = 350.  
**Avg fill price** = (100×190.10 + 250×190.20)/350 = 190.17.  
**Slippage** = 190.17 − 190.25 = −0.08 (better fill).

---

> ⚡️ *Build, test, and deploy your matching engine for high-performance trading analytics!*