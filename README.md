# vim-setup
My vim setup file

## Install vim setup files

```bash
$ vim ~/.vimrc
```

Copy this scripts.

```
"syntax related configuration
set backspace=2
"set paste
syntax on
"set foldmethod=syntax

map <F2> :NERDTreeToggle<CR>
"autocmd vimenter * NERDTree
autocmd StdinReadPre * let s:std_in=1
autocmd VimEnter * if argc() == 1 && isdirectory(argv()[0]) && !exists("s:std_in") | exe 'NERDTree' argv()[0] | wincmd p | ene | exe 'cd '.argv()[0] | endif

"Indentation related settings

set autoindent
"set cindent
set shiftwidth=4
set softtabstop=4
set expandtab
set number
set hlsearch




"view related changes
set nu
"set background=dark
colorscheme Monokai


"...
"SETTING UP THE VIM-PLUG PLUGIN MANAGER

"Start of vim-plug manager
call plug#begin() 

	Plug 'scrooloose/nerdtree'
	Plug 'scrooloose/syntastic'
	Plug 'bling/vim-airline'
	Plug 'flazz/vim-colorschemes'
        Plug 'ervandew/supertab'
        Plug 'SirVer/ultisnips'

call plug#end() 
"End vim-plug manager



"nerdTree plugin settings
:map <C-n> :NERDTree
"autocmd vimenter * NERDTree



"ULTI SNIP SETTINGS
" Trigger configuration. Do not use <tab> if you use https://github.com/Valloric/YouCompleteMe.
let g:UltiSnipsExpandTrigger="<tab>"
let g:UltiSnipsJumpForwardTrigger="<c-b>"
let g:UltiSnipsJumpBackwardTrigger="<c-z>"
"If you want :UltiSnipsEdit to split your window.
let g:UltiSnipsEditSplit="vertical"
let g:UltiSnipsSnippetsDir="~/.vim/st-ulti-snippets"
let g:UltiSnipsSnippetDirectories = ['st-ulti-snippets']



"syntasctic settings //syntax checking pluignin
set statusline+=%#warningmsg#
set statusline+=%{SyntasticStatuslineFlag()}
set statusline+=%*

let g:syntastic_always_populate_loc_list = 1
let g:syntastic_auto_loc_list = 1
let g:syntastic_check_on_open = 1
let g:syntastic_check_on_wq = 0

"vim javascript configurations


let g:javascript_plugin_jsdoc = 1
let g:javascript_plugin_ngdoc = 1
let g:javascript_plugin_flow = 1
let g:javascript_conceal_function       = "ƒ"
let g:javascript_conceal_null           = "ø"
let g:javascript_conceal_this           = "@"
let g:javascript_conceal_return         = "⇚"
let g:javascript_conceal_undefined      = "¿"
let g:javascript_conceal_NaN            = "ℕ"
let g:javascript_conceal_prototype      = "¶"
let g:javascript_conceal_static         = "•"
let g:javascript_conceal_super          = "Ω"
let g:javascript_conceal_arrow_function = "⇒"



"javascript libratry syntax Plug 'othree/javascript-libraries-syntax.vim'

let g:used_javascript_libs = 'jquery,angularjs,angularui,angularuirouter,chai'

"adding some angular syntak for removing syntastic to throw error
let g:syntastic_html_tidy_ignore_errors = ['proprietary attribute "ng-']
let g:syntastic_html_tidy_ignore_errors = ['proprietary attribute "ui-']
let g:syntastic_html_tidy_ignore_errors = ['proprietary attribute "rr-']
let g:syntastic_html_tidy_ignore_errors=[
    \'proprietary attribute "ng-',
    \'proprietary attribute "uib-',
    \'proprietary attribute "pdk-',
    \'proprietary attribute "ui-'
    \'proprietary attribute "rr-'
    \'proprietary attribute "layout'
    \]
"markdown
"autocmd BufNewFile,BufReadPost *.md set filetype=markdown
filetype plugin indent on
```


## Install vim-plug manager 

```
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

## Install NERDTree 

```
$ git clone https://github.com/scrooloose/nerdtree.git ~/.vim/pack/vendor/start/nerdtree
$ vim -u NONE -c "helptags ~/.vim/pack/vendor/start/nerdtree/doc" -c q
```
Then put ```autocmd vimenter * NERDTree``` in .vimrc file.

### Here are the basics of how to use the plugin:

Use the natural vim navigation keys hjkl to navigate the files.
Press o to open the file in a new buffer or open/close directory.
Press t to open the file in a new tab.
Press i to open the file in a new horizontal split.
Press s to open the file in a new vertical split.
Press p to go to parent directory.
Press r to refresh the current directory.
All other keyboard shortcuts can be found by pressing ?. It will open a special help screen with the shortcut listings. Press ? again to get back to file tree.

To close the plugin execute the :NERDTreeClose command.

Typing ```:NERDTree``` and ```:NERDTreeClose``` all the time is really inconvenient. 

Or mapped the toggle command :NERDTreeToggle to the F2 key. by putting ```map <F2> :NERDTreeToggle<CR>``` in your .vimrc file.

## Installation Syntastic

<a name="requirements"></a>

### 2.1\. Requirements

Syntastic itself has rather relaxed requirements: it doesn't have any external
dependencies, and it needs a version of [Vim][vim] compiled with a few common
features: `autocmd`, `eval`, `file_in_path`, `modify_fname`, `quickfix`,
`reltime`, `statusline`, and `user_commands`. Not all possible combinations of
features that include the ones above make equal sense on all operating systems,
but Vim version 7 or later with the "normal", "big", or "huge" feature sets
should be fine.

Syntastic should work with any modern plugin managers for Vim, such as
[NeoBundle][neobundle], [Pathogen][pathogen], [Vim-Addon-Manager][vam],
[Vim-Plug][plug], or [Vundle][vundle]. Instructions for installing syntastic
with [Pathogen][pathogen] are included below for completeness.

Starting with Vim version 7.4.1486 you can also load syntastic using the
standard mechanism of packages, without the help of third-party plugin managers
(see `:help packages` in Vim for details). Beware however that, while support
for packages has been added in Vim 7.4.1384, the functionality needed by
syntastic is present only in versions 7.4.1486 and later.

Last but not least: syntastic doesn't know how to do any syntax checks by
itself. In order to get meaningful results you need to install external
checkers corresponding to the types of files you use. Please consult the
[manual][checkers] (`:help syntastic-checkers` in Vim) for a list of supported
checkers.

<a name="installpathogen"></a>

### 2.2\. Installing syntastic with Pathogen

If you already have [Pathogen][pathogen] working then skip [Step 1](#step1) and go to
[Step 2](#step2).

<a name="step1"></a>

#### 2.2.1\. Step 1: Install pathogen.vim

First I'll show you how to install Tim Pope's [Pathogen][pathogen] so that it's easy to
install syntastic. Do this in your terminal so that you get the `pathogen.vim`
file and the directories it needs:
```sh
mkdir -p ~/.vim/autoload ~/.vim/bundle && \
curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim
```
Next you *need* to add this to your `~/.vimrc`:
```vim
execute pathogen#infect()
```

<a name="step2"></a>

#### 2.2.2\. Step 2: Install syntastic as a Pathogen bundle

You now have pathogen installed and can put syntastic into `~/.vim/bundle` like
this:
```sh
cd ~/.vim/bundle && \
git clone --depth=1 https://github.com/vim-syntastic/syntastic.git
```
Quit vim and start it back up to reload it, then type:
```vim
:Helptags
```
If you get an error when you do this, then you probably didn't install
[Pathogen][pathogen] right. Go back to [Step 1](#step1) and make sure you did the
following:

1. Created both the `~/.vim/autoload` and `~/.vim/bundle` directories.
2. Added the `execute pathogen#infect()` line to your `~/.vimrc` file
3. Did the `git clone` of syntastic inside `~/.vim/bundle`
4. Have permissions to access all of these directories.

<a name="settings"></a>

## 3\. Recommended settings

Syntastic has numerous options that can be configured, and the defaults
are not particularly well suitable for new users. It is recommended
that you start by adding the following lines to your `vimrc` file, and
return to them after reading the manual (see `:help syntastic` in Vim):
```vim
set statusline+=%#warningmsg#
set statusline+=%{SyntasticStatuslineFlag()}
set statusline+=%*

let g:syntastic_always_populate_loc_list = 1
let g:syntastic_auto_loc_list = 1
let g:syntastic_check_on_open = 1
let g:syntastic_check_on_wq = 0
```

<a name="faq"></a>
