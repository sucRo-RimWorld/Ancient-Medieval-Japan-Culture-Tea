# Tea — pre-owner historical research and archived technical probes

> **Historical source record migrated from** [Project study at commit 7d78d2a](https://github.com/sucRo-RimWorld/Ancient-Medieval-Japan-Project/blob/7d78d2a0c4c3d0e692f6b24e57ff1501356aafc4/Docs/Research/TeaAndBarleyDrinksCandidate.md).  
> Its former owner/status statements, old barley-only recipe and prototype nutrition=0 are **superseded** by the new Tea [Docs/Design.md](../Design.md).  
> All historical citations and unfinished audit limitations below are retained as research evidence, not as a competing live specification. Relative Project links in the original body should be understood against the source linked above.

# AMJ 茶・こがし湯 — 日常飲料の基本設計

**記録:** 2026-10-16 JST  
**状態（2026-10-20 作者採用）:** 日常の非ドラッグ飲料を扱う独立小規模Mod「AMJ Tea（仮）」に、**茶とこがし湯**の二飲料を集約する設計・所有範囲を採用。こがし湯は当面**米・大麦**を原料とし、こがしの食品版はGrainsが将来所有する。旧「大麦限定の麦湯」案と「Grains未導入時は飲料そのものを非表示」という案を撤回する。史料・実装可否・既存Mod監査の未了部分、具体値、リポジトリ新設と本番実装は別ゲートであり、**生産XML/C#・GitHub製品Repo・公開は未実施**。

## 0. 2026-10-20 確定した所有・製法の境界

- **Tea（将来の独立Mod）:** 茶の栽培・加工・飲用と、「こがし湯」の製造・飲用・非ドラッグ娯楽を所有する。Grains必須依存ではない。Vanilla `RawRice` を使う米こがし湯を基本経路にし、Grains導入時は食用大麦 `AMJC_Barley` も飲用レシピの選択原料に追加する。原料により完成飲料やBillを重複させない。別の大麦追加Modは現物Defを監査後、条件付き原料として個別に追加する。
- **Grains:** 穀物の栽培・脱穀・製粉、および将来の**こがし粉を食品として食べる**工程・栄養・Recipeを所有する。Teaの飲用完成品・飲用Joy/摂取Jobは所有しない。こがし食品の初回Grains公開への追加は要求しない。Grainsの既存粉は未焙煎なので「こがし」と無条件で同一視しない。
- **史料上の境界:** 10世紀の米麦炒り粉、1587年の茶の代用「こがし」を参照する。後世の煮出す麦湯・近現代の冷たい麦茶をAMJの標準飲料にしない。米・大麦以外（小麦・アワ・ヒエ・キビ・ソバ等）は、可能性だけで「全穀物こがし」に一括登録せず、原料ごとの史料確認後に判定する。
- **栄養・娯楽:** 茶は栄養補給の手段ではない。こがし湯は穀粉を飲食するため、**原料と摂取量に相応する小さい正の栄養を持つ**。両者とも少量の娯楽回復のみで、薬物Comp・依存・離脱・心情Thought・気付け・Rest/作業バフを持たない。`Nutrition`、Joy、原料数・工数の具体値は未確定。
- **実装ゲート:** 上記は仕様採用であって、製品Repo作成・XML/C#実装・検証完了の主張ではない。従前のXML-only試作は大麦専用かつ栄養0等の旧仮説であり、製品仕様へそのまま昇格させない。

## 1. 目的と範囲

- 生活者が日常的に飲む**茶（チャノキ由来）**と**こがし湯（焙煎米・大麦等の粉由来）**を二種類の飲料として区別する。
- 飲む理由は小規模な娯楽・休息。**精神崩壊危険時の強力な心情回復薬、覚醒剤、治療薬、酒の代用品とはしない。**
- 古代から戦国末期までの日本を扱う。史料で庶民に一般化した時期は茶と炒り穀物で異なるため、時代・階層・地域について製品説明で区別する。
- 初期には二飲料のみ。茶会、茶室、茶道具の品質差、闘茶、儀礼、贈答、複数の銘柄・等級、茶店、家族ごとの嗜好Trait、カフェインNeed、独自の水分Needは**対象外**。
- 茶とこがし湯を研究・料理UIやMod依存のためだけに分割・重複させず、一つの小規模飲料Mod内で工程と遊び上の違いだけを残す。

### 1.1 飲用史料を先に固定する（2026-10-16再調査、実装・効果数値より優先）

**茶の三方式は同じ「緑茶」ではない。** 中世史研究者・橋本素子「[やさしい茶の歴史（一）](https://company.books-yagi.co.jp/archives/7872)」によれば、(a) 9世紀前半に唐風の葉茶を**煮出す煎茶法**、(b) 12世紀に宋風の粉末茶に熱湯を注ぐ**点茶法**が伝わり、(c) 揉んだ葉を浸して抽出する**淹茶法**は17世紀までに明から伝わる後世の方式。現代的な煎茶の完成法については[お茶百科「日本でのお茶の歴史」](https://www.ocha.tv/history/japanese_tea_history/)が1738年の宇治製法を示す。**RimWorldの製品ラベルを「緑茶」とするだけで現代式淹茶・水出しへ置き換えない。**

| 時代・史料 | 調製して飲んだ形態 | 飲んだ場面・道具 | AMJの解釈 |
|---|---|---|---|
| 815年『日本後紀』、[橋本（一）](https://company.books-yagi.co.jp/archives/7872) | 僧・永忠が茶を**煮出して**嵯峨天皇をもてなす | 貴人への接待、献茶。最初から薬に限定された飲み物ではない | 煮出し茶は初期からあるが、全国の庶民が常飲した証拠にはしない |
| 1211年『喫茶養生記』、[橋本（八）](https://company.books-yagi.co.jp/archives/8299) | 摘みたてを**蒸す→焙炉で乾燥→保存**。飲む場合は**粉末茶に熱湯**を注ぐ | 点茶。茶の粉砕道具が必要な方式であり、葉茶の単純な淹茶ではない | 茶葉の蒸し乾燥を代表工程として採用可。ただし煮出しと点茶の手順を同一史実と書かない |
| 1256年醍醐寺の法会、[橋本（十三）](https://company.books-yagi.co.jp/archives/8929) | **煮出した茶**が供される。1262年史料には点茶・煮出しの両方式 | 寺院の役割別に一杯を配分。下層の人々による回し飲みも推測される | **中世に煮茶と点茶は併存**。茶碗・杯で提供する描写は自然だが、全国的な家庭用湯飲み・茶道具セットを前提にしない |
| 1403年東寺の茶売り請文、[京都府・東寺百合文書WEB](https://hyakugo.pref.kyoto.lg.jp/?p=118) | その場で湯を沸かし、茶を点てて売る | 門前にござ・炉。釜・水桶を担いで茶売りをする。**飲用に食卓が必須という史料ではない** | 茶を持ち歩く完成ペットボトルでなく、**茶葉／茶道具を運びその場で淹れる（点てる）**運用を想定 |
| 10世紀『和名類聚抄』を引く[全国麦茶工業協同組合](https://www.mugicya.or.jp/history/) | **米・麦を乾燥し、炒って粉にして湯水に点じる** | 粉を水や湯に混ぜて飲食。大麦単独・透明な浸出液を意味するわけではない | 麦由来の穀粉飲食は成立。ただし「透明な現代の麦茶」を同一視せず、**粉自体を摂る**点を忘れない |
| 1587年北野大茶湯の高札、[『香煎の歴史』2011年](https://agriknowledge.affrc.go.jp/RN/2010813889.pdf)、[世界大百科事典「香煎」](https://kotobank.jp/word/%E9%A6%99%E7%85%8E-62521) | **茶がなくても「こがし」で代用可** | 茶会への参加条件として、釜・水汲み道具・飲物を持参するよう求める。こがしには麦のほか**米や香味料を用いる系統**もある | **こがし=麦こがし限定、とは断定不可**。AMJでは米と大麦の双方を初期原料にするが、全穀物・全時代で同じ製法があったと一般化しない |
| 江戸の[『本朝食鑑』1697年の伝承を含む麦茶工業協同組合](https://www.mugicya.or.jp/history/)、[常陸屋本舗「麦茶」](https://www.hitachiya-honpo.co.jp/product/mame/AB-mugicha.html) | 麦粉を冷水で練る例、後には炒り麦を煮出して飲む麦湯・茶屋 | 江戸の屋台、明治の家庭、昭和の冷却麦茶 | **後世の「麦湯」「麦茶」の飲み方を中世の全期間へ遡及させない** |

**携帯容器と中身を分離する:** ひょうたん・竹筒を水筒に使う歴史そのものはある（[サントリー・水筒の歴史](https://www.suntory.co.jp/eco/teigen/water/jiten/world/07/)）。しかし、**中世日本で出来上がった冷たい麦茶を水筒に詰めて常飲したという史料は今回確認できない。** **乾燥した炒り穀粉を携帯し、後から水や湯に混ぜる**方が、現代の完成飲料の携帯より当時の加工・保存形態に適合する。とはいえ粉を携帯した具体的な時期・場面は引き続き原史料で検証する。**1686年の香煎を竹筒に入れた記録は江戸期であり、中世の直接証拠に格上げしない**（上記『香煎の歴史』）。

**栄養・飲み方の重要な設計差（2026-10-20採用）:** 煮出した茶は抽出液であり、こがし湯は**炒った米または大麦の粉そのものを湯水に混ぜて口に入れる**。茶を栄養補給として扱わない一方、こがし湯には原料量に応じて少量の正の栄養を与える。両者を同じNutrition=0の透明な飲料とはしない。正確な数値は未決で、強い薬物・特殊効果・食中毒を導入する理由にはならない。

**テーブル・携帯UXの再評価（2026-10-16、後続の作者指摘を反映）:** 先に作者が茶の`AteWithoutTable`ペナルティを「許容」としたのは**ゲーム上の容認であり、中世喫茶史上の適切さを保証しない**。実際、表千家不審菴の[茶の飲み方](https://www.omotesenke.jp/list5/list5-1/list5-1-2/)では、茶室の客は畳に座り、茶碗を膝前の畳に置き、手に取って飲む。**卓は必須ではなく、茶道の茶で『食卓がないから不満』は文化的に不適合**。これは後世まで継承された作法の説明であり、中世の全方式が同一だったとの一次証拠にはしない。一方[裏千家の茶の歴史](https://www.urasenke.or.jp/textb/shiru/spirit/spirit3.html)では室町後期の珠光→戦国の武野紹鷗→利休にわび茶の成立を位置付けており、**815年の煮茶や鎌倉初期の庶民にも完成した茶道作法を遡及しない**。**後続の全体方針（2026-10-16）:** 食卓・椅子への文化的な必要性判断は、茶だけではなく**AMJ - Culture**候補の`AteWithoutTable`見直しが所有する（[CultureCandidate](CultureCandidate.md)）。茶だけの技術回避をCultureの機能と重複して作る必要はない。**Tea単独プレイでもCultureを必須にはしない**。Teaのみで飲用のテーブル関連Thoughtをどう扱うかは、史料・実際の1.6飲用挙動確認後に決定する。独立の食事台専用Modは再開しない。1403年の露天茶売りもテーブル必須を示さない。麦こがしを「水筒から飲む」専用アクションや水筒アイテムは現時点で追加しない。

**史料評価:** 上記には中世の一次史料を研究者が引用・解釈した高信頼の事例と、後代文献・業界史説を混ぜている。各行の時期・根拠を越える一般化は不可。「水筒入りの麦茶」「冷たい麦湯」を中世の標準とする仮説、あるいは「中世の庶民は全員抹茶」等の単一方式は採用しない。

## 2. 完成品の仕様目標

| 項目 | 茶（製法上は煮茶） | こがし湯 |
|---|---|---|
| 歴史上の根拠 | 唐風の煮出し茶と宋風の点茶が中世に共存。寺院の接待・儀礼（1256年醍醐寺）、一服一銭茶売り（1403年東寺）を含む。全国の庶民が全年代で常飲したとはしない | 10世紀の米麦炒り粉を湯水に混ぜる飲食法、1587年の茶代用「こがし」（**麦だけと断定不可**）。江戸の煮出し麦湯・近現代の冷たい麦茶と同一視しない |
| 原料 | チャノキの葉 | **Vanilla `RawRice`（米）／Grains `AMJC_Barley`（導入時の大麦）**。別Mod大麦は監査後の任意互換 |
| 加工 | 摘採 → 加熱・乾燥 → 煮出す（最小二工程） | 原料の米または大麦を炒って粉にし、湯で溶く（最小一Recipeへの抽象化可） |
| 娯楽 | **小**。こがし湯より素材・供給を少し手間のかかる位置に置く | **小**。安価な常用向け |
| 心情 | 薬物由来の強い気分変化、特別なMood Thoughtを付けない。娯楽回復が中心 | 同左 |
| 眠気／覚醒 | **機械的な気付け・RestNeed回復・作業速度上昇なし**。実在茶のカフェインを誇張しない | **なし**。カフェインを含まない |
| 身体・健康 | 専用依存、耐性、離脱、過量服用、副作用、薬物中毒、治療効能を付けない | **完全に同様**。飲料固有の不利益なし |
| 食中毒・アレルギー | この飲料の飲用を食中毒・アレルギーの発生経路にしない | **なし**。食中毒・アレルギー等の追加仕組みは実装しない |
| 栄養 | 茶は栄養補給にならない。実装APIの都合で微量の正のNutritionを技術試験する余地は残すが、ゲーム上の食事とは扱わない | **こがし湯には原料穀粉に応じた小さい正のNutritionを与える**。粉末そのものを摂るため抽出液と同一の0栄養にはしない。量は原料・製品調整で未確定 |
| ゲーム操作 | Pawnが地面上の一杯を右クリックして手動で飲み、娯楽時間には自発的に飲める。所持品タブからの摂取は別途検証。Drug Policyには結びつけない | 同左 |
| 在庫・交易 | 茶葉／茶の一般的な保存・交易を候補とする。頻度・価格は未決 | 麦を消費して作れる安価な飲料。輸入飲料の一般化は不要 |

**ノーリスクの正確な意味:** このゲームシステムでは二飲料の摂取から、薬物由来の病状、依存、離脱、疲労・意識低下、食中毒等を発生させない。製造には通常の材料・作業コストがあるだけで、罰則やリスクを足して帳尻を合わせない。完成品の品質階層も初期には作らない。過剰摂取専用の制御を追加せず、Vanillaの娯楽飽和／自発行動の制限を基本とする。最終的な飲用UIと自発摂取の方式はロード済みDef検証による。

**バランスの原則:** 二品のJoy数値・調理Work・原料個数・保存日数は**未確定**。Vanillaの食事や酒の心情効果を模して付与しない。茶を入手した途端に常時Joy満タンとなる連続服用が起きないよう、実際の娯楽飽和と摂取優先度を測って調整する。

## 3. 最小の供給・製法ループ

### 3.1 茶

1. **原料調達:** チャノキから茶葉を得る。チャノキは実際の常緑多年生の茶樹であり、穀物のように毎回株が消える一年草にしないのを目標とする。葉の繰り返し採集には、既存Plant/harvest APIや先行Modの実装を監査する。新しい採集Job・Harmonyを最初から前提としない。
2. **製茶:** 摘んだ葉を**加熱（蒸す／湯通しの抽象化）して乾燥**し、一種類の「乾燥茶葉」にする。必要なら加工は1Recipeへ集約する。現代式の揉み工程、機械、遮光栽培、茶の等級分けは不要。
3. **飲用:** 乾燥茶葉から一杯の**煮茶**を作る。**普通の茶をRimWorldのPsychite teaへリネームしない。** 点茶・抹茶の文化は史実上認めるが、初期の別アイテム・茶臼・茶筅は増やさない。
4. **地域・時代:** 古代～鎌倉前期の庶民が全国的に常飲していたとする説明・初期全国自生を避ける。室町～戦国の庶民の利用は史料で確認。茶の栽培をどのBiomesで可能にするか、初期供給（栽培／交易）と普及頻度はEnvironment・歴史確認後に別決定する。既存AMJ地形・生態系を理由なく変更しない。

### 3.2 こがし湯

1. **原料:** Grainsなしでも使えるVanilla `RawRice` を基本経路とする。Grains存在時は食用大麦 `AMJC_Barley` を同じ飲用完成品の原料へ条件追加する。米・大麦以外の穀物は時代・製法の個別根拠と各ModのThingDef確認を条件に将来判断し、自動で穀物全般を受け入れない。
2. **製法:** 米または大麦を**炒る→粉砕する→湯に溶く**。粉の摂取なので、現代の透き通った煮出し麦茶・江戸の麦湯とは区別する。初回は一つの飲用Recipeへ工程を抽象化してよいが、焙煎しないGrainsの `AMJC_BarleyFlour` をそのまま「こがし」に転用しない。
3. **粉の食品版:** 粉をそのまま食べる食品形態はGrainsの将来の穀物料理領域。Tea側で同じ「こがし粉」の食品Defや食用Recipeを重複所有しない。食品用中間品を共有するかTeaが原料から直接一服を作るかは実装時のレシピ設計で決める。現段階でGrains初回公開にこがしを追加しない。
4. **栄養:** 茶と違い、こがし湯は穀粉の摂取による小さい正の栄養を持つ。食事の代わりに大量摂取する仕様にはせず、原料消費量と一服のNutritionを整合させる（具体数値未定）。非ドラッグ、健康副作用なし、少量Joyのみ。
5. **設備と互換:** 既存の低技術の焚き火・かまど・調理台を優先。別Modの大麦は存在確認できた個別の原料ThingDefのみ条件付きで追加し、誤った粉・穀束の自動受入を避ける。TeaはGrains・MOを必須にしない。

### 3.3 装置・作業ルール

- 最初から**専用製茶小屋、茶室、茶道具、喫茶施設を新設しない**。既存調理設備で足りるか比較する。
- 飲料は「原料」か「完成品」かUI上判別でき、普通の調理Bill／手動摂取で完結すること。専用水分Need・酒造の発酵工程・DBHの水システムは必須にしない。
- 飲む際に食中毒判定が発生する設計を採らない。RimWorld内部の食事／薬物／嗜好品のどのThingDef実装がこの契約を満たすかは実Def/実機検証で選定する。**ゲーム内のリスクを増やす技術的な回避策は採らない。**
- 完成飲料を手動摂取できることを優先。放置時の行動AI・RimWorldのDrug Policyとの関係は、無断自動飲用や依存Trait誤適用が起きない方式を監査してから選ぶ。

## 4. 所有範囲・互換

- **現在の正本:** 専用Teaリポジトリ設置までProjectが茶・こがし湯の採用済み設計を保持する。作者は小規模独立飲料Modへの分離を採用したが、実製品Repository・PackageId・既存Mod必要性ゲート・製品版Defは未確定／未実装。所有リポジトリが成立した後、Teaの確定設計をその設計正本へ移す。
- **Tea:** 茶・こがし湯の製造と飲用完成品、非ドラッグ娯楽・摂取UIを所有する。Vanilla `RawRice` でこがし湯を作る基本経路を持ち、Grains有無に拘束されない。
- **Grains:** `RawRice`（Vanilla再利用）、`AMJC_Barley`、栽培・穀類一次加工・一般の穀物料理を所有。**食べるこがし（炒り粉）**はGrainsの将来範囲。Teaの飲用レシピをGrainsが重複追加しない。Grainsの初回公開食品・既存加工値は今回変更しない。
- **外部大麦:** 他Modの大麦は名前一致だけで取り込まず、実Def・入手法・加工段階を確認してから任意で条件付き原料に加える。Vanillaには大麦Defを新設しない。VEコンテンツは既定方針に従い公式互換しない。
- **Environment:** 茶樹の自然配置・Biome・気候は独立監査後の任意連携であり、Environmentへ無断でPlantDefを追加しない。
- **MO:** 設備の任意再利用可。ただしGrainsやMOを飲料Modの必須依存にはしない。
- **Culture/薬物UX:** DrugDesire、Alcohol、ChemicalNeed、Health Hediffを編集しない。茶・こがし湯を非常用薬物に置き換えない。卓の文化的ThoughtはCultureが所有。
- **発酵・酒造:** 酒・発酵液の生産工程を含めない。
- **画像:** 茶樹・茶葉・乾燥茶葉・茶の完成品・こがし湯完成品が最小候補。既存Grains画像は変更しない。未採用の画像を製品として生成しない。

## 5. 既存Mod比較（実装可否のゲート、2026-10-16）

**前提・互換の確定方針（2026-10-16 作者修正、2026-10-20内容名更新）:** 茶とこがし湯は中世日本の歴史再現に必要な要素だけで成立させる。**VE系Modを必須依存・公式互換・追加統合の対象にしない。** 緑茶1品のために余計なコーヒー、紅茶、酒造設備、研究や他の時代外コンテンツを持ち込まない。VEを調べる目的は実装方式・重複機能の比較のみで、歴史的に不適切な内容を取り込む根拠にしない。VE利用者向けの任意互換を将来の予定にも加えない。外部Modとの同時ロードは意図的に妨害しないが、VEとの機能的な共存は検証・保証しない。独立の CCTO for VPE の役割はこの茶の仕様の対象外。


| 先行Mod | 確認できる機能 | 結論・未検証 |
|---|---|---|
| [Vanilla Brewing Expanded - Coffees and Teas](https://steamcommunity.com/sharedfiles/filedetails/?id=2275449762)（VE） | 緑茶・紅茶などの先行品目。**公開旧ソース1.3**では緑茶 `VBE_GreenTea` が **VanillaCookingExpanded連携フォルダ**に属し、`DrugBase` 継承・`drugCategory=Social`・`CompProperties_Drug` 付き。レシピはエスプレッソマシン＋砂糖。旧版実Defと現在Workshop配布物は同一とは未確認 | **AMJでは前提化も公式互換も行わない**。中世日本の茶と製法・依存・娯楽/ドラッグ分類が異なる。旧ソースの仕組みは先行研究のみ、現行1.6配布XML・最終ロードは未監査 |
| [Erin's Hot Drinks](https://steamcommunity.com/sharedfiles/filedetails/?id=2520989125)（非VE） | 茶樹、茶葉、単独の **Tea**（日本語のMod紹介では「紅茶」）、コーヒー・チョコレート・ラテ・モカを提供。公式説明でTeaは非依存性。**緑茶として区別した飲料は確認できない** | **AMJの中世日本の茶をそのまま満たす直接の代替とは評価しない**。植物・抽出／調理Bill・飲用・Joy挙動についての参考／限定的任意互換候補。英語公式説明は単にTeaであり紅茶製法のDefまで未監査。日本語Mod紹介の紅茶表記と緑茶アイテムの不在を区別して記録 |
| [Simple Immersion - VBE Coffees and Teas](https://steamcommunity.com/sharedfiles/filedetails/?id=3681298244) | VE茶/コーヒーの抽出台・音・任意MO燃料互換を追加 | 飲料自体は追加しないため一次代替ではない。専用茶台が不可欠との根拠にもならない |
| [八十吉「Rimworldに食事を追加するMODの作り方 10」](https://note.com/85638/n/nfdd33ef49d39)（非VE技術解説） | `SBK_Sencha` 煎茶の飲用例、`JoyGiver_Ingest`・独自`JoyKindDef`・`joy=0.10`、加えて腎機能10%・心情+2/6時間の`Hediff`付きの例 | **非VEの実装例**として有用。AMJが採用しない健康・心情バフは除外。記事だけで独立配布Modの現行1.6実Defや依存・実ゲーム互換を確認したことにはしない |

**証拠範囲（2026-10-16）:** [Erin's Hot Drinks公式Workshop説明](https://steamcommunity.com/sharedfiles/filedetails/?id=2520989125)にはTea、Coffee、Hot Chocolate、Latte、Mochaを記載。日本語紹介[2game Erin's Hot Drinks](https://rimworld.2game.info/detail.php?id=2520989125)はTeaを「紅茶」と表記。独立した「緑茶」の記載は双方に見つからない。VBEは[公式Workshop](https://steamcommunity.com/sharedfiles/filedetails/?id=2275449762)と[関連Texture Modの対象飲料一覧](https://rimmods.com/mods/food-texture-variety-vanilla-expanded-coffee-and-tea)でGreen Tea／Black Teaの別アイテムが確認できる。**いずれも配布XMLの実Def・レシピ加工や最終ロード挙動は今回未監査**であり、茶葉を緑茶に日本化する簡単な置換で十分とは断定しない。

**VE系は先行研究だけに使用し、AMJ側で公式互換・依存を作らない。** Erin's Hot Drinksも中世日本の緑茶を直接満たすものではない。中世日本に必要な**茶とこがし湯の最小範囲**だけを対象とし、既存小規模Modや実装技法の調査、必要最小限の史実準拠実装（ライセンスを順守）を比較する。非VEの候補も時代外の余計な内容や依存があれば採用しない。独立実装の場合はProject `Docs/Research/ExistingModAudit.md` のVE+非VE・原XML・ロード結果・依存・ライセンス比較とdecision recordを満たす。調査はVEとの統合や実ゲーム互換を求めるためではない。

## 6. テスト項目と段階

| 項目 | 前提・期待（採用時の要件） | 現状 |
|---|---|---|
| 薬物外の飲用 | 茶・こがし湯にはChemicalDef/依存/耐性/離脱がなく、摂取しても薬物Hediff/Needを作らない | 設計のみ |
| こがし湯の安全性と栄養 | 飲用時に食中毒・過剰摂取・アレルギー・薬物副作用のトリガーなし。**食べる穀粉として少量の正の栄養**を持ち、強いMood Thoughtなし | 設計のみ |
| 娯楽 | 自発的／手動で飲める。少量のJoy、連続飲用による無制限回復なし | 設計のみ |
| 茶の供給 | 長期栽培のチャノキ／茶葉収穫／乾燥／煮出しが成立。既存PlantDef・収穫ルールと共存 | 技術選定待ち |
| こがし湯の供給 | Vanilla `RawRice` で成立。Grains併用時は食用大麦を同じ完成飲料Recipeの選択原料に追加。焙煎→粉砕→湯で溶く | 独立Tea所有と原料2種の方針確定、未実装 |
| 非導入 | Tea単独でも米こがし湯が利用可能。Grains未導入で `AMJC_Barley` への欠落Def/NullRefが発生しない | 未実装 |
| 想定プロファイル | Vanilla単独／Grains／MO／Environment等、AMJで公式に対応する組合せで完成品・研究・飲料の二重登録なし。VEプロファイルは対象外 | 未検証 |
| セーブ | 追加・解除に伴うDef参照とDrugPolicyの正常性を検証。必要なら旧セーブ互換は本当に導入実績がある対象だけ評価 | 未検証 |
| 実ゲーム | 実際の収穫、調理Bill、摂取、Joy、トレード、ロード済Def、正常終了・ERROR=0 | 未実施 |

**実装の採用順:** ①既存Modの先行技術比較と所有者決定（VE統合なし） → ②原料/茶葉加工と麦の使い分けを最小化した実装 → ③Joy/自発摂取/副作用なしのロード済み証拠 → ④Grains・MO等のAMJ対象プロファイルの機能検証 → ⑤現物画像と実プレイ。導入対象ゲームバージョンは現行主軸の1.6を優先し、1.7は別途検証する。

## 7. 技術的成立性の調査（2026-10-16、製品ソース未実装）

**確定したのは実装経路の候補であり、RimWorld 1.6での実動作PASSではない。** 以下のC#一次資料は公開逆コンパイルリポジトリ `josh-m/RW-Decompile` の `master`（古いゲーム版、1.6一致を未確認）であり、1.6正式アセンブリの最終根拠とはしない。

| 必要な動作 | 確認済みコードの仕組み | 最小設計と残る検証 |
|---|---|---|
| チャノキの反復収穫 | [`PlantProperties.cs`](https://github.com/josh-m/RW-Decompile/blob/master/RimWorld/PlantProperties.cs) `HarvestDestroys => harvestAfterGrowth <= 0`。[`Plant.cs`](https://github.com/josh-m/RW-Decompile/blob/master/RimWorld/Plant.cs) `PlantCollected()` で `harvestAfterGrowth > 0` なら株を残して成長度を戻す | `PlantDef.plant.harvestAfterGrowth` を正の値にする。植栽・自然採取・成長・枯死・繰返し収穫を実ゲームで検証。専用Job/Harmonyはまず作らない |
| 低リスク飲料の自発摂取 | [`JoyGiver_Ingest.cs`](https://github.com/josh-m/RW-Decompile/blob/master/RimWorld/JoyGiver_Ingest.cs) は `thingDefs` 対象に対して `IsIngestible`、`joyKind`、`joy > 0`、`pawn.WillEat`、到達可否・禁制・ポリシー等を検査し、標準 `JobDefOf.Ingest` を作る | **既存の `Gluttonous` 娯楽と `JoyGiver_Ingest` を第一候補**とする。専用の娯楽種類／C#は作らず、既存 `EatChocolate` への追加で表示文言・競合が不適切な場合にのみXMLの専用 `JoyGiverDef` を比較する。飲料をDrugとして定義せず、専用健康`Hediff`やThoughtを付けない。飲用頻度は`baseChance`、Joy飽和と在庫で調整。娯楽用として実際に選択されるかを検証 |
| 微量栄養と飲用UI | [`IngestibleProperties.cs`](https://github.com/josh-m/RW-Decompile/blob/master/RimWorld/IngestibleProperties.cs) は`Nutrition==0`の場合に`NeverForNutrition`を要求。旧[`ThingDef.cs`](https://github.com/josh-m/RW-Decompile/blob/master/Verse/ThingDef.cs) の`IsNutritionGivingIngestible` は `CachedNutrition>0`。[`ITab_Pawn_Gear.cs`](https://github.com/josh-m/RW-Decompile/blob/master/RimWorld/ITab_Pawn_Gear.cs) はこれで所持品の摂取ボタンを表示できる条件を判定 | **小さい正のNutrition**（`0.01`は試験例、固定数値ではない）、`preferability=NeverForNutrition`、`foodType=Processed, Fluid`、`maxNumToIngestAtOnce=1` を第一実機比較候補にする。薬物に変更する必要はない。旧コードのためRimWorld 1.6で実際のUIとJobを確認する |
| 薬物ポリシーへの非介入 | `JoyGiver_Ingest.CanIngestForJoy` は `t.def.IsDrug` 時だけDrugPolicy／DrugDesireの処理を持つ | `drugCategory`、`CompProperties_Drug`、化学依存Outcomeを一切定義せず、Pawnの化学嗜好Traitが茶・こがし湯を薬物扱いしないことを試す |
| Grains大麦への接続 | Grains main `Defs/ThingDefs_Items/Items_StageA_Grains.xml` に **`AMJC_Barley`**、`Defs/ThingDefs_Items/Items_GrainsFlour.xml` に **`AMJC_BarleyFlour`** が現存。製粉は `Recipes_GrainsMilling.xml` が所有 | こがし湯はVanilla `RawRice` を標準原料にし、Grains併用時の可食大麦 `AMJC_Barley` を追加選択原料とする。粒を焙煎→粉砕→湯で溶く工程を一Recipeに抽象化。Grainsの既存栽培・加工・栄養・粉食は変更しない |

**手動飲用UIと微量栄養の見直し（2026-10-16、以前の「微量栄養不可」を修正）:** 公開旧逆コンパイル [`FloatMenuMakerMap.cs`](https://github.com/josh-m/RW-Decompile/blob/master/RimWorld/FloatMenuMakerMap.cs) の地面右クリックは`ingestible`・`CanEverEat`・`IngestibleNow`で候補にする。一方、[`ITab_Pawn_Gear.cs`](https://github.com/josh-m/RW-Decompile/blob/master/RimWorld/ITab_Pawn_Gear.cs) の所持品摂取ボタンは`IsNutritionGivingIngestible || IsNonMedicalDrug`を必要とする。**DrugにせずNutritionを少し正にする方法を試すことは許容**する。`FoodUtility.BestFoodSourceOnMap()` は通常の人間Pawnの空腹時に`NeverForNutrition`より上位の`minPref`を求め、`FoodOptimality`も`NeverForNutrition`を最低評価するため、**微量Nutritionと`NeverForNutrition`の併用は通常の食事選択からの除外と整合する見込み**（動物／特殊Pawnは別途確認）。[`Thing.IngestedCalculateAmounts`](https://github.com/josh-m/RW-Decompile/blob/master/Verse/Thing.cs) はNutritionで割って摂取個数を計算するので、0より小さくない**正の値なら0除算の危険も避けられる**。一服上限`maxNumToIngestAtOnce=1`を維持し、右クリック／所持品／娯楽自発摂取を実機で別々に確認する。**0.01は試験値であり、栄養の最終バランス値は未承認。**

**実装前の優先順位（2026-10-16歴史調査で修正）:** 第一に**茶の煮出し／点茶と、粉を湯水に混ぜるこがしの実態・携帯・栄養を区別する**。その結果に従って品目・飲用操作・原料量を決める。茶の暫定製造はチャノキ→生茶葉→加工茶葉→茶、こがし湯はVanilla米およびGrains導入時の大麦由来。史料で正当化できない新しい器・茶銘柄・砂糖・エスプレッソマシン・薬効・専用研究・新しい娯楽系C#は作らない。**微量Nutritionで手動／自発Ingestが成立するかは、その後の技術ゲート**。`AteWithoutTable`の**一般食事の文化的見直しはCultureが所有する候補**。Teaは飲料そのものと手動/自発飲用だけを所有し、Cultureを必須依存にしない。Tea単独でのThought挙動は別途検証する。

**先行実装の具体的な限界（公開GitHub 1.3ソース）:**
- [VBE GreenTea ThingDef](https://github.com/juanosarg/VanillaBrewingExpanded---Coffees-and-Teas/blob/main/1.3/Mods/VanillaCookingExpanded/Defs/ThingDefs_Items/Drinks_GreenTea.xml)：`VBE_GreenTea` が `DrugBase` + Social drug + `CompProperties_Drug` + `Nutrition=0.08` + `joy=0.25`。AMJではこの分類・数値をコピーしない。
- [VBE GreenTea Recipe](https://github.com/juanosarg/VanillaBrewingExpanded---Coffees-and-Teas/blob/main/1.3/Mods/VanillaCookingExpanded/Defs/RecipeDefs/Recipes_Tea_Cooking.xml)：`VBE_MakeGreenTea` は `VBE_Tea`・`VCE_RawSugar` とエスプレッソマシンを使用。旧ソースでは緑茶そのものがVanilla Cooking Expanded連携領域。現行Workshop版ではないので将来の挙動・必須依存を確定したとはしない。
- [八十吉の非VE煎茶チュートリアル](https://note.com/85638/n/nfdd33ef49d39)：薬物ではない飲用JoyGiverの実装例。ただし腎機能+10%・心情+2の健康Buffや本文に示す煎茶の加工仕様は、AMJの基本設計と一致しない。別Modとしての配布現物を確認したとは言わない。
- [Erin's Hot Drinks](https://steamcommunity.com/sharedfiles/filedetails/?id=2520989125)：Teaは確認されるが個別の緑茶・中世の製法は確認できない。実配布Def不明につき既存Mod必要性の正式監査ゲートは**まだ完了していない**。

### 設計上の所有者候補（まだ正式決定ではない）

**2026-10-20 作者採用の所有者構成は、小規模独立の「AMJ Tea（仮）」:** 茶樹、茶葉、製茶・飲用Joyに加え、米・大麦を用いる**こがし湯Recipe**を同じ飲料所有者が持つ。Grains無しでもVanilla `RawRice` でこがし湯が成立し、Grains有効時のみ `AMJC_Barley` を原料に追加する。一方、**粉を食べるこがし食品**はGrainsの将来責務で、Teaとは完成品・レシピを重複させない。独立実装の必要性ゲートおよび専用Repoは未完了。

**開始ゲート:** 所有者を確定する前にProjectのVE+非VE既存Mod監査要件に則り、実配布物にアクセス可能な候補は原XML/依存も比較する。未実査を「先行Mod不存在」とは判定せず、現時点では`ready`状態の実装許可を発行しない。新repo作成、配布向けXML、Art、リリース作業は未実施。

### 2026-10-16 市場監査追補：緑茶の先行Modは存在する

**重要な訂正:** 先の候補調査で日本語の緑茶Modが見つからなかったのは検索不足。**「緑茶の先行Modなし」とは言わない。**

| 既存例 | 実際に確認できる点 | AMJとの相違と採用判定 |
|---|---|---|
| [Azuki＆Matcha / ID 3800894716](https://rimworld.2game.info/detail.php?id=3800894716)（非VE、公開表示は1.6対応、2026-09-27更新） | 緑茶、水出し緑茶、抹茶セット、抹茶ラテ、小豆・茶葉の栽培、専用調理台、団子・たい焼き・ようかん等。飲料に寒暑耐性効果がある。2gameの2026-09-14利用者報告では「ドラッグ扱い」で薬物嗜好Pawnが繰返し摂取するという指摘があり、**2026-10-16作者が効果付きドラッグ方式と認識しAMJ不適合と判定** | **直接採用・前提依存・公式互換の候補から除外。** 中世日本の日常茶に強い身体状態効果やDrugシステムを持ち込まない。原XMLは未監査なので具体的なChemicalDef/Comp/Hediffの実装内訳は未確定。比較する場合は茶樹の栽培・収穫など独立した技術部分だけを扱い、同Modそのものを利用・改変して採用しない |
| [Cake, Tea, and War Crimes / ID 2180178970](https://steamcommunity.com/sharedfiles/filedetails/?id=2180178970)（非VE、説明は1.6対応） | 茶樹、茶葉、茶。説明によればPawnが自発摂取し、飲茶で心情+16。ケーキ、人肉・人体由来の料理／茶を含む | 茶単独の飲用実装例として比較可能だが、強烈な心情バフと史実に不適合なコンテンツが多い。**直接の前提Mod・公式互換候補にはしない**。現行配布Defs未監査 |
| [Erin's Hot Drinks](https://steamcommunity.com/sharedfiles/filedetails/?id=2520989125)（非VE） | 茶の木、Tea、コーヒー、ホットチョコレート等。緑茶を別アイテムとして確認できない | 茶の摂取経路の先行研究のみ。上記の和製緑茶Modの存在を否定する根拠ではない |
| [Vanilla Brewing Expanded - Coffees and Teas](https://steamcommunity.com/sharedfiles/filedetails/?id=2275449762)（VE） | 旧GitHubソースでは緑茶が VCE連携・砂糖／エスプレッソマシン使用のDrugBase | AMJでは前提・公式互換なし。現行版未検証 |

**公式の実装対象を狭く保つ理由:** 茶という共通機能は複数の先行Modが持つ。しかし、既存Modの全体内容・依存ツリー・時代範囲・非薬物という飲用仕様を合わせると、**必要な煮茶と米・大麦のこがし湯だけを読み込み、不要部分をロード後に非表示化しないAMJの方針に一致する先行完成品は今回確認できない**。特に**Azuki＆Matchaは効果付きドラッグとしての設計思想そのものが不一致**であり、前提化・飲料Def再利用・互換Patchは行わない。現行の原XMLによる技術的内訳の確認は未了だが、採用候補に戻すための監査は不要。研究価値がある場合のみ茶樹・収穫等の実装技法を限定的に調べる。独立実装の開始に必要なVE+非VEの既存Mod監査・代替必要性判断は、別途所定のゲートに従う。

### 2026-10-16 ローカル実装プローブ（GitHub未導入）

**旧仕様（大麦限定・Grainsがないとこがし湯無し）の検証用XML-only試作ZIPを会話の一時コンテナに構築。2026-10-20採用の米・大麦こがし湯とは仕様が異なるため、製品にそのまま流用できない。** プロジェクトRepoはゲーム実装の所有者ではないため、この試作XMLはProjectの本番ファイルとしてコミットしていない。別所有Modの新リポジトリも未作成。試作ファイルは会話添付にのみ存在し、**GitHub mainに「実装済み」として反映された状態ではない**。

- About: 試作用packageId `sucro.ancientmedievaljapan.tea.prototype`、RimWorld 1.6のみ、未公開。
- 本体: チャノキ `AMJT_TeaPlant`（`harvestAfterGrowth=0.45`）、生葉 `AMJT_FreshTeaLeaves` →加熱乾燥`AMJT_DriedTeaLeaves` → 煮茶 `AMJT_BoiledTea`。
- Grains連携: `loadFolders.xml` で `sucro.ancientmedievaljapan.core` 有効時だけ `AMJC_Barley`→`AMJT_BarleyDrink` のDef／Recipe／Joyパッチを読み込む。本体はGrainsがなくても欠落した大麦Defを参照しない。
- Joy: Vanilla `EatChocolate` の `thingDefs` に `AMJT_BoiledTea` を追記。Grains有効時は麦湯も追記。専用Job・Harmony・Health/Hediff/DrugCompなし。飲料の `Nutrition=0`、`preferability=NeverForNutrition`、`joyKind=Gluttonous`、`maxNumToIngestAtOnce=1`、`IngredientValueGetter_Volume`（既存クラスで個数相当の材料消費）を試す。ここでの体制は**試作**であり、1.6で自発摂取成功の実証はない。
- XMLは10ファイルすべて構文チェックPASS、8固有Def名の重複0、本体にGrains固有Refなし、BarleyDrink非薬物・栄養0・レシピ制約等の静的チェックPASS。**旧ゲーム逆コンパイルを参考にした仮説検証であり、正規1.6ゲームのDefロード／Pickle／Pawn行動／食中毒非発生の実機PASSではない。**
- 試作にはVanillaの既存画像パスへの**仮参照のみ**を置き、元画像・承認済みProduction画像は一切作成・変更していない。収穫量・Work・Joy等は未承認の仮値。配布・Workshop非対象。
- **次の実施条件:** 本番所有者（専用Teaリポジトリ等）の正式決定と必要性ゲート。採用後は試作XMLを移管し、RimWorld 1.6原本の実ロード（Grainsなし／あり）→2回目収穫→調理→自発/手動Ingest→Joy/健康・依存副作用なし→日英表示/画像・ERROR0を確認。Azuki＆Matchaをロードする互換テストは対象外。実機でNutrition0の摂取が失敗した場合は原因を検証して設計に戻す。大量の飲料・複数Mod前提・現代料理を回避するという方針は維持。

## 8. 基本仕様の精錬・v1境界（2026-10-16）

### 8.1 採用する遊びと製法

| 論点 | v1の仕様方針 | 根拠・除外 |
|---|---|---|
| プレイヤー向け名称 | **茶**（乾燥茶葉を煮出した飲料）、**こがし湯**（米または大麦を焙煎・粉砕し湯に溶く飲料）。「煮茶」は製法説明のみ。「麦湯」「麦茶」を中世飲料の表示名にしない | 後世の麦粒抽出液と区別する。日英の文章校閲は別途 |
| 内容品目 | チャノキ／摘採茶葉／加熱乾燥済み茶葉／一服の茶／一服のこがし湯。Vanilla米を基本、Grains食用大麦を任意の原料とする。粉の食品版はGrainsの将来範囲 | 茶臼・茶筅・茶室・茶銘柄・派生ラテ・抹茶などを増やさない |
| 茶の製造 | 採葉→加熱乾燥（1 Bill）→煮出す（1 Bill）。蒸し・焙乾・煮出しを代表工程へ抽象化。団茶に必要な成形も独立中間品にしない | [農水省の伝統的飲料解説](https://www.maff.go.jp/e/policies/market/dento_syoku/bunrui/inryou.html)は当初の団茶と後の宋風点茶を区別。蒸し乾燥葉の煮出しを全年代の唯一の製法という史実主張にはしない |
| こがし湯の製造 | `RawRice`／任意の`AMJC_Barley` を焙煎→粉砕→湯水に混ぜる。調理Bill 1回で抽象化できる。**穀粉を摂取する少量の栄養を持つ** | 透明な煮出し麦茶ではない。未焙煎のGrains穀粉流用は禁止。食品版・携帯粉の実装はGrainsとの境界で別途判断 |
| 設備・水 | 既存の低技術の焚き火・かまど・調理台を利用。水は調理工程に抽象的に含め、独立水アイテム／水分Need／DBH前提を新設しない | 新調理台・熱源研究・自動機械・大型飲料パックを要求しない |
| 摂取の扱い | **茶は非栄養の娯楽飲料、こがし湯は少量の栄養がある非ドラッグ娯楽飲料**。食事を代替する過剰摂取はさせず、少量のJoyのみ。Health・Mood Thought・Rest・作業速度・温度耐性・化学依存・Drug Policyへの影響なし | こがし湯のNutritionは正の値を要するが未確定。茶の微量Nutritionは技術試験限り。既存`Gluttonous`娯楽・`NeverForNutrition`使用は実機確認を要する |
| 利用頻度 | 食事・薬物Policyに依存させず、娯楽時間に自発摂取。少量かつ飽和する娯楽として扱い、回数強制や「定時茶飲み」専用Jobを加えない | 過剰な娯楽補充や麻薬嗜好Traitによる連続摂取を避ける。既存Joy経路の調整に留める |
| 最初の供給 | 茶株は生き残り、摘採後に再成長。**初期には日本全域の野生茶樹を自動配置しない**。栽培はVanillaに存在する植栽経路を第一候補とし、交易による乾燥茶葉の供給は実装必要性が確認できた場合のみ | 史料上の栽培・普及時期と、ゲーム内の「植えられる」という機能を混同しない。茶樹専用Seeds、時代横断の全Faction持参を追加しない |
| 商品区分と保存 | 新鮮葉は製茶の原料であって主食の生食材ではない。乾燥茶葉は保存可能。**調製済みの茶・こがし湯は短期消費品**とし、無制限に備蓄する保存食にはしない | 原料・調整済みの飲料をFoodRawの汎用料理Ingredientへ混入させない。必要なら既存の腐敗→消滅で表現し、新Healthリスクは付けない |
| 生育・対価 | チャノキの再収穫可能性は採用。**自動的な無病・全気候無制限・無労働の資源源にはしない**。摘採・製茶・火を使う加工と、大麦を飲料へ転用する機会費用を残す | 収穫量・成熟時間・Joy・Work・腐敗日数・価格は**試作値のまま正式確定しない**。まず成否と普通の食物・娯楽とのバランスを1.6で検証 |
| 互換 | Tea本体はVanilla米でこがし湯も成立、Grains存在時のみ大麦原料を追加。他の大麦Modは実Def確認後に個別判断。**VE・Azuki＆Matchaとの公式互換なし**。MO/Environmentは必要に応じ個別監査 | 必須依存を増やさず、完成飲料・Billの重複を避ける |

**テーブル・食中毒・食事ルートの技術資料（歴史的整合を先に評価）:** [`Toils_Ingest.FinalizeIngest`](https://github.com/josh-m/RW-Decompile/blob/master/RimWorld/Toils_Ingest.cs) は `IsNutritionGivingIngestible && chairSearchRadius>10` のとき `AteWithoutTable` を判定する。**文化的な食卓必要性の再評価はCulture所有**。Tea単独の飲用がVanillaのテーブルなしThoughtを発生させるか実機観測する。旧微量栄養試作の`chairSearchRadius=0`/`ingestHoldUsesTable=false`は飲用時のUI/Job技術研究としてのみ保留し、**茶の製品仕様として確定した処置ではない**。CultureをTeaにハード依存させず、同じグローバルThoughtパッチをTeaに重複搭載しない。[`Thing.Ingested`](https://github.com/josh-m/RW-Decompile/blob/master/Verse/Thing.cs) は `FoodPoisonChanceFixedHuman` を参照するため、飲料は同Statを**0と明示**し、通常のFoodPoisonable Comp・専用Health効果を持たせない。栄養を微量正値にしても`NeverForNutrition`を維持し、`maxNumToIngestAtOnce=1`で食事目的の連続摂取を防ぐ。旧コードから1.6の実動作が保証されたわけではない。動物による摂取やModによる食事カテゴリ操作も無害か確認する。

**微量栄養の別試作（2026-10-16）:** 既存の`Nutrition=0` ZIPを改変せず、**別のローカル試作**で茶・麦こがし湯を`Nutrition=0.01`（テスト用の一例）、`NeverForNutrition`、`maxNumToIngestAtOnce=1`、`chairSearchRadius=0`、`FoodPoisonChanceFixedHuman=0`とした。`Tests/test_static.py` を固定値一致から**小さい正値の範囲チェック**に変更し、XML構文と10 XML文書・8固有Def・条件付きGrainsを静的再検証済み。**新試作もProject GitHubに本番XMLとしてコミットしておらず、1.6原本／Pawn実行は未検証。** これは栄養数値の正式承認ではない。

**試作XMLから正式採用前に直すべき点:** (1) `AMJT_FreshTeaLeaves` は現試作で `PlantFoodRaw` に入っているが通常の調理食材として誤認させないカテゴリへ修正（実際の1.6カテゴリ名を確認）、(2) 二つの完成飲料は `CompRottable` 未設定なので屋内保管で長期保存できてしまう。短期間の腐敗→消滅を前提にするならそのCompと実動作を追加検証、(3) `AMJT_TeaPlant` の `neverBlightable=true` は特別扱いの根拠がなく、一般の栽培と同程度に扱う方向で見直す、(4) `EatChocolate` に新商品を直接追加した際、娯楽ラベル・他の菓子との競合・摂取頻度のUXを検査する。**これらは現行試作で直したという報告ではない。**

### 8.2 優先受入試験と失敗時の対処

| 試験 | 判定に必要な観測 | ゲート |
|---|---|---|
| Teaのみの1.6新規起動 | Grains/VE/Azukiなしでも茶・Vanilla `RawRice` こがし湯のDef/Recipe/Joyが解決、関連ERROR=0 | 未実施 |
| Tea + Grainsの1.6新規起動 | Vanilla米のこがし湯に `AMJC_Barley` が選択原料として増える。完成飲料は一種類で、Grainsの麦粒／粉／料理は不変。Tea単独には麦Defへの不正参照なし | 未実施 |
| チャノキの採葉サイクル | 栽培→初回摘採→株存続→成長→**同じ株から二度目の摘採**。気候・生育が適切に制約 | 未実施 |
| 製造経路 | 茶の2工程、麦の1工程が既存低技術設備の実Billで完了。原料は正しい品目・量のみ消費し、完成品は各1服 | 未実施 |
| 非薬物・微量栄養 | `IsDrug=false`、`IsPleasureDrug=false`、`Nutrition>0`の微量サンプル、`NeverForNutrition`、DrugPolicy対象外。Health/Hediff/Trait/Rest/Mood効果なし。単なる「栄養を与える」ではなく通常の空腹解消ジョブに選ばれないことを観測 | 未実施 |
| 実際に飲める | 地面上の右クリック、所持品タブからの手動飲用、娯楽時間の自発的`Ingest`をそれぞれ観測。一服1個が消費され、わずかな栄養と少量のJoyだけを得る。Job例外・無限再試行なし | 未実施 |
| 所持品UIと通常挙動 | 茶とこがし湯を混同せず、各飲用方法（地面／所持品／娯楽）を実機確認。茶とこがし湯の異なるNutritionによる摂取UI表示、空腹時の通常食選択除外、`FoodPoisonChanceFixedHuman=0`・健康効果なしを確認。**Tea単独の飲用を実機検証**（Tea単独、将来Cultureとの任意併用）し、Cultureの一般食事規範と抑止責務を重複させない。こがし食品と一般料理のテーブル処理はTeaから変更しない | 旧ソース確認済・1.6実動作未検証 |
| 保存・中間素材 | 茶葉は正常保管、調製済み飲料は短期で腐敗・消滅。茶葉は無関係の食事Billに混入しない | 未実施 |
| レクリエーション競合 | 食事として消費されず、過剰な連続飲用・強力な心情回復・チョコレートUI文言流用が発生しない | 未実施 |
| 日英・最終画面 | 名称/調理Bill/飲用命令・製品説明、通常ゲーム画面の文字・画像・ゼロERROR。試作仮画像は採用せず | 未実施 |

**判定（2026-10-20更新）:** **米・大麦のこがし湯の製法・原料・栄養・所有境界は採用済み。** その他の穀物の史料、具体値、原XML/独立Mod必要性と実機動作の検証は別ゲート。 試作のXML文法・参照構造の静的PASSを実ゲームPASSと混同しない。自発飲用が失敗したら`joyKind`／`JoyGiverDef`／`WillEat`／Thingカテゴリ／職務選択の実ログを確認。**固定のNutrition=0は要件から外し、非ドラッグ・通常食事として選ばれない・少量娯楽・健康副作用なしというゲーム上の契約を優先する。** 栄養値やJoyは実機試験後に確定する。

## 9. 主な史料と設計上の注意

- [表千家不審菴「形とふるまい：お茶をのむ」](https://www.omotesenke.jp/list5/list5-1/list5-1-2/)：客は茶室に座り、茶碗を膝前の畳に置いてから手に取り飲む。**現在の流派の作法**を中世全期間の直接史料としない。
- [裏千家「茶の歴史」](https://www.urasenke.or.jp/textb/shiru/spirit/spirit3.html)・[中之島香雪美術館「茶の湯の茶碗」](https://www.kosetsu-museum.or.jp/nakanoshima/exhibition/chanoyunochawan/)：室町後期から戦国にかけて成立した茶の湯と、鎌倉初期に伝わった点茶の時代差を確認する。


- [京都府立京都学・歴彩館「大変だった？茶店のはじまり その1」](https://hyakugo.pref.kyoto.lg.jp/?p=118)：1403年の一服一銭茶売りの誓約書、露店の炉・茶具・水を参照する具体例。茶が常に食卓を要したとの根拠にはしない。
- [橋本素子「鎌倉時代中期の煎茶法と点茶法の茶」](https://company.books-yagi.co.jp/archives/8929)：1256年醍醐寺で煮茶が供された記録、1262年の点茶・煮茶・生茶葉の区別。
- [小学館『日本大百科全書』「麦こがし」](https://kotobank.jp/word/%E9%BA%A6%E3%81%93%E3%81%97-140297)・[平凡社『世界大百科事典』「香煎」](https://kotobank.jp/word/%E9%A6%99%E7%85%8E-62521)：大麦だけでなく米や香草類も「こがし・香煎」の文脈に含まれる。麦粉を練る場合は可食の穀粉として扱う。
- [小川正巳・猪谷『香煎の歴史』（2011）](https://agriknowledge.affrc.go.jp/RN/2010813889.pdf)：16世紀北野大茶会の「こがし」許容と、17世紀以降の香煎材料・竹筒保存に関する後代史料を区別する。


- 橋本素子「[やさしい茶の歴史（一）](https://company.books-yagi.co.jp/archives/7872)」：唐風煮茶（煎茶法）／宋風点茶（粉末＋湯）／江戸期の淹茶法を区別。
- 橋本素子「[栄西と茶――やさしい茶の歴史（八）](https://company.books-yagi.co.jp/archives/8299)」：`喫茶養生記`の摘採→蒸し→焙乾と点茶法。
- 橋本素子「[金沢文庫文書にみる茶の生産](https://company.books-yagi.co.jp/archives/10744)」：実生栽培、煮茶と点茶で茶葉は加熱・乾燥、揉み工程なし。
- 橋本素子「[中世の茶屋について](https://www.jstage.jst.go.jp/article/rakuhoku/11/0/11_1/_article/-char/ja)」：営利の一服一銭、寺院由来の接待茶屋。茶を日常性だけで時代横断して扱わない。
- [全国麦茶工業協同組合「麦茶の歴史」](https://www.mugicya.or.jp/history/)・[国立国会図書館レファレンス協同DB](https://crd.ndl.go.jp/reference/entry/index.php?id=1000319793&page=ref_view)：炒り穀粉/こがしと、後世の大麦粒抽出の麦湯を区別。
- Project [薬物と庶民喫茶の史実監査](PsychoactiveSubstancesCandidate.md)：根拠の適用範囲と「茶は緊急薬物の代用品ではない」契約を保持。

**残る作業:** 独立TeaのRepo作成・既存Mod必要性ゲート、チャノキの複数回収穫実装、こがし湯の米・大麦の実Defと一服Nutrition・Joy・Work・保存・交易の数値、任意の外部大麦Defの監査、日英表示文章、実ロードと飲用検証。茶とこがし湯の所有者／Grains食品境界／当初原料2種は2026-10-20に決定済み。製品XML・About・画像は未実装。
