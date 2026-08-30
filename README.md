# AppADay #115 — Basket Ledger

A grocery price tracker. Log what you bought, what it cost, and where, and Basket Ledger turns that running log into a price trend chart per item and a ranked list of which store runs cheapest overall.

**Live app:** https://augustineiacopelli.github.io/appaday-115-basket-ledger/
**Portfolio:** https://augustineiacopelli.github.io/appaday/

## What it does

- Scan a receipt: take or upload a photo, and Claude reads off the store, date, and each item's price. Results land in an editable review list, so nothing is added to the ledger until you confirm it.
- Log a price manually: item name, price, store, and date.
- Price over time: pick any logged item from a dropdown and see a Chart.js line chart of its price across every store, once at least two prices are logged for that item.
- Store averages: a ranked, price-tag styled list showing the average price per logged entry at each store, cheapest first.
- Full entry list: a toggleable list of every entry with a delete button on each row.

## How it works

Single `index.html` file, no build step, no frameworks. All ledger data lives in `localStorage` under one key holding an array of entry objects, with every read and write wrapped in try/catch so the app degrades gracefully if storage is unavailable. Items and stores are grouped using a trimmed, lowercased key so "Milk" and "milk" are treated as the same item, while the original casing is preserved for display.

The receipt scanner is AI-powered. A chosen photo is downscaled client-side on a canvas, sent as an image to the Claude API along with a prompt asking for store, date, and a structured item and price list, and the response is parsed and shown for review before anything is saved. The app calls the API directly from the browser using a personal Anthropic API key, entered through the Settings modal in the header and stored only in this browser's local storage under its own key, separate from ledger data. The key is never shown anywhere else in the app.

## Stack

HTML, CSS, and vanilla JavaScript, with Chart.js (via CDN) for the trend chart, the Claude API for receipt reading, and Google Fonts (Big Shoulders Display, IBM Plex Mono, IBM Plex Sans) for type.

## Category

Data (D), AI-powered

---

Part of [AppADay](https://augustineiacopelli.github.io/appaday/) — one complete, functional, mobile-friendly web app shipped every day.
