# Ancient & Medieval Japan — Culture Tea / 中世日本 - 文化・茶

**Owner:** [Ancient-Medieval-Japan-Culture-Tea](https://github.com/sucRo-RimWorld/Ancient-Medieval-Japan-Culture-Tea)  
**Owner classification (2026-10-20 author revision):** Culture-family child `Culture-Tea`, like Culture-Characters. Independent optional runtime; **no hard dependency** on Culture, Grains or MO. `Culture-Tea` owns both tea and kogashi-yu drink Defs/Recipes/Joy; Culture core keeps existing drugs, tobacco/alcohol policies and global table/Thought behavior. Existing tea `AMJT_*` Def names remain stable; pre-release packageId is now `sucro.ancientmedievaljapan.culture.tea`. The repository rename is not evidence of 1.6/1.7 validation.

**Decision date:** 2026-10-20. **State:** scope accepted; initial XML source exists but is not yet accepted as loaded/gameplay-tested. Numeric values and graphics are provisional.  
**Historical evidence and superseded experiments:** [PreOwnerStudy](Research/PreOwnerStudy.md). This file is the **current specification**, not the older candidate's status text.

## 2026-10-20 author-approved caffeine rule — excess tea only

**This is the current decision and supersedes conflicting v1 no-Hediff/no-Rest-effect exclusions below.** Tea remains **non-drug** (not a chemical, DrugCategory or DrugPolicy item), has no addiction, tolerance, dependency, withdrawal, caffeine Need, stimulant boosts or ordinary Rest restoration. However, repeated tea consumption within a short span may temporarily **lower sleep recovery efficiency**, not forcibly prevent sleep. Kogashi-yu has **no caffeine effect**. If powdered tea is implemented later, the same rule applies to its drink rather than a separate addiction system; powdered tea itself is not added by this change.

**Small XML-only implementation / explicitly provisional tuning (standard BodySize=1 pawn):** each cup of `AMJT_BoiledTea` adds 0.35 severity to temporary non-addictive `AMJT_TeaCaffeineLoad`. A hidden 0..0.9 stage has **no effect**; at 0.9 or more (usually **three cups within roughly 2–3 in-game hours**) a visible stage applies `RestRateMultiplier -0.15` during sleep, approximately 15% less rest gain at baseline. Severity naturally falls **1.4 per game day**, and Hediff disappears at zero. The penalty ends when severity falls below 0.9, even though the hidden harmless remainder persists for a short time. Maximum severity 1.4 prevents any additional escalating effect. No positive awake effects, mood penalty, medical disease or custom C# tick required. These numerical thresholds are **implementation candidates**, not play-balance acceptance.

**Game acceptance remains pending:** inspect actual 1.6 XML load, ingestion outcome + severity merge/decay, 1/2/3 servings with elapsed time, sleep recovery only above threshold, no drug handling and no penalty for kogashi-yu. No game-run PASS is claimed; API expectations below were corroborated from older decompiled code only, not the actual installed 1.6 assemblies.

## 1. Purpose and v1 scope

Provide **exactly two modest everyday consumables**, `茶` (historically prepared tea) and `こがし湯` (grain flour toasted and stirred into hot water), as **non-drug** sources of small recreation. Preserve historical Japanese production without a drug/addiction system, dependency, withdrawal, positive stimulant/Rest buffs, strong mood boosts or emergency mental-break rescue. Repeated tea consumption alone has the narrowly approved transient sleep penalty described above.

This is a **Culture-series independent child Mod**, not an embedded module of Culture. Neither Grains, Culture, MO, Environment nor VE is a required runtime dependency. Do not add modern bottled/cold barley tea, coffee, black tea, matcha ceremonies, tea rooms, caffeine needs, new water need, addiction policy, medical/health buffs or extensive variant recipes. Do not relabel RimWorld's psychite tea as ordinary tea.

## 2. Finished goods and recipes

| Output | Source | Minimum processing | Nutrition / recreation |
|---|---|---|---|
| **茶** | Tea shrub → fresh tea leaves → dried heated leaves | Harvest regenerating shrub; heat/dry leaves (one Bill); boil prepared tea (one Bill) | **Not a food/energy source**; small recreation |
| **こがし湯** | **Vanilla `RawRice`**; with Grains also edible `AMJC_Barley` | **Toast grain → grind → mix flour into water**, abstractable as **one** existing-stove/campfire cooking Bill | **Small positive nutrition** reflecting swallowed toasted flour, plus small recreation |

`こがし湯` is a **single** finished ThingDef/recipe whose allowed ingredients are extended conditionally. Never multiply drink products/Bills for each supported grain. Vanilla rice ensures the drink remains possible without Grains; do not create duplicate Tea-side barley, rice or a fallback barley crop.

The definite first two grain types are **rice and barley only**. Wheat, awa, hie, kibi, soba and other grains require individual historical evidence and actual Def compatibility before inclusion. An external barley Mod may receive optional support only after confirming its real ingredient ThingDef and processing stage; matching label text does not authorize broad food filters. Do not require VE content or ship a VE compatibility patch. No indiscriminate reuse of **unroasted** Grains `AMJC_BarleyFlour` as finished kogashi.

**Eating kogashi flour / plain edible toasted-grain food belongs to [Grains](https://github.com/sucRo-RimWorld/Ancient-Medieval-Japan-Grains/blob/main/Docs/Design.md), not Tea**, and is a future Grains scope outside its first-release nine dishes. The Tea drink's own recipe may abstract flour preparation; do not duplicate a separate edible grain product. **Author-approved processing split gate (2026-10-21):** Keep the current single direct `RawRice` or optional `AMJC_Barley` → `AMJT_KogashiYu` Cooking Bill; roasting, grinding, and mixing with hot water are abstracted within that one task. Do **not** introduce a separate roasted-grain item, roasting Bill, or standalone kogashi intermediate just for the low-effect drink. When Grains later develops actual confectionery/edible kogashi, reconsider a distinct `こがし` intermediate **only if a demonstrated shared ingredient is useful for multiple meaningful outputs and outweighs extra labor, Bills, storage and compatibility complexity**. Adding just one sweet does not automatically justify splitting the chain. If such a Grains-owned ingredient is eventually approved, Culture Tea still owns the drink and must retain its Vanilla-only rice-based direct route when Grains is absent; in Grains-enabled configurations prefer one coherent production path rather than simultaneously exposing redundant finished-drink Bills. Preserve existing Def names and evaluate migration/stock/ingredient handling before any production change. No intermediate, sweets, recipe or numeric change is approved for v1 by this design decision.

## 3. Historical boundaries

- Early Japanese tea includes boiling leaves; Song-derived powder/whisked tea appears later and coexists with boiling tea. Modern steeped sencha and standard tea-bag/cold tea are not automatically appropriate for the entire AMJ time span.
- Historical `こがし` includes **roasted grain powders involving rice and barley**; the 1587 Kitano tea-gathering allowed `こがし` as a substitute for tea. This is not proof that all cereal grains were interchangeable.
- **Kogashi-yu is consumed with the actual flour**, unlike later barley-kernel extract `麦湯` or modern clear `麦茶`. Those later drinks are **not** v1 products.
- Early tea's circulation differs by century, class and region. Do not imply all peasants consumed it equally since antiquity. No global wild tea spawning without ecology/historical review.

## 4. Gameplay and integration contract

- Manual right-click drinking and ordinary **voluntary** recreational ingestion should work. Prefer Vanilla Def/Recipe/Joy pathways before C#/Harmony/novel Jobs; do not require DrugPolicy, chemical-drug comps or a custom need.
- Ordinary hunger/job selection must **not** treat tea or kogashi-yu as staple meals. Nevertheless, kogashi-yu needs a **positive** nutrition value consistent with swallowed grain; a technical micro-nutrition experiment is not an accepted final balance value.
- Both give **small, saturating recreation**, with no addiction/withdrawal, chemical drug category, strong Thoughts, Rest restoration, working-speed buffs or built-in food-poisoning risk. The **sole exception to the old no-Hediff rule** is the hidden cumulative tea status becoming a short sleep-rest penalty after overconsumption; it is not a drug or addiction.
- Tea plant remains after harvesting and can be harvested again, subject to growth/work. Use existing plant mechanisms where feasible; do not confer magic blight immunity.
- Use existing low-tech fire/cooking benches where viable; no mandatory special tea building, MO mill or research just for this module. Preparations/finished drinks should be distinguishable in stockpiles and UI. Dried tea is storable, finished drinks should not become indefinite stores.
- **Culture** owns general `AteWithoutTable` interpretation. Tea must not copy its global Thought patch. Verify standalone eating/drinking behavior independently.
- **Environment** owns habitat/biome changes; optional natural tea distribution requires evidence and separate alignment.
- Compatibility with unrelated drinks Mods is not guaranteed. Preserve normal coexistence unless a demonstrated conflict justifies a narrow patch.

## 5. Pending implementation details / non-approvals

1. Complete VE **and** non-VE current-source / dependencies / license / era and finished-Def prior-art audit, with Project's entry-decision record; the pre-owner comparison is evidence, **not** a completed implementation gate.
2. Verify actual RimWorld 1.6 Vanilla `RawRice` and existing `JoyGiver_Ingest` / food classes; choose a non-drug, zero-drug-Comp ingestion design and two-harvest plant design. Historical one-off XML prototypes are superseded.
3. Choose proportionate numbers: tea and kogashi nutrition, ingredient quantities, Joy, work cost, spoilage, plant days and value. These are **not yet final**. Do not inherit prototype `Nutrition=0` for kogashi.
4. Create source files/required Japanese+English labels/art only when implementation entry is cleared and art is accepted. Independently prove loaded Defs, rice and optional barley Bills, manual/voluntary drinking, health absence, and repeat harvest.
5. Run minimal consolidated 1.6 Vanilla and Tea+Grains acceptance. 1.7 compatibility is not presumed. No automatic expensive test runs or publication.

## 6. Current XML implementation (2026-10-20; unverified candidate)

The Tea repository now contains **source XML**, not a released or game-tested Mod: `About/About.xml`, `Defs/ThingDefs/TeaPlants.xml`, `Defs/ThingDefs/TeaItems.xml`, `Defs/RecipeDefs/TeaRecipes.xml`, `Patches/TeaJoy.xml`, `Patches/GrainsBarley.xml`, and Japanese ThingDef/RecipeDef translations. Existing-Mod decision evidence is `Docs/Research/ExistingDrinksAudit.md` and `Docs/Research/ExistingModDecision.json`.

- **Plant contract:** `AMJT_TeaPlant` has `harvestAfterGrowth=0.45` and `harvestMinGrowth=0.75`, following the game's documented non-destructive plant harvest logic; 12 nominal growDays, 6 leaves per harvest. Two-harvest in-game behavior is **unverified**.
- **Tea Bill:** 5 fresh leaves => 5 dried; 2 dried leaves => 1 cup of `AMJT_BoiledTea`. `Nutrition=0.01` is an ingestion/UI technical placeholder only, **not** intended as useful sustenance; `joy=0.08`. No drug category, CompProperties_Drug or mood effects. The later author-approved tea-only temporary overconsumption Hediff and negative sleeping efficiency effect supersede the initial no-Hediff/rest specification.
- **Kogashi-yu Bill:** three Vanilla `RawRice` => one `AMJT_KogashiYu`; same recipe accepts Grains `AMJC_Barley` through an exact-display-name conditional patch. `Nutrition=0.05`, `joy=0.06`. These values are **provisional**, not balance approval.
- **Work / storage placeholders:** Cooking bills `workAmount=250, 180, 230`; drinks rot after 2 days, fresh leaves after 6 days. Low-tech Vanilla `Campfire`, `FueledStove`, `ElectricStove` only.
- **Joy:** existing Vanilla `EatChocolate` giver is patched to include the two drink Defs. This avoids drug policies but needs actual loaded-game confirmation. Positive micro-nutrition for tea permits gear-tab consumption under the legacy `IsNutritionGivingIngestible` contract; confirm on 1.6 before release.
- **Images:** product XML references **unapproved temporary Vanilla texPaths**, not finished Tea graphics. Do not distribute as an art-complete or accepted subscriber package.
- **Not tested:** source Def resolution, XML patches, jobs/Bills, ingredient filters, two tea harvests, actual consumption, table Thought, Joy saturation, no unwanted food poisoning, original graphic paths, any 1.7 behavior. A static structure review is not a RimWorld PASS.

All material implementation decisions must be reconciled with the accepted drink boundary and newer author-approved caffeine rule; graphics and numerical balance remain unaccepted for publication.
