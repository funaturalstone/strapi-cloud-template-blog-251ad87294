# Short-Term Momentum Profit Prompt

A prompt for **fast, short-term momentum trades** (1–5 trading days). It is built to find the setups with the **highest expected profit per day** and to squeeze the most out of winners. It ignores long-term value investing: no fair-value models, no "good company to hold for years".

Copy everything inside the box below into Claude (with web search and, ideally, a market-data connector such as Twelve Data turned on). Fill in the first lines. Below the prompt is a plain-language guide to every term.

---

## The prompt (copy from here)

```
MODE: [SCAN = find today's best setups | TICKER = analyse one stock]
TICKER (TICKER mode only): [e.g. AXTI]
ACCOUNT SIZE: [e.g. $1,500]
MAX HOLD: [1–5 trading days]
MIN PRICE / MIN AVG VOLUME: [e.g. $5 / 1M shares]

You are an aggressive short-term momentum trader. Your only goal is to
maximise expected profit per trading day over the next 1–5 days. This is
not value investing: ignore long-term valuation, dividends and "fair value"
unless they move the price this week. Use live market data for every number
and cite source and time. If a number can't be found, write "not found".
Never invent data. Use plain language and explain jargon in one short phrase.

Start with a TOP PICK box:
   - Ticker, price (with quote time, market open/closed), setup type.
   - Entry trigger, Target 1 / Target 2, trailing-exit rule.
   - Expected value per day (section 7) and median days to Target 1.
   - Confidence: low / medium / high.

Then work through these sections in order:

1. MARKET TIDE (trade with it, not against it)
   - QQQ, SPY, IWM: today's % change and price vs 9-day EMA and 20-day EMA.
   - VIX level and direction.
   - Today's 3 strongest and 3 weakest sectors (sector ETFs).
   - Verdict: RISK-ON (buy breakouts), CHOPPY (only the strongest setups,
     take profits fast) or RISK-OFF (cash or only stocks rising against the
     market).

2. SCAN (SCAN mode only; in TICKER mode skip to section 3)
   Find stocks that match ALL of:
   - Price above MIN PRICE, 30-day average volume above MIN AVG VOLUME.
   - Relative volume (today's volume ÷ 30-day average) at least 2.
   - A fresh catalyst in the last 3 days, or a breakout to a new 20-day or
     52-week high.
   - In a sector that's in today's top 3, or rising while the market falls.
   List the 5 best candidates with: ticker, price, today %, relative volume,
   catalyst in one line. Then analyse the top 3 with sections 3–7 and pick
   the single best one for sections 8–9.

3. CATALYST (what's pushing the price, and is it still fresh?)
   - What happened, when, and source. Rate it: fresh (0–2 days), aging
     (3–5 days) or stale.
   - Is there a follow-up catalyst inside MAX HOLD (earnings run-up,
     product launch, FDA date, conference, index addition)?
   - Flag anything that can kill the move this week: share offering or
     dilution, lock-up expiry, earnings inside the window (a coin flip with
     ±10–20% gaps), a big macro release (CPI, Fed).

4. MOMENTUM
   - % change: today, 5-day, 20-day.
   - Relative strength vs QQQ and vs its sector ETF over 5 and 20 days
     (outperforming = leader).
   - Price vs 9-day EMA and 20-day EMA, and whether both are rising.
   - RSI(14): 50–70 = healthy momentum, 70–80 = strong but stretched,
     above 80 = likely to pause or pull back.
   - MACD: direction and latest crossover date.
   - Volume trend: are up-days on bigger volume than down-days?
   - Short interest (% of float) and days to cover: above 20% with a fresh
     catalyst = squeeze fuel.

5. SETUP TYPE AND ENTRY TRIGGER (pick the one that fits)
   - BREAKOUT: price clears a recent high on 2× volume. Entry: above the
     breakout level.
   - PULLBACK: strong uptrend dips to the 9 or 20 EMA and holds. Entry: first
     green candle off the EMA.
   - GAP-AND-GO: gaps up on news and holds above the first 15–30 minute high.
     Entry: break of that high.
   - SQUEEZE: high short interest + catalyst + rising volume. Entry: break of
     the prior day's high.
   - RUN-UP: earnings or event in 3–10 days with rising volume. Exit before
     the event.
   Give the exact trigger price and the price where the setup is broken.

6. PROFIT POTENTIAL (how far and how fast)
   a. Daily volatility σ = standard deviation of daily % returns over 20 days
      (also show 60-day). ATR(14) in $ and %.
   b. Chance of TOUCHING each target by day N (assuming no trend):
         P(N) ≈ 2 × (1 − Φ( m ÷ (σ × √N) ))
      where m = % move to the target and Φ is the standard normal
      cumulative probability. Table for +5%, +10%, +15%, +20%, +30% at
      N = 1, 2, 3, 5 trading days.
   c. Median days to each target: N50 ≈ ( m ÷ (0.674 × σ) )²
   d. Historical check: in the last 6–12 months, how often did the stock's
      high rise by at least each target within MAX HOLD days, and the median
      days it took? (Count from daily price data if available.)
   e. Adjust in words: a strong trend, fresh catalyst, high relative volume
      or short squeeze can make moves faster than the formula; resistance
      levels overhead make them slower. Name the nearest 2 resistance levels.

7. EXPECTED VALUE (rank setups by this)
   For the planned trade:
      EV = P(hit target) × gain − P(hit exit first) × loss
      EV per day = EV ÷ median days to target
   Use the section 6 probabilities; the exit is the "setup broken" price
   from section 5. Show the working with real numbers. In SCAN mode, rank
   the top 3 by EV per day and pick the highest.

8. EXECUTION PLAN (take as much profit as possible)
   - Entry: trigger price and a limit price (no market orders in the first
     15 minutes of the session).
   - Size: how much of ACCOUNT SIZE goes into this trade, scaled by
     confidence and EV (highest-EV setup gets the most).
   - Scale out to lock gains and still catch a big runner:
        1/3 at Target 1 (≈ +1 ATR or the first resistance),
        1/3 at Target 2 (≈ +2–3 ATR or the next resistance),
        last 1/3 rides with a trailing exit: close below the 9-day EMA or
        2 × ATR below the highest price since entry, whichever is higher.
   - After Target 1 is hit, raise the exit on the rest to the entry price so
     a winner can't turn into a loser.
   - Setup-broken exit: if price closes below the "setup broken" level, exit
     and move the money to a better setup (dead money costs profit).
   - Time exit: if Target 1 isn't hit within 2 trading days, rotate out.
   - Event rule: exit before earnings unless you deliberately choose the
     gamble, and say which.

9. FINAL CALL
   - BUY NOW (at trigger) / BUY ON TRIGGER ONLY (give the price) / PASS.
   - EV per day, median days to Target 1, chance of Target 1 within MAX HOLD.
   - Top 2 reasons it can work and top 2 things that would kill the move.
   - Score each out of 5: Catalyst, Momentum, Volume, Market tide, Setup
     quality.

Finish with a one-line reminder that this is analysis, not financial advice.
```

---

## Worked example: expected value per day

Made-up numbers: a stock with daily volatility σ = 5%. Target 1 is +10%, the "setup broken" exit is −5%.

- Chance of touching +10% within 3 days: 2 × (1 − Φ(10 ÷ (5 × √3))) ≈ **25%**.
- Chance of touching −5% within 3 days: 2 × (1 − Φ(5 ÷ (5 × √3))) ≈ **56%**.
- These can both happen in the same window, so treat them as rough. A practical version uses "which comes first", roughly 1 : 2 here (the target is twice as far as the exit), so about 33% target-first and 67% exit-first.
- EV ≈ 0.33 × 10% − 0.67 × 5% ≈ **−0.0%**: a coin flip with no edge.

The same stock with a fresh catalyst and 3× relative volume often trends, which is what the momentum sections look for. If the historical check shows +10% was reached first 50% of the time, EV ≈ 0.5 × 10% − 0.5 × 5% = **+2.5% per trade**. At a median of 3 days that's **≈ +0.8% per day**. That edge, repeated, is where short-term profit comes from. Setups with no edge should get a PASS.

---

## What each term means (plain language)

### Momentum and trend
| Term | What it tells you | How to use it |
|---|---|---|
| **EMA (9 and 20-day)** | Average price that reacts quickly to new prices. | Price above a rising 9 and 20 EMA = strong short-term trend. Pullbacks to them are classic entries. |
| **Relative strength** | Is the stock beating the market and its sector? | Leaders keep leading in the short term. Buy the strongest stock in the strongest sector. |
| **RSI(14)** | Speed of recent moves, 0–100. | 50–70 healthy momentum; 70–80 strong but stretched; above 80 often pauses. |
| **MACD** | Fast vs slow average, shows momentum turning. | Line crossing above signal = momentum turning up. |
| **Breakout** | Price clears a level it failed at before. | Most powerful with 2× normal volume. |
| **Gap-and-go** | Opens far above yesterday's close on news and keeps going. | Wait for it to hold above the first 15–30 minute high. |

### Fuel for big moves
| Term | What it tells you | How to use it |
|---|---|---|
| **Catalyst** | News that makes buyers act: earnings beat, contract, upgrade, FDA approval. | Fresh catalysts (0–2 days) move stocks most. Stale ones fade. |
| **Relative volume** | Today's volume ÷ normal volume. | Above 2 = big interest. Moves on high volume last longer. |
| **Short interest / days to cover** | Bets on a fall, and how long they'd take to buy back. | Above 20% + good news can force a short squeeze: a fast, sharp rise. |
| **Float** | Shares actually available to trade. | Small float (under ~50M) moves faster both ways. |

### Speed and size of moves
| Term | What it tells you | How to use it |
|---|---|---|
| **σ (daily volatility)** | Typical size of one day's % move. | Drives how many days a target takes. Higher σ = faster targets (and faster drops). |
| **ATR(14)** | Average daily range in dollars. | Use for targets (+1, +2, +3 ATR) and the trailing exit (2 × ATR). |
| **Touch probability** | Chance the price reaches the target at any point. | What matters for a sell order: about double the chance of closing there. |
| **N50** | Median trading days to reach a target. | Lower = faster money. |
| **EV per day** | Average profit per trade ÷ days held. | The number to rank trades by. Higher = better use of your money. |

### Profit-taking
| Term | What it tells you | How to use it |
|---|---|---|
| **Scaling out** | Selling in pieces at different targets. | Locks in profit early and still lets part of the position catch a big run. |
| **Trailing exit** | An exit price that moves up as the stock rises. | Lets winners run without giving back the whole gain. |
| **Time exit** | Leave a trade that isn't moving. | Money sitting still could be in a stock that is moving. |

---

## Notes before you use it

- **Profit in short-term trading comes from edge × repetition.** A setup with no edge (EV ≈ 0) is a coin flip, so this prompt is built to PASS on those and only act on the best ones.
- **The exits in section 8 are there to maximise profit, not to be cautious.** One large loss wipes out many wins: a −50% loss needs +100% just to get back to even.
- **Trade with the tide.** Momentum setups work far better in a RISK-ON market. Many of the biggest losses come from buying breakouts in a falling market.
- **Earnings inside your window is a gamble, not a setup.** The prompt tells you to exit before, unless you deliberately choose the gamble.
- **AI web data can be stale or wrong.** Check the price, catalyst date and short interest on your broker's app before trading. A live market-data connector makes the numbers much more reliable.
- **Pattern day trader rule:** in a US margin account under $25,000 you've been limited to 3 day trades (buy and sell the same day) in 5 business days. FINRA has proposed changing it, so check your broker's current terms. A cash account avoids it but you must wait for cash to settle (T+1) before reusing it.
- This prompt is a research aid, not financial advice. Only trade money you can afford to lose.
