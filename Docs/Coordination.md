# AMJ Culture Tea Coordination — main only

## CULTURE-TEA-OWNER-RENAMED-20261020 — author-directed child Mod identity

**Owner:** `sucRo-RimWorld/Ancient-Medieval-Japan-Culture-Tea`; rename integrated by [Culture Tea PR #5](https://github.com/sucRo-RimWorld/Ancient-Medieval-Japan-Culture-Tea/pull/5), main `edf4ac5e4c0d86a1da74c8be48f0f98708d21aee`. This entry supersedes the old repository-name and packageId mentions below, not the old feature history.

- Culture Tea is an **optional standalone Culture-family child** like Culture-Characters. Culture core is **not** a hard runtime dependency. If present, load the child after Culture; Grains remains optional as an extra barley input.
- PackageId before publication: `sucro.ancientmedievaljapan.culture.tea`; display name Culture Tea. All `AMJT_*` ThingDef/RecipeDef IDs unchanged. No published/validated saves under the older packageId are known.
- [Current Tea specification](https://github.com/sucRo-RimWorld/Ancient-Medieval-Japan-Culture-Tea/blob/main/Docs/Design.md), parent [Culture boundary](https://github.com/sucRo-RimWorld/Ancient-Medieval-Japan-Culture/blob/main/Docs/Design.md), [Grains edible kogashi boundary](https://github.com/sucRo-RimWorld/Ancient-Medieval-Japan-Grains/blob/main/Docs/Design.md), and [Project owner pointers](https://github.com/sucRo-RimWorld/Ancient-Medieval-Japan-Project/blob/main/Docs/Roadmap.md) have been aligned. No additional code gameplay, graphics or native acceptance was completed by rename.
- **Next work:** original Tea test acceptance and implementation completeness, particularly actual two-drink load, reharvest, bills, ingestion and original art. Do not revisit the settled ownership split unless an observed conflict requires it.


## TEA-V1-XML-SOURCE-20261020 — two drinks source implemented; native acceptance pending

**Owner:** `sucRo-RimWorld/Ancient-Medieval-Japan-Tea`. **Source main:** `26b198bd0dc8f1bc70d3b3a39f9db1a241963149` ([Tea PR #2](https://github.com/sucRo-RimWorld/Ancient-Medieval-Japan-Tea/pull/2)). **State:** first XML source integrated, **not game-tested or publication ready**.

- **Implemented source:** `About/About.xml`; renewable tea shrub `AMJT_TeaPlant` (using `harvestAfterGrowth=0.45`), fresh/dried leaves, boiled tea, `AMJT_KogashiYu`, three low-tech Cooking Bills, optional Grains barley from `AMJC_Barley` into the **one same** kogashi drink recipe, optional 1.6 `EatChocolate` JoyGiver patch, Japanese labels/descriptions. Tea and kogashi-yu remain non-drug; no chemical drug classes, comp, needs or buffs.
- **Prior-art gate evidence:** `Docs/Research/ExistingDrinksAudit.md` and `Docs/Research/ExistingModDecision.json`, comparing 1.6 VE and non-VE source and Erin's public contents. Decision is narrow standalone implementation. **Project script `validate_rule_contract.py --decision` was not run in a checked-out local Project/Tea workspace**; the branch received direct structured-field, XML tag-stack, Def uniqueness and non-drug marker review, not the official validator's PASS. Finish official validation before treating the implementation entry gate as fully verified.
- **Source static checks:** 8 XML well-formedness-like tag/ampersand scans passed; 8 expected owned defNames present, duplicate0; RawRice and conditional barley refs present; DrugComp/DrugCategory references0 in own ingestibles. These tests do **not** load RimWorld Defs or establish actual in-game workability.
- **Provisional values:** tea `Nutrition=0.01` purely to allow ordinary manual/inventory ingestion without becoming a food source; kogashi-yu `0.05`; recreation `0.08/0.06`, growDays12, ingredient counts/work/rot times as captured in `Docs/Design.md`. None are final approved balance.
- **Temporary Vanilla texPaths:** graphical assets are not accepted; no original Tea image files exist. Do not advertise visuals as finished. Source is not a release candidate.
- **Next concrete acceptance:** run the official pre-implementation decision validator in a real workspace; check native 1.6 loading (all XML/paths, tea shrub can be sown and harvested twice, three Cooking Bills and reagent consumption, tea and kogashi-yu manual/inventory+voluntary drinking, Joy gain, positive but small kogashi nutrition, no DrugPolicy/Hediff/food poisoning/table aberrations) using **minimum** Vanilla and optional Grains profile. Confirm exact Grains matching loaded Mod name for conditional patch; 1.7 is not claimed.
- **Outside this slice:** food-form edible kogashi remains Grains future, not its nine-food initial release. Other barley Mods remain unverified; no VE compatibility. No Steam upload, native Actions or expensive automated tests authorized merely by merging source.

**Canonical specification:** `Docs/Design.md`. **Historical source archive:** `Docs/Research/PreOwnerStudy.md`. Cross-repo Grains food/drink boundary already documented in its own `Docs/Design.md`. No user relay required.
