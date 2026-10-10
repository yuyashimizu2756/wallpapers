# Iso Harbour

アイソメ調の港町をテーマにしたライブ壁紙。Lively Wallpaper に登録して使う。

## 動くもの

- 工場のコンベアをパレットが流れ、フォークリフトがそれを積載場へ運ぶ
- 平板トラックが町を一周するルートを走り、倉庫のドックで荷下ろし
- ワンボックスが倉庫から海辺のコンビニへ配達
- 貨物列車がレールを西へ走って通過
- ボートが湾を渡り、カモメが空を旋回する

## 昼夜

- 1 日 = 実時間 4 分（`DAY_LEN`）。
- 夕暮れ（18:06〜19:48）で配色全体が夜のパレットへ滑らかに沈む。窓・街灯・ランプが先に灯る。
- 夜明け（5:24〜7:30）で日中の配色に戻る。

## テーマ

- OS のダーク／ライトに自動追従（`prefers-color-scheme`）。
- URL に `#dark` か `#light` を付けると固定。

## つかいかた

- `index.html` をダブルクリック（`file://` 対応、网络アクセス不要）。
- Lively Wallpaper にはフォルダごと追加すると、自動認識される。

## ファイル

```
iso-harbour/
  index.html          壁紙本体（自己完結）
  LivelyInfo.json     Lively 用の設定
  preview.png         プレビュー（夜）
  preview-day.png     プレビュー（昼）
  README.md
  lib/three.min.js    Three.js r160（UMD）
```

## 元ネタ

- 視覚言語・等角投影カーネル: [Khalidabdi1/factory](https://github.com/Khalidabdi1/factory)（MIT）
- 投影の考え方: [ai-iso-skill](https://github.com/MrBongoC/ai-iso-skill)（MIT © Tolga Cohce）