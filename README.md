# KharidoProducts

**Hostel se hostel, seedha deal.** A marketplace for students to buy and sell second-hand items between hostels: books, cycles, heaters, calculators, room gear and more.

## Features

- **Browse** listings with search, category chips, a hostel filter and sorting by price or newest
- **Sell** an item with a title, price (₹), condition, a negotiable flag, a description and up to 3 photos (resized in the browser before upload)
- **Buy requests**: make an offer and suggest a pick-up time; the seller accepts (the item becomes *Reserved*) or declines
- **My listings**: mark items Available / Reserved / Sold, edit or delete them
- **Hostel profile**: hostel, room and an optional WhatsApp number, with a one-tap WhatsApp button for contacting the other person
- Light and dark themes, mobile-friendly layout

## How it runs

`index.html` is a single self-contained page (HTML, CSS and JavaScript, no build step).

It currently keeps shared data (listings, photos, requests) through the **claude.ai artifact runtime** (`window.claude.use("db")` and `window.claude.use("user")`). That means:

- On claude.ai the page works fully: <https://claude.ai/artifact/XCLkHRNYmmqnJueKDh5S75>
- Opened anywhere else (locally, or on GitHub Pages) the page loads and shows a notice, but listings won't appear until it's connected to a backend.

### Data model

| Path | Contents | Who can write |
|---|---|---|
| `sellers/<userId>` | `profile` (hostel, room, phone), `items[]`, `responses{requestId: accepted/declined}` | that user (owner can moderate) |
| `images/<userId>/pics/<itemId>-<n>` | one compressed JPEG data URL per photo | that user |
| `requests/<userId>` | `list[]` of buy requests sent by that user | that user |

To host it independently, swap the `db` and `user` calls for a backend such as Firebase (Firestore + Auth) or Supabase. The data model above maps directly onto Firestore collections.

## Running locally

Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
```
