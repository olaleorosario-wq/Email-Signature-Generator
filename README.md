# Email Signature Generator

A single-page builder that produces table-based HTML email signatures.

**Live:** https://olaleorosario-wq.github.io/Email-Signature-Generator/

Fill in the per-person fields, check the signature on both a light and a dark
ground, then hit **Copy signature** and paste straight into Gmail, Outlook or
Apple Mail. No build step, no dependencies — one `index.html`.

## Why HTML and not an exported image

Image-only signatures are the common mistake. Outlook and Gmail block remote
images by default for external senders, so the whole signature collapses into a
grey placeholder on first contact. Nothing is selectable or clickable, screen
readers get nothing, and a high image-to-text ratio raises the spam score.

The generated markup uses tables and inline CSS — `<style>` blocks, classes,
flexbox and grid are all stripped by Outlook's Word rendering engine and by
Gmail. Images are limited to the logo, the optional headshot and the optional
social icons, each with `alt` text and fixed `width`/`height` so the layout
still holds when images are blocked.

## Constraints worth knowing

| Constraint | Why |
|---|---|
| PNG only, never SVG | SVG doesn't render in most mail clients |
| Assets on a permanent HTTPS host | `data:` URIs are blocked by Gmail and Outlook |
| Headshot circle masked into the PNG | Outlook ignores `border-radius` |
| One wordmark file for everyone | Email can't swap an image by colour scheme |
| Under 10,000 characters | Gmail's signature limit; the builder counts live |
| Web-safe font stack | Custom brand fonts never load in mail clients |

## Before rollout

1. Confirm each social URL points at the intended account.
2. Host the PNGs on a company asset account, not an individual's — if the host
   lapses, every signature breaks at once.
3. Send a test from Outlook desktop on Windows with remote images blocked.

## Editing

Asset URLs and social links live in the `ASSETS` and `SOCIALS` objects at the
top of the inline `<script>` in `index.html`. Asset URLs are also editable from
the UI under **Hosted asset URLs**.
