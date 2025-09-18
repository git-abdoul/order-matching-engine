# Intraday Trade Matching & Slippage Analysis

---

## 📈 Scenario

You are given two real-time event streams from an equity trading system:

### 1. Orders (placed by the trading desk)
```json
{"order_id": 101, "symbol": "AAPL", "side": "BUY", "qty": 500, "limit_px": 190.25, "ts": 1712345678.1}
```
- **Side** ∈ {“BUY”,“SELL”}
- **Limit price** (order is valid only if filled at or better than this)

### 2. Market trades (tape feed of all market executions)
```json
{"symbol": "AAPL", "px": 190.10, "qty": 100, "ts": 1712345678.3}
```

---

## 🛠️ Task

Build an in-memory matching engine to simulate how much of each order gets filled, and then compute the slippage vs. the order’s limit price.

---

## ✅ Requirements

1. **Maintain all active orders** in a suitable data structure for fast matching against trades.
    - Assume FIFO priority for equal prices.
    - Orders can be partially filled and remain live until qty=0.
2. **As market trades arrive:**
    - Match them against eligible orders (respecting limit price and side).
    - Allocate fills in timestamp order of orders.
    - Update order’s filled qty and compute realized PnL contribution.
3. **At any time, support queries:**
    - `get_open_orders(symbol)` → list of remaining qty per order
    - `get_filled(order_id)` → total filled qty and avg fill price
    - `get_slippage(order_id)` → realized avg fill price − limit price (sign adjusted for side)
4. **Efficiency matters:** design so that per-trade matching is O(log N) or better on average, not O(N).

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

> ⚡️ *Design for speed, clarity, and robust analysis. Make your matching engine efficient and insightful!*
