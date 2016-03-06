# Vim 篇
```
"关闭Vi的兼容模式
set nocompatible
" Windows快捷键
source $VIMRUNTIME/mswin.vim
behave mswin
""""""""""""""""""""" 编码设置 """"""""""""""""""""""""""
if has("multi_byte")
  " 可自动识别的文件类型为带 BOM 字符的 Unicode 文件、UTF-8 编码的文件和 GBK 编码的文件。
  "set bomb
  set fileencodings=ucs-bom,utf-8,chinese,taiwan,japan,korea,latin1
  " CJK environment detection and corresponding setting
  if v:lang =~ "^zh_CN"
    " Simplified Chinese, on Unix euc-cn, on MS-Windows cp936
    set encoding=chinese
    set termencoding=chinese
    if &fileencoding == ''
      set fileencoding=chinese
    endif
  elseif v:lang =~ "^zh_TW"
    " Traditional Chinese, on Unix euc-tw, on MS-Windows cp950
    set encoding=taiwan
    set termencoding=taiwan
    if &fileencoding == ''
      set fileencoding=taiwan
    endif
  elseif v:lang =~ "^ja_JP"
    " Japanese, on Unix euc-jp, on MS-Windows cp932
    set encoding=japan
    set termencoding=japan
    if &fileencoding == ''
      set fileencoding=japan
    endif
  elseif v:lang =~ "^ko"
    " Korean on Unix euc-kr, on MS-Windows cp949
    set encoding=korea
    set termencoding=korea
    if &fileencoding == ''
      set fileencoding=korea
    endif
  endif
   " Detect UTF-8 locale, and override CJK setting if needed
  if v:lang =~ "utf8$" || v:lang =~ "UTF-8$"
    set encoding=utf-8
  endif
else
  echoerr 'Sorry, this version of (g)Vim was not compiled with "multi_byte"'
endif
""""""""""""""""""""" 编码设置 """"""""""""""""""""""""""
" 指定菜单语言
set encoding=utf-8
set termencoding=utf-8
set langmenu=zh_CN.UTF-8
language message zh_CN.UTF-8
source $VIMRUNTIME/delmenu.vim
source $VIMRUNTIME/menu.vim
"隐藏菜单栏
"set guioptions-=m
"隐藏工具栏
set guioptions-=T
"显示工具按钮
"隐藏具体按钮
"aunmenu ToolBar.Make
"aunmenu ToolBar.TagJump
"aunmenu ToolBar.SaveSesn
"aunmenu ToolBar.LoadSesn
"aunmenu ToolBar.RunScript
"aunmenu ToolBar.FindHelp
"aunmenu ToolBar.Help
"aunmenu ToolBar.Print
"set guioptions-=L " 隐藏左侧滚动条
set guioptions-=r " 隐藏右侧滚动条
"set guioptions-=b " 隐藏底部滚动条
"set showtabline=0 " 隐藏Tab栏
" 设置字体
set guifont=Monaco\ 10.5
" 设置开启的窗口大小
set lines=35 columns=90
" 设置首选文件编码
set fileencodings=ucs-bom,utf-8,cp936,gb18030,gb2312,big5,latin-1
" 设置新文件的编码为 UTF-8
set fileencoding=utf8
" 标题栏显示编码类型
auto BufEnter * let &titlestring =  expand("%:p") . " (" . &fenc . ")"
" 设置为智能缩进
set smartindent
" 解决自动换行格式下, 如高度在折行之后超过窗口高度结果这一行看不到的问题
set display=lastline
" 启动时不显示 捐赠提示
set shortmess=atI
" 自动切换当前目录为当前文件所在的目录
set autochdir
" 实时搜索
set incsearch
" 搜索时高亮显示被找到的文本
set hlsearch
" 显示括号匹配
set showmatch
"搜索时忽略大小写
set ignorecase
" 自动换行
set wrap
"折叠
"set foldmethod=indent
"设定显示行数
set number
"设置文件保存格式
set fileformats=unix,dos
" 命令行补全
set wildmenu
" 上下可视行数
set scrolloff=3
" 拼写检查
set spell
" 设置标尺代码对其
set cuc
" 不生成备份文件
set nobackup
" 不生成交换文件
set noswapfile
" 在状态栏显示运行命令
set showcmd
"语法高亮显示
syntax enable
syntax on
" 当前主题
colorscheme desert
" 高亮当前行
setlocal cursorline
" Table大小为4 且为空格
"显示多少空格
set tabstop=4
"在编辑模式时，按退格键退回缩进的长度
set softtabstop=4
"在每一级缩进的长度
set cindent shiftwidth=4
set autoindent shiftwidth=4
"缩进用空格表示
set expandtab
" set noexpandtab 表示用制表符表示缩进
" 插入模式下上下左右移动光标
inoremap <c-h> <left>
inoremap <c-l> <right>
inoremap <c-j> <c-o>gj
inoremap <c-k> <c-o>gk
"""""""""" Plugin Vundle Start """"""""""
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
Plugin 'gmarik/Vundle.vim'
"airline
"Plugin 'bling/vim-airline'
" Indent
Plugin 'Shougo/neocomplete.vim'
" HTML
Plugin 'mattn/emmet-vim'
"Markdown
Plugin 'godlygeek/tabular'
Plugin 'plasticboy/vim-markdown'
" Sync
Plugin 'scrooloose/syntastic'
"Tree
Plugin 'scrooloose/nerdtree'
call vundle#end()
filetype off
filetype plugin on
filetype indent on
"""""""""" Plugin Vundle End """"""""""
"""""""""" Plugin Config detial """"""""""
" neocomplete
let g:acp_enableAtStartup = 0
let g:neocomplete#enable_at_startup = 1
let g:neocomplete#enable_fuzzy_completion = 1
let g:neocomplete#enable_smart_case = 1
let g:neocomplete#sources#syntax#min_keyword_length = 2
inoremap <expr><TAB>  pumvisible() ? "\<C-n>" : "\<TAB>"
inoremap <expr><Space> pumvisible() ? neocomplete#close_popup() : "\<Space>"
autocmd FileType css setlocal omnifunc=csscomplete#CompleteCSS
autocmd FileType html,markdown setlocal omnifunc=htmlcomplete#CompleteTags
autocmd FileType javascript setlocal omnifunc=javascriptcomplete#CompleteJS
autocmd FileType python setlocal omnifunc=pythoncomplete#Complete
autocmd FileType xml setlocal omnifunc=xmlcomplete#CompleteTags
" Emmet
let g:user_emmet_mode='i'
let g:user_emmet_expandabbr_key='<c-e>'
"Markdown
let g:vim_markdown_folding_disabled=1
" Sync
set statusline+=%#warningmsg#
set statusline+=%{SyntasticStatuslineFlag()}
set statusline+=%*
let g:syntastic_always_populate_loc_list = 1
let g:syntastic_auto_loc_list = 1
let g:syntastic_check_on_open = 1
let g:syntastic_check_on_wq = 0
" NERDTree config
 map <F2> :NERDTreeToggle<CR>
 autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTreeType") &&b:NERDTreeType == "primary") | q | endif
" <F5> 运行python程序
map <F5> :w<cr>:!python %<cr>
```
* 这里使用的是Vundle来管理vim的包，很方便。首先要安装Vundle:
`$ git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim`
* 插件安装： `:PluginIntall`
* 插件升级： `:PluginUpdate`
* 插件删除： 首先把`.vimrc` 里面的`Plugin xxx`删除，然后运行`:PluginClear`
* 收集的一些不错的关于Vim的站点：
    - http://vimawesome.com/
    - http://vimcolors.com/
    - http://lilydjwg.is-programmer.com/
    - http://wiki.hotoo.me/Vim.html
    - http://edyfox.codecarver.org/html/vim_fileencodings_detection.html
    - http://zshou.is-programmer.com/
    - http://vim-adventures.com/
    - http://blog.nootn.com/tag/_vimrc/
    - http://wklken.me/posts/2013/06/11/linux-my-vim.html
    - http://www.study-area.org/tips/vim/Vim-9.html
