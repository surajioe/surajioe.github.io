# Blog — Claude Instructions

## When adding a new blog post

When the user asks to add a new page or blog post, follow these steps in order:

### 1. Create the HTML file

Place the new `.html` file in the project root. Follow the visual style established in `async_python_blog.html`:
- Dark theme CSS variables (`--bg`, `--surface`, `--border`, `--accent`, `--text`, `--text-dim`, `--text-bright`)
- Fonts: Playfair Display (headings), DM Sans (body), IBM Plex Mono (code, labels, meta)
- Chapter-based structure with `<div class="chapter">` and `<div class="chapter-number">Chapter 0N</div>`
- Header with grid background, glow effects, category tag, `<h1>`, subtitle, and metadata strip
- Hand-applied syntax highlighting in code blocks using spans: `.code-keyword`, `.code-fn`, `.code-comment`, `.code-string`, `.code-number`, `.code-highlight`
- A "← Back" link in the header area pointing to `index.html`
- Footer with a one-line description of the post topic
### 2. Validate dates in the HTML file

Before indexing, grep the file for any year or date references (e.g. `2025`, `January 2026`) and verify each matches today's date. Update any stale ones. This step applies whether Claude created the file or the user did.

### 3. Categorize the post

Assign the post to one of these categories based on its primary topic:

| Category | Covers |
|----------|--------|
| **Python** | Language internals, asyncio, stdlib, libraries, CPython behavior, performance |
| **Systems** | OS internals, networking, databases, infrastructure, concurrency at the system level, Linux/Unix, compilers |
| **Software** | Architecture, design patterns, engineering practices, tooling, debugging, career |

If the post genuinely doesn't fit any of these, introduce a new category with a short, clear name. Do this sparingly.

### 4. Update `index.html`

- Add a post card for the new post under the correct `<section class="category">` block.
- If the category doesn't exist yet, create a new section (see layout rules below).
- Each post card must include: title, excerpt (1–2 sentences), at least one tag, and the publication date.
- Within each category, sort posts newest first.

### 5. Update the header description in `index.html`

The `<header>` of `index.html` contains a short description line:

```html
<p>Writing about Python, systems and software.</p>
```

If a new category was introduced that isn't already reflected in this line, update it to naturally include the new theme. Keep it to one short sentence. Examples:
- Adding a "Security" category → "Writing about Python, systems, software and security."
- The existing three categories are already covered — no change needed.

---

## `index.html` layout rules

**Header**
- Author name as `<h1>` using Playfair Display
- One-line description of blog themes as `<p>`
- No navigation links — the index is the home page

**Body — category sections**
- One `<section class="category">` per category
- Each section starts with a `.section-label` (e.g. `Python`, `Systems`)
- Post cards are stacked vertically inside `.posts-list`
- No sidebar, no pagination, no infinite scroll

**Post card structure**
```html
<a href="post-filename.html" class="post-card">
  <div class="post-card-meta">
    <span class="tag">CategoryTag</span>
    <span class="post-date">Month YYYY</span>
  </div>
  <h2>Post Title</h2>
  <p>One or two sentence excerpt describing what the post covers.</p>
</a>
```

**Category ordering in index.html**
Order sections: Python → Systems → Software → any new categories alphabetically.

---

## Post file naming

Use lowercase, hyphen-separated names that match the post topic:
- `async-python-concurrency.html` ✓
- `linux-memory-model.html` ✓
- `MyNewPost.html` ✗
