# Academic Poster Template

九州産業大学理工学部下川研用の学会発表ポスターテンプレートです。A0サイズの学会ポスター作成に最適化されたテンプレートで、tikzposterを使用した美しいレイアウトを提供します。

## 🚀 主な機能

- **A0サイズ対応**: 学会発表用の標準的なポスターサイズ
- **tikzposterベース**: 柔軟なブロックレイアウトシステム
- **日本語完全対応**: LuaLaTeX + luatexjaで最適化
- **自動PDF生成**: プルリクエスト時にPDFプレビューを自動作成
- **カスタマイズ可能**: 複数のテーマとブロックスタイルから選択
- **縦向き・横向き**: レイアウト変更が容易

## 📁 ファイル構成

```
├── a0poster.tex       # メインポスター文書（tikzposter形式）
└── .github/workflows/ # 自動ビルド設定
```

## 🔧 使用方法

### 自動セットアップ（推奨）
[thesis-management-tools](https://github.com/smkwlab/thesis-management-tools)の自動セットアップスクリプトを使用：

#### 下川研学生向け
```bash
DOC_TYPE=poster /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/smkwlab/thesis-management-tools/main/create-repo/setup.sh)"
```

#### それ以外の皆さん向け
```bash
INDIVIDUAL_MODE=true DOC_TYPE=poster /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/smkwlab/thesis-management-tools/main/create-repo/setup.sh)"
```

**自動セットアップの特徴**:

**下川研学生向け**:
- 学籍番号・ポスター名の対話的入力
- リポジトリ名: `学籍番号-ポスター名` (例: `smkwlab/k21rs001-jxiv2025-poster`)

**それ以外の皆さん向け**:
- リポジトリ名: `ポスター名` (例: `my-conference-poster`)

**共通機能**:
- リポジトリの自動作成とLaTeX環境の追加

### 手動セットアップ
1. このテンプレートから新しいリポジトリを作成
2. 下記手順でポスター作成を開始

### ポスター作成と編集

### 1. ポスター編集
`a0poster.tex` を編集してポスターを作成：
- **タイトル設定**: `\title{}`, `\author{}`, `\institute{}`
- **ブロック追加**: `\block{タイトル}{内容}`でセクション作成
- **レイアウト**: `\begin{columns}` でカラムレイアウト

### 2. PDF生成
- **自動生成**: プッシュ時に自動でPDFが生成
- **確認方法**: GitHub Actionsタブで状況確認
- **ダウンロード**: Artifactsから生成PDFを取得

### 3. ローカルビルド（オプション）
```bash
# LuaLaTeXでコンパイル（推奨）
lualatex a0poster.tex

# または一括処理
latexmk a0poster.tex
```

#### 基本的なポスター構造
`a0poster.tex` を編集してポスターを作成：

```latex
\documentclass[25pt, a0paper, portrait]{tikzposter}
\usepackage{luatexja}
\usepackage{luatexja-fontspec}

\usetheme{Simple}
\useblockstyle{Slide}

\title{ポスタータイトル}
\author{著者名}
\institute{所属機関}

\begin{document}

\maketitle

\begin{columns}
    \column{0.5} % 左カラム（幅50%）

    \block{研究背景}{
        研究の背景や動機を記述...
    }

    \block{研究目的}{
        研究の目的を明確に...
    }

    \column{0.5} % 右カラム（幅50%）

    \block{研究手法}{
        使用した手法の説明...
    }

    \block{結果と考察}{
        得られた結果と考察...
    }

\end{columns}

\end{document}
```

#### テーマとスタイルのカスタマイズ

**利用可能なテーマ** (`\usetheme{}`で指定):
```latex
\usetheme{Simple}   % シンプルでクリーン（デフォルト）
\usetheme{Minimal}  % 最小限の装飾
\usetheme{Basic}    % 伝統的なアカデミックスタイル
\usetheme{Autumn}   % 暖色系のカラフルなデザイン
\usetheme{Desert}   % 砂漠をイメージした色合い
```

**ブロックスタイル** (`\useblockstyle{}`で指定):
```latex
\useblockstyle{Slide}    % モダンなプレゼンスタイル（デフォルト）
\useblockstyle{Minimal}  % シンプルなブロック
\useblockstyle{Basic}    % 伝統的な枠線付き
\useblockstyle{Default}  % 標準のtikzposterスタイル
```

#### レイアウトオプション

**縦向き（portrait）から横向き（landscape）への変更**:
```latex
% 縦向き（デフォルト）
\documentclass[25pt, a0paper, portrait]{tikzposter}

% 横向き
\documentclass[25pt, a0paper, landscape]{tikzposter}
```

**カラム数の調整**:
```latex
% 2カラム（50%ずつ）
\begin{columns}
    \column{0.5}  % 左カラム
    \column{0.5}  % 右カラム
\end{columns}

% 3カラム
\begin{columns}
    \column{0.33}  % 左
    \column{0.33}  % 中央
    \column{0.33}  % 右
\end{columns}

% 非対称レイアウト（40% + 60%）
\begin{columns}
    \column{0.4}
    \column{0.6}
\end{columns}
```

#### よく使用する要素

**図の挿入**:
```latex
\block{実験結果}{
    \begin{tikzfigure}[実験データのグラフ]
        \includegraphics[width=0.8\linewidth]{figure.pdf}
    \end{tikzfigure}
}
```

**数式**:
```latex
\block{数理モデル}{
    提案手法は以下の式で表される：
    \begin{equation}
        f(x) = \sum_{i=1}^{n} w_i x_i + b
    \end{equation}
}
```

**箇条書き**:
```latex
\block{研究の特徴}{
    \begin{itemize}
        \item 高速な処理アルゴリズム
        \item 高精度な予測モデル
        \item スケーラブルな実装
    \end{itemize}
}
```

**表の作成**:
```latex
\block{実験結果の比較}{
    \begin{tabular}{|l|c|c|}
    \hline
    手法 & 精度 & 処理時間 \\
    \hline
    提案手法 & 95.2\% & 1.2秒 \\
    既存手法 & 89.7\% & 3.5秒 \\
    \hline
    \end{tabular}
}
```

### PDF生成とワークフロー

#### ローカルでのビルド
VS Code でファイル保存時に下記の latexmk が実行される
開発環境での確認用：

```bash
# latexmk使用（推奨）
latexmk a0poster.tex

# lualatex使用（個別実行の場合）
lualatex a0poster.tex

# クリーンアップ
latexmk -c
```

#### 自動PDF生成
GitHub Actionsにより以下のタイミングで自動的にPDFが生成される。

**プルリクエスト時（プレビュー）**:
1. ブランチを作成して変更をコミット
2. プルリクエストを作成
3. 自動的にPDFが生成され、ActionsのArtifactsからダウンロード可能
4. レビュー・修正のサイクルが効率化

**mainブランチへのプッシュ時**:
- 自動的にPDFをビルドして検証
- エラーがある場合はActionsログで確認可能

**タグ作成時（正式リリース）**:
```bash
git tag v1.0.0
git push origin v1.0.0
```
- 自動的にGitHubリリースが作成
- 完成版PDFがリリースに添付
- 学会提出前の最終版管理に最適

## 📋 適用シーンと選択指針

### このテンプレートが最適な用途
- **学会発表ポスター**: 国内・国際学会での研究発表
- **研究室紹介ポスター**: オープンキャンパスや研究室見学
- **研究成果ポスター**: 学内発表会や研究報告会
- **プロジェクト紹介**: 研究プロジェクトの概要説明

### 利用モードの比較

| 項目 | 下川研学生向け | それ以外の皆さん向け（INDIVIDUAL_MODE） |
|------|-----------|------------------------------|
| **対象ユーザー** | 学生 | 教員・研究者・一般ユーザー |
| **学籍番号** | 必須 | 不要 |
| **リポジトリ名** | `k21rs001-jxiv2025-poster` | `jxiv2025-poster` |
| **作成先** | smkwlab組織 | 個人アカウント |
| **管理体制** | 組織管理下 | 個人管理 |
| **使用例** | 学生の学会発表 | 教員の研究発表・プロジェクト紹介 |

## ⚙️ 環境詳細

### LaTeX エンジン
- **TeXLive 2025**: 最新の日本語LaTeX環境
- **LuaLaTeX**: Unicode対応の最新LaTeXエンジン
- **tikzposter**: 学術ポスター専用ドキュメントクラス
- **luatexja**: 日本語フォント最適化

### デザイン仕様
- **用紙サイズ**: A0 (841mm × 1189mm)
- **フォントサイズ**: 25pt（視認性重視）
- **レイアウト**: ブロックベースの柔軟な配置
- **カラー**: テーマごとに最適化された配色

### 自動化機能
- **依存関係更新**: TeXLive環境の自動更新チェック
- **PDF生成**: プッシュ時の自動ビルド
- **アーティファクト管理**: プレビュー版と正式版の自動管理

## 🔧 カスタマイズ

### ファイル名の変更
`.github/workflows/latex-build.yml` の `files` パラメータを編集：

```yaml
files: a0poster, another-poster
```

デフォルトでは `a0poster.tex` のみビルドされます。

### 用紙サイズの変更
```latex
% A0サイズ（デフォルト）
\documentclass[25pt, a0paper, portrait]{tikzposter}

% A1サイズ
\documentclass[25pt, a1paper, portrait]{tikzposter}

% A2サイズ
\documentclass[25pt, a2paper, portrait]{tikzposter}
```

## 🆘 トラブルシューティング

### コンパイルエラー
1. GitHub Actionsのログを確認
2. ローカル環境での構文チェック
3. 文字エンコーディング（UTF-8）の確認
4. LuaLaTeXの使用を確認（pLaTeX/upLaTeXではビルドできません）

### PDF生成されない
1. `.tex` ファイル名が `files` パラメータと一致しているか確認
2. ファイルの構文エラーがないか確認
3. GitHub Actionsの実行権限を確認

### 日本語表示の問題
1. 文字エンコーディングがUTF-8であることを確認
2. `\usepackage{luatexja}` の記述確認
3. LuaLaTeXエンジンの使用を確認

### レイアウトが崩れる
1. カラム幅の合計が1.0を超えていないか確認
2. ブロック内のコンテンツサイズを調整
3. フォントサイズを調整（documentclassのオプション）

## 💡 ポスター作成のヒント

### 効果的なポスターデザイン
- **視認性**: 3メートル離れても読めるフォントサイズ
- **シンプル**: 情報を詰め込みすぎない
- **視覚要素**: グラフや図を効果的に使用
- **カラー**: 統一感のある配色を選択

### 推奨される構成
1. **タイトル**: 研究内容が一目で分かるタイトル
2. **背景**: 研究の動機と重要性
3. **目的**: 何を明らかにするか
4. **手法**: どのように研究したか
5. **結果**: 何が分かったか（図表中心）
6. **結論**: 研究の意義と今後の展望

## 📚 関連リンク

- [LaTeX環境構築ガイド](https://github.com/smkwlab/latex-environment)
- [論文執筆テンプレート](https://github.com/smkwlab/sotsuron-template)
- [tikzposter公式ドキュメント](https://www.ctan.org/pkg/tikzposter)
- [下川研究室](https://shimokawa-lab.kyusan-u.ac.jp/)

## 📄 ライセンス

このテンプレートは研究・教育目的での利用を想定しています。
