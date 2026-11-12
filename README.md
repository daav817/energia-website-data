# energia-website-data

Source data for two pages on energiapower.llc:

- `pjm-capacity.json` — PJM Base Residual Auction (BRA) results shown on /tools/capacity-explainer
- `energy-choice-states.json` — electricity / natural gas retail choice status by state, shown on /tools/deregulation-guide

A weekly Claude routine updates these files. Every Monday a workflow in the
website repo downloads them, validates every field, and opens a pull request
there for human review. **Nothing here goes live until a person merges that PR.**

## Format rules (enforced by the website's validator — anything else is rejected)

### pjm-capacity.json
- Keys: `lastUpdated` (YYYY-MM-DD), `nextAuction` (≤300 chars, may be ""), `auctions`, `commentary` (≤4 paragraphs, ≤700 chars each), `sources` (≤400 chars).
- `auctions`: consecutive delivery years in ascending order; never remove an existing year. Each entry:
  `deliveryYear` ("2028/29"), `period` (always "Jun–May"), `priceMwDay` (number, RTO-wide clearing price in $/MW-day),
  `auctionDate` (YYYY-MM-DD the results were posted), `note` (≤120 chars, may be "").

### energy-choice-states.json
- Keys: `lastUpdated` (YYYY-MM-DD), `asOf` ("November 2026"), `sources` (≤400 chars), `states`.
- `states`: exactly the 50 states + "Washington D.C.", once each, sorted alphabetically. Each entry:
  `state`, `elecStatus` (≤20 chars), `elecType` ("full" | "limited" | "regulated"), `elecSince` ("1999" or "—"),
  `gasStatus` (≤20 chars), `gasType` ("full" | "limited" | "regulated"), `note` (≤220 chars).

### All text fields
Plain sentences only: no links/URLs, email addresses, phone numbers, or the characters `< { } \` and backtick.
