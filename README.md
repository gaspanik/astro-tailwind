# Astro + Tailwind CSS + Biome

このプロジェクトは、Astroベースのスターターキットに **Tailwind CSS v4** と **Biome** を追加した開発環境です。

## 🛠️ 技術スタック

- **[Astro](https://astro.build)** - モダンな静的サイトジェネレーター
- **[Tailwind CSS v4](https://tailwindcss.com)** - ユーティリティファーストのCSSフレームワーク
- **[Biome](https://biomejs.dev)** - 高速なリンター・フォーマッター
- **[pnpm](https://pnpm.io)** - 高速で効率的なパッケージマネージャー
- **[Lucide (lucide-astro)](https://lucide.dev/guide/packages/lucide-astro)** - 軽量なオープンソースアイコンセット（Astro向けパッケージ）

## 🚀 プロジェクト構造

プロジェクトの主要なフォルダとファイル:

```text
/
├── public/                 # 静的アセット
├── src/
│   ├── assets
│   │   └── astro.svg
│   ├── components
│   │   └── Welcome.astro
│   ├── layouts
│   │   └── Layout.astro
│   ├── pages
│   │   └── index.astro
│   └── styles
│       └── global.css
├── astro.config.mjs        # AstroとTailwind CSSの設定
├── biome.json              # Biomeの設定
└── package.json
```

Astroプロジェクトの構造について詳しくは、[公式ガイド](https://docs.astro.build/ja/core-concepts/project-structure/)をご覧ください。

### 🎨 設定ファイル

- **`astro.config.mjs`**: Astroの設定とTailwind CSS v4のViteプラグイン設定
- **`biome.json`**: リンター・フォーマッターの設定
- **`src/styles/global.css`**: Tailwind CSSのインポート

## 🧞 コマンド

すべてのコマンドは、プロジェクトルートディレクトリから実行してください：

| コマンド                    | アクション                                         |
| :------------------------ | :----------------------------------------------- |
| `pnpm install`            | 依存関係をインストール                               |
| `pnpm dev`                | 開発サーバーを `localhost:4321` で起動              |
| `pnpm build`              | 本番用サイトを `./dist/` にビルド                    |
| `pnpm preview`            | ローカルでビルド結果をプレビュー                      |
| `pnpm lint`               | Biomeでソースコードをリント                         |
| `pnpm format`             | Biomeでソースコードをフォーマット                    |
| `pnpm check`              | Astro checkでTypeScript検証（`.astro`ファイル含む） |
| `pnpm astro ...`          | Astro CLIコマンド（例：`astro add`, `astro check`） |
| `pnpm astro -- --help`   | Astro CLIのヘルプを表示                           |

## � 開始方法

1. 依存関係をインストール:
   ```bash
   pnpm install
   ```

2. 開発サーバーを起動:
   ```bash
   pnpm dev
   ```

3. ブラウザで `http://localhost:4321` を開いて確認

### 🔣 Lucide Icons (lucide-astro)

簡単な使用例（Astroコンポーネント内）:

```astro
---
import { IconActivity } from 'lucide-astro';
---

<IconActivity class="w-6 h-6 text-blue-500" />
```

詳しくは公式ガイドを参照してください:

- https://lucide.dev/guide/packages/lucide-astro

## 📚 参考資料

- **[Astro](https://docs.astro.build/ja/)** - Astroの公式ドキュメント
- **[Tailwind CSS](https://tailwindcss.com)** - Tailwind CSSの公式ドキュメント
- **[Biome](https://biomejs.dev)** - Biomeの公式ドキュメント
- **[Lucide](https://lucide.dev/guide/packages/lucide-astro)** - Lucideの公式ドキュメント

