# New Prokect on Storelib

This repository is linked to a Storelib site. Each file in `sections/` is one
section of the site, written in the Storelib Builder Framework.

## How changes reach the site

1. Change or add a file named `sections/<type>.storelib` (lower case, digits,
   `_` and `-`).
2. Commit and push to `main`.
3. Storelib compiles every changed section file and saves it to the site as a
   draft. A builder that is open shows it within a few seconds, and a new
   section is placed on the page being edited.
4. The commit gets a status named "Storelib": green when every file compiled,
   red with the first error when one did not. A file that does not compile is
   not saved; fix it and push again.
5. Nothing is live until the creator presses Publish in the builder.

Only `sections/*.storelib` is read. Other files in this repository are yours
and Storelib ignores them. Deleting a section file here does not remove the
section from the site, because a page may be using it.

## Writing a section

The full reference is at https://storelib.com/developers, and all of it as one
text file is at https://storelib.com/llms-full.txt. Read it before writing.
The rules that are refused most often:

- A section file has `<template>`, `<style scoped>`, `<schema>` and an
  optional `<script>`. The template language is `{{ }}`, `{% if %}`,
  `{% for %}` and filters. It is not Vue, React, JSX or Liquid.
- Every name the template or CSS reads must be declared in the schema.
- Colours come from `--scheme-*` variables and the root reads
  `data-scheme="{{ settings.color_scheme }}"`.
- Links built from a setting go through `| url`.
- The schema's `name` must not be the name of another section on the site.

## Writing for this website

A section should look and read like the rest of New Prokect, not like a
template. Before writing one:

- Use the site's colour schemes through `var(--scheme-*)` and its type
  styles. Never introduce a new palette or font.
- Write copy about what the site really sells, in its own voice. Never invent
  a product, a price, a discount or a review.
- Products reach a section as `products` (title, formatted price, picture,
  page URL). Link a card to `{{ block.settings.url | url }}`, or straight
  to checkout with `/checkout?productId={{ block.id }}&src=website`.
- Never build a payment form or load a payment or tracking script. Storelib
  checkout takes the payment.

The whole of that is at https://storelib.com/developers/selling.
