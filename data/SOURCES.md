# データ出典・ライセンス / Data Sources & Licenses

このリポの地理データ（`*.geojson`）は第三者のオープンデータに由来し、各ライセンスに従う。**コード（MIT）とは別ライセンス**。
「地球でえた」は世界地図（地球儀）であり、世界データも日本データも同じ枠組みに載る。

| レイヤ id | ファイル | 元データ | 提供 | ライセンス | 帰属表示 |
|---|---|---|---|---|---|
| `world` | `world.geojson` | 国境（1:110m Admin 0 – Countries） | [Natural Earth](https://www.naturalearthdata.com/) | パブリックドメイン | 「Made with Natural Earth」 |
| `admin` | `admin.geojson` | 行政区域データ（N03） | 国土交通省 国土数値情報 ／ packaging: [dataofjapan/land](https://github.com/dataofjapan/land) | CC BY 4.0 | 「国土数値情報（行政区域データ N03）国土交通省」 |
| `forest` | `forest.geojson` | 都道府県別森林率（令和4年3月31日現在） | [林野庁](https://www.rinya.maff.go.jp/j/keikaku/genkyou/r4/1.html) | 政府標準利用規約（CC BY 4.0 互換） | 「都道府県別森林率・人工林率（令和4年）林野庁」 |
| `crafts` | `crafts.geojson` | 伝統的工芸品 都道府県別 指定品目数（令和7年10月27日現在） | [経済産業省](https://www.meti.go.jp/press/2025/10/20251027001/20251027001-b.pdf) | 政府標準利用規約（CC BY 4.0 互換） | 「伝統的工芸品指定品目一覧（令和7年）経済産業省」 |
| `mining` | `mining.geojson` | 鉱区データ（C22, 昭和59年=1984） | [国土交通省 国土数値情報](https://nlftp.mlit.go.jp/ksj/gmlold/datalist/gmlold_KsjTmplt-C22.html) | CC BY 4.0（国土数値情報 利用約款） | 「国土数値情報（鉱区データ C22）国土交通省」 |
| `water` | `water.geojson` | 河川・湖 中心線（1:110m Rivers + Lakes） | [Natural Earth](https://www.naturalearthdata.com/) | パブリックドメイン | 「Made with Natural Earth」 |
| `energy` | `energy.geojson` | 世界の発電所（容量1,000MW以上を抽出） | [WRI Global Power Plant Database v1.3.0](https://github.com/wri/global-power-plant-database) | CC BY 4.0 | 「Global Power Plant Database v1.3.0, World Resources Institute — CC BY 4.0」 |

## 加工について
- 投影：EPSG:4326（WGS84 経緯度）。`mining` の C22 は旧測地系の可能性があるが地球儀スケールで誤差は無視。
- `world`：Douglas–Peucker（eps≈0.2°）＋2桁丸め。属性は `name / name_ja / iso`。
- `admin`：Douglas–Peucker（eps≈0.008°）＋3桁丸め。属性 `id / nam / nam_ja`。
- `forest`：都道府県重心の点。値＝森林率(%)（`ratio`）。併せ `area_ha`,`jinko`。**v0軽量版**（本格A13ポリゴンはv1）。
- `crafts`：都道府県重心の点。値＝指定品目数（`count`）。市区町村レベルの産地ジオコードはv1。
- `mining`：鉱区4,902件の重心を約1km統合（4,313点・単一MultiPoint）。**昭和59年(1984)の歴史データ**。
- `water`：Natural Earth 110m の主要河川(13)＋湖(24)を統合。属性 `name / name_ja / featurecla`。線として描画（湖は外周線）。
- `energy`：WRI 全34,936件から容量1,000MW以上の1,618件を抽出した重心点。属性 `name / country / capacity_mw / fuel`。明るさ＝容量(bmax 3000)。**v0**（全量・容量しきい値はlayers.jsonで調整可）。
- 加工は表示用であり、出典データの正確性・最新性を保証しない。

## ライセンス義務（要約）
- **表示（Attribution）**：出典・提供者・ライセンスを明記（画面フッター＋本ファイル）。Natural Earth は表示不要だが慣例として記載。
- 改変表示：上記「加工について」が該当。
- CC BY 4.0 全文：https://creativecommons.org/licenses/by/4.0/

## レイヤを追加する人へ
新しい `*.geojson` を足すときは **この表に1行追加** して出典・ライセンス・帰属を記載。
`data/layers.json` の `credit` がフッターに自動表示される。
