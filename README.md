# Project: News Intelligence Reader

## Overview
This Colab notebook demonstrates a news intelligence reader powered by the Gemini API. It fetches news headlines from various RSS feeds, processes them using a Large Language Model (LLM) for cleaning, summarization, and scoring, and then presents the top news stories in a user-friendly HTML format.

## Architecture Diagram

```mermaid
graph TD
    A[RSS Feeds (BBC, The Verge, TechCrunch)] --> B{Python: Fetch RSS Items (feedparser)}
    B --> C[Raw News Headlines (raw_blob)]
    C --> D{LLM Call 1: Clean & Deduplicate (Gemini API)}
    D --> E[Cleaned & Deduplicated Items (clean_items)]
    E --> F{LLM Call 2: Summarize (Gemini API)}
    F --> G[Summarized News Briefs (news_cards)]
    G --> H{LLM Call 3: Score Urgency & Impact (Gemini API)}
    H --> I[Scored News Items (scores)]
    I --> J{Python: Sort & Filter Top K News (TOP_K)}
    J --> K[Ranked Top News (top_news)]
    K --> L{Python: Generate HTML Output}
    L --> M[Display HTML in Notebook]
```

## Components

### 1. RSS Feed Fetching
*   **Purpose:** Gathers raw news headlines from specified RSS feeds.
*   **Technology:** Python's `feedparser` library.
*   **Output:** A `raw_blob` string containing a list of headlines, sources, and links.

### 2. LLM Call 1: Cleaning & Deduplication
*   **Purpose:** Takes the raw headlines, removes duplicates, normalizes titles, and ensures a clean set of distinct stories.
*   **Technology:** Gemini API (via `google.genai` library).
*   **Output:** `clean_items`, a JSON list of cleaned news items.

### 3. LLM Call 2: Summarization
*   **Purpose:** For each cleaned news item, generates a short paragraph summary and three key bullet points.
*   **Technology:** Gemini API.
*   **Output:** `news_cards`, a JSON list of news items with added summaries and key points.

### 4. LLM Call 3: Scoring
*   **Purpose:** Evaluates each summarized news item for its urgency (0-5) and impact (0-5).
*   **Technology:** Gemini API.
*   **Output:** `scores`, a JSON list containing the urgency, impact, and a reason for the score for each news item.

### 5. Sorting & Filtering
*   **Purpose:** Combines the summarized news with their scores, calculates a total score (urgency + impact), and sorts them in descending order. It then filters to display only the top `TOP_K` news items.
*   **Technology:** Python scripting.

### 6. HTML Output Generation
*   **Purpose:** Formats the top news stories into a visually appealing HTML output, suitable for display within the Colab notebook or export.
*   **Technology:** Python scripting, `IPython.display.HTML`.

## Setup and Usage
1.  **Install Dependencies:** Run the `pip install` cells to ensure all necessary libraries are installed.
2.  **API Key Setup:** Obtain a Gemini API key from [Google AI Studio](https://aistudio.google.com/app/apikey) and set it in the `GEMINI_API_KEY` environment variable in the designated cell.
3.  **Execute Cells:** Run all the cells in sequential order to fetch news, process it with the LLM, and display the final ranked news brief.
