# Basic snapshotting
## `git add`
ファイルの内容を index に追加する

## `git status`
working tree の状態を表示する

## `git diff`
コミット間の差分，あるいはコミットと working tree の差分などを表示する

## `git commit`
変更をリポジトリに記録する

## `git reset`
HEAD を指定した状態に設定する

## `git rm`
working tree や index からファイルを削除する

## `git mv`
ファイル（またはディレクトリやシンボリックリンク）の移動や名前の変更をする

# Branching and Merging
## `git branch`
ブランチの表示，作成，削除をする

## `git checkout`
ブランチの切り替えや，working tree のファイルの復元をする

## `git merge`
二つ以上の開発履歴をマージする

## `git mergetool`
マージの競合を解決するツールを実行する

## `git log`
コミットのログを表示する

## `git stash`
作業中ディレクトリの dirty な変更を待避させておく

## `git tag`
GPG で署名されたタグオブジェクトの作成，表示，削除および検証をする

## `git worktree`
複数の working tree を管理する

# Sharing and Updating Projects
## `git fetch`
別のリポジトリからオブジェクトや ref をダウンロードする

## `git pull`
別のリポジトリやローカルのブランチから取得したり，統合したりする

## `git push`
関連づけられたオブジェクトでリモートの ref を更新する

## `git remote`
追跡されたリポジトリの集合を管理する

## `git submodule`
サブモジュールの初期化や更新，検査をする

# Inspection and Comparison
## `git show`
さまざまな種類のオブジェクトを表示する

## `git log`
コミットログを表示する

## `git diff`

## `git shortlog`
`git log` の出力を要約する

## `git describe`
利用できる ref に基づき，人間に読みやすい名前のオブジェクトを与える

# Patching
## `git apply`
ファイルや index（あるいは両方）にパッチを適用する

## `git cheery-pick`
あるコミットで導入される変更を適用する

## `git diff`

## `git rebase`
他の base tip の先端のコミットを再適用する

## `git revert`
あるコミットを元に戻す

# Debugging
## `git bisect`
二分探索によりバグが混入したコミットを検索する

## `git blame`
あるファイルの各行について，最後の変更はどのリビジョンで誰によるものか表示する

## `git grep`
パターンにマッチする行を表示する

# Email
## `git am`
メールボックスからパッチの列を適用する

## `git apply`

## `git format-patch`
メールで投稿するためのパッチを準備する

## `git send-email`
パッチを集めたものをメールで送信する

## `git request-pull`
保留中の変更の要約を生成する

# External Systems
## `git svn`
Subversion と Git 間での操作を行う

## `git fast-import`
fast Git data importer のためのバックエンド

# Server Admin
## `git daemon`
Git リポジトリのためのシンプルなサーバ

## `git update-server-info`
dumb なサーバを助けるための補助情報ファイルを更新する

# Administration
## `git clean`
追跡されていないファイルを working tree から削除する

## `git gc`
不要なファイルを削除し，ローカルリポジトリを最適化する

## `git fsck`
データベース中のオブジェクトの connectivity と validity を検証する

## `git reflog`
reflog (reference log) の情報を管理する

## `git filter-branch`
ブランチを書き換える

## `git instaweb`
gitweb で作業中のリポジトリを browse する

## `git archive`
named tree からファイルのアーカイブを作成する

## `git bundle`
オブジェクトと ref を移動する（アーカイブで？） 
