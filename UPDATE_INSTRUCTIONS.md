# Clarity — automatic article analysis patch

## What changed
- Clicking **Examine story** now immediately calls `/api/analyse` and displays the analysis report on that story’s page.
- The report distinguishes publisher feed preview from an entire article, so no unearned truth score appears.
- It extracts candidate factual assertions and language signals even if optional AI/API keys are missing.
- A **Analyse full text** button allows a permitted article extract to be pasted for deeper review.
- API or service failures are displayed visibly instead of silently presenting an empty report.

## Update on GitHub without deleting the repository
You only need to replace **two existing files**:
1. `public/app.js`
2. `server.mjs`

On GitHub: navigate to each file, select **Edit this file** (pencil icon), replace its content with the content of the corresponding file in this ZIP, then **Commit changes**. Alternatively use GitHub Desktop to sync the entire updated folder, which replaces files at matching paths and keeps the same Vercel connection. GitHub’s web upload tool is awkward for overwriting files.

Once committed, Vercel automatically redeploys (if connected). Open a headline and click **Examine story**. It should show an analysis report automatically.

### Important next steps
This patch does **not** grant full text rights or independently verify every claim. AI text analysis requires the `OPENAI_API_KEY` server environment variable; evidence search requires `BRAVE_SEARCH_API_KEY`; published fact-check retrieval requires `GOOGLE_FACTCHECK_API_KEY`. Add keys in Vercel > Project Settings > Environment Variables (never commit secrets to GitHub). Without those, the app still performs a basic claim/wording scan and openly marks unsupported conclusions as unverified. Human evidence evaluation and evidence-source quality review remain essential before showing trust scores.
