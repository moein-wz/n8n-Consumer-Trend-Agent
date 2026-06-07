# n8n-Consumer-Trend-Agent

# Consumer Trend Discovery — n8n Workflow

An AI-powered n8n workflow that generates consumer trend reports for home decor rug categories. Given a product category and Amazon.com URLs, it scrapes product data, pulls social trends from Instagram and Pinterest, and produces a fully structured HTML trend report with AI-generated visuals.

---

## What It Does

1. **Parses user input** — accepts a rug category and Amazon.com product or collection URLs via chat
2. **Scrapes Amazon** — extracts product names, prices, and feature details from product pages (supports both direct `/dp/` links and collection/search pages)
3. **Fetches social trend data** — pulls Instagram posts, Pinterest boards, blog articles, and market data from a FastAPI backend
4. **Runs AI analysis (Google Gemini)** — classifies products, normalizes attributes (color, material, pattern, style), identifies micro-segments, and extracts visual trends
5. **Generates trend images (HuggingFace FLUX)** — creates AI-generated visual mockups for each identified micro-segment
6. **Produces an HTML report** — assembles all sections into a downloadable, styled trend report with embedded images

---

## Supported Categories

| Input keyword | Category |
|---|---|
| `area rug` / `area rugs` | Area Rug |
| `outdoor rug` / `patio rug` | Outdoor Rug |
| `hallway runner` / `runner rug` | Hallway Runner |
| `shag rug` / `shaggy rug` | Shag Rug |

---

## Workflow Architecture

```
Stage 1 → Input Parsing & Validation
Stage 2A → Amazon Scraping (collection + direct product URLs)
Stage 2B → Social Data Fetching (Instagram, Pinterest, Blogs, Market)
Stage 3 → AI Processing (Gemini — classify, extract attributes, identify micro-segments)
Stage 4 → Image Generation (HuggingFace FLUX-schnell)
Stage 5-6 → Merge & HTML Report Assembly
```

---

## Prerequisites

- **n8n** (self-hosted or cloud)
- **Google Gemini API** — used for all AI analysis steps (set up as an n8n credential)
- **HuggingFace API** — used for FLUX image generation (set up as an n8n credential)
- **FastAPI backend** — a custom server that serves Instagram, Pinterest, blog, and market trend data. The workflow expects it at `http://<your-server-ip>:8000`

---

## Setup

1. Import `Consumer_Trend_Discovery.json` into n8n (drag onto canvas or use **File → Import from file**)
2. Configure credentials:
   - Add your **Google Gemini API key** under n8n credentials
   - Add your **HuggingFace API key** under n8n credentials
3. Update the FastAPI server URLs in the following nodes to point to your own server:
   - `Fetch Instagram`
   - `Fetch Pinterest`
   - `Fetch Blogs`
   - `Fetch Market Data`
4. Activate the workflow

> ⚠️ **Note:** The workflow currently contains hardcoded references to `http://34.196.186.128:8000`. Replace this with your own FastAPI server address before deploying.

---

## Usage

Open the n8n chat trigger and send a message like:

```
Category: Outdoor Rug
https://www.amazon.com/s?k=outdoor+rugs
https://www.amazon.com/dp/B08XYZ1234
```

The workflow will process the input and return a downloadable HTML trend report.

---

## Tech Stack

- **n8n** — workflow automation
- **Google Gemini** — AI analysis and trend generation
- **HuggingFace FLUX-schnell** — AI image generation
- **Cheerio** — Amazon HTML parsing
- **Custom FastAPI server** — social & market data ingestion

---

## Project Structure

```
/
├── Consumer_Trend_Discovery.json   # Main n8n workflow
└── README.md
```

---

## Author

**Mohammad Rumee**  
[linkedin.com/in/moein-rumee](https://linkedin.com/in/moein-rumee)
