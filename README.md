# Clarity — evidence-first news reader

A deployable, responsive web-app foundation for a politically neutral, evidence-led news publication. Designed for a non-coding founder. **It is not a licensed universal news archive or an automated truth oracle.**

## Start it in 3 steps

1. Install **Node.js 22 or newer** from https://nodejs.org.
2. Open a terminal in this folder and run `npm start`.
3. Visit **http://localhost:3000**.

There are **no dependencies to install**. The feed attempts live public RSS headlines immediately. Publisher availability depends on network connectivity and feed access. If no feeds can be read, a clearly identified demonstration headline is shown.

To run automated tests: `npm test`.

## Optional integrations

Make a copy of `.env.example` named `.env`, then paste in keys for:

- `GNEWS_API_KEY`: broader headlines and metadata subject to GNews rights and licensing. https://docs.gnews.io/
- `GOOGLE_FACTCHECK_API_KEY`: existing published ClaimReview fact checks retrieved through Google's Fact Check Tools API. https://developers.google.com/fact-check/tools/api/reference/rest/v1alpha1/claims/search
- `BRAVE_SEARCH_API_KEY`: linked web-search evidence candidates, not independently verified sources. https://api.search.brave.com/
- `OPENAI_API_KEY`: optional AI-assisted summaries, framing and claim review. The model may only link to supplied retrieved URLs; no AI-generated independent verdicts. https://platform.openai.com/docs/

All keys are stored server-side, never placed in the browser. Restart the server after changing keys. No provider account or API keys have been provisioned for you. Provider billing, usage restrictions and licence permissions are your responsibility.

## What works now

- Live-feed aggregation through a list of publisher RSS endpoints; feed-availability diagnostics; optional GNews headlines; search/filter/refresh; story details and source links.
- Reader-pasted text analysis, conservative checkable-claim extraction, language-cue tagging; independent separate sections for facts, sourcing, context, language, framing and author disclosures.
- Optional retrieval of existing published fact-check reports and web-search leads; optional AI-assisted synthesis with source-URL allowlisting.
- Exports individual analysis as JSON; source provenance, limited article coverage and uncertain/unknown state displayed.
- Public methodology page; mobile-responsive layout; no paywall bypass; no publisher full-text copying.

## Critical limitations

**No automatic 0–100 truth score is issued in this version.** All six dimensions and the overall score show *Not assessed* unless a sufficiently evidence-backed, accountable review pipeline is implemented. This is intentional: plausible-looking algorithmic numbers would undermine the editorial mission. An AI model and third-party snippets alone cannot verify exact claims or detect meaningful omissions across full articles.

**No universal access to news articles.** Every major mainstream outlet cannot be accessed lawfully as full text without explicit publisher permissions, commercial licences or approved APIs. This app ingests metadata and excerpts from feeds only. RSS URLs may stop working without notice. Sources with no suitable RSS, such as Reuters/AP in the starter configuration, require a licensed data supplier. Some Google News links may redirect through the aggregator. A product that republishes substantial articles typically requires rights review.

**No claim-level in-text highlighting of publisher-protected full articles.** Claim cards appear for user-supplied text. Adding accurate inline span ranges for licensed full text is a next milestone; do not imply an article has been fully analysed when only the headline or an excerpt is accessible.

**No documented political stance determination without external evidence.** The system does not infer authors' affiliations or ideology from word choice or demographics. A properly sourced disclosures registry and transparent appeals process would be required before this is displayed.

**No production-grade review workflow yet.** Production needs authenticated editors, source snapshots/archiving rights, independent claim adjudication, review sign-off, an immutable audit trail, published scoring rules, corrections, community appeals, bias audits, handling breaking stories and defamation/legal review.

**Security before public deployment:** add external rate limits and request quotas, privacy/consent policies, TLS and production hosting, monitoring, persistent storage, admin authentication, paid API usage controls, threat modelling, editorial oversight, abuse protection, legal and licensing review. Current JSON analysis results live only in server memory and reset on restart. Avoid submitting personal or confidential text.

## Planned credible 100-point methodology (not implemented as an automatic score)

Give each assessed dimension a **separate coverage and confidence indicator**. For claims, require source links with exact matching quotations/data, a date, search retrieval timestamp, reviewer notes and a right of appeal. For context, independently check missing denominators, timeframes, counterexamples and quoted uncertainty. Language and framing are signals only and must not mechanically imply falsehood. Disclosed conflicts of interest may inform transparency without acting as a political penalty. Publish composite scores only after the scoring formula, thresholds, inter-reviewer reproducibility and calibration have been independently tested. If there is inadequate evidence, display **Not assessed**, not zero.

## Proposed next delivery phases

1. Rights/licensing and publisher partner selection; robust feeds/API integration (BBC, Guardian, Sky, tabloids, FT, Reuters/AP via agreements).
2. Production database, retrieval queues, editorial review panel, primary document citations and reproducible evidence bundles.
3. Licensed full-text parsing with precise highlighted spans and human-verified claims; display verified fraction of article.
4. Calibrate scores on a labelled corpus across differently oriented outlets, independent double-blind reviewers, appeal procedures and open corrections.
5. Account management, deployment, analytics, accessibility and commercial product launch.

## Included files

`server.mjs` — Node web server, feed adapters, conservative analysis and API.
`public/index.html` — app interface.
`public/app.js` — feed and article interaction, analysis report.
`public/styles.css` — responsive design.
`server.test.mjs` — automated tests.
`previous-prototype.html` — original demo snapshot.

### Published service/API references

- BBC main news RSS: https://feeds.bbci.co.uk/news/rss.xml
- Guardian Open Platform access: https://open-platform.theguardian.com/access/
- Google Fact Check Tools API: https://developers.google.com/fact-check/tools/api/
- GNews docs: https://docs.gnews.io/

This app is a substantial functional MVP foundation, **not yet a fully verified, universal live-article fact-checking service**. Not all publisher feeds or legal reuse rights are guaranteed.

## Deploy to the internet (when ready)

The included `render.yaml` is a starting blueprint for Render web hosting; `Dockerfile` is an alternative for Docker-compatible hosts. You will need your own hosting account and a code repository to deploy them. This code has not been deployed to a public URL, and hosting services may change free-tier support. Before public launch, implement the production safeguards and editorial review pipeline listed above.

## Vercel deployment (Clarity UK beta)

This package includes native Vercel functions in `api/` and `vercel.json`. No local Node server needs to stay running on Vercel. Keep **Application Preset: Node**, **Root Directory: `./`**, and set the **Output Directory to `public`** if Vercel doesn't read `vercel.json` automatically. After GitHub receives these updated files, Vercel will deploy the static interface and API endpoints together.

**Important:** Do not upload ZIP as a single GitHub file. Replace `server.mjs` and upload the **contents** of the `api/` directory and `vercel.json`; existing files in `public/` may remain unchanged. Avoid uploading `.env` or secret keys.

Smoke checks after deployment: `https://YOURDOMAIN.vercel.app/api/health` should return `{ "ok": true, ... }`. The homepage should load without missing styles, and the feed should show either current publisher headlines or a clearly labelled demo fallback with feed errors. The `Analyse` tab should detect candidate claims without inventing a truth score.

**Caution:** This is an early, publicly viewable beta — *not production ready*. Because there is no account-level rate limiting or usage quota, do not activate chargeable API keys for an unrestricted public deployment until a rate limiter, usage caps, and abuse controls exist. The free/Hobby Vercel plan may restrict commercial usage; check the current plan terms before any commercial launch. News APIs and publisher licences are not included in your hosting budget.

Vercel functions are ephemeral: the current in-memory article map and review records may disappear between requests or deployments. Persistent storage is not yet included. Live feed items appear on the homepage because the feed response includes the entire story metadata, but `/api/article/:id` may return 404 on a different function instance until persistent storage or a shared cache is added.

The Vercel dynamic article route is under `api/article/[id].mjs`. No API key is required to demonstrate the feed and conservative candidate-claim scan.
