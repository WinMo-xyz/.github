# WinMo

The leveraged ETF protocol for every asset onchain.

WinMo creates non-liquidatable ERC-20 tokens that provide spot, leveraged (2x/3x), and inverse (-1x/-2x) exposure to stocks, indices, commodities, forex, and crypto. No KYC. No liquidation. Fully permissionless.

**Live at [app.winmo.xyz](https://app.winmo.xyz)**

---

## What is WinMo?

Traditional leveraged ETFs (ProShares TQQQ, Direxion SPXL, etc.) represent a $60B+ market in TradFi. In DeFi, this product category barely exists.

WinMo fixes that.

| Tier | How it works | Example |
|------|-------------|---------|
| **Spot** | Backed by the real underlying asset | sAAPL, sSPX, sGOLD, sBTC |
| **2x Long** | 2x leveraged perp position | sAAPL-2x, sSPX-2x, sGOLD-2x |
| **3x Long** | 3x leveraged perp position | sAAPL-3x, sSPX-3x, sBTC-3x |
| **-1x Inverse** | Short perp position | sAAPL-1xS, sSPX-1xS, sBTC-1xS |
| **-2x Inverse** | 2x short perp position | sAAPL-2xS, sSPX-2xS, sBTC-2xS |

### 5 Asset Classes

- **Equities** — Apple, Tesla, Nvidia, Microsoft, Amazon, Meta, Google, and more
- **Indices** — S&P 500, Nasdaq 100, Dow Jones
- **Commodities** — Gold, Silver, Oil
- **Forex** — EUR/USD, GBP/USD, JPY/USD
- **Crypto** — BTC, ETH, SOL

### TradFi Equivalents

| TradFi | WinMo Onchain |
|--------|--------------|
| SPY (spot S&P 500) | sSPX |
| SSO (2x S&P 500) | sSPX-2x |
| SPXL (3x S&P 500) | sSPX-3x |
| SH (-1x S&P 500) | sSPX-1xS |
| SDS (-2x S&P 500) | sSPX-2xS |
| GLD (spot Gold) | sGOLD |
| UGL (2x Gold) | sGOLD-2x |
| GLL (-2x Gold) | sGOLD-2xS |
| BITO (spot BTC) | sBTC |
| BITX (2x BTC) | sBTC-2x |

TradFi has **no** leveraged ETFs for individual stocks. WinMo creates them onchain (sAAPL-2x, sTSLA-3x, sNVDA-2xS, etc.).

---

## How It Works

1. **Deposit** — User deposits USDC into a vault, receives an ERC-20 token
2. **Hold** — The vault manages the underlying position (real asset for spot, perp position for leveraged/inverse). Daily rebalancing maintains precise leverage. Four-layer safety system prevents liquidation.
3. **Redeem** — Redeem tokens at Net Asset Value anytime. No lock-ups.

### Architecture

- **Spot tokens** — Backed by the real underlying asset. No perps involved.
- **Leveraged tokens (2x, 3x)** — Vault opens a leveraged long perpetual futures position.
- **Inverse tokens (-1x, -2x)** — Vault opens a short perpetual futures position.
- All tokens are **ERC-20s on Arbitrum**. Hold in any wallet, trade on any DEX, compose with any DeFi protocol.

### Four-Layer Safety System (Leveraged/Inverse Tokens)

| Layer | Trigger | Action |
|-------|---------|--------|
| **Daily Rebalance** | Every day at market close | Resets leverage to target. Margin resets to 50%. |
| **Intraday Threshold** | Leverage drifts outside allowed band | Keepers trigger intraday rebalance |
| **Emergency Ripcord** | Underlying drops 12.5%+, leverage > 2.5x | Deleverages to 1.5x. Callable by anyone. |
| **Circuit Breaker** | Leverage exceeds 3.0x | Closes all positions. Minting paused. |

Liquidation would require a 47.5% single-day drop with zero rebalancing. No major asset in recorded financial history has ever dropped that much in a single day.

---

## Why Not Lending?

IndexCoop's FLI proved demand ($200M AUM) but used Aave lending for leverage. It was:

- **5-10x more expensive** to rebalance (Uniswap 0.3% vs 0.03% on perps)
- **Limited to 2 crypto assets** (ETH, BTC only)
- **Long only** (no inverse exposure)
- **Dependent on Aave governance** (no control over own leverage engine)
- **Sunset** due to structural costs

WinMo uses **perp-based architecture** — direct leverage, unlimited asset coverage, both long and inverse, 10x cheaper rebalancing.


## Links

- **App**: [app.winmo.xyz](https://app.winmo.xyz)
- **Website**: [winmo.xyz](https://winmo.xyz)
- **Twitter/X**: [@winaborat](https://x.com/winaborat)
