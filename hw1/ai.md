Prompts:

Q1: From 2000, pull US and European 10-year government bonds, public equity, high yield credit, and global commodities data. Compute returns using geometric mean to show annualized mean returns.
- Directed AI to use DGS10 (FRED) for US bonds and German 10Y Bund (FRED IRLTLT01DEM156N) for EU bonds.
- For commodities, instructed AI to focus on futures-based instruments (DBC) since that is how macro investors trade them.
- For EU HY credit, no FRED total return index was available; AI identified iShares EXHA.DE (Xetra ETF) as proxy. For US HY credit, AI switched from FRED (BAMLHYH0A0HYM2TRIV, which is now restricted to ~3 years of history) to HYG (Yahoo Finance) to recover full history from 2007.

Q2: Use pandas to display annual vols, ann_vols = returns.std() * np.sqrt(12), in table format.

Q3-onwards:
Data Sources: Instructed AI to examine the data source markdown and revise descriptions for accuracy, coverage dates, and instrument details. AI restructured the section into a table format and added a note explaining why EU HY credit (0.46%) underperforms the EU 10Y bond (2.96%) despite carrying a spread premium.

Write-Up Revision: Instructed AI to cross-check all markdown write-ups against actual numerical outputs and revise any incorrect claims. 

Style: Instructed AI to make all write-ups more concise.

AI Role: AI was used to implement code, source data, identify errors in both data and write-ups, and refine wording for clarity and concision.

