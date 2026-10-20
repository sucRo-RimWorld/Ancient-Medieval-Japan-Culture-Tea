# AMJ Culture Tea — Agent Instructions

## Start here

1. Read this file and **`main:Docs/Coordination.md`** first.
2. Read [Docs/Design.md](Docs/Design.md) and the Project [AGENTS.md](https://github.com/sucRo-RimWorld/Ancient-Medieval-Japan-Project/blob/main/AGENTS.md) / [SharedRules.md](https://github.com/sucRo-RimWorld/Ancient-Medieval-Japan-Project/blob/main/Docs/SharedRules.md) before changing gameplay.
3. When changing historical description, consult [Docs/Research/PreOwnerStudy.md](Docs/Research/PreOwnerStudy.md) and the Project historical-prose procedure.

## Ownership

- This is the **optional Culture-family child Mod** `Ancient-Medieval-Japan-Culture-Tea`, analogous in grouping to Culture-Characters. It does **not** require Culture at runtime. Keep the standalone Vanilla tea/rice-kogashi route, and support optional Culture/Grains co-installation without moving existing Culture drug/Thought systems.

- Tea solely owns the tea plant/leaves, historical tea production, tea and **kogashi-yu** finished drinks, drink Recipe/Def, Joy, ingestion and local compatibility patches.
- Tea provides a **Vanilla-only** path: tea and rice-based kogashi-yu; optionally adds Grains `AMJC_Barley` as another ingredient to the **same** kogashi-yu product when Grains is installed.
- Grains owns growing/processing barley, rice and other cereal crops, and any future **edible (non-drink)** kogashi flour/food. Do not duplicate Grains' flour, edible recipes, grain texture assets or change Grains' first release.
- Parent Culture owns global cultural dining/table Thought changes, historic drug restrictions and intoxication systems. Culture Tea drinks are not drugs; keep those responsibilities separate. Environment owns biomes/biogeography; add no default tea trees to Environment.

## Entry and release gates

New production Defs/XML/C# await the Project's VE + non-VE existing-Mod implementation-necessity audit (see [ExistingModAudit](https://github.com/sucRo-RimWorld/Ancient-Medieval-Japan-Project/blob/main/Docs/Research/ExistingModAudit.md)). Prior historical research and disposable XML-only experiments are **not** shipped implementations. No Steam publication is authorized by source edits.

Implement approved features before discretionary new tests; use targeted static/build checks then the smallest final real-game acceptance, with no automatic native tests. No direct writes to `main`: topic branch → PR → confirmed checks → merge, verifying resulting SHA. Do not invent art acceptance, tested outcomes or finalized numeric balance.

## Coordination

Use only `main:Docs/Coordination.md` as the live owner-to-owner handoff/status log; do not maintain a branch-specific competing copy. Confirmed specification belongs in `Docs/Design.md` and production source when built; coordination is not a specification authority. Record cross-owner handoffs directly in the corresponding main coordination log, not through the author.
