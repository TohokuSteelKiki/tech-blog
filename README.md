# Tech Blog

機器開発チームの技術ブログサイトです。MkDocsを使用して静的サイトを生成し、GitHub Pagesでホスティングしています。

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

## Git管理とワークフロー

このリポジトリは**2つのブランチ**で管理されています：

### mainブランチ（手動管理）
- **内容**: Markdownソースファイル（`docs/`）、設定ファイル
- **役割**: コンテンツの開発とバージョン管理
- **操作**: 通常のGit操作でcommit & push

### gh-pagesブランチ（自動管理）
- **内容**: ビルドされたHTMLファイル（`site/`の内容）
- **役割**: GitHub Pagesでの公開
- **操作**: `mkdocs gh-deploy`が自動的に管理

### 推奨ワークフロー

```bash
# 1. 記事を作成・編集
# docs/articles/新しい記事.md を作成

# 2. ローカルで確認
mkdocs serve

# 3. mainブランチにcommit & push（ソースファイルの管理）
git add docs/articles/新しい記事.md
git commit -m "新しい記事を追加"
git push origin main

# 4. GitHub Pagesにデプロイ（HTMLの生成と公開）
mkdocs gh-deploy --clean
```

### ブランチの役割

| ブランチ | 管理対象 | 操作方法 | 目的 |
|---------|---------|---------|------|
| `main` | Markdownソース | 手動commit/push | ソース管理・共同作業 |
| `gh-pages` | ビルドHTML | `mkdocs gh-deploy` | Webサイト公開 |

**重要**: 
- `docs/`は**mainブランチで管理**（.gitignoreに入れない）
- `site/`は**ビルド成果物**（.gitignoreに入れる、gh-pagesブランチで管理）
- `mkdocs gh-deploy`を実行しても、mainブランチへの自動commitは行われないため、**手動でcommitが必要**
