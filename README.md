# my-vim

## Neovim
```bash
brew install neovim
# for who are not native English speakers
brew tap daipeihust/tap && brew install im-select
# the config file
mkdir -p ~/.config/nvim && vim ~/.config/nvim/init.lua
```

```lua
-- [[ ~/.config/nvim/init.lua ]]

--2 try

vim.g.mapleader = " "
local g = vim.g

-- vimscript make map easier
vim.cmd([[
mapclear!

" brew tap daipeihust/tap && brew install im-select
inoremap <C-c> <C-c>:!im-select com.apple.keylayout.ABC<CR><CR>
nnoremap <leader>vf va{Vo
" special copy and paste
vnoremap <leader>y "*y
nnoremap <leader>y "*y

noremap <leader>w :w<CR>
" quick .rc
noremap cv :silent! luafile %<CR>:silent! source %<CR>

" move with center
noremap <C-d> <C-d>zz
noremap <C-u> <C-u>zz
noremap n nzzzv
noremap N Nzzzv
]])


-- [[ vars ]]
g.t_co = 256
g.background = "dark"

-- [[ opt ]]
local opt = vim.opt

opt.number = true
opt.relativenumber = true 
opt.scrolloff = 7                
opt.signcolumn = "number"

opt.syntax = "ON"
opt.termguicolors = true

opt.ignorecase = true            
opt.smartcase = true             
opt.hlsearch = false             

opt.expandtab = true             
opt.shiftwidth = 4               
opt.softtabstop = 4              
opt.tabstop = 4                  

opt.splitright = true            
opt.splitbelow = true            

-- [[ plug ]]
-- Update the packpath
vim.o.packpath = vim.o.packpath .. ',' .. vim.fn.stdpath('config') .. '/site'
local map = vim.api.nvim_set_keymap
-- try

map('n', '<leader>ps', ':PackerSync<CR>', {noremap = true})

require('mini.completion').setup() -- auto show completion
require('mini.cursorword').setup() -- highlight current word
require('mini.pairs').setup() -- ()[]{}""''

return require('packer').startup({function(use)
    --2 try 
    use 'mhinz/vim-startify'
    use 'jghauser/mkdir.nvim'

    use 'wakatime/vim-wakatime'
    use 'github/copilot.vim'

    use 'echasnovski/mini.nvim'
    use {'kana/vim-textobj-entire', -- yae
    requires = 'kana/vim-textobj-user' }
    use 'tpope/vim-surround' -- S
    use 'tpope/vim-sensible' -- nothing
    use 'tpope/vim-commentary' -- gcc

end,
config = {
    package_root = vim.fn.stdpath('config') .. '/site/pack'
}})

```
