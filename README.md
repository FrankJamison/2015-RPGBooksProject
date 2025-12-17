# 2015 RPG Books Project

A static HTML site that catalogs a personal tabletop RPG book collection. The homepage links out to game systems (currently: D&D 3E/4E/5E placeholders and an active Pathfinder section), with thumbnail cover images and category pages.

This project is designed to be simple to host: it’s just HTML/CSS/JS + images.

## What’s in here

- A system landing page at `index.html`.
- A Pathfinder section under `Pathfinder/` with category index pages and item-list pages (for example, `Pathfinder/Adventure Paths/index.html` linking to individual Adventure Path pages).
- Shared assets under `resources/`:
  - `resources/css/style.css` – site styling.
  - `resources/js/footer.js` – writes the footer into each page.
  - `resources/images/` – cover images organized by system/category.

## Tech notes

- Pages use an XHTML 1.1 doctype and declare `charset=iso-8859-1`.
- Layout is table-based (each category page is a grid of three columns per row).
- Thumbnails are consistently rendered at `width="200" height="258"`.

## View the site locally

Because this site uses relative paths (and some folders include spaces), the most reliable way to view it is through a small local static file server.

### Option A: Python (recommended)

From the project root:

```bash
python -m http.server 8000
```

Then open:

- `http://127.0.0.1:8000/index.html`

### Option B: Open the HTML file directly

You can also open `index.html` directly in a browser (double-click), but some browsers handle spaces/encoding in paths more reliably when served over HTTP.

## Content organization

### Root

- `index.html` – main entry point with system tiles.
- `DnD3E/`, `DnD4E/`, `DnD5E/` – currently contain images and “Coming Soon” placeholders.

### Pathfinder

- `Pathfinder/index.html` – Pathfinder landing page.
- `Pathfinder/Core Rulebooks/index.html` – category index (currently present).
- `Pathfinder/Adventure Paths/index.html` – Adventure Paths index.
- `Pathfinder/Adventure Paths/[###-###] <Name>.html` – a page listing all items for a specific Adventure Path.
- `Pathfinder/Campaign Settings/index.html` – category index (currently present).

### Images

Images are stored under `resources/images/pathfinder/…` and mirrored by category name, for example:

- `resources/images/pathfinder/core rulebooks/…`
- `resources/images/pathfinder/adventure paths/[001-006] Rise of the Runelords/…`

File naming commonly includes bracketed product codes and ranges (examples you’ll see throughout the project):

- `[PZO1110] …`
- `[001-006] …`

## Editing / adding content

This site is intentionally “manual HTML”: adding books is typically a matter of adding an image, then adding a new table cell block linking to it.

### Add a new thumbnail tile to a category index

1. Add the cover image under the appropriate folder in `resources/images/…`.
2. Edit the category index page (for example, `Pathfinder/Adventure Paths/index.html`).
3. Add a new `<td>` block following the existing pattern.

A typical tile looks like this:

```html
<td style="width:33%">
  <div class="splitcontentleft">
    <h2>Display Title</h2>
    <h3>&nbsp;</h3>
    <div class="box">
      <a href="Some Page.html" title="Descriptive title">
        <img src="../../resources/images/pathfinder/.../cover.jpg"
             alt="Alt text" width="200" height="258" />
      </a>
    </div>
  </div>
</td>
```

### Add a new item to an Adventure Path page

Adventure Path pages (for example, `Pathfinder/Adventure Paths/[001-006] Rise of the Runelords.html`) use the same 3-column table layout.

1. Put the image in the matching Adventure Path image folder under `resources/images/pathfinder/adventure paths/<AP folder>/…`.
2. Add a new `<td>` block with:
   - `<h2>` for the item name/number.
   - `<h3>` for the product code.
   - `<a href="…" target="_blank">` if you want the tile to open an external document.

### Filename + link hygiene (important)

- Prefer avoiding `&` in *new* filenames (use `and` instead). In HTML/XHTML, `&` is a reserved character and can cause link parsing/validation issues.
- Spaces in filenames/folders work in many browsers, but if you see broken images, try serving the site via a local server (see “View the site locally”).
- Keep paths relative and consistent with neighboring pages (most pages reference shared assets with `../` or `../../`).

## Styling

The site uses the shared stylesheet at `resources/css/style.css`. If you change layout/styling, try to keep these stable conventions so existing pages remain consistent:

- 3-column grid via a table
- `div.box` wrapping each thumbnail
- thumbnail size `200×258`

## Footer

The footer is injected by JavaScript:

- `resources/js/footer.js`

If you need to change footer text/links, do it in that one file.

## Known gaps

- D&D 3E/4E/5E sections are marked “Coming Soon” and currently link to `#` placeholders.
- Several Pathfinder nav links (Modules/Companions/Society/Misc) are present in the UI but not fully wired up everywhere.
- Page `<meta name="description">` and `<meta name="keywords">` are still template placeholders.

## Credits

- Template/CSS is based on “YourHost” (Ken Dahlin) and “andreas08” (Andreas Viklund), as referenced in `resources/css/style.css`.
- Footer text/credits are defined in `resources/js/footer.js`.
