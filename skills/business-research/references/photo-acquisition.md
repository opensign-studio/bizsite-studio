# Photo Acquisition Pipeline

Battle-tested process for getting a business's real public photos into the project as files. Ordered by what actually works.

## Step 1 — Find the photo set

BestProsInTown mirrors all Google Business photos at `https://www.bestprosintown.com/<state>/<city>/<business-slug>/photos/`. The images are hosted on `localdatacdn.com` CDN subdomains. Facebook page photos are an alternative source.

## Step 2 — Extract every image URL (browser JS)

On the photos page, via the browser javascript tool:

```js
Array.from(document.querySelectorAll('img'))
  .map(i => i.src || i.dataset.src)
  .filter(s => s && s.includes('localdatacdn'))
```

**Critical detail:** each image lives on one specific subdomain (`cdn.`, `cdn2.`, `cdn3.`, …, redirecting to `s1.`, `s2.`, …). Subdomains are NOT interchangeable — fetching an image from the wrong cdnN returns 404. Keep the exact URLs.

## Step 3 — Review as a contact sheet

Replace the page body with a numbered grid to evaluate all photos in one or two screenshots:

```js
document.body.innerHTML = '<div style="display:grid;grid-template-columns:repeat(6,1fr);gap:4px">'
  + urls.map((u,i)=>`<div style="position:relative"><img src="${u}" style="width:100%;height:160px;object-fit:cover"><span style="position:absolute;top:2px;left:2px;background:#000;color:#fff;font:bold 14px sans-serif;padding:2px 6px">${i}</span></div>`).join('')
  + '</div>'; document.body.style.margin='0';
```

Screenshot, pick winners by index, check `naturalWidth/Height` of candidates (originals are often only 537–1536px — fine for web, but know what you have).

## Step 4 — Download (what works and what doesn't)

**Works (preferred):** run curl on the user's machine (Desktop Commander / Bash, wherever there is real network access):

```bash
UA="Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36"
curl -sSL -m 30 -A "$UA" -o storefront.jpg "https://cdn2.localdatacdn.com/.../original/XXXX.jpg"
```

Both flags are mandatory: `-L` (the CDN 301-redirects cdnN → sN) and the browser `-A` (default curl UA gets an HTML error page). Verify with `file *.jpg` — anything that says "HTML document" failed.

**Fails — don't waste time:**
- Browser-triggered downloads (`a.download` + blob): Chrome allows only the FIRST automatic download per site, then silently blocks the rest. Trusted-gesture clicks and fresh tabs do not reliably unblock it. eTLD+1 grouping means different subdomains share the block.
- Cross-origin `fetch()` of the images in the page: blocked by CORS (no ACAO header).
- Returning image bytes as base64 through JS tool results: blocked/truncated by the tool layer.
- Sandboxed shells usually have no general network egress (proxy 403) — that's why the download must run on the user's machine.

## Step 5 — Optimize for web (Pillow)

```python
from PIL import Image, ImageOps
im = ImageOps.exif_transpose(Image.open(src)).convert('RGB')
w,h = im.size
if max(w,h) > 1200:
    r = 1200/max(w,h); im = im.resize((round(w*r), round(h*r)), Image.LANCZOS)
im.save(out, 'JPEG', quality=85, optimize=True, progressive=True)
```

Keep originals in `assets/photos/` (git-tracked, not deployed), optimized copies in `images/` (deployed). Originals stay under the business's implicit license — these are the business's own public marketing photos being used to build the business's own site; do not reuse them for anything else.
