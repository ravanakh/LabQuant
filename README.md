# LabQuantSim

### Understand the risk. Explore the return.

**LabQuantSim** is an interactive quantitative-finance research dashboard that turns historical stock prices into possible future scenarios. It brings simulation, downside-risk analysis and portfolio diversification together with explanations designed for people without a quantitative-finance background.

> **This is the public showcase repository. The application source code is maintained in a separate private repository and is not included here.**

**Live app:** Not deployed yet. The verified Streamlit link will be added here after deployment.

<!-- After deployment, replace the line above with:
[Open LabQuantSim](https://YOUR-ACTUAL-APP-SUBDOMAIN.streamlit.app/)
Do not insert a guessed or unverified address.
-->

## A look inside

The screenshots below show the actual local Streamlit application running **synthetic sample data**, not live stock forecasts.

![LabQuantSim simulation dashboard](assets/dashboard.jpg)

![Portfolio analysis and efficient frontier](assets/portfolio.jpg)

## Features

- Select a stock or ETF and choose the historical period to study.
- Set a separate future horizon and compare five simulation models.
- Explore percentile bands, simulated returns and the probability of a loss.
- Inspect Value at Risk, expected shortfall, volatility, Sharpe ratio and historical drawdown.
- Compare portfolio allocations along an efficient frontier for two to five assets.
- Review correlations to understand diversification.
- Import daily-price CSVs and export reproducible reports.
- Use synthetic sample mode without an account or a paid data connection.
- Optionally request free historical data and view a separate TradingView reference chart.
- Read short explanations and limitations beside the results.

## Architecture

![Private source, public app, public showcase architecture](assets/architecture.svg)

The **private GitHub repository** holds the Python application, numerical models, tests and dependencies. Streamlit Community Cloud runs that repository as a **public website**. Visitors interact with the app without receiving repository access. This separate **public showcase** contains documentation and presentation assets only.

Streamlit and authorized repository collaborators necessarily have access to the source required to run and administer the app. The app's public viewing setting does not change the GitHub repository's visibility.

## Tech stack

| Layer | Technology |
| --- | --- |
| Application | Python, Streamlit |
| Numerical analysis | NumPy, pandas, SciPy |
| Interactive charts | Plotly |
| Optional historical data | yfinance / Yahoo Finance |
| Reference market chart | TradingView widget |
| Quality checks | pytest, Streamlit AppTest |
| Hosting | Streamlit Community Cloud |
| Source hosting | Separate private GitHub repository |

No paid hosting, database or paid API is required for the sample/CSV experience. Free market-data availability and data-use rights are separate considerations.

## Methodology overview

**Monte Carlo / geometric Brownian motion** explores randomized price paths based on historical average daily movement and volatility. It is an interpretable baseline, but its stable-distribution assumptions are strong.

**Historical bootstrap** rearranges sampled days from the selected history. It reflects the sample's observed distribution but cannot invent daily shocks that are absent from it.

**Block bootstrap** resamples short stretches of history to retain some short-term dependence and periods of market turbulence.

**Student-t stress scenarios** explore heavier-tailed shocks. The model's average terminal price is unstable; median and percentile outcomes are more informative than its finite-run mean.

**GARCH-style volatility scenarios** allow risk to change after shocks. This version uses illustrative fixed parameters, not a statistically fitted GARCH forecast.

**Efficient frontier analysis** estimates the lowest-volatility, fully invested, long-only portfolio at each target return. It uses shared historical dates and estimated correlations. The reported highest-Sharpe allocation is selected from the displayed frontier points.

All models are conditional on their inputs and assumptions. Agreement between models is not independent evidence: they reuse the same history. Percentile bands describe simulated variability, not certainty about future stock performance.

## Roadmap

- [x] Python/Streamlit research dashboard
- [x] Five simulation models and model explanations
- [x] Downside-risk measures and interactive charts
- [x] Efficient frontier, allocations and correlations
- [x] CSV import, reproducible reports and numerical tests
- [ ] Publish the first public Streamlit deployment
- [ ] Add walk-forward evaluation and parameter uncertainty
- [ ] Fit and validate volatility-model parameters
- [ ] Expand currency and corporate-action handling
- [ ] Improve accessible chart summaries and data-quality diagnostics

## Data and privacy

Synthetic sample data is explicitly labeled. CSVs are processed in app-server session memory and are not deliberately saved to disk or shared through a global cache. Do not upload confidential portfolio/account information. Reports include the input prices, so users should share them only when permitted.

The optional Yahoo connector is unofficial and may be unavailable or rate-limited on shared hosting. The yfinance documentation notes personal-use data restrictions; no public redistribution license is implied. Sample and user-provided CSV analysis remain available independently. TradingView is an independent reference chart and does not feed the simulation calculations.

## Disclaimer

LabQuantSim is an educational research project, not financial advice, a reliable forecasting service, or an automated trading system. Historical performance does not guarantee future results. Models can omit structural changes, liquidity, fees, taxes and events absent from the sample. No recommendation to buy or sell any security is made.

## Repository scope

This repository intentionally contains only this README and screenshots/architecture artwork. It contains no application source, Python modules, simulation implementation, tests, dependency files, secrets, market-data dumps or source archives.
