# Daily AI Notes — post format

A daily job publishes one note by adding **one file** on the `master` branch. The site rebuilds from that commit. Do not edit any other file.

## Path

```
_posts/YYYY-MM-DD-slug.md
```

- `YYYY-MM-DD` is the calendar day in `Asia/Kolkata`. It must match the `date` below.
- `slug` is lowercase words separated by hyphens. No spaces.
- Example: `_posts/2026-11-19-opensearch-memory-for-agents.md`

## File

```yaml
---
layout: post
title: "Short note title"
date: 2026-11-19 09:00:00 +0530
summary: "One or two sentences. This is the index card, the feed summary, and the social description."
tags:
  - agents
  - customer-experience
references:
  - title: "Source article title"
    url: "https://example.com/story"
  - title: "Second source"
    url: "https://example.com/docs"
---

A few sentences of the note itself, in Markdown. Newest posts are listed first automatically.
```

Rules:

- `title`, `date`, `summary`, `tags`, and `references` are required. Keep `layout: post`.
- Quote `title` and `summary` when they contain a colon.
- `date` must include `+0530`. A date-only value can shift the calendar day on the build clock.
- `tags` is a YAML list of strings.
- `references` is a YAML list of items with `title` and `url`. Use absolute `https://` links that you have opened.
- The filename date and the `date` field must be the same calendar day.
- A note dated today is published on the next build. The site does not hold a same-day note back when the build clock is still on the previous UTC date.
- Two notes on the same day need different slugs.
- Do not put a phone number in the note.

The sample post in the repo follows this format.

## GitHub API

Commit only that file to `master`:

```http
PUT /repos/lsdvaibhav/lsdvaibhav/contents/_posts/YYYY-MM-DD-slug.md
```

```json
{
  "message": "Add daily AI note: slug",
  "branch": "master",
  "content": "<base64 of the markdown file>"
}
```

Creating a new file omits `sha`. Updating an existing file requires the blob `sha` from `GET` on the same path.

The push to `master` runs `.github/workflows/pages.yml`, which publishes the site. No separate build commit is required.

## Where it shows up

- Index: `/notes/` (newest first)
- Post: `/notes/YYYY/MM/DD/slug/`
- Feeds: `/feed.xml` (Atom) and `/rss.xml` (RSS)
- Live site: https://lsdvaibhav.github.io/lsdvaibhav/

## Preview

```bash
bundle install
bundle exec jekyll serve
```

Open `http://127.0.0.1:4000/lsdvaibhav/`.
