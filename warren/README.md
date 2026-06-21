# WARREN - Stock Analysis App

## Overview

This application is designed to transform a list of tickers into a structured, analyst-style research packet. It combines market data, financial statement information, valuation signals, ownership context, benchmark comparison, and recent web enrichment to produce a decision-ready stock analysis output.

The app is meant to support a workflow similar to that of an experienced equity analyst. Instead of only pulling raw data, it organizes the information into a format that can be reviewed directly by a human or passed into a swarm of specialized AI agents.

## What the app does

The application performs the following workflow:

1. Accepts a user-defined list of tickers.
2. Pulls market and company data.
3. Classifies instruments such as equities, indices, funds, or other asset types.
4. Builds normalized data packets for each ticker.
5. Computes core analytical views such as returns, margins, cash flow, valuation, and benchmark-relative context.
6. Uses a multi-agent workflow to generate structured analysis.
7. Produces a final investment-style report.

## Architecture

The app can be understood as a seven-layer system.

### 1. Input layer

This layer defines the user’s requested tickers and general runtime settings.
Typical inputs include: Ticker list, Benchmark ticker.

### 2. Data extraction layer

This layer retrieves the raw financial and market information.

Typical extracted data may include:
- Price history.
- Company profile fields.
- Financial statements.
- Earnings dates.
- Analyst estimates.
- Recommendations.
- Ownership information.
- News and event data.

The purpose of this layer is not interpretation. It is reliable collection and normalization.
The output of the engineering stage is packed into standardized objects, one per ticker.
Each packet typically includes:

- Profile.
- Market data.
- Fundamentals.
- Valuation.
- Expectations.
- Ownership.
- Events.
- Risk flags.
- Data quality notes.

This is the key design decision of the app. Agents do not inspect random raw fields. They reason over a stable schema.

### 3. Multi-agent analysis layer

This layer runs the analytical swarm.

A common role structure includes:
- Research analyst.
- Writer or investment-committee drafter.
- Benchmark analyst.
- DCF analyst.
- Final critic or CIO reviewer.

Each agent has a specific job, and the process is sequential so later agents refine what earlier agents produced.

### 7. Output and delivery layer

This layer saves and distributes the results.

Typical outputs include:
- Final text report.
- Per-agent output log.
- Structured JSON files.
- Telegram message.
- Notebook artifacts for review.

## Suggested system flow

A practical run looks like this:

1. User enters a list of tickers.
2. App retrieves and normalizes data.
3. App classifies the instruments.
4. App computes analytical metrics.
5. App creates ticker packets.
6. App runs the agent workflow.
7. App saves the final report and all agent outputs.

## Recency rules for web enrichment

The analytical core should come from structured market and financial data. External web research should be used only as enrichment.

Recommended policy:
- Prefer sources from the last 14 days.
- Avoid sources older than 30 days unless they are uniquely important.
- Treat older sources as background context, not fresh evidence.
- Make a clear distinction between data-derived analysis and web-derived commentary.

This keeps the system grounded and reduces the risk of stale narratives driving the conclusion.

## How to make it work

### Setup requirements

A typical implementation needs:
- Python environment, often Colab for prototyping.
- Access to market-data libraries or APIs.
- LLM access for the multi-agent workflow.
- Optional search API for recent web enrichment.
- Optional Telegram integration for delivery.

### Core implementation steps

1. Set the configuration and load keys.
2. Fetch market and financial data for each ticker.
3. Normalize the raw outputs.
4. Classify each ticker.
5. Compute analytical metrics.
6. Build a standardized packet per ticker.
7. Run the multi-agent analysis process.
8. Save the final report and intermediate outputs.

## Output format

A useful final output usually contains:
- Market snapshot.
- Benchmark view.
- One section per focus ticker.
- Bull, base, and bear framing where appropriate.
- Margin-of-safety discussion.
- Risks and what to monitor.
- Data caveats.

In addition to the final report, the app should save all agent outputs for auditability and debugging.
