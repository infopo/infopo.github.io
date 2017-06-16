---
layout: post
title: Vim 설정
category: Ubuntu
---

## 플러그인 매니저 Vundle

1. 다운로드
    ```
    $ git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
    ```
2. 설정  

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
3. 설치
    `vim`을 실행하고, `:PluginInstall`로 Vundle을 설치하면 됩니다.


## AutoComplPop, The-NERD-tree, taglist-plus 플러그인 설치

아래의 내용을 `vimrc`에 추가합니다
```vim
" Vim에서 자동완성 기능(Ctrl + P)을 키입력하지 않더라도 자동으로 나타나게 됩니다.
Plugin 'AutoComplPop'

" Vim에서 파일 탐색기를 사용할 수 있게 합니다.
Plugin 'The-NERD-tree'

" 열려있는 소스파일의 클래스, 함수, 변수 정보 창을 보여줍니다.
Plugin 'taglist-plus'


"Nerd Tree, tag list plugins에 대한 설정입니다.
" NERD Tree를 왼쪽에 생성합니다.
let NERDTreeWinPos = "left"

" Tag list 창을 오른쪽으로 생성합니다.
let Tlist_Use_Right_Window = 1

" Tag list가 사용하는 ctags의 경로 설정입니다.
let Tlist_Ctags_Cmd = "/usr/bin/ctags"
let Tlist_Inc_Winwidth = 0
let Tlist_Exit_OnlyWindow = 0
let Tlist_Auto_Open = 0

"f4, f8로 껐다가 켤 수 있습니다.
nnoremap <F4> :NERDTreeToggle<CR>
nmap <F8> :TlistToggle<CR>

"vim에 들어갈 때 자동으로 NERDTree 시작합니다.
autocmd VimEnter * NERDTree

"새탭 열었을 때 NERDTree자동 생성
autocmd BufWinEnter * NERDTreeMirror
```

아까와 동일하게 `:PluginInstall`로 설치합니다.

## auto-pairs, toggle_mouse 플러그인 설치
```
$ git clone https://github.com/jiangmiao/auto-pairs
$ git clone https://github.com/nvie/vim-togglemouse
```
받은 파일 중에서 `toggle_mouse.vim`과 `auto-pairs.vim`을 `~/.vim/plugin`아래에 옮깁니다. (만약 해당 디렉토리가 없으면 생성해주면 됩니다.)  

`auto-pairs`는 괄호를 자동으로 닫아주는 기능을 합니다.  

`toggle_mouse`는 `f12`를 눌러 활성화/비활성화 시킵니다. `Mouse is for terminal`상태에서는 본문을 한 화면밖에 드래그할 수 없지만, `Mouse if for Vim (a)`상태에서는 한 화면 이상 드래그가 가능해집니다.  

## 기타 설정

```vim
";키를 누르면 자동으로 :로 변경해줍니다(vim 명령어 실행시).
nnoremap ; :

set ignorecase      " Do case insensitive matching
set smartcase       " Do smart case matching
set incsearch       " Incremental search

"검색결과를 하이라이팅합니다.
set hlsearch

",/을 연속으로 누르면 검색결과 하이라이팅이 사라집니다.
nmap <silent> ,/ :nohlsearch<CR>

"tab관련 설정입니다.
set shiftwidth=4
set smarttab      " insert tabs on the start of a line according to
                  "shiftwidth, not tabstop

" allow backspacing over everything in insert mode
set backspace=indent,eol,start

"use multiple of shiftwidth when indenting with '<' and '>'"
set shiftround

"터미널 상단의 탭에 해당 파일의 제목을 설정합니다.
set title

"syntax color change
colorscheme hybrid

"vi 실행시 number line을 생성합니다.
set nu

"줄 번호의 색깔을 지정합니다.
hi LineNr ctermfg=3

"선택된 코드블럭의 색을 지정합니다.
hi Visual term=reverse cterm=reverse guibg=Grey

"INSERT상태에서 붙여넣기를 실행할 때, f2를 누르면 내용이 정렬된 상태로 붙여넣기가 됩니다.
set pastetoggle=<F2>

"코드 작성시 블럭을 접는 것이 가능해집니다.
set foldmethod=indent
set foldlevel=99

"스페이스바로 접기가 가능해집니다.
nnoremap <space> za

"기본 인코딩을 utf-8로 지정합니다.
set encoding=utf-8

"sudo 모드가 아닐 때에도 파일 저장이 가능해집니다.
cmap w!! w !sudo tee % >/dev/null

"스칼라 언어 설정입니다.
set ic
set hls
set lbr
set autoindent
```
