# Firecrawl

AI-ready web scraper. Turn any website into LLM-ready markdown or structured data.

## Local Development

```bash
docker compose up
```

API available at `http://localhost:3002`.

## Usage

```bash
curl -X POST http://localhost:3002/v1/scrape \
  -H "Content-Type: application/json" \
  -d '{"url": "https://example.com"}'
```

## Deploy on StackBlaze

This template includes a `stackblaze.yaml` for deployment.
