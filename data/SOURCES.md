# データ出典・ライセンス / Data Sources & Licenses

このフォルダの地理データ（`*.geojson`）は第三者のオープンデータに由来し、
それぞれのライセンス（CC BY 4.0）に従う。**コード（MIT）とは別ライセンス**。

| レイヤ id | ファイル | 元データ | 提供 | ライセンス | 帰属表示 |
|---|---|---|---|---|---|
| `admin` | `admin.geojson` | 行政区域データ（N03） | 国土交通省 国土数値情報 ／ packaging: [dataofjapan/land](https://github.com/dataofjapan/land) | CC BY 4.0 | 「国土数値情報（行政区域データ N03）国土交通省」 |
| `forest` | `forest.geojson` | 都道府県別森林率・人工林率（令和4年3月31日現在）の森林率 | [林野庁](https://www.rinya.maff.go.jp/j/keikaku/genkyou/r4/1.html) | 政府標準利用規約（CC BY 4.0 互換） | 「都道府県別森林率・人工林率（令和4年）林野庁」 |

## 加工について
- 投影：EPSG:4326（WGS84 経緯度）に統一。
- `admin`：Douglas–Peucker（eps≈0.008°）＋座標3桁丸め。属性は `id / nam / nam_ja` のみ保持。
- `forest`：点は **都道府県の重心**（`admin.geojson` から算出）、値は **森林率(%)**（属性 `ratio`）。
  併せて `area_ha`（森林面積）, `jinko`（人工林率%）を保持。**v0は軽量版（点表現）**。
  本格的な森林地域ポリゴン（国土数値情報 A13）は v1 の PMTiles 化時に差し替え予定。
- 加工は表示用であり、出典データの正確性・最新性を保証するものではない。

## CC BY 4.0 / 政府標準利用規約 の義務（要約）
- **表示（Attribution）**：出典・提供者・ライセンスを明記（本リポは画面フッター＋本ファイルで表示）。
- 改変した場合はその旨を示す（上記「加工について」が該当）。
- CC BY 4.0 全文：https://creativecommons.org/licenses/by/4.0/

## レイヤを追加する人へ
新しい `*.geojson` を足すときは、**必ずこの表に1行追加**して出典・ライセンス・帰属を記載すること。
`data/layers.json` の各エントリの `credit` 文字列が画面フッターに自動表示される。
