# Wikipedia Autobiographical Promotion Detector

### **[▶ Launch the tool](https://nethahussain.github.io/wikipedia-promo-detector/)**

A client-side tool that scans Wikipedia biography articles for signals of autobiographical promotion. Enter a category name, and the tool analyses each article across five quantitative dimensions to produce a composite POV score.

---

## What it detects

| Signal | Weight | What it measures |
|---|---|---|
| **Editor Concentration** | 30% | Byte share of the top editor — flags articles largely written by one person |
| **Peacock Language** | 25% | Density of promotional terms from WP:PEACOCK and WP:WEASEL word lists |
| **Length Anomaly** | 20% | Article size relative to the category median — flags suspiciously long articles |
| **Citation Quality** | 15% | Proportion of self-published, primary, or obscure sources vs reliable ones |
| **Account Signals** | 10% | Whether the creator is a new or single-purpose account |

## Features

- **Live autocomplete** for Wikipedia category names with page counts
- **Biography filtering** — automatically skips non-biography articles using "Living people" and birth/death year categories
- **Subcategory traversal** — optional recursive scanning up to 3 levels deep
- **Sortable results table** — click any column header to re-sort
- **Expandable detail rows** — click + on any article to see full breakdown: top editors, detected peacock terms, flagged citation domains, account age
- **Configurable depth** — control max articles (up to 500) and revision analysis depth

## How it works

The tool runs entirely in the browser. It queries the [MediaWiki API](https://www.mediawiki.org/wiki/API:Main_page) in real time using `origin=*` CORS. No server, no data stored.

For each article in the selected category:

1. Fetches revision history and computes editor byte-share concentration
2. Retrieves wikitext and scans for 60+ peacock/weasel terms
3. Compares article size against the category median
4. Extracts citation URLs and checks domains against self-published and reliable source lists
5. Checks the article creator's account age and edit scope

Sub-scores are normalised to 0–1 and combined into a weighted composite.

## Interpretation

- 🔴 **≥ 65** — Strong autobiographical promotion signals
- 🟠 **40–64** — Worth a closer look
- 🟢 **< 40** — Likely organic

This is a heuristic screening tool — always verify manually before taking any editorial action.

## Limitations

- Uses revision-level byte deltas, not token-level authorship (WikiWho)
- Citation analysis checks domain patterns, not full source reliability
- Some legitimate articles about obscure-but-notable people may score high
- Rate limited by the MediaWiki API (~200 req/min for anonymous clients)

## Built with

Built by [Netha Hussain](mailto:nethahussain@gmail.com) using Claude AI Opus 4.6.

## License

MIT
