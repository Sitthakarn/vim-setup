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
Here are the basics of how to use the plugin:

Use the natural vim navigation keys hjkl to navigate the files.
Press o to open the file in a new buffer or open/close directory.
Press t to open the file in a new tab.
Press i to open the file in a new horizontal split.
Press s to open the file in a new vertical split.
Press p to go to parent directory.
Press r to refresh the current directory.
All other keyboard shortcuts can be found by pressing ?. It will open a special help screen with the shortcut listings. Press ? again to get back to file tree.

To close the plugin execute the :NERDTreeClose command.

Typing :NERDTree and :NERDTreeClose all the time is really inconvenient. Therefore I have mapped the toggle command :NERDTreeToggle to the F2 key. This way I can quickly open and close Nerd Tree whenever I want. You can also map it to F2 by putting ```map <F2> :NERDTreeToggle<CR>``` in your .vimrc file.
