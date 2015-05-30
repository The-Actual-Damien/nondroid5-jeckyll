---
layout: post
title: Mac homebrew設定
---

MacにHomebrewでインストールしておくべきものをリストアップしてみた

grepやackよりもagでは！

```
$ brew install the_silver_searcher
```

ターミナルのスクリーン分割tmux

```
$ brew install tmux
```

diffを色付きで表示させる colordiff

```
$ brew install colordiff
```

.zshrcにdiffをcolordiffにエイリアスすると便利

```
$ alias diff='colordiff'
```

cmake

```
$ brew install cmake
```

```
$ brew install hub
```

```
$ brew install pstree
```

```
$ brew install tree
```

```
$ brew install wget
```

現在のシェルを確認

```
$ dscl localhost -read Local/Default/Users/$USER UserShell
```

インストールされているシェルとそのパスを確認

```
$ cat /etc/shells
```

結果の確認

```
/bin/bash
/bin/csh
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
```

~/.zshrc を編集

```
$ vi ~/.zshrc
```

テーマの変更(デフォルトでは、robbyrussell)

```
$ vi ~/.zshrc
```

テーマはここにおいてあります

[robbyrussell/oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh/wiki/Themes)
