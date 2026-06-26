============================================================
 DEPLOY ON VERCEL — app + multi-index TRI fetcher
============================================================

Folder layout:
  index.html            <- the app (rename of cashflow-simple.html)
  api/benchtri.js       <- server-side fetcher for EXACT Nifty TRI (any index)
  vercel.json           <- (optional) config

Why a function: niftyindices.com blocks browser scripts (CORS). The function runs
on Vercel's server, where that block doesn't apply, and returns clean JSON. The app
calls /api/benchtri automatically.

------------------------------------------------------------
 STEP 1 — rename
------------------------------------------------------------
Rename  cashflow-simple.html  ->  index.html  in this folder.

------------------------------------------------------------
 STEP 2 — deploy (pick one)
------------------------------------------------------------
EASIEST (CLI):
  1. Install once:   npm i -g vercel
  2. In this folder: vercel
  3. Follow prompts (accept defaults). It gives you a live URL.
  4. For production:  vercel --prod

OR (Git):
  1. Push this folder to a GitHub repo.
  2. vercel.com -> Add New -> Project -> import the repo -> Deploy.
  Every push auto-redeploys.

------------------------------------------------------------
 STEP 3 — test the function
------------------------------------------------------------
Open in a browser:
  https://YOUR-APP.vercel.app/api/benchtri?index=NIFTY%2050%20TRI&start=01-Jan-2020
You should see JSON with a "series" list. Try other indices too:
  ...?index=NIFTY%20500%20TRI
  ...?index=NIFTY%20SMALLCAP%20250%20TRI

------------------------------------------------------------
 STEP 4 — use it
------------------------------------------------------------
Open the app -> Portfolio -> Dashboard -> "Portfolio vs Benchmark".
Pick an index from the dropdown (Nifty 50 / 500 / Smallcap 250 / Midcap 150 ...)
and tap "Fetch". Badge shows "Exact <index>" when the function works.

Supported indices in the dropdown:
  Nifty 50 TRI, Nifty Next 50 TRI, Nifty 100 TRI, Nifty 200 TRI, Nifty 500 TRI,
  Nifty Midcap 150 TRI, Nifty Midcap 50 TRI, Nifty Smallcap 250 TRI,
  Nifty Smallcap 100 TRI, Nifty MidSmallcap 400 TRI

------------------------------------------------------------
 IF AN INDEX RETURNS {"error": ...}
------------------------------------------------------------
The index name must match niftyindices exactly. If one fails, the others may still
work. Tell me which index errored and I'll fix its name/params. (For Nifty 500 only,
the app falls back to an index-fund proxy so the card still shows something.)

You can always upload a TRI CSV (from niftyindices.com -> Historical Data) with the
"CSV" button as an exact override for the selected index.
