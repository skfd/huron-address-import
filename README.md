# huron-address-import

The **Huron County checkout** of the address-import family — dataset #17 in
the onboarding pass, scaffolded 2026-08-16 by the breadth-first loop (engine
`future-work/multi-city/onboarding-queue.md`), admitted by the 2026-08-16
licence review (verbatim-verified OGL-Canada clone, in the drafted LWG
variant-review email). Status: **onboarding**. No proposal published, no
uploads made; the config is a first draft for conflation baseline runs.

The pipeline lives in the engine repo,
[`address-importer-friend`](https://github.com/skfd/address-importer-friend)
(see its README for setup). This repo carries only Huron's `config.toml`,
credentials (`.env.*`, gitignored, from the `.example` files), and — locally,
gitignored — `data/` with the OSM extract and `data/huron/tool.db`.

```bash
cd ../address-importer-friend
python run.py --city-dir ../huron-address-import
```

Source data: County of Huron `Municipal_911_Address` via the sibling
[`ontario-address-changes`](https://github.com/skfd/ontario-address-changes)
tracker (`data/huron/huron.db`, 38,312 rows / ~34,530 civic at snapshot 26,
2026-08-08 — tracker fresh AND the source is alive: rows grow weekly, the
county actively maintains the layer).

Structural facts (details in config comments): the cleanest schema in the
portfolio so far — **StreetName is typed and mixed-case** (the tracker
street is conflation-ready, a rarity), StreetNumber keeps its letter
suffixes, and 9 lower-tier municipalities ride a 100%-populated `Mun` field
that keys the collapse (Hamilton-style parcel stacks: 654 stacked groups,
deepest 174). `full` is synthesized because FullAddress is ALL-CAPS and
embeds units in reordered form ("111 ANGLESEA STREET 5 APT") — dodging both
the Guelph trap and TODO §9 at once. Tiles ride the 17 named Fire and
Emergency Response Zones (99.99% point-test; the 88-polygon Urban_Area
fabric repeated the settlement trap at 62%).

Entry state probed 2026-08-16 (`onboarding/entry-state-2026-08-16.json`):
**greenfield (NRCan import, 2018)** — 1,307 of 1,378 sampled elements last
touched by **LogicalViolinist**'s April 2018 "adding missing addresses"
NRCan import, no wiki page, no import-tagged changesets, light activity
since (carpbunker's 2018 StatCan building import; jessica-rod added a
street address 2026-08-04). `addr:city` follows the **municipality**, not
the town (North Huron 479 vs Wingham 16 in the Wingham box) — matching the
source's `Mun` field, convenient for any eventual import. Contacts:
LogicalViolinist, Matthew Darwin.

Before any production upload: LWG reply on the licence, then wiki proposal
page, forum announcement, and feedback window per the
[OSM Import Guidelines](https://wiki.openstreetmap.org/wiki/Import/Guidelines)
— Toronto's [`IMPORT_PROPOSAL.mediawiki`](https://github.com/skfd/toronto-2-address-import/blob/main/IMPORT_PROPOSAL.mediawiki)
is the template.

MIT licensed.
