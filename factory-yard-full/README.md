# Factory Yard — 本家ビルド

[Khalidabdi1/factory](https://github.com/Khalidabdi1/factory) を **この PC 上で実際にビルド**した静的サイト。
自作の `factory-yard`（移植版）とは別物で、これは上流の本家そのままです。

## 何が入ってるか

上流の全力です。`wallpapers/factory-yard` の移植版より広いです。

| 場所 | 内容 |
|---|---|
| 旧町 | 工場 Plant 01、倉庫 01、海辺の Corner Market、警察署、消防署、円形交差点、通りと住宅 |
| Car Works | プレス → ボディ → 塗装 → 組付 → 最終検査のライン、溶接ロボット、プレス 3 基、天井クレーン |
| Sahel | 新都市。金融地区の高層群、Sahel Central の組子、メトロ 2 線、Metrobus、Sahel Motors、コンテナ港 |
| 東の国 | Harrow Ridge、Raven Gorge の吊り橋、High Moor、Beacon Hill 観測台 |
| Millbrook | 線端の農業村。羊・牛・馬・鶏、納屋、干草刈り、風車、水車、苹果園 |
| Gull Spit Starbase | Starship の製造・打ち上げ。33 基の Raptor、SPMT 輸送車、chopsticks によるブースター回収 |

さらにイベントとして、銀行・店・港の**強盗**（警察・ヘリコプター・銃撃戦・逃走・道路封鎖まで）、**煙突火災**（消防車 ENG-1）、**オンライン注文**（宅配 PKG-1 の追跡）、雨と霧、そして **Starship の打ち上げ**。

## setup

Node 20 以上が必要（この PC では v24）。

```powershell
git clone https://github.com/Khalidabdi1/factory
cd factory
npm install
npm run build        # out/ に静的サイト
```

- `npm run dev` → localhost:3000（開発用。壁紙には要らない）
- `npm run preview` → `out/` を配信

## 壁紙として使う

このフォルダは**すでにビルド済み**なので、`npm install` も `npm run build` も**不要**です。

Lively Wallpaper で、このフォルダを指定するだけ。

- `LivelyInfo.json` の `FileName` は `index.html`、`Arguments` は `?wallpaper&hour=21` です。
  Lively はファイル URL に引数を付けるので、wallpaper モードが自動で入ります。
- `file://` で動くのは、`next.config.ts` の `assetPrefix: '.'` を入れたからです。
  上流の既定は `/_next/...` というルート絶対パスで、`file://` では壊れる。

### wallpaper モード的效果

`?wallpaper` を付けると:

- ダッシュボード（ナビ・ツール・カード・キャプション）が消える
- 余白 0・角丸 0 で、キャンバスが画面全寸
- 配色はダーク固定（デスクトップのアイコンが読めなくなるため）
- 右端に画角レール（画面右端 x=3830 付近。デスクトップアイコンは左上に固まっているので被らない）

### マウス操作について（重要）

**デスクトップ上ではマウス操作が wallpaper に届きません。**
カーソル位置のウィンドウは常に `Progman`（デスクトップ本体、explorer.exe）で、
wallpaper のウィンドウより手前にあるためです。これは Windows の仕様で、Lively の設定でも変更できません。

ブラウザで直接開いた場合（`index.html` をダブルクリック）は一般的な 3D 操作ができます:

| 操作 | 動作 |
|---|---|
| 左ドラッグ | 平行移動（地面に沿って） |
| 中ドラッグ / 右ドラッグ | 回転（地球儀のように上下左右へ自由） |
| ホイール | ズーム |

回転に極角制限はほぼありません。真上（0.9°）から真下（179.1°）まで回せます。
横から見たときや真下から見ても破綻しません（塗りは両面描画）。

### ナビゲーションギズモ

画面**右下**に Blender 風のワイヤーフレームの地球儀があります。

- **赤いリング** = X 軸（既定の真右・down-right）
- **緑のリング** = Y 軸（海の方）
- **青いリング** = Z 軸（真上）
- **破線の外側リング** = 自由回転
- **中心のハブ** = 自由回転
- 各軸の先端にドットと文字（+ 側が塗り、− 側が白抜き）

つかみ方:

| つかむ場所 | 動作 |
|---|---|
| 色付きリング | その軸，围绕して回転（Z を回して水平回転、など） |
| 外側の破線リング / 中心のハブ | 上下左右へ自由回転 |
| ギズモの外 | 何も起きない（地図側のパネルに抜ける） |

ギズモは毎フレーム実際のカメラから計算しているので、どこから見ているかを常に示します。
Blender と同じく、リングは奥行き方向に短縮されて楕円になります。

感度は控えめです（軸まわしはドラッグ 1 あたり 0.4 倍、自由回転は 0.006 倍/px）。
指先で追える速さなので、回している間に街を見失わずに済みます。

### 角度プリセット

ギズモの**真上**に、主要な角度へのボタンが並んでいます。押すとその角度へ滑らかに動きます。

| ボタン | 角度 (polar, azimuth) | 内容 |
|---|---|---|
| **Iso** | 54.7°, 45° | 既定の斜め俯瞰（一番の見え方） |
| **Plan** | 2°, 45° | 真上からの俯瞰（街全体の地図） |
| **Front** | 78°, 0° | 海から見た正面 |
| **Side** | 78°, 90° | 海岸線に沿って横から |
| **Low** | 38°, 45° | より浅い角度（立体感を出す） |

- 押すと `aria-current` が付き、選択中の角度が分かります。
- ギズモを自分で回すと、プリセットの選択は解除されます（現在の角度はギズモが示します）。

**デスクトップから画角を変えるには Lively の Customise パネルを使います。**
ライブラリの「Factory Yard (Original)」を右クリック → **Customise** で、次が選べます:

| 項目 | 内容 |
|---|---|
| Viewpoint | 画角（Panorama / Factory / Warehouse / Shop / Town / Coast / Car Works / Sahel / Metro / Motors / Port / East / Village / Sky / Starbase） |
| Zoom % | ズーム（100 = パノラマ標準） |
| Pan speed % | 平行移動の速さ（ブラウザ内のみ効果） |
| Rotate speed % | 回転の速さ（ブラウザ内のみ効果） |

設定はディスクに保存され、次回起動時に復元されます。

コマンドラインからも変更できます:

```powershell
Lively.exe setprop --property "viewpoint=13"   # Starbase
Lively.exe setprop --property "viewpoint=0"    # Factory
Lively.exe setprop --property "zoom=150"
```

### 2 画面（横長）への対応

2 台の 16:9 显示器を並べると 32:9（3840×1080）になります。この場合:

- `WallpaperArrangement` が **span** なら 1 枚のパノラマとして繋がる（要設定）
- 街を横に寝かせる浅い画角（`WIDE_ISO`）で、横幅を埋める
- 東端（Millbrook / Starbase）を少し切って、2 つの町を大きく見せる

Lively の設定（`%LocalAppData%\Lively Wallpaper\Settings.json`）:

```json
"WallpaperArrangement": 1,   // 0=per（独立）, 1=span（1枚）, 2=duplicate
"DisplayIdentification": 2   // 2=screenLayout
```

### URL で指定できること

| パラメータ | 効果 |
|---|---|
| `?wallpaper` | 壁紙モード |
| `&hour=21` | 開始時刻を 21 時に固定（その後は時計が流れます） |
| `&theme=light` | ライト配色（既定はダーク） |
| `&os` | OS の配色に追従させる |
| `&wide=0` | 横長最適化を無効（正方形の画角に戻す） |
| `&zoom=1.2` | 横長時のズーム倍率 |
| `&trim=0.17` | 横長時に削る東端の割合 |

`LivelyInfo.json` の `Arguments` を書き換えると、Lively から固定の見た目を作れます。

```json
"Arguments": "?wallpaper&hour=21"               // 夜
"Arguments": "?wallpaper&hour=8&theme=light"   // 朝の明るい配色
```

1 日 = 実時間 6 分（1 秒 = 4 分）なので、起動から数分で昼夜がひと周ります。

## 検証済み

Chrome + Playwright で 2560×1440 と 1920×1080、`hour` を 10・19・21 に変えてスクリーンショットを撮り、
上下の状態が正しいこと（night フラグ、背景色、描画コール 約 1700）を確認済み。
ギズモとプリセットについても、回転（ハブの自由回転・軸固定回転）が極限角度まで破綻せず動くこと、
各プリセットが指定角度へ正確に収束すること、真上（0.9°）・真下（179.1°）・水平（90°）でも NaN が出ないこと
を実測で確認しています。


## ファイル

```
factory-yard-full/
  index.html              Next.js の静的出力（Lively が直接読む）
  _next/                  JS / CSS / フォント（WOFF2 同梱、通信不要）
  LivelyInfo.json         FileName=index.html, Arguments=?wallpaper&hour=21
  LivelyProperties.json   Customise パネルの画角・ズーム設定
  preview-night.png       夜（サムネイル）
  preview-day.png         昼
  preview-dusk.png        夕暮れ
  README.md               このファイル
  .gitignore              node_modules やエディタ設定などの除外設定
  404.html, *.txt         Next.js の補助ファイル
```

`404.html` と `*.txt` は Next.js の静的出力に必ず付いてくる補助ファイルで、
壁紙の動作には直接関与しませんが、消すと `out/` のコピーが上流と一致しなくなります。

> このフォルダは**ビルド成果物**です。ソースは別に clone してあり（下記「変更点」参照）、
> ここから `git clone` して動かすフォルダではありません。あくまで完成版の置き場です。

## ライセンス

上流 [Khalidabdi1/factory](https://github.com/Khalidabdi1/factory)（MIT）。
等角カーネルの考え方は [ai-iso-skill](https://github.com/MrBongoC/ai-iso-skill)（MIT © Tolga Cohce）。

## この PC での変更点（`main` からの差分）

ソース側（clone した `factory-src`）で 5 ファイルだけを変更しています。

- `next.config.ts` — `assetPrefix: '.'` を追加（`file://` で動かすため）
- `app/globals.css` — `body.wallpaper` のスタイル、右端の画角レール `.rail`、ギズモ `canvas.gizmo` を追加
- `components/YardFigure.tsx` — `?wallpaper` / `?hour=` / `?theme=` の処理、レールとギズモの markup を追加
- `yard/shared.ts` — `WALLPAPER` / `WIDE` / `WIDE_ISO` / `WIDE_TRIM` / `VIEWPOINTS` を追加
- `yard/view.ts` — 横長フレーミング、`refit()`、自由回転（OrbitControls の turntable 設定）、
  ナビゲーションギズモ（描画とつかみ）、画角レール、そして `livelyPropertyListener`
  （Lively Customise パネルから画角・ズーム・速度を変更）

これで上流の挙動はそのままに、壁紙用の入口だけが増えています。

ビルドし直す場合:

```powershell
cd C:\Users\PC_User\AppData\Local\Temp\opencode\factory-src
npm run build
Copy-Item out\* C:\Users\PC_User\wallpapers\factory-yard-full -Recurse -Force
```
