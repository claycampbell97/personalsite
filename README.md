# personalsite

clay's personal site. Plain HTML + one stylesheet: no framework, no build step, no JS.

```
site/
  index.html      about (the front page)
  projects.html   stuff i've made
  photos.html     photography
  books.html
  movies.html
  games.html
  404.html
  style.css       all styling; colors are variables at the top
  favicon.svg
wrangler.jsonc    tells Cloudflare to serve ./site
```

## editing

Open a page, replace the `[bracketed]` placeholders, commit, push. Cloudflare redeploys on push.

- **Add a tab:** copy a page (say `games.html` → `music.html`), then add
  `<li><a href="/music">music</a></li>` to the `<ul class="tabs">` in **every** page,
  and move `aria-current="page"` to the new tab in the new file.
- **List entries** (books/movies/games/projects) use the same shape:
  ```html
  <li>
    <span class="r">★★★★☆</span>
    <div><cite>Title</cite> — Author
      <span class="note">one line</span></div>
  </li>
  ```
- **Photos:** put images in `site/photos/` and use the commented-out `.gallery` block in `photos.html`.
- **Colors:** change the variables in `:root` at the top of `style.css`. Dark mode has its own block just below.
- Update the "last updated" date in the footers when you feel like it.

## preview locally

```
npx serve site
```
(`serve` handles clean URLs like `/books`; opening the files directly in a browser won't follow the tab links.)

## deploy (Cloudflare)

1. **Domain:** dash.cloudflare.com → Domain Registration → Register Domains → buy the domain.
2. **Site:** Workers & Pages → Create → Import a repository → pick `personalsite`.
   Leave the build command empty; the deploy command `npx wrangler deploy` reads `wrangler.jsonc`.
   Production branch: `main`.
3. **Hook up the domain:** open the new worker → Settings → Domains & Routes → Add → Custom domain →
   enter the domain. Add `www.` the same way if you want it.

Every push to `main` redeploys in about 30 seconds.
