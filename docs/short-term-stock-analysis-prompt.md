# Short-Term Stock Analysis Prompt

Copy everything inside the box below into Claude (with web search turned on) and fill in the first lines. The buy price and target are whatever you're considering; the prompt estimates **how many trading days** the target is likely to take and the **probability** of reaching it within your holding time. Below the prompt you'll find a plain-language guide to every number it asks for.

---

## The prompt (copy from here)

```
TICKER: [e.g. AMD]
MY PLANNED BUY PRICE: [a price, or "current price"]
MY TARGET PRICE: [a price, or a % such as "+8%"]
MAX HOLDING TIME: [e.g. 5 trading days]
ACCOUNT SIZE: [e.g. $5,000]   MAX RISK PER TRADE: [e.g. 1% of account]

You are a careful short-term trading analyst. I am a beginner trading US stocks.
My main question: based on probability, how many trading days is my target
likely to take, and what are the odds of reaching it within my max holding time?
Use live web search for every number and cite the source and date next to it.
If a number can't be found, write "not found". Never invent data. Write in plain
language and explain any jargon in one short phrase.

Start your answer with a QUICK ANSWER box:
   - Price used, with the time it was quoted and whether the market was open
     or closed at that time.
   - ⚠️ EARNINGS WARNING if the next earnings date falls inside my holding time.
   - Estimated median days to touch my target, and the probability of touching
     it within my max holding time (from section 9).
   - Final verdict (from section 11).

Then work through these sections in order:

1. SNAPSHOT
   - Company, sector, industry, market cap, current price (with quote time and
     market open/closed), today's % change.
   - 52-week high and low, and where the price sits in that range.
   - Next earnings date. If it falls inside my holding time, say so clearly:
     earnings can move a stock ±10–20% overnight in either direction, and it
     makes the probability estimate in section 9 unreliable.

2. LATEST NEWS AND ITS LIKELY EFFECT (last 7–14 days)
   - List the 3–6 most important news items with date and source.
   - For each: is it positive, negative or neutral for the price, how big is
     the likely effect (small / medium / large), and is it short-term noise or
     something that changes the business?
   - Note any upcoming catalysts inside my holding time: earnings, product
     events, FDA decisions, lawsuits, Fed meetings, CPI/jobs reports, index
     rebalances, lock-up expiries, share offerings.
   - Has the price already reacted to the news ("priced in"), or not yet?

3. PEER COMPARISON
   - Pick the 3 closest competitors in the same industry.
   - Make a table: ticker, price, 1-week %, 1-month %, P/E (forward),
     revenue growth (YoY), RSI(14).
   - Is my stock leading or lagging its peers, and is the whole industry
     moving (sector rotation) or just this stock?

4. ANALYST VIEWS
   - Consensus rating (buy/hold/sell) and number of analysts.
   - Average, high and low price target, and % upside from today.
   - Any upgrades, downgrades or target changes in the last 30 days.

5. FUNDAMENTALS (brief: for a short trade these matter less than momentum)
   - Revenue and EPS growth (last quarter YoY), profit margin, free cash flow.
   - Forward P/E and P/S vs the peer average: cheap, fair or expensive?
   - Debt-to-equity and cash position: any balance-sheet red flags?
   - Last earnings: beat or miss, and how did guidance change?

6. SUPPLY AND DEMAND
   - Today's volume vs 30-day average volume (relative volume).
   - Float (shares available to trade) and shares outstanding.
   - Short interest as % of float and days to cover. Is a short squeeze
     possible, or is heavy shorting a warning sign?
   - Institutional and insider buying/selling in the last 3 months.
   - Unusual options activity if reported (large call or put buying).

7. TECHNICAL MEASUREMENTS (most important for a short trade)
   - Price vs 9-day EMA, 20-day SMA, 50-day SMA and 200-day SMA (above/below).
   - RSI(14): overbought (>70), oversold (<30), or neutral.
   - MACD: bullish or bearish crossover, and when.
   - ATR(14) in dollars and as % of price (the stock's typical daily range).
   - Standard deviation of daily % returns over the last 20 and 60 trading
     days (the stock's typical day-to-day move; needed for section 9).
   - Beta (how much it moves vs the S&P 500).
   - Nearest support levels (2) and resistance levels (2) with prices.
     Flag any resistance between my buy price and my target.
   - Chart pattern if obvious (breakout, pullback to support, range, downtrend).

8. OVERALL MARKET: BULL OR BEAR?
   - S&P 500 and Nasdaq: above or below their 50-day and 200-day averages?
   - VIX level (fear gauge): calm (<15), normal (15–20), nervous (20–30),
     fear (>30).
   - This stock's sector ETF (e.g. XLK, SMH, XLF, XLE, XBI) trend.
   - Key macro events inside my holding time (Fed, CPI, jobs, big-tech earnings).
   - Verdict: bull, bear or choppy, and whether it helps or hurts this trade.

9. HOW MANY DAYS TO REACH MY TARGET? (probability estimate, NOT a forecast)
   a. Required move: m = (target − buy) ÷ buy, in %.
   b. Daily volatility σ = standard deviation of daily % returns over the last
      20 trading days (show the 60-day figure too; if they differ a lot, give
      results for both). Only if neither can be found, use ATR% ÷ 1.3 as a
      stand-in and say so. (ATR includes intraday swings and gaps, so it
      overstates day-to-day volatility and makes targets look too easy.)
   c. Probability of TOUCHING the target at any point by day N (the price
      only has to reach it once for a sell order to fill), assuming no trend:
         P(N) ≈ 2 × (1 − Φ( m ÷ (σ × √N) ))
      where Φ is the standard normal cumulative probability.
      Show a table for N = 1, 2, 3, 5, 10 and 20 trading days, plus my max
      holding time if it isn't in that list.
   d. Days estimate:
         Median days (50% chance of touching):  N50 ≈ ( m ÷ (0.674 × σ) )²
         75% chance of touching:                N75 ≈ ( m ÷ (0.319 × σ) )²
      If N50 is longer than my max holding time, say plainly that the target
      is unlikely within my holding time, and say what target would have a
      50% chance within it: m50 = 0.674 × σ × √(max holding days).
   e. Historical check: if daily price history for the last 12 months is
      available, count how often the stock's high rose by at least m within
      my max holding time, and the median number of days those moves took.
      Otherwise write "not found".
   f. Adjust in words, not numbers: a strong uptrend, catalyst or high
      relative volume can make it faster; resistance between buy and target,
      a downtrend or a bear market can make it slower. If earnings fall inside
      the window, say the estimate is unreliable.
   g. Show all working with the actual numbers. Finish with one line:
      "Estimate: about X trading days median; about Y% chance of touching the
      target within my max holding time." State plainly that this is based on
      past volatility and is not a prediction.

10. TRADE PLAN AND RISK
   - Entry zone (ideal buy price range) and what would confirm the entry.
   - Stop-loss price, placed just below a support level or about 1.5 × ATR
     below entry, and the % loss if hit.
   - FEASIBILITY CHECK (do this first): reward-to-risk must be at least 2:1,
     so the target must be at least 2 × (entry − stop) above entry. With a
     1.5 × ATR stop that means at least 3 × ATR. If my target is closer than
     that, say so before anything else and recommend skipping the trade or
     using a tighter stop at a real support level.
   - Target 1 (partial profit) and Target 2 (full target).
   - Reward-to-risk ratio. Recommend skipping the trade if below 2:1.
   - Position size, showing the calculation with my numbers:
       risk shares = (account size × max risk %) ÷ (entry − stop)
       max affordable shares = account size ÷ entry
       shares to buy = the smaller of the two.
   - Gap risk: a stop-loss does not guarantee my exit price. If the stock
     opens below my stop (e.g. after overnight news), the order fills at the
     open price, so the loss can be bigger than planned.
   - Exit rule if neither stop nor target is hit by my max holding time.
   - The 3 biggest risks to this trade.

11. FINAL VERDICT
   - One of: BUY NOW / WAIT FOR A BETTER ENTRY (give the price) / AVOID.
   - Confidence: low / medium / high, with the 2–3 main reasons.
   - Invalidation: what price or event would prove this trade idea wrong.
   - Score each out of 5: News, Momentum/Technicals, Supply-Demand,
     Fundamentals, Market backdrop.

Finish with a one-line reminder that this is analysis, not financial advice.
```

---

## How the "how many days" estimate works

The prompt treats daily price moves like random steps of typical size σ (the stock's daily volatility). Over N days the typical spread of outcomes grows with √N, not N, so doubling the distance to your target roughly **quadruples** the days it takes.

**Worked example** (made-up numbers): σ = 3% per day, target +10%.

| Trading days (N) | Chance of touching +10% by day N |
|---|---|
| 1 | ~0.1% |
| 2 | ~2% |
| 3 | ~5% |
| 5 | ~14% |
| 10 | ~29% |
| 20 | ~46% |

- Median days: (10 ÷ (0.674 × 3))² ≈ **25 trading days**.
- Target with a 50% chance in 5 days: 0.674 × 3% × √5 ≈ **+4.5%**.

Things the formula ignores: trends, news, earnings and resistance levels. That's why section 9 asks for a historical check and a plain-language adjustment.

---

## What each measurement means (plain language)

### Price and trend
| Measurement | What it tells you | How to read it for a short trade |
|---|---|---|
| **SMA / EMA (moving averages)** | The average price over the last N days. EMA reacts faster to recent prices. | Price above the 9 EMA and 20 SMA = short-term uptrend. Above the 50 and 200 = longer uptrend. Buying in an uptrend is easier. |
| **Support** | A price where buyers have stepped in before. | A good place to buy near, and to put your stop-loss just under. |
| **Resistance** | A price where sellers have pushed it down before. | The price often stalls here. If your target is above strong resistance, it's harder to reach. |
| **52-week range** | The lowest and highest price in the last year. | Near the high = strong momentum but less room. Near the low = cheap but often for a reason. |

### Momentum
| Measurement | What it tells you | How to read it |
|---|---|---|
| **RSI(14)** | Speed of recent moves on a 0–100 scale. | Above 70 = "overbought", may pull back. Below 30 = "oversold", may bounce. 40–60 = neutral. |
| **MACD** | Compares a fast and slow moving average to show momentum turning. | MACD line crossing above its signal line = momentum turning up (bullish). |

### Volatility (how fast it moves)
| Measurement | What it tells you | How to read it |
|---|---|---|
| **Daily volatility (σ)** | The typical size of one day's % move (standard deviation of daily returns). | The key input for the "how many days" estimate. σ of 3% means most days move less than ±3%. |
| **ATR(14)** | Average daily price range in dollars, including intraday swings and gaps. | Good for placing stops. Usually 1.2–1.5× bigger than σ, so don't use it for probabilities unless σ isn't available. |
| **Touch probability** | The chance the price reaches your target at any point, not just at the end. | Roughly double the chance of *closing* above the target on the last day. This is what matters for a limit sell order. |
| **Beta** | How much the stock moves compared with the S&P 500. | Beta 2 = moves roughly twice as much as the market, both up and down. |
| **VIX** | The market's "fear index". | High VIX = bigger, scarier swings everywhere. |

### Supply and demand
| Measurement | What it tells you | How to read it |
|---|---|---|
| **Volume / relative volume** | How many shares traded vs normal. | Relative volume above 1.5–2× means unusual interest. Price rising on high volume is more trustworthy than on low volume. |
| **Float** | Shares actually available to trade. | Small float (under ~50M shares) can move very fast in both directions. |
| **Short interest (% of float)** | Shares borrowed and sold by people betting on a fall. | Above 15–20% = a lot of bearish bets. Good news can trigger a "short squeeze" (fast rise), but it also means many pros think it will fall. |
| **Days to cover** | Days it would take shorts to buy back, based on average volume. | Higher = more squeeze potential. |
| **Insider / institutional activity** | Whether executives and big funds are buying or selling. | Insider buying is usually a positive sign; selling is often routine. |

### Valuation and fundamentals
| Measurement | What it tells you | How to read it |
|---|---|---|
| **P/E (forward)** | Price ÷ expected earnings per share. | Compare with peers. Much higher than peers = expectations are high, so a disappointment hurts more. |
| **P/S** | Price ÷ sales. Useful when a company has no profit yet. | Same idea: compare with peers. |
| **Revenue / EPS growth** | How fast sales and profits are growing. | Fast growth supports a higher price. |
| **Debt-to-equity** | How much debt vs shareholder money. | Very high = riskier, especially when rates are high. |
| **Analyst price target** | Where analysts think the price will be in ~12 months. | Useful for mood, not timing. Upgrades and downgrades often move the price for a day or two. |

### Risk
| Measurement | What it tells you | How to read it |
|---|---|---|
| **Stop-loss** | The price where you sell to cap your loss. | Decide it *before* buying, and don't move it lower. It doesn't protect you from overnight gaps. |
| **Reward-to-risk** | Potential gain ÷ potential loss. | Aim for 2:1 or better. Example: buy $10, stop $9.50 (risk $0.50), target $11 (reward $1) = 2:1. |
| **Position size** | How many shares to buy so a stop-out only loses a small, fixed part of your account. | $5,000 account × 1% = $50 risk. Stop $0.50 below entry, so 100 shares, as long as that's no more than your account can buy. |

---

## Honest notes before you use it

- **The "how many days" number is a probability, not a prediction.** No one can know when a stock will hit a price. The prompt estimates odds from how much the stock has moved in the past.
- **Bigger targets take much longer.** Because time grows with the square of the distance, a target twice as far away takes about four times as many days.
- **Earnings inside your holding time is a coin flip with big swings.** The volatility-based estimate doesn't hold across an earnings report. Many short-term traders avoid holding through earnings.
- **AI web data can be stale or wrong.** Check the price, earnings date and short interest yourself on a free site such as Finviz, Yahoo Finance or your broker's app before trading.
- **Pattern day trader rule:** in a US margin account under $25,000, you've been limited to 3 day trades (buy and sell the same day) in 5 business days. FINRA has proposed changing this rule, so check your broker's current terms. Holding overnight avoids the issue either way.
- This prompt is a research aid, not financial advice. Only trade money you can afford to lose.
