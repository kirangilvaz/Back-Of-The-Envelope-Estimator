# Back-of-the-Envelope Estimations

A single-file calculator for quick capacity math: API traffic, database storage, and cache memory.

## Getting started

Double-click `index.html`. That's it — no install, no server, no internet needed.

Everything recalculates as you type. Number fields accept shorthand: `500k`, `10M`, `1.2B`.

## API Traffic

Enter reads/day, writes/day, the payload size for read APIs and write APIs, and a peak multiplier (defaults to 5×, use the −/+ buttons).

You get back:

- **Read QPS / Write QPS** — requests per day ÷ 86,400
- **Total QPS** — read QPS + write QPS
- **Peak QPS** — total QPS × the peak multiplier
- **Bandwidth table** — read, write, total, and peak rows in bytes/s, Mbps, Gbps, Tbps, and Pbps

## Database Storage

Enter how much data one write stores and how many writes happen per day. Leave the *Use writes/day from API section* box checked to reuse the number you already typed above.

You get storage totals for 1 day, 30 days, 1 year, and 5 years. This ignores indexes, replication, and compression.

## Cache Memory (80/20)

Pick a working set from the dropdown — 1 day, 30 days, 1 year, or 5 years of database data — or choose **Custom value** to type your own size.

Memory needed = working set × the hot data share (20% by default). Set the RAM per cache node to also see how many nodes that takes.

## Units

Sizes use binary units (1 KB = 1024 B). Network rates use decimal bits (1 Mbps = 1,000,000 bits/s, 8 bits per byte). All results are rounded to 2 decimals.

---

**Note on Save / Load / Reset**

- **Save** writes all your inputs to a JSON file. The first time, a file picker appears — save it as `boe-estimations.json` next to `index.html`. After that, Save overwrites that same file silently. In browsers without file-write support (Firefox, Safari), it downloads the file instead.
- **Load** opens a saved JSON file and fills every field back in. Saving afterwards overwrites the file you just loaded.
- **Reset** clears everything back to the default values, after a confirmation prompt. It does not touch your saved JSON file.

Your inputs are also cached in the browser, so a plain refresh restores your last session without needing to load a file.
