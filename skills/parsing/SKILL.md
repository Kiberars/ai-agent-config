# Skill: Data Parsing

## Purpose
Extract structured data from websites, APIs, and documents (YouTube, kwork, HH.ru, etc.)

## Trigger
Use this skill when asked to: parse, scrape, extract, collect data from web sources.

---

## Quick Reference

### Stack
- `httpx` or `aiohttp` — HTTP requests (async preferred)
- `BeautifulSoup4` — HTML parsing
- `yt-dlp` — YouTube metadata (no API key needed)
- `playwright` — dynamic JS-rendered pages

### Output formats
- JSON (default)
- CSV (for tabular data)
- Markdown (for documentation)

---

## Patterns

### YouTube metadata
```python
import yt_dlp

def get_video_info(url: str) -> dict:
    with yt_dlp.YoutubeDL({'quiet': True}) as ydl:
        return ydl.extract_info(url, download=False)
```

### HH.ru (HeadHunter) API
```python
import httpx

BASE = "https://api.hh.ru"
HEADERS = {"User-Agent": "your-app/1.0"}

def search_vacancies(query: str, area: int = 1) -> list:
    r = httpx.get(f"{BASE}/vacancies", params={"text": query, "area": area}, headers=HEADERS)
    r.raise_for_status()
    return r.json()["items"]
```

### HTML parsing
```python
from bs4 import BeautifulSoup
import httpx

def parse_page(url: str, selector: str) -> list[str]:
    r = httpx.get(url, headers={"User-Agent": "Mozilla/5.0"})
    soup = BeautifulSoup(r.text, "html.parser")
    return [el.get_text(strip=True) for el in soup.select(selector)]
```

### Rate limiting
```python
import asyncio

async def scrape_with_delay(urls: list, delay: float = 1.0):
    results = []
    for url in urls:
        results.append(await fetch(url))
        await asyncio.sleep(delay)  # Always add delay
    return results
```

---

## Rules

- Always add User-Agent header
- Always add delays between requests (min 1 second)
- Always handle rate limit errors (429) with exponential backoff
- Store raw data before processing — never lose source data
- Validate output schema before returning

---

## Output Structure

```python
{
    "source": "youtube | hh | kwork | ...",
    "fetched_at": "ISO timestamp",
    "count": N,
    "items": [...]
}
```
