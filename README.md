# Harvard Philippine Forum website

The 2026 rebuild of the HPF website (replacing https://philippineforum.weebly.com/), to live at **harvardphilippineforum.org**.

It's a plain static site: HTML pages, one stylesheet, a few lines of JavaScript. There's no build step, so you can edit any page in a text editor (or on GitHub) and Netlify publishes it.

## Pages

| File | Page |
| --- | --- |
| `index.html` | Home |
| `about.html` | What is HPF, who can join, executive board, FIND/District One |
| `culture.html` | Performances, brunches and study breaks, past performances |
| `education.html` | Speaker events, FILC |
| `j-term.html` | J-Term trip: applications, 2026 photos, 2023 and 2013 archive |
| `events.html` | Event posters and the 2025–26 recap |
| `get-involved.html` | Interest form, mailing list, Instagram, contact |
| `404.html` | Not-found page |

Images are in `assets/img/` and styles are in `assets/css/style.css`. Search the pages for `TODO` to find spots waiting on content (Cultural Rhythms 2026 video, 2026 J-Term reflections).

## Preview locally

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploy on Netlify

1. Log in to Netlify with GitHub, then go to **Add new site → Import an existing project → GitHub** and pick `chloekmm/2026hpfwebsite`.
2. Netlify reads `netlify.toml`, so leave the build command empty and the publish directory as `.`. Click **Deploy**.
3. Every push to `main` redeploys the site automatically.

`netlify.toml` also redirects the old Weebly URLs (such as `/service1.html` and `/executive-board.html`) to the matching new pages.

## Connect harvardphilippineforum.org (Namecheap)

1. In Netlify, open **Domain management → Add a domain** and enter `harvardphilippineforum.org`.
2. In Namecheap, go to **Domain List → Manage → Advanced DNS**, delete the default parking records, and add:
   - **A record**: Host `@`, Value `75.2.60.5` (Netlify's load balancer; double-check the value Netlify shows you)
   - **CNAME record**: Host `www`, Value `<your-site-name>.netlify.app`
3. Wait for DNS to propagate (minutes to a few hours). Netlify then issues a free HTTPS certificate automatically.
