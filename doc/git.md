# git

`git` はバージョン（履歴）管理システムです．

一つ一つのファイル単位ごとにバージョン管理しているわけではなく，一連の変更をまとめて一つのバージョンとすることができます．
どこまでの変更を一つのバージョンとするかはユーザが決めます（ユーザが任意の時点で新しいバージョンを作ることができます）．

`git` で管理されている最新のバージョンは `HEAD` と呼ばれます．
次のバージョンを作るときに反映される変更箇所は index と呼ばれます．
ファイルシステム（working tree）上で変更されたファイルも，ユーザが指定しない限りは index には追加されません．

たとえば，`foo.c`，`bar.c`，`baz.c` にまとめて変更した後，一旦 `foo.c` と `bar.c` の変更だけを次のバージョンに反映させ，その次のバージョンで `baz.c` の変更を反映させることもできます．

## `git add`

working tree 上で変更したファイルたちを index に追加するためのコマンドです．

```
$ git add foo.c  # foo.c を index に追加
```

`git add -i` を使うと対話的に操作を行うこともできます．

```
$ git add -i
           staged     unstaged path
  1:    unchanged        +1/-1 sample/bar.c
  2:        +1/-1      nothing sample/foo.c

*** Commands ***
  1: status	  2: update	  3: revert	  4: add untracked
  5: patch	  6: diff	  7: quit	  8: help
What now> 
```

この状態では，`bar.c` は `+1/-1`，すなわち 1 行の追加と 1 行の削除があったものの，それは index には追加されていない（unstaged）ことになっています．
また，`foo.c` は `+1/-1` の変更が index に追加されて（staged）いることがわかります．unstaged が nothing になっていることから，index に追加された状態と working tree 上での状態が同じであることもわかります．

ここから `bar.c` も index に追加したいときは，2 を選択します．

```
What now> 2
           staged     unstaged path
  1:    unchanged        +1/-1 sample/bar.c
Update>> 1
           staged     unstaged path
* 1:    unchanged        +1/-1 sample/bar.c
Update>> 
updated 1 path

*** Commands ***
  1: status	  2: update	  3: revert	  4: add untracked
  5: patch	  6: diff	  7: quit	  8: help
What now> 7
Bye.
```

プロンプトが `>` のときは単一選択で，`>>` のときは複数選択が可能です．
`>>` の詳細はこの章の最後に説明します．

ここで，先程 index に追加した `foo.c` を index から削除したいときは以下のようにします．

`git revert` とは別物のはず．

```
$ git add -i
           staged     unstaged path
  1:        +1/-1      nothing sample/bar.c
  2:        +1/-1      nothing sample/foo.c

*** Commands ***
  1: status	  2: update	  3: revert	  4: add untracked
  5: patch	  6: diff	  7: quit	  8: help
What now> 3
           staged     unstaged path
  1:        +1/-1      nothing sample/bar.c
  2:        +1/-1      nothing sample/foo.c
Revert>> 2
           staged     unstaged path
  1:        +1/-1      nothing sample/bar.c
* 2:        +1/-1      nothing sample/foo.c
Revert>> 
reverted 1 path

*** Commands ***
  1: status	  2: update	  3: revert	  4: add untracked
  5: patch	  6: diff	  7: quit	  8: help
What now> 1
           staged     unstaged path
  1:        +1/-1      nothing sample/bar.c
  2:    unchanged        +1/-1 sample/foo.c

*** Commands ***
  1: status	  2: update	  3: revert	  4: add untracked
  5: patch	  6: diff	  7: quit	  8: help
What now> 7
Bye.
```

unstaged になっていることがわかります．

patch はパッチを当てます．ここで変更したものが staged になります．
デフォルトでは `HEAD` の状態からファイルシステム上のファイルへの変更をするパッチを当てますが，編集したパッチを当てた場合は，index のみがその変更の対象になります（working tree 上のファイルはそのままです）．
patch をしたファイルに update した場合，ファイルシステム上で起きた変更が staged になります．

5 を選んだあと `e` を入力するとエディタが起動し，パッチの編集ができます．
開かれたエディタに方法が書かれていますが，`-` の行が消される行で，`+` の行が追加される行ですので，`-` を取り消したいときは `-` を ` ` にし，`+` を取り消したいときはその行全体を消せばよいです．

diff は HEAD の状態と staged の状態の差分を表示します．

`-N` オプションわからない．

untracked がよくわかってない．

### 選択の例
- `>> 2` 
  - `2` を追加
- `>> 2-5,7,9-`
  - `2` から `5` と `7` と `9` 以降を追加
- `>> -4`
  - `4` を削除（`4` 以前を追加ではない）

## `git mv`
`mv` コマンドのように，ファイルの移動や名前の変更を行い，その変更を staged の状態にします．

## `git rm`
`rm` コマンドのように，ファイルの削除を行い，その変更を staged の状態にします．

`--cached` オプションをつけると，index から staged な変更を取り消し，ファイルも消したことにしますが，working tree にあるファイルはそのまま残ります．

## `git commit`
新たなコミットを作ります．
これは，現在 index に入っている差分とその内容を記述するログメッセージ（ユーザが記述する）からなるものです．

この新しいコミットは `HEAD` の直接の子になります．
`HEAD` は通常現在のブランチの先端で，そのブランチは新しいコミットを指すようになります．
working tree に結びつけられたブランチが無く，`HEAD` が detached な場合は話が別です．

index に差分を追加する方法として，`git add` (`mv`, `rm`) を使うほか，`git commit` の引数にファイル名を与えるものもあります．
また，`git commit -a` によって全てのファイルを追加できるほか，`--interactive` オプションで対話的に行うこともできます．

ログメッセージは `-m` オプションで与えるとシェル上で行えますが，オプションなしで `commit` するとエディタ上で書くことができます．

```
$ git commit -m Nya
```

`COMMIT_EDITMSG`
```
  1 
  2 # Please enter the commit message for your changes. Lines starting 
  3 # with '#' will be ignored, and an empty message aborts the commit.
  4 #
  5 # On branch master
  6 # Your branch is ahead of 'origin/master' by 4 commits.
  7 #   (use "git push" to publish your local commits)
  8 #
  9 # Changes to be committed:
 10 #       modified:   foo.c
 11 #  
```

`--amend` オプションによって，直前のコミットのメッセージを書き直すことができます．

## `git reset`

`HEAD` を指定した状態に変更します．

`--soft`, `--hard`, `--mixed` を指定することで，index や working tree 上のファイルもリセットするかどうかを指定します．


