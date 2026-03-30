# COG Downloader

COG (Cloud Optimized GeoTIFF) からデータを取得し、PNG画像として保存するCLIツールです。

## 必要環境

- Node.js

## インストール

```bash
npm install
```

## 使い方

```bash
# URLを直接指定
node index.js <COG_URL> [options]

# プリセットを使用
node index.js -p natural-earth [options]
```

### オプション

| オプション | 説明 | デフォルト |
|---|---|---|
| `-p, --preset <name>` | プリセット名 | - |
| `--list-presets` | 利用可能なプリセット一覧を表示 | - |
| `-o, --output <path>` | 出力ファイルパス | `output.png` |
| `-w, --width <number>` | 出力幅 | 元画像のサイズ |
| `-h, --height <number>` | 出力高さ | 元画像のサイズ |
| `--max-width <number>` | 最大幅 | `1024` |
| `--max-height <number>` | 最大高さ | `1024` |
| `-i, --image-index <number>` | 画像インデックス | `0` |
| `-s, --samples <numbers>` | バンド指定（カンマ区切り） | `0,1,2` |
| `-b, --bbox <coords>` | 地理的境界（west,south,east,north） | - |
| `--info` | 画像情報のみ表示（PNGを保存しない） | - |

### 使用例

```bash
# Natural Earthプリセットで地形図をダウンロード
node index.js -p natural-earth -o earth.png

# 画像情報を確認
node index.js -p natural-earth --info

# 特定の範囲を切り出し（日本周辺）
node index.js -p natural-earth -b 122,20,154,46 -o japan.png

# サイズを指定して出力
node index.js -p natural-earth -w 512 -h 256 -o small.png

# 利用可能なプリセット一覧を表示
node index.js --list-presets
```

### プリセット一覧

| 名前 | 説明 |
|---|---|
| `natural-earth` | Natural Earth I（陰影起伏付き地形図） |
| `natural-earth-gray-dark` | Natural Earth I グレースケール（暗色背景） |
| `natural-earth-gray-light` | Natural Earth I グレースケール（明色背景） |

## 依存ライブラリ

- [geotiff](https://www.npmjs.com/package/geotiff) - GeoTIFFファイルの読み込み
- [sharp](https://www.npmjs.com/package/sharp) - PNG画像の生成
