# Clarity — update GitHub and deploy on Vercel

You already uploaded Clarity to a private GitHub repository and opened the Vercel New Project screen. Leave that screen open for now.

## Update GitHub

1. Open your existing `clarity-news` GitHub repository and select **Add file → Upload files**.
2. Unzip `clarity_vercel_ready.zip` locally, open its folder and select all its contents.
3. Drag those contents to the GitHub upload page. GitHub will display new files under `api/`, a new `vercel.json`, and replacements such as `server.mjs`.
4. If GitHub displays a conflict or doesn't allow overwriting a file via the upload page, stop. Use GitHub's file edit option for `server.mjs` or GitHub Desktop to commit the updated folder. Do not create duplicate nested folders.
5. Commit the changes to `main` with message `Add Vercel deployment support`.

## Back in Vercel

1. Keep project name `clarity-news`, Root Directory `./`, and the Node preset.
2. The included `vercel.json` tells Vercel to publish the `public` directory and compile serverless API functions from `api/`.
3. Do not add API keys yet. Click **Deploy** to test a limited demo/beta.
4. Visit the new site's homepage and `/api/health`.
5. If a build fails, copy the error text (without secrets) back into ChatGPT.

## Expectations

The homepage and limited candidate-claim analysis can work without paid APIs. RSS availability depends on publishers. Comprehensive full-text verification and reliable numerical scores are **not** ready; those require licensed text access, evidence review, persistent storage, and safeguards before public promotion.
