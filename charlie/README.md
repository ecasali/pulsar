# Charlie - Morning News Intelligence App

## Overview

This application is designed to turn a noisy morning news flow into a concise, decision-ready briefing. The app collects fresh news, filters it for relevance, summarizes the most important developments, and delivers a structured morning digest that can be read quickly by an operator, executive, or investor.

The goal is not to maximize the volume of information. The goal is to reduce cognitive load and increase signal quality by surfacing what matters, why it matters, and what may need follow-up.

## What the app does

The app performs a simple but high-value workflow:

1. Pulls recent news from selected sources or search results.
2. Filters and ranks the items based on relevance.
3. Applies recency rules so stale news is deprioritized.
4. Summarizes the selected items into a compact briefing.
5. Sends the final output to the user, for example through Telegram.

Depending on the implementation, the app can be configured around topics, companies, keywords, geographies, or personal interest areas.

## Architecture

The app is best understood as a pipeline with five layers.

### 1. Input and configuration layer

This layer defines what the system should track.

Typical inputs include:
- Topic list or watchlist.
- Preferred sources.
- Time window for freshness.
- Delivery settings.
- Summarization length.

This layer is intentionally simple so the app can be adjusted quickly without changing core logic.

### 2. Retrieval layer

This layer fetches the raw news items.

Possible retrieval methods include:
- Search APIs.
- News APIs.
- RSS feeds.
- Curated websites.

The retrieval layer should attach metadata to each item such as title, source, URL, timestamp, and search query or category.

### 3. Filtering and ranking layer

This is where the raw feed becomes useful.

Typical logic includes:
- Remove duplicates.
- Drop low-quality or irrelevant items.
- Favor fresh items.
- Rank by importance or likely decision value.
- Group similar stories into one cluster.

This layer is critical because a good briefing depends more on selection quality than on summary quality.

### 4. Summarization and synthesis layer

The selected articles are turned into readable output.

A good summary stage should produce:
- Headline.
- One- or two-sentence explanation.
- Why it matters.
- Optional action prompt or follow-up question.

This layer can be single-agent or multi-agent, but the key requirement is clarity and compression.

### 5. Delivery layer

This layer sends the output to the final destination.

Common channels include:
- Telegram.
- Email.
- Markdown file.
- Dashboard.
- Google Doc or Notion export.

For a morning-use app, delivery quality matters almost as much as retrieval quality. The briefing should be easy to consume on mobile and fast to scan.

## Suggested system flow

A practical end-to-end flow looks like this:

1. User defines topics or entities to monitor.
2. App retrieves fresh candidate articles.
3. App removes duplicates and stale items.
4. App scores relevance.
5. App summarizes the top items.
6. App packages the output in a standard format.
7. App sends the final digest.

## Recency and freshness rules

This app works best when it is strict about time.

Recommended freshness policy:
- Prefer items from the last 12 to 24 hours for a morning briefing.
- Allow up to 7 days only when the item remains highly relevant.
- Flag older items explicitly as background context.
- Avoid mixing old commentary with fresh breaking news unless the distinction is clear.

This helps prevent the common failure mode of news agents: producing polished but stale briefings.

## How to make it work

### Setup requirements

A typical setup includes:
- Python environment, often Google Colab for prototyping.
- API keys for search or news retrieval if needed.
- LLM access for summarization.
- Optional Telegram bot token for delivery.

## Output format

A strong morning briefing usually includes:
- Date and time.
- Topic or watchlist sections.
- Top headlines.
- Short explanation per item.
- Why it matters.
- Optional links for deep reading.




That framing makes the project look like a real decision-support system rather than a generic news summarizer.
