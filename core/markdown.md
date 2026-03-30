# Markdown Parser

The `Markdown` class converts Markdown to HTML with built-in XSS sanitisation.

## Usage

```php
// Convert Markdown to HTML
$html = Markdown::parse($markdownText);

// Render with format detection
$html = Markdown::render($content, 'markdown');  // force Markdown
$html = Markdown::render($content, 'html');       // sanitise HTML only
$html = Markdown::render($content, 'auto');       // detect by content
```

## Supported Syntax

- Headings (`# H1` through `###### H6`)
- Bold (`**text**` or `__text__`)
- Italic (`*text*` or `_text_`)
- Strikethrough (`~~text~~`)
- Bold italic (`***text***`)
- Links (`[text](url)`)
- Images (`![alt](url)`)
- Inline code (`` `code` ``)
- Code blocks (4-space indent)
- Unordered lists (`- item` or `* item`)
- Ordered lists (`1. item`)
- Blockquotes (`> text`)
- Horizontal rules (`---`, `***`, `___`)
- Raw HTML (safe tags only)

## XSS Protection

The parser strips dangerous elements to prevent stored-XSS attacks:

**Removed tags:** `script`, `style`, `iframe`, `object`, `embed`, `applet`, `form`, `input`, `button`, `select`, `textarea`

**Removed attributes:** `onclick`, `onload`, `onerror`, and all `on*` event handlers

**Removed URLs:** `javascript:` and `data:` in `href` and `src` attributes

**Safe HTML tags** (allowed through): `div`, `table`, `p`, `ul`, `ol`, `li`, `h1`-`h6`, `a`, `img`, `strong`, `em`, `code`, `pre`, `blockquote`, `video`, `audio`, and more.

This protection mitigates the class of vulnerabilities found in Anchor CMS (CVE-2025-46041).
