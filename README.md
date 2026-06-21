# 地球でえた / chikyu-de-eta

線だけで描かれた、裏側が透ける地球儀。「データで見る地球」。
主題は **日本の素材・資源**。ポータルではなく、**座標を持つものだけ**を載せる。
銀河儀（主観の星図）の双子＝この現実球。 — #全人類UX改善

**Live:** https://osakenpiro.github.io/chikyu-de-eta/

![地球でえた](https://osakenpiro.github.io/chikyu-de-eta/)

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
   - `kind:"point"` … 