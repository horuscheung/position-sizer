# Position Sizer

Free lot-size calculator for forex, gold, indices and crypto CFDs. Single static page — no build, no dependencies, no sign-up.

**Live: https://horuscheung.github.io/position-sizer/**

## Usage

Use the hosted page above, or open `index.html` directly in a browser.

## Inputs

- **Account**: currency (USD/HKD), balance, risk per trade (% of balance or fixed amount).
- **Market**: preset instruments (FX majors/crosses, XAUUSD, HK50, US indices, BTC/ETH) or `CUSTOM` with editable contract size + quote currency.
- **Prices**: entry and stop loss. Direction (long/short) is inferred from which side the stop is on.
- **Conversion rate**: shown only when the instrument's quote currency differs from the account currency. Auto-filled for USD-base pairs (1 ÷ entry); other pairs are auto-fetched from [frankfurter.app](https://frankfurter.app) (ECB reference rates, no API key). Manual entry overrides the fetched value; if offline or the fetch fails, the field falls back to manual input.

## Outputs

- Lot size, floored to 0.01 step.
- Risk amount, stop distance (pips/points), per-lot pip value, actual risk after rounding.
- 3R target price and reward (1:3 risk-reward baseline).

## Formula

```
risk_per_lot = |entry − stop| × contract_size × (quote → account rate)
lots         = floor(risk_amount / risk_per_lot, 0.01)
```

Contract specs are common CFD defaults (FX 100k, gold 100 oz, indices/crypto 1/point). If your broker differs, use `CUSTOM`.
