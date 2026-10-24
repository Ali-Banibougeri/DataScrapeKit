# Contributing to DataScrapeKit

DataScrapeKit is intended to make Persian-language web data collection easier to maintain and reuse. Contributions are welcome, especially focused crawler improvements, better text cleaning, clearer documentation, and reproducible bug reports.

## Before opening a pull request

1. **Keep changes focused.** Prefer one crawler, parser, or documentation concern per pull request.
2. **Describe the result.** Explain the problem, what changed, and how you checked it.
3. **Protect collected data.** Do not commit scraped datasets, personal information, cookies, credentials, API keys, or local database files.
4. **Respect data sources.** Review the source website's terms, robots.txt, applicable law, and any licensing or attribution requirements before collecting or redistributing content.
5. **Be considerate with requests.** Use reasonable concurrency and delays. Stop when a source signals that access is not allowed; do not bypass authentication, CAPTCHAs, access controls, or rate limits.

## Adding a crawler

The project README describes a crawler as a module that returns a list of article-like records. Keep its output consistent with the documented shape:

```python
{
    "url": "...",
    "title": "...",
    "content": "...",
    "published_at": "..."
}
```

- Use stable, descriptive field names.
- Handle missing titles, empty content, and absent publication dates gracefully.
- Keep source-specific parsing inside the source's own crawler instead of mixing it into shared cleaning or storage utilities.
- Avoid hard-coding credentials or machine-specific paths.
- Document source-specific configuration and any limitations.

## Local checks

Install the dependencies documented in `README.md`:

```bash
pip install -r requirements.txt
```

Before submitting, run the relevant crawler against a small, permitted sample and check that:

- the returned records have the expected fields;
- empty or malformed pages do not crash the run;
- repeated pages or records are handled sensibly;
- request pacing and failure handling are reasonable; and
- generated databases and scraped output are not included in the diff.

If automated tests are added to the project, include tests for new parsing and cleaning behavior and run them before opening the pull request.

## Pull request checklist

- [ ] The change has one clear purpose.
- [ ] The README or configuration examples are updated when behavior changes.
- [ ] I have tested the change or explained why testing was not possible.
- [ ] No secrets, personal data, or scraped output are included.
- [ ] The change respects the source website and describes any material limitations.

For bugs and feature ideas, open an issue in this repository with a concise reproduction or use case.
