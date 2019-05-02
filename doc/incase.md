# こんなときどうしよう？

## staged にした変更を unstaged にしたい
`git add -i` から revert を選び，指示に従う．

## HEAD と unstaged な変更との差分を見たい
```
$ git diff
```

## HEAD と staged な変更との差分を見たい
```
$ git diff --cached
```

## working tree 上での変更を取り消し，HEAD の状態に戻したい
一旦コミットしてから `git revert` するべき？

パッチをつくって修正する方法は以下．
```
$ git apply --reverse <(git diff dir/to/file)
```

