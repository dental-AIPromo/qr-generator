# QRコード ジェネレーター (Private source)

このリポジトリはブラウザ完結型のQRコード生成ツール（初期版）の Private source です。

サイト名と公開 URL:
- 表示名: QRコード ジェネレーター
- Public（Pages）リポジトリ: dental-aipromo/qr-generator
- Pages 本番ベース: /qr-generator/
- Pages 開発ベース: /qr-generator/dev/
- 想定公開 URL:
  - Production: https://dental-aipromo.github.io/qr-generator/
  - Dev: https://dental-aipromo.github.io/qr-generator/dev/

ビルドと公開のポイント:
- Vite の base はデフォルトで "/qr-generator/" に設定しています。開発用に "/qr-generator/dev/" でビルドする場合は環境変数 PUBLIC_BASE を設定してビルドしてください。
  - 例（Linux/macOS）: PUBLIC_BASE=/qr-generator/ npm run build
  - 例（Dev ビルド, Linux/macOS）: PUBLIC_BASE=/qr-generator/dev/ npm run build
  - 例（Windows PowerShell）: $env:PUBLIC_BASE = '/qr-generator/'; npm run build
- GitHub Actions (.github/workflows/sync-to-public.yml) は dist を public repo の docs（または docs/dev）にコピーして PR を作成します。自動マージは行いません。repo の secrets に PUBLISH_TOKEN(PAT) を設定してください。

その他:
- 目的・要点: React + TypeScript + Vite + Vitest + ESLint 構成、サーバー送信なし、GPL-3.0-only ライセンス
- 依存ライブラリと理由: NOTICE を参照
- ブランド資産: assets/icons/、出典と SHA256 は assets/icons/LICENSE.md を参照。Public への配布は法務/ブランド承認が必要です。

Supported output formats and constraints:

- PNG: フル機能（中央アイコン・文字・背景透過/不透過をサポート）。透過は許可（background を transparent に設定可能）。
- JPEG: ラスター出力（背景を必ず描画；透過不可）。
- SVG: ベクター出力（外部参照を行わない自己完結SVGを生成）。ただし、中央に画像や埋め込みテキスト等のデザイン要素がある場合は安全に埋め込めないため、UI上では該当設定時に SVG を選択できません。URL モード（中央要素無し）のみ有効です。
- EPS: ベクター出力（基本モジュールを PostScript 命令で生成）。中央要素の埋め込みは未対応です。現状、EPS は中央要素が無い単純な QR のみサポートし、デザイン要素がある場合は UI で選択不可または生成時にエラーになります。

Note: ベクター形式（SVG/EPS）は、中央要素（画像/文字/アイコンなど）を Canvas 上で合成した結果を安全に反映できないため、その組合せでは選択肢を表示しません。デザインを含む QR は PNG/JPEG をご利用ください。
