# Notion ChatGPT Widget — Netlify Deploy Guide

What I changed
- Split the single file into:
  - index.html (frontend widget)
  - netlify/functions/chat.js (serverless function)
  - netlify.toml (Netlify build & headers)
- The function now handles OPTIONS preflight (CORS), returns consistent JSON responses, and includes an X-Frame-Options header so the widget can be embedded in Notion.

Deploy steps
1. Add these files to the repository root and commit.
2. On Netlify, connect the repository and deploy. Netlify will auto-detect and deploy the site (no build command required).
3. In your Netlify site settings, under "Site settings → Build & deploy → Environment", add:
   - `OPENAI_API_KEY` with your OpenAI API key.
4. (Optional) If you prefer a different model, edit `netlify/functions/chat.js` and change the `model` field (note: availability depends on your OpenAI plan).
5. Embed the published site URL into Notion using the Embed block (Notion requires that the page allows framing; netlify.toml includes header settings for that).

Security notes
- Do NOT commit your OpenAI API key to the repo.
- Consider adding rate limiting, request validation, and authentication if you plan to make the endpoint public.

If you want, I can:
- Add a simple package.json for local testing with Netlify CLI.
- Switch the function to use the `gpt-4o-mini` model (or attempt a fallback strategy).
- Create a minimal form-based authentication or token check so only your Notion embeds can use the function.
