# rippers-names

The first Rippers Unmasked Foundry VTT module. **Content only — no code.** It ships the campaign's
name registries as compendium packs so the GM can roll or browse them in-table, and it establishes
the reusable module scaffold (`module.json` + `src/packs/*` one-JSON-per-document + `npm run pack`
→ LevelDB) that the later Rippers plugins copy.

Layers on the **Project FU** system (`projectfu`), Foundry **v13**. A personal-table module —
original Rippers content, **not for redistribution**, and it ships **no** Project FU or Fabula Ultima
content.

## Packs

| Pack | Type | Contents |
|---|---|---|
| **Lodge Recruiters** (`recruiters`) | RollTable | `1d8` over the eight Lodge members a new character may name as recruiter (Hesketh, Threlfall, Fugo, Vane, Ashe, Wray, Chapel, Johann). The ninth option is always "Someone else" (free text). |
| **Name & Pronunciation Registry** (`name-registry`) | JournalEntry | One journal, 8 browsable pages: How-to-use, London, The Lodge, The Spine Cast, The Medjay, The Irish Thread, The Deck, The Vocabulary — respelled pronunciations with the ✓ / • / ⚠ confidence marks. |

Source content: `lodge-docs/NAMES-pronunciation.md` and the recruiter roster in `lodge-docs/PLAYER-GUIDE-full.md`.

## Build

```
npm install       # once — pulls @foundryvtt/foundryvtt-cli
npm run pack      # compiles src/packs/<pack>/*.json  ->  packs/<pack> (LevelDB)
npm run unpack    # reverse: packs/<pack>  ->  src/packs/<pack>/*.json
```

Edit the JSON under `src/packs/`, re-run `npm run pack`, and the LevelDB packs re-derive. `packs/`
(the built LevelDB) and `node_modules/` are build output — not committed.

## Install (personal table)

Copy this folder into your Foundry `Data/modules/` directory (as `rippers-names`, with the built
`packs/`), then enable it in your Project FU world. The RollTable and Journal appear in their
compendium sidebars. First-load note: the RollTable result and Journal-page shapes target v13;
verify once on first open (Foundry migrates any legacy fields automatically).

## Scaffold reuse (plugins 2–4)

Copy `module.json`, `package.json`, and `tools/pack.mjs` / `tools/unpack.mjs` verbatim; change the
`id`, `title`, `packs[]`, and drop new one-JSON-per-document sources under `src/packs/`. For Item/Actor
packs (classes, skills, heroics) add `"system": "projectfu"` to each pack entry so items validate
against FU's data models.
