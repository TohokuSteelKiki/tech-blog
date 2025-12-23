# Tech Blog

個人の技術ブログサイトです。MkDocsを使用して静的サイトを生成し、GitHub Pagesでホスティングしています。

## セットアップ

```bash
# 仮想環境の作成と有効化
python -m venv .venv
.venv\Scripts\Activate.ps1  # Windows PowerShell
# source .venv/bin/activate  # Linux/Mac

# 依存パッケージのインストール
pip install -r requirements.txt
# または
pip install mkdocs mkdocs-material
```

## ローカル開発

```bash
# 開発サーバーの起動
mkdocs serve

# ブラウザで http://127.0.0.1:8000 にアクセス
```

## ビルド

```bash
# サイトのビルド
mkdocs build

# クリーンビルド（推奨）
mkdocs build --clean
```

## デプロイ

```bash
# GitHub Pagesへデプロイ（クリーンビルド推奨）
mkdocs gh-deploy --clean
```

### ⚠️ 重要: クリーンビルドの必要性

MkDocsのインクリメンタルビルドは、ファイルの依存関係を正しく検出できず、**古いHTMLファイルが残る場合があります**。

以下の場合は必ず`--clean`オプションを使用してください：

- 記事を更新した後のデプロイ
- レイアウトやテーマを変更した後
- 古いコンテンツが表示される問題が発生した場合

```bash
# 常にクリーンビルドを使用（推奨）
mkdocs gh-deploy --clean
```

または、手動でsiteディレクトリを削除：

```powershell
Remove-Item -Path site -Recurse -Force
mkdocs build
```

## プロジェクト構成

```
tech_blog/
├── docs/              # Markdownソースファイル
│   ├── index.md       # トップページ
│   └── articles/      # 記事ディレクトリ
├── site/              # ビルド出力（生成されるHTML）
├── mkdocs.yml         # MkDocs設定ファイル
└── README.md          # このファイル
```

## 記事の追加

1. `docs/articles/`に新しいMarkdownファイルを作成
2. ファイル名の推奨形式: `YYYY-MM-DD_タイトル.md`
3. ローカルで確認: `mkdocs serve`
4. デプロイ: `mkdocs gh-deploy --clean`
