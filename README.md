# 自作ライブ壁紙（Lively Wallpaper 用）

Three.js / WebGL で作った、自分専用の「動く壁紙」集です。
Windows の標準機能には動く壁紙がないため、無料アプリ **Lively Wallpaper** に登録して使います。

## 収録内容

| # | 名前 | フォルダ | 内容 |
|---|------|----------|------|
| ★ | Panel Iso | `panelui-iso` | panelui.dev 風。アイソメ調・モノクロ（紙とインク）。**OSのダーク/ライトに自動追従** |
| ★ | Panel Iso Dark | `panelui-iso-dark` | 同上のダーク固定版 |
| ① | Car Factory | `car-factory` | ネオン工場。コンベアで車が流れ、ロボットアームが動く |
| ② | Synthwave Drive | `synthwave-drive` | レトロ・シンセウェーブ。ネオンのグリッドが前方へ流れる |
| ③ | Spiral Galaxy | `galaxy` | 5万パーティクルの渦巻き銀河 |
| ④ | Neon Plexus | `neon-plexus` | ノードが線で結ばれるテック系ネットワーク |
| ⑤ | Warp Tunnel | `warp-tunnel` | ネオンのリングをくぐるワープ・トンネル |
| ⑥ | Factory Yard | `factory-yard` | アイソメの海辺の工場町。**5分周期の昼夜**・クリックで+6時間スキップ・**OSのダーク/ライトに自動追従** |
| ★ | Iso Harbour | `iso-harbour` | アイソメの港町（工場・倉庫・埠頭・灯台）。**4分周期の昼夜**・物流と船とカモメが動く・**OSのダーク/ライトに自動追従** |
| ★★ | Factory Yard (本家) | `factory-yard-full` | [Khalidabdi1/factory](https://github.com/Khalidabdi1/factory) を**Next.js でビルドした本家**。海辺の町＋新市 Sahel＋農業村＋観測台＋Starship 打ち上げ場。**1日=6分** |

各フォルダの `preview.png` は実際に描画したプレビュー画像（Lively のサムネイル兼用）です。

## まず「見る」（サーバー不要）

- **まとめて見る**: `start-gallery.cmd` をダブルクリック、または `gallery.html` をダブルクリック。
  → ブラウザで6つが**同時に動きます**。
- **1つだけ見る**: 各フォルダの `index.html` をダブルクリック。

> 旧版は ES モジュールを使っていたため「ファイル直開きでは真っ暗」でした。
> 現在は `lib/three.min.js`（UMDビルド）を通常の `<script>` で読み込む方式なので、
> **ダブルクリックでそのまま動きます**（`file://` 対応）。

## Lively Wallpaper に登録する

1. Microsoft Store か GitHub から **Lively Wallpaper** をインストール。
2. Lively を開き、右上の「**壁紙を追加（Add Wallpaper）**」をクリック。
3. 各壁紙フォルダ（例: `C:\Users\PC_User\wallpapers\galaxy`）を選ぶ、またはフォルダごとドラッグ＆ドロップ。
4. プレビューが出たら「OK」。`LivelyInfo.json` があるので自動認識されます。

## 改造する

- 各 `index.html` は自己完結した Three.js シーンです。色・速度・数を変えれば見た目が変わります。
- 3D ライブラリは各フォルダ内の `lib/three.min.js`（Three.js r160, UMD）を参照。
  各フォルダは自己完結しているので、フォルダ単体を Lively に追加できます。
- マウスに反応する壁紙（②③④）は、ポインタ移動でカメラが動きます。

## 構成

```
wallpapers/
  start-gallery.cmd        ギャラリーを開く（ワンクリック）
  gallery.html             5つを一括プレビュー
  README.md
  <各フォルダ>/
    index.html             壁紙本体
    LivelyInfo.json        Lively 用の設定
    preview.png            プレビュー画像
    lib/three.min.js       Three.js（フォルダ内で完結）
```
