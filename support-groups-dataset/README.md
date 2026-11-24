# PASD Support Groups Dataset

A cleaned dataset of the Parkinson's Association of San Diego (PASD) support groups, plus a simple map, built for the Biokind Analytics x PASD Events & Services Map.

## Files

| File | What it is |
|---|---|
| `pasd_support_groups.csv` | The dataset: 21 support groups, one per row (includes the `SITE_CATEGORIES` column). |
| `pasd_support_groups_scraper.ipynb` | Beginner-friendly Google Colab notebook that walks through the scrape and cleaning steps. |
| `support-group-map.html` | A standalone map of the groups. Open it in any browser. |

## Method

1. **Scrape.** Group listings were collected from the PASD "Search for Support Groups" page (https://parkinsonsassociation.org/search-for-support-groups/) with a small JavaScript snippet run in the browser, and the same logic is reproduced in Python in the notebook.
2. **Clean with regex.** Raw text was split into fields (venue, street address, ZIP, city) and the meeting schedule was parsed into `FREQUENCY_CLEAN`, `DAY_OF_WEEK`, `WEEK_OF_MONTH` and `TIME_LOCAL` using regular expressions. The original text is kept in `FREQUENCY_RAW`. Zoom groups use `virtual` as the address.
3. **Geocode.** In-person addresses were turned into latitude/longitude (`LAT`, `LON`) using OpenStreetMap (Nominatim).

## Things to double-check

- **Inferred ZIP codes.** Some listings had no ZIP, so it was inferred from the address. Those rows are flagged with "verify" in `NOTES` and should be confirmed with PASD.
- **Chula Vista Central** (First United Methodist Church, 1200 E H St, Chula Vista 91910, contact Anna Silsbee) is a new group not yet on the website. Its meeting schedule is **TBD** and needs to come from PASD.
- Other rows may have small notes in `NOTES` (for example, a mismatched contact email).

## Columns

`EVENT_NAME, GROUP_ORG, EVENT_TYPE, VENUE_NAME, STREET_ADDRESS, ZIP_CODE, CITY, STATE, FREQUENCY_RAW, FREQUENCY_CLEAN, DAY_OF_WEEK, WEEK_OF_MONTH, TIME_LOCAL, FORMAT, AUDIENCE, SITE_CATEGORIES, LANGUAGE, REGION, CONTACT_NAME, CONTACT_PHONE, CONTACT_EMAIL, LAT, LON, SOURCE, NOTES`
