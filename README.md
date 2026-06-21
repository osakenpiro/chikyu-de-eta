# 地球でえた / chikyu-de-eta

線だけで描かれた、裏側が透ける地球儀。「データで見る地球」。
主題は **日本の素材・資源**。ポータルではなく、**座標を持つものだけ**を載せる。
銀河儀（主観の星図）の双子＝この現実球。 — #全人類UX改善

**Live:** https://osakenpiro.github.io/chikyu-de-eta/

## v0
- 背骨レイヤ＝行政区域（都道府県境）。
- 描画＝Three.js（Globe.gl 流ワイヤーフレーム）。透明球＋経緯線＋境界線を、
  AdditiveBlending と depth-fade（手前濃・奥淡）で「平面に潰さず球に見せる」。
- 単一 `index.html` + `data/*.geojson`。GitHub Pages 完結（ビルド不要・ゼロコスト）。
- 表示パラメータ（不透明度／裏側フェード／経緯線密度／色／自動回転）は localStorage 永続。

## データ
| レイヤ | 出典 | ライセンス |
|---|---|---|
| 行政区域 admin (N03) | 国土数値情報「行政区域データ」国土交通省 ／ packaging: [dataofjapan/land](https://github.com/dataofjapan/land) | CC BY 4.0 |

> 簡略化＝Douglas–Peucker（eps≈0.008°）＋座標3桁丸め。47都道府県・約180KB。

## 構成
```
index.html            単一HTML（Three.js / 描画・UI・depth-fade shader）
data/admin.geojson    都道府県境（簡略化）
```

## ロードマップ
- **v1** PMTiles 化（大データ対応）＋ CODH 歴史地名層
- **v2** deck.gl で arc（交易・海路）／hexbin（産地集積）／時間軸アニメ
- 追加レイヤ（v0 上積み）：森林 A13・鉱区 C22・伝統的工芸品の産地
- 派生 **「からだの地図」** — 同じワイヤーフレーム＋データ層フレームワークを人体表面へ（足の裏＝地球のブリッジ）

---
osakenpiro · Visionium / 全人類UX改善
