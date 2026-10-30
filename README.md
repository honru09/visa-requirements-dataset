# Visa Requirements Dataset — every passport × every destination

A machine-readable matrix of visa requirements for ordinary passports: **199 passports × 199 destinations = 39,402 routes**, each with a requirement status and, where the official source states one, a maximum stay.

Maintained by [visafreely.com](https://visafreely.com), where every route also has a human-readable page (e.g. [Japan passport → Cape Verde](https://visafreely.com/visa/japan/cape-verde/)).

## What makes this dataset different

Most visa datasets are scraped once and go stale quietly. This one is being **re-verified destination by destination against primary official sources** — government gazettes, immigration authorities, foreign ministries — with the source named on every verified row.

Current state (release of **2026-10-30**):

| | |
|---|---|
| Total routes | 39,402 |
| Individually verified against an official source | **9,664** (24.5%) |
| Corrections applied to the seed data so far | 3,887 |
| Destinations fully verified | 58 of 199 |

Unverified rows carry the seed value and are marked `verified = false`. They are a starting point, not a claim. The verification queue is worked in the open: progress, corrections and sources are published in the [data changelog](https://visafreely.com/changelog/), and regime-level changes are tracked on the [visa policy changes](https://visafreely.com/visa-policy-changes/) page.

## Files

- `visa-requirements.csv` — the full matrix, one row per route.
- `visa-requirements.json` — the same data as a JSON array.

## Columns

| Column | Meaning |
|---|---|
| `passport_code` / `passport` | ISO 3166-1 alpha-2 code and name of the passport country (plus HK/MO as separate passport entries) |
| `destination_code` / `destination` | Code and name of the destination |
| `status` | One of: `visa free`, `visa on arrival`, `e-visa`, `eta`, `visa required`, `no admission` |
| `max_stay_days` | Maximum stay in days as published by the official source; empty when the source publishes none |
| `verified` | `true` if this route was individually checked against the named official source |
| `last_verified` | Date of that check (verified rows only) |
| `source_url` / `source_name` | The official source behind the verification (verified rows only) |

Scope: ordinary passports, short tourist/short-visit entry. Work, study, residence and diplomatic/official passports follow different rules and are out of scope.

## Methodology, briefly

For each destination, the governing official texts are read first-hand (the exemption table, the gazette order, the e-Visa portal's own terms). A route is marked verified only when an official source settles both its status and — where one exists — its duration. Where official texts state no duration, `max_stay_days` is left empty rather than filled from aggregators. Full notes per destination are kept in the visafreely data-quality backlog.

## Provenance and licence

The seed layer derives from the open [passport-index-dataset](https://github.com/ilyankou/passport-index-dataset) (MIT), snapshot February 2026. The verification layer — corrections, verified flags, sources and dates — is original work by visafreely.

- Verification layer: **CC BY 4.0** — use it, credit visafreely.com.
- Seed portions remain under the upstream MIT licence.

## Caveats

Visa rules change constantly; a row is a statement about its source on its `last_verified` date (or about the February 2026 seed snapshot if unverified). Always confirm with the destination's official source before travelling. Found an error? The pair pages on visafreely.com name the source behind every verified claim, which makes mistakes easy to pin down — issues and pull requests are welcome.
