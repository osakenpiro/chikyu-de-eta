# 地球でえた / chikyu-de-eta

線だけで描かれた、裏側が透ける地球儀。「データで見る地球」。
主題は **日本の素材・資源**。ポータルではなく、**座標を持つものだけ**を載せる。
銀河儀（主観の星図）の双子＝この現実球。 — #全人類UX改善

**Live:** https://osakenpiro.github.io/chikyu-de-eta/

## 特徴
- **線だけ・裏が透ける**ワイヤーフレーム地球儀。透明球＋経緯線＋データ層を
  AdditiveBlending と depth-fade（手前濃・奥淡）で「平面に潰さず球に見せる」。
- **単一 `index.html`**。ビルド不要・GitHub Pages 完結・ゼロコスト／ゼロメンテ。
- **依存は three.js のみ、しかも同梱**（`vendor/`）＝CDNが消えても動く完全自己完結。
- 表示パラメータ（不透明度／裏フェード／経緯線密度／色／自動回転／層ON-OFF）は localStorage 永続。

## レイヤーの足し方（3手）
このプロジェクトは「見た目（renderer）」と「データ（レイヤー）」を分けてある。
**コードを触らずレイヤーを増やせる。**

1. `data/` に GeoJSON を置く（**EPSG:4326 / 経緯度**。重ければ Douglas–Peucker で簡略化）。
2. `data/layers.json` の `layers` に1エントリ追加：
   ```json
   {
     "id": "forest",
     "name": "森林（森林率）",
     "file": "data/forest.geojson",
     "kind": "point",
     "color": "#c79a4a",
     "opacityMul": 1.0,
     "altitude": 0.012,
     "sizeField": "ratio", "sizeScale": 3.5, "sizeBase": 1.2,
     "enabled": true,
     "credit": "森林率（林野庁）— 出典明記"
   }
   ```
   - `kind:"line"` … ポリゴン/線を枠線で描画（県境・鉱区など）
   - `kind:"point"` … 点を発光ドットで描画。`sizeField` 指定でデータ値に応じ点サイズ可変
3. `data/SOURCES.md` の表に出典・ライセンス・帰属を1行追記し、push。以上。

> `credit` 文字列は画面フッターに自動掲載される（CC BY の表示義務を自動で満たす設計）。

## 構成
```
index.html                 単一HTML（描画・UI・depth-fade shader・manifest駆動）
data/layers.json           レイヤー台帳（これを編集して層を増やす）
data/admin.geojson         都道府県境（N03・簡略化）
data/SOURCES.md            データ出典・ライセンス・帰属
vendor/three.module.min.js three.js r160（同梱・MIT）
vendor/addons/controls/    OrbitControls（同梱・MIT）
LICENSE                    コードのMITライセンス
```

## ライセンス（二層）
- **コード**：MIT（`LICENSE`）。同梱の three.js も MIT。
- **データ**：`data/*.geojson` は各オープンデータ由来で **CC BY 4.0**（`data/SOURCES.md`）。
  再配布・改変時は出典表示が必要。

## ロードマップ
- **v0**（現在）行政区域＋（次）森林・鉱区・伝統工芸の産地
- **v1** PMTiles 化（大データ対応）＋ CODH 歴史地名層
- **v2** deck.gl（GlobeView）で arc（交易・海路）／hexbin（産地集積）／時間軸アニメ
  — 見た目スキンは上に載せ替えるので、この地球儀の表情は維持する
- 派生 **「からだの地図」** — 同じ「スキン＋レイヤー台帳」フレームワークを人体表面へ
  （足の裏＝地球のブリッジ）

---
osakenpiro · Visionium / 全人類UX改善
