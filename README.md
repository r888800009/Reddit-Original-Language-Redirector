# Reddit Original Language Redirector

A tiny Chrome extension that prevents Reddit links containing `?tl=zh-hant` from opening in Reddit's translated Traditional Chinese view.

When a Reddit page URL contains `tl=zh-hant`, the extension redirects the top-level page navigation by:

1. removing the `tl` query parameter, and
2. adding or replacing `show=original`.

Example:

```text
https://www.reddit.com/r/example/comments/abc123/title/?tl=zh-hant
```

becomes:

```text
https://www.reddit.com/r/example/comments/abc123/title/?show=original
```

## Purpose

The purpose of this extension is to avoid Reddit translating content into Cantonese or other unwanted zh-Hant translated output, and to show the original Reddit page instead.

It is intentionally small and uses the minimum permissions needed to do this safely.

## Privacy and permissions

This extension follows a least-privilege design:

- Uses Manifest V3.
- Uses `declarativeNetRequestWithHostAccess` instead of reading page content.
- Only requests host access for Reddit URLs:
  - `https://reddit.com/*`
  - `https://*.reddit.com/*`
- Only acts on top-level Reddit page navigations.
- Does not use content scripts.
- Does not use a background service worker.
- Does not use `tabs`, `storage`, `cookies`, or `webRequest`.
- Does not collect, store, transmit, or inspect browsing data.

The extension only declares one static redirect rule in `rules/reddit-original-language.json`.

## Files

```text
manifest.json
rules/reddit-original-language.json
README.md
```

## Install locally

1. Unzip this package.
2. Open Chrome and go to `chrome://extensions/`.
3. Enable **Developer mode**.
4. Click **Load unpacked**.
5. Select the unzipped extension folder.

## Test

Open a Reddit URL containing `tl=zh-hant`, for example:

```text
https://www.reddit.com/r/example/comments/abc123/title/?tl=zh-hant
```

Chrome should redirect it to the same Reddit URL with `tl` removed and `show=original` added.

## Design notes

This extension uses a static Declarative Net Request rule because it is more privacy-preserving than intercepting requests with JavaScript. The browser performs the redirect based on the packaged rule, so the extension does not need to read the page, access Reddit content, or run code on Reddit pages.
