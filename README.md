Source for Henry Ou's personal website: https://henryou.net.

## Preview and maintain

Run `python3 -m http.server 8765 --bind 127.0.0.1` from this directory, then open http://127.0.0.1:8765. No build or install is required. The repository root is the static document root.

Edit HTML and the shared `style.css`; follow [AGENTS.md](AGENTS.md) for content and publishing rules. `main` pushes automatically deploy through the existing Cloudflare Pages project, so preview-only work must not be pushed. Keep raw documents, drafts and test pages outside this directory. Do not create empty `writing/` or project pages.

## Logo status

University of Sydney remains text-only by Henry’s choice. Do not add a logo unless requested. Its [official logo request page](https://www.sydney.edu.au/about-us/affiliates-and-contractors/logo-requests.html) states that use requires written University approval (checked 9 September 2026). No approved asset or permission has been supplied, so no logo was copied. Once available, save the official, unmodified asset in `assets/logos/` and record its exact source and permission here; insert an image between the date and details using `class="institution-logo" width="32" height="32" alt=""` (the adjacent institution name supplies the label).

## Shared article layout

Use `.article-page`, `.article-header` and `.prose` for every article: a centred date and Writing link above the title, left-aligned body at up to 720px, 20px text (18px on phones), 1.75 line height and 24px paragraph spacing. This follows the supplied editorial spacing reference while retaining the site’s Baskerville/Chinese serif stack. Article photos use `<figure class="photo">`: full reading-column width and a shared 3:2 display ratio, with proportional centre cropping through `object-fit: cover`. Use sufficiently large originals; replace or omit undersized photos instead of mixing display sizes. Check that cropping preserves the subject. Diagrams and screenshots keep their full content using a plain `figure`. Place images beside relevant paragraphs without invented captions. Change shared CSS rather than adding per-article styles.

The first article is `writing/on-the-way/index.html`, dated 2026-02-16; its URL stays fixed if its title changes. The four local WebP photos have been resized without upscaling and stripped of metadata. Original screenshots and HEIC/JPEG files stay outside this repository. Go Review AI links to the verified repository and a read-only demo, not an online analysis service.

## HTML templates

These are maintenance snippets, not published content. Replace every `{{...}}` with real, checked content; omit unavailable links. Copy the existing Experience list item for another real experience. Wrap real Projects and Writing lists in a `.section` with an `h2`, after Experience, in that order. Do not create a section until it has a real entry.

Project entry:

```html
<ul class="project-list">
  <li>
    <h3>{{Project name}}</h3>
    <p>{{One factual sentence}}</p>
    <div class="project-links"><a href="{{Verified URL}}">Code</a></div>
  </li>
</ul>
```

Writing list (same markup for homepage latest five and complete archive; sort newest first). Use a real ISO date and display date. Do not add an All writing link on the homepage; the article metadata Writing link opens the archive.

```html
<ul class="writing-list">
  <li>
    <time class="entry-date" datetime="{{YYYY-MM-DD}}">{{Display date}}</time>
    <a href="/writing/{{stable-slug}}/">{{Title}}</a>
  </li>
</ul>
```

Archive shell — `writing/index.html` lists all real articles:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Writing — Henry Ou</title>
  <link rel="canonical" href="https://henryou.net/writing/">
  <link rel="stylesheet" href="/style.css?v=8">
</head>
<body>
  <main>
    <a class="back-link" href="/">Home</a>
    <h1>Writing</h1>
    <!-- Insert the complete real writing-list here. -->
  </main>
</body>
</html>
```

Article shell — `writing/<stable-slug>/index.html`; use the original language, a stable slug, the supplied date or actual Sydney publication date:

```html
<!doctype html>
<html lang="{{en or zh-Hans}}">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>{{Title}} — Henry Ou</title>
  <link rel="canonical" href="https://henryou.net/writing/{{stable-slug}}/">
  <link rel="stylesheet" href="/style.css?v=8">
</head>
<body>
  <main class="article-page">
    <article>
      <header class="article-header">
        <div class="article-meta">
          <time datetime="{{YYYY-MM-DD}}">{{Display date}}</time>
          <a href="/writing/" lang="en">Writing</a>
        </div>
        <h1>{{Title}}</h1>
      </header>
      <div class="prose">
        <p>{{Edited original paragraph}}</p>
        <!-- Add only elements required by the original, in their proper positions. -->
      </div>
    </article>
  </main>
</body>
</html>
```

Body elements when the original needs them:

```html
<figure class="photo">
  <img src="/assets/writing/{{stable-slug}}/{{image.webp}}" alt="{{Meaningful description}}" width="{{Original width}}" height="{{Original height}}">
  <figcaption>{{Genuine caption; omit if none}}</figcaption>
</figure>
<ul><li>{{Original list item}}</li></ul>
<blockquote><p>{{Original quotation}}</p></blockquote>
<pre tabindex="0" aria-label="Code"><code>{{HTML-escaped code}}</code></pre>
<div class="table-scroll" tabindex="0" role="region" aria-label="{{Table topic}}">
  <table>
    <caption>{{Table title}}</caption>
    <thead><tr><th scope="col">{{Column heading}}</th></tr></thead>
    <tbody><tr><td>{{Original cell}}</td></tr></tbody>
  </table>
</div>
```

To publish later: give Codex the TXT/DOCX and say “编辑后直接上线” (or “只做草稿” for preview). Codex reads and edits it, extracts/places images, creates the article, updates both lists, checks and publishes only when authorised. No real Word document has been used to validate that workflow yet.
