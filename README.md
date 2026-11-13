# Pre-Send Preference Checker (prototype)

Prototype for The Date Crew Product Growth Assessment.

**Live demo:** https://rajakarigohi.github.io/tdc-preference-checker/

**Problem:** about 35% of rejected profiles are rejected for reasons the client had already stated in their preferences. Those shares are avoidable.

**Idea:** before a matchmaker emails a profile, check it against the client's structured preferences. Profiles that break a deal-breaker are blocked with the reason shown; the rest are ranked by fit.

## What the prototype does

1. **Check profiles before sending**
   - Pick a client and see their preferences, each marked *Deal-breaker* or *Flexible*.
   - The shortlist is checked with deterministic rules: `Pass` or `Blocked` with the exact reason.
   - Passing profiles are ranked by a fit score (share of flexible preferences met).
   - A blocked profile can still be sent, but only with a written reason, which is logged.
2. **Tag rejection feedback**
   - Paste a client's free-text rejection.
   - The tool returns a category, whether that reason was already in the client's preferences, and a suggested action.

## Run it

No build step and no dependencies. Open `index.html` in a browser.

## Notes and limits

- All data is mocked and every person is fictional.
- The rejection tagger uses keyword rules as a stand-in. In the real solution this step is an LLM call that returns JSON in the same shape (`categories`, `already_stated`).
- Not included: real client data, Gmail integration, authentication, persistence.

## Code map

Everything is in `index.html`:

- `CLIENTS`, `POOL` – mock data
- `RULES` – one check per preference field
- `checkProfile(profile, client)` – returns blocked / reasons / fit score
- `rankPool(pool, client)` – orders the shortlist
- `tagFeedback(text, client)` – categorises a rejection and flags already-stated reasons
