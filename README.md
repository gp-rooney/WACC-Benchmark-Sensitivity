# WACC Benchmark Sensitivity — Are SPY Betas Always Appropriate?

## Overview
This was a short, curiosity-driven check into whether using the S&P 500 (SPY) as the automatic beta benchmark — like Bloomberg does when it spits out a WACC — is always sensible. A friend pointed out Bloomberg used an S&P-based beta for a company whose business is mainly in China, even though that stock didn’t move with the U.S. market. That made me wonder how many S&P names actually *aren’t* tightly tied to SPY. :contentReference[oaicite:0]{index=0}

## Research question
When terminals auto-compute a beta versus the S&P 500, is that benchmark appropriate for every S&P 500 company? Or do some stocks have such low correlation with SPY that using SPY as the default makes the beta (and therefore the WACC) noisy or misleading?

## What I did (data & method)
- Universe: current S&P 500 constituents (snapshot at the time of analysis).  
- Window: weekly returns over the past three years.  
- For each stock I ran a simple regression of the stock’s weekly returns on SPY weekly returns and saved the **R²**. R² is a straightforward measure of how much of the stock’s return variation is explained by SPY — i.e., how “tied” the stock is to the index. Implementation is a small Python script that downloads prices, computes weekly returns, runs regressions, and makes plots. :contentReference[oaicite:1]{index=1}

## What I found (high level)
- Big, well-known names aren’t uniformly highly correlated to SPY. Some headline MAG-7 firms rank much lower in R² than you’d expect. The MAG-7 ranks I computed (rank among S&P tickers, with reported R²) were:  
  - **MSFT:** rank 10 (R² = 0.547)  
  - **AAPL:** rank 14 (R² = 0.524)  
  - **AMZN:** rank 15 (R² = 0.522)  
  - **NVDA:** rank 22 (R² = 0.514)  
  - **GOOG:** ranks 137, 145 (R² = 0.373)  
  - **TSLA:** rank 248 (R² = 0.291)  
  - **META:** rank 288 (R² = 0.248)  
  Those numbers show that several MAG-7 names (GOOG, TSLA, META) have materially lower explanatory power versus SPY than the largest tech names. :contentReference[oaicite:2]{index=2}

- By sector, **financials and conglomerates** tended to show higher R² with SPY; **healthcare and consumer defensive** names often had lower R² (more independent movement). :contentReference[oaicite:3]{index=3}

## Practical takeaway
- **Default to SPY**, but don’t treat it as a one-size-fits-all. If a firm’s revenues, geography, or business model decouple it from the U.S. market, the SPY beta can be noisy.  
- Low R² means the beta estimate is unreliable — for WACC work you should either:
  - run sensitivity checks (show WACC under alternative betas), or  
  - consider a benchmark more tightly tied to the company’s cash flows (regional index, sector index, or a bespoke multi-factor beta).  
- In short: Bloomberg’s default WACC is often fine, but verify when the company’s economic exposure looks different from the U.S. index. :contentReference[oaicite:4]{index=4}
