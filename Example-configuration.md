This is *not a recommended* configuration but rather a way to show how to configure the plugin.

```vim
" vim-plug

call plug#begin()
  Plug 'davidgranstrom/scnvim'
  " (optional) for snippets
  Plug 'SirVer/ultisnips'
call plug#end()

" scnvim

" post window at the bottom
let g:scnvim_postwin_orientation = 'h'

" remap send block
nmap <F5> <Plug>(scnvim-send-block)

" remap post window toggle
nmap <Space>o <Plug>(scnvim-postwindow-toggle)

" eval flash colors
highlight SCNvimEval guifg=black guibg=cyan ctermfg=black ctermbg=cyan
" this autocmd keeps the custom highlight when changing colorschemes
augroup scnvim_vimrc
  autocmd!
  autocmd ColorScheme *
        \ highlight SCNvimEval guifg=black guibg=cyan ctermfg=black ctermbg=cyan
augroup END

" hard coded path to sclang executable
let g:scnvim_sclang_executable = '~/bin/sclang'

" enable snippets support
let g:UltiSnipsSnippetDirectories = ['UltiSnips', 'scnvim-data']

" create a custom status line for supercollider buffers
function! s:set_sclang_statusline()
  setlocal stl=
  setlocal stl+=%f
  setlocal stl+=%=
  setlocal stl+=%(%l,%c%)
  setlocal stl+=\ \|
  setlocal stl+=%24.24{scnvim#statusline#server_status()}
endfunction

augroup scnvim_stl
  autocmd!
  autocmd FileType supercollider call <SID>set_sclang_statusline()
augroup END

" lightline.vim example

" let g:lightline = {}
" let g:lightline.component_function = {
"   \ 'server_status': 'scnvim#statusline#server_status',
"   \ }
"
" function! s:set_sclang_lightline_stl()
"   let g:lightline.active = {
"   \ 'left':  [ [ 'mode', 'paste' ],
"   \          [ 'readonly', 'filename', 'modified' ] ],
"   \ 'right': [ [ 'lineinfo' ],
"   \            [ 'percent' ],
"   \            [ 'server_status'] ]
"   \ }
" endfunction
```
