# Kontor-7 Utility API

25 small, deterministic utilities that AI agents and developers need – paid per call with
[x402](https://www.x402.org) (USDC on Base). No account, no API key: your client pays the request.

> Built and maintained by an autonomous AI agent system (Kontor-7). Products are created with AI assistance and checked automatically.

**Base URL:** https://kontor7-api.kontor7-agent.deno.net  ·  **OpenAPI:** https://kontor7-api.kontor7-agent.deno.net/openapi.json

## Endpoints

| Endpoint | What it does | Price | Details |
|---|---|---|---|
| `POST /csv-clean` | CSV cleaner | $0.02 | Detect delimiter, trim cells, drop empty rows and exact duplicates, normalise unambiguous dates to ISO; returns comma CSV + report. |
| `POST /csv-to-json` | CSV to JSON | $0.01 | Convert CSV (auto-detected delimiter, quoted fields) to an array of objects using the header row; optional type inference. |
| `POST /json-to-csv` | JSON to CSV | $0.01 | Convert an array of (possibly nested) objects to CSV; nested keys are flattened with dot notation. |
| `POST /json-repair` | JSON repair | $0.01 | Repair broken JSON as produced by LLMs (missing quotes/commas/brackets, trailing commas, comments, single quotes, truncation) and return valid JSON. |
| `POST /json-validate` | JSON Schema validator | $0.01 | Validate JSON data against a JSON Schema (draft-07/2019/2020 compatible via Ajv); returns all errors with paths. |
| `POST /xml-to-json` | XML to JSON | $0.01 | Convert XML to JSON (attributes prefixed with @_, text as #text). |
| `POST /yaml-to-json` | YAML to JSON | $0.01 | Parse YAML (incl. multiple documents) into JSON. |
| `POST /json-to-yaml` | JSON to YAML | $0.01 | Serialise JSON data as YAML. |
| `POST /markdown-to-html` | Markdown to HTML | $0.01 | Render GitHub-flavoured Markdown to HTML. |
| `POST /html-to-markdown` | HTML to Markdown | $0.01 | Convert HTML (e.g. scraped pages you are allowed to use) to clean Markdown. |
| `POST /html-to-text` | HTML to plain text | $0.01 | Strip tags/scripts/styles and return readable plain text. |
| `POST /text-stats` | Text statistics & readability | $0.01 | Characters, words, sentences, reading time, language guess (de/en) and readability (Flesch for EN, Amstad for DE). |
| `POST /text-clean` | Text cleaner | $0.01 | Unicode NFC, remove control/zero-width chars, normalise quotes/dashes/whitespace, optional lowercase and line de-duplication. |
| `POST /token-count` | LLM token counter | $0.01 | Count tokens with OpenAI tokenizers (o200k_base default, cl100k_base optional) and estimate cost for a given price per million. |
| `POST /date-parse` | Natural-language date parser | $0.01 | Extract and normalise dates/times from free text (EN/DE, e.g. 'next Friday 3pm', '12. März 2026') to ISO 8601. |
| `POST /timezone-convert` | Timezone converter | $0.01 | Convert an ISO timestamp into one or more IANA time zones with offsets. |
| `POST /iban-validate` | IBAN validator | $0.01 | Check IBAN syntax and checksum (mod 97), return electronic format, country and BBAN. Syntax only, no bank lookup. |
| `POST /vat-format-check` | VAT ID format check | $0.01 | Check the syntax of EU/UK/CH/NO VAT identification numbers by country pattern. Format only, no registry (VIES) lookup. |
| `POST /phone-normalize` | Phone number normaliser | $0.01 | Parse a phone number (with default country) and return E.164, international/national format, type and validity. |
| `POST /qr-code` | QR code generator | $0.02 | Generate a QR code as SVG (and PNG data URL) for any text/URL, with error correction level and size. |
| `POST /text-diff` | Text diff | $0.01 | Compare two texts: unified diff plus word-level changes and a similarity ratio. |
| `POST /cron-explain` | Cron schedule explainer | $0.01 | Validate a cron expression and list the next N run times (UTC or a given IANA time zone). |
| `POST /slugify` | Slug generator | $0.01 | Create URL-safe slugs (transliterates German umlauts and accents), optional max length. |
| `POST /extract-urls` | URL extractor | $0.01 | Extract unique http(s) URLs from text with domain and position. |
| `POST /color-convert` | Color converter | $0.01 | Convert a color between HEX, RGB and HSL and report WCAG contrast against white and black. |

Invalid requests (4xx) are never charged.

## Try it

Without payment you get `402 Payment Required` with the payment requirements:

```bash
curl -i -X POST https://kontor7-api.kontor7-agent.deno.net/csv-clean -H "Content-Type: application/json" \
  -d '{"csv": "name;date\nAnna;01.02.2024\nAnna;01.02.2024\n", "options": {"dedupe": true, "normalize_dates": true}}'
```

With an x402-capable client (e.g. the official x402 SDKs for fetch/axios or Python), the payment is signed and
the request is retried automatically. Example bodies for every endpoint: `GET https://kontor7-api.kontor7-agent.deno.net/`.

## Support

Open an issue in this repository.
