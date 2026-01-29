# git-flowツールガイド

Git-flowワークフローを手動で実行することもできますが、「git-flow」という専用のコマンドラインツールを使用することで、このワークフローをより簡単に実践できます。

---

## git-flowツールとは

git-flowツールは、Git-flowワークフローの各操作を簡略化するための拡張機能です。ブランチの作成、マージ、削除といった一連の操作を、シンプルなコマンドで実行できます。

---

## git-flowツールのインストール

### Windows（Git for Windowsを使用している場合）

- 多くの場合、Git for Windowsにgit-flowが同梱されています
- 確認方法: コマンドプロンプトで `git flow version` を実行
- インストールされていない場合は、公式サイト（https://github.com/nvie/gitflow）の手順に従ってインストール

### macOS（Homebrewを使用）

```
brew install git-flow-avh
```

### Linux（Debian/Ubuntu）

```
sudo apt-get install git-flow
```

---

## git-flowツールの基本的な使い方

### 1. リポジトリの初期化

既存のGitリポジトリでgit-flowを使い始める際は、まず初期化を行います：

```
git flow init
```

このコマンドを実行すると、各ブランチの命名規則を設定するための質問が表示されます。通常はデフォルト値（Enterキーを押す）で問題ありません。

### 2. 新機能の開発（featureブランチ）

**新機能の開発を開始**

```
git flow feature start 機能名
```

- developブランチから `feature/機能名` ブランチが作成され、自動的にチェックアウトされます

**機能開発が完了したら**

```
git flow feature finish 機能名
```

- featureブランチがdevelopブランチにマージされます
- featureブランチが自動的に削除されます
- developブランチにチェックアウトされます

### 3. リリースの準備（releaseブランチ）

**リリース準備を開始**

```
git flow release start バージョン番号
```

- developブランチから `release/バージョン番号` ブランチが作成されます

**リリース準備が完了したら**

```
git flow release finish バージョン番号
```

- releaseブランチがmainとdevelopの両方にマージされます
- mainブランチにバージョン番号のタグが作成されます
- releaseブランチが自動的に削除されます

### 4. 緊急修正（hotfixブランチ）

**緊急修正を開始**

```
git flow hotfix start バージョン番号
```

- mainブランチから `hotfix/バージョン番号` ブランチが作成されます

**修正が完了したら**

```
git flow hotfix finish バージョン番号
```

- hotfixブランチがmainとdevelopの両方にマージされます
- mainブランチにバージョン番号のタグが作成されます
- hotfixブランチが自動的に削除されます

---

## git-flowツールを使うメリット

- **操作の簡略化**: 複数のGitコマンドを組み合わせる必要がなく、1つのコマンドで完結します
- **ミスの防止**: マージ先の間違いやブランチの削除忘れを防げます
- **チーム全体での統一**: 全員が同じコマンドを使用することで、運用の一貫性が保たれます
- **学習コストの軽減**: Git-flowワークフローを理解していれば、直感的にコマンドを使用できます

---

## git-flowツールの注意点

- **リモートとの同期は手動**: git-flowツールはローカルでの操作を自動化しますが、リモートへのプッシュは別途実行する必要があります
- **ツールへの依存**: git-flowツールに慣れすぎると、基本的なGitコマンドを忘れてしまう可能性があります。基礎知識は維持することが重要です
- **GUIツールとの併用**: Fork、SourceTree、TortoiseGitなどのGUIツールでも、git-flowの操作をサポートしている場合があります

---

## よく使うコマンド一覧

### featureブランチ

```
git flow feature start <機能名>     # 機能開発を開始
git flow feature finish <機能名>    # 機能開発を完了
git flow feature publish <機能名>   # リモートに公開
git flow feature pull <機能名>      # リモートから取得
```

### releaseブランチ

```
git flow release start <バージョン>   # リリース準備を開始
git flow release finish <バージョン>  # リリースを完了
git flow release publish <バージョン> # リモートに公開
```

### hotfixブランチ

```
git flow hotfix start <バージョン>    # 緊急修正を開始
git flow hotfix finish <バージョン>   # 緊急修正を完了
git flow hotfix publish <バージョン>  # リモートに公開
```

---

## トラブルシューティング

### git-flowコマンドが見つからない

**確認方法**

```
git flow version
```

バージョンが表示されない場合は、インストールされていません。上記のインストール手順を参照してください。

### finishコマンドでマージの競合が発生した

競合が発生した場合は、通常のGitの手順で競合を解決してください：

1. 競合ファイルを編集して解決
2. `git add <ファイル名>` で変更をステージング
3. `git commit` でコミット
4. 再度 `git flow <ブランチタイプ> finish <名前>` を実行

### リモートにプッシュされない

git-flowツールは、ローカルでのマージ操作のみを行います。リモートにプッシュするには、別途以下のコマンドを実行してください：

```
git push origin main
git push origin develop
git push --tags
```

---

## まとめ

git-flowツールを使用することで、Git-flowワークフローを簡単かつ確実に実践できます。特に、チーム全体で統一されたワークフローを維持したい場合に有効です。

ただし、ツールに依存しすぎず、基本的なGitコマンドの理解も維持することが重要です。
