# Meridian — AI Operations Workbench

Meridian is a static demonstration of an AI data-annotation workbench and an automation testing lab. The catalog review queue contains **150 individually named cosmetic products** across 15 families, including cleansers, serums, moisturizers, sunscreens, toners, lip color, mascara, shampoo, conditioner, hand cream, cleansing balms, eye creams, face masks, and lip balms. Each product record includes a SKU, GTIN, lot, packaging, ingredient list, use directions, suitability, claims, taxonomy proposal, and a generated catalog illustration.

## Product review workflow

1. Open **Product taxonomy v3** and select an item from the 150-item queue.
2. Inspect the product illustration, front-of-pack label, and detailed catalog record.
3. Confirm the model’s proposed taxonomy label, change it using the taxonomy selector, or escalate an unclear item.
4. Choose confidence and submit. Category changes and escalations require a short evidence-based rationale. The queue records the decision, reports whether it matches the synthetic reference label, and advances to the next pending item.
5. Use queue filters to revisit reviewed records. **Reset progress** clears the local demo queue.

## Work ticket workflow

Open a ticket directly from a product review or create one from **Work tickets**. Record an issue type, summary, detailed evidence, linked SKU, priority, and assignee. Move tickets through Open → In progress → Resolved → Closed, add internal handoff notes, review the activity history, and reopen a closed ticket if the issue returns. Filter active, resolved, and closed work. Ticket data persists in this browser.

Queue decisions and ticket records persist in the current browser using local storage. The 150 catalog images are distinct, locally generated SVG studio packshots, one per SKU. Each includes package geometry, product identity, brand, family, net contents, SKU, lot, reflections, and studio lighting details. The app builds each SVG from catalog metadata and embeds it directly in the image URL, so a separate asset folder, API key, or remote image host is not required. Optional standalone copies can be regenerated offline with `node work/generate-product-packshots.cjs`. These are polished vector representations rather than photographs and work under GitHub Pages project subpaths.

The overview's label accuracy is calculated from the trainee's submitted category decisions against the sample reference labels. It starts as pending until at least one category decision is scored; skipped and escalated items are excluded from that accuracy calculation.

## Checkout QA lab

The test area contains a self-contained browser storefront fixture. The eight-check runner clicks the fixture's product, cart, promotion, shipping, guest-checkout, and order controls, then asserts the rendered browser state. Build 184 starts with two behavior defects: the SAVE10 promotion does not reduce the subtotal (a $48.00 item should become $43.20), and the confirmation screen does not wait for the order-created event. Apply either or both scoped fixture patches and rerun the same journey to see which assertions pass. Recent run results are retained in this browser.

The fixture runs entirely in the browser. It does not submit a real order, reach a live storefront, run Playwright, or change a production app. It is an executable QA training fixture rather than a connected staging pipeline.

## Workflow safeguards

Resetting annotation progress now opens a confirmation dialog that reports how many completed decisions will be cleared. Category changes and escalations require at least 20 characters of rationale; the rationale is saved with the browser-local review record. Queue, ticket, and QA text use a larger minimum type scale, and the annotation layout uses one tablet and one mobile breakpoint plan.

## Run and deploy

Open `index.html` in a modern browser; no build step is needed. To publish free with GitHub Pages, add the project files at the root of a GitHub repository, then select **Settings → Pages → Deploy from a branch → main → /(root)**.

This is a front-end training application. It has no authentication, live product data, production storefront, or server-side work capture. All brands and catalog records are fictional.

## Server-side review preparation

The `supabase/` folder contains a not-yet-connected backend scaffold for authenticated submissions, private answer keys, ticket/workflow data, and reviewer PDF reports. The current site remains in local demo mode until a Supabase project is configured and the front end is wired to it. Follow [the backend setup guide](supabase/README.md) before enabling scored assignments. Do not publish the private reference seed or use the current client-side answer key for blind assessment.


