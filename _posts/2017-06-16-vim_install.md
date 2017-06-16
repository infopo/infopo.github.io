---
layout: post
title: Vim 설정
category: Ubuntu
---

## 플러그인 매니저 Vundle

1. setup Vundle
    ```
    $ git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
    ```
2. configure
    `/etc/vim` 아래에 vimrc 파일이 있습니다. 혹시 저 위치에 없다면 `$ locate vimrc`로 찾으면 됩니다. `vimrc`로 들어가 아래의 내용을 붙여 넣습니다.

    ```vim
    set nocompatible              " be iMproved, required
    filetype off                  " required

    " set the runtime path to include Vundle and initialize
    set rtp+=~/.vim/bundle/Vundle.vim
    call vundle#begin()

    " let Vundle manage Vundle, required
    Plugin 'VundleVim/Vundle.vim'

    " The following are examples of different formats supported.
    " Keep Plugin commands between vundle#begin/end.

    " plugin on GitHub repo
    Plugin 'tpope/vim-fugitive'

    " Git plugin not hosted on GitHub
    Plugin 'git://git.wincent.com/command-t.git'

    " git repos on your local machine (i.e. when working on your own plugin)
    Plugin 'file:///home/gmarik/path/to/plugin'

    " The sparkup vim script is in a subdirectory of this repo called vim.
    " Pass the path to set the runtimepath properly.
    Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}

    " All of your Plugins must be added before the following line
    call vundle#end()            " required
    filetype plugin indent on    " required
    ```
