# NoTrack — Strip Tracking from URLs

Every link you click is stuffed with hidden parameters that track who you are, where you came from, and what you clicked. NoTrack strips them in your browser. Nothing is sent anywhere.

---

## How it works

Paste a URL. NoTrack parses it client-side, identifies known tracking parameters, removes them, and gives you a clean link. Auto-cleans on paste.

The URL never leaves your browser. There is no backend.

---

## Privacy Architecture

NoTrack is built around a single guarantee: **your URLs are never transmitted anywhere**.

This is enforced at multiple levels:

1. **Client-side only** — All parsing happens in JavaScript in your browser. No server, no API, no database.
2. **`connect-src 'none'` CSP header** — Even if malicious code were somehow injected, the browser blocks all outbound network connections. Your URLs are literally unable to leave the page.
3. **`form-action 'none'`** — Forms cannot submit data to any endpoint.
4. **No third-party scripts** — Only Google Fonts CSS (no JS). Zero analytics, zero tracking pixels, zero telemetry.
5. **Static hosting only** — There is no backend, no server-side code, no database.

---

## What Gets Stripped

* **Google:** gclid, gclsrc, gbraid, wbraid, dclid, _ga, _gl, _gac
* **Meta / Facebook:** fbclid, fb_action_ids, fb_action_types, fb_ref, fb_source, fbc, fbp
* **UTM (all platforms):** utm_source, utm_medium, utm_campaign, utm_content, utm_term, utm_id
* **Microsoft:** msclkid
* **Twitter / X:** twclid, twsrc, twgr, twcamp, twcon
* **TikTok:** ttclid, tt_medium, tt_content
* **LinkedIn:** li_fat_id, li_lean_id
* **Instagram:** igshid, ig_mid, ig_rid
* **Mailchimp:** mc_eid, mc_cid
* **HubSpot:** _hsenc, _hsmi, hsa_cam, hsa_grp, hsa_mt, hsa_src, hsa_ad, hsa_acc, hsa_net
* **Marketo:** mkt_tok
* **Yandex:** yclid, _openstat
* **General:** ref, source, click_id, campaign_id, ad_id, zanpid, oly_enc_id, vero_id, s_cid, s_kwcid, irclickid, irgwc, and more

100+ tracking parameters covered.

---

## Security Headers (vercel.json)

| Header | Value | Purpose |
|--------|-------|---------|
| `Content-Security-Policy` | `connect-src 'none'; form-action 'none'; frame-ancestors 'none'` | Blocks all outbound requests, form submissions, and embedding |
| `Permissions-Policy` | `camera=(), microphone=(), geolocation=()` | Denies hardware access |
| `Referrer-Policy` | `no-referrer` | No data leaked via referer |
| `Strict-Transport-Security` | `max-age=63072000; includeSubDomains; preload` | HTTPS only, 2 years |
| `Cross-Origin-Embedder-Policy` | `require-corp` | Prevents cross-origin data leakage |
| `Cross-Origin-Opener-Policy` | `same-origin` | Isolates browsing context |
| `X-Frame-Options` | `DENY` | Cannot be iframed / clickjacked |
| `X-Content-Type-Options` | `nosniff` | MIME type cannot be overridden |

---

## Deploy to Vercel

1. Fork or clone this repo
2. Go to [vercel.com](https://vercel.com) → New Project
3. Import your GitHub repo
4. Click **Deploy**

No build step. No framework. Just static HTML.

---

## Local Development

```
open index.html
```

Or:

```
npx serve .
```

---

## Project Structure

```
notrack/
├── index.html      # Entire app — single file, no dependencies
├── vercel.json     # Deployment config + security headers
├── LICENSE         # MIT
└── README.md       # This file
```

---

## License

MIT — free to use, modify, and deploy.

---

Made by [@gitpushnico](https://github.com/gitpushnico)
