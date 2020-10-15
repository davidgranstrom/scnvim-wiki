## Syntax highlighting

Call `:SCNvimTags` after starting SuperCollider to generate a file used for syntax highlighting.

The command will also generate a file with snippet definitions for all
object creation methods and also a `tags` file which can be used to navigate to
references using the built-in vim command `C-]` (jump to definition).

If you write or install new classes you will need to run this command again to update the syntax/tags/snippets files.

## Snippets

Call `:SCNvimTags` to generate the snippet definitions.

You will also need a snippet engine like [UltiSnips](https://github.com/SirVer/ultisnips) in order to use the snippets. To let UltiSnips know about the snippets, put the following line in your init.vim:

```vim
let g:UltiSnipsSnippetDirectories = ['UltiSnips', 'scnvim-data']
```

## Status line widgets

scnvim provides some functions suitable to use in your vim statusline.

* `scnvim#statusline#server_status`

See the [example configuration](#example-configuration) for a status line example.

Call `:SCNvimStatusLine` to get feedback in the status line.

If you always want to display the server status, put the following in your `startup.scd`.

```supercollider
// scnvim
if (\SCNvim.asClass.notNil) {
    Server.default.doWhenBooted {
        \SCNvim.asClass.updateStatusLine(1, \SCNvim.asClass.port);
    }
}
```

## Plugin configuration

The following variables are used to configure scnvim. This plugin should work
out-of-the-box so it is not necessary to set them if you are happy with the
defaults.

Run `:checkhealth scnvim` to diagnose common problems with your config.

### Post window

```vim
" vertical 'v' or horizontal 'h' split
let g:scnvim_postwin_orientation = 'v'

" position of the post window 'right' or 'left'
let g:scnvim_postwin_direction = 'right'

" default is half the terminal size for vertical and a third for horizontal
let g:scnvim_postwin_size = 25

" automatically open post window on a SuperCollider error
let g:scnvim_postwin_auto_toggle = 1
```

### Eval flash

```vim
" duration of the highlight
let g:scnvim_eval_flash_duration = 100

" number of flashes. A value of 0 disables this feature.
let g:scnvim_eval_flash_repeats = 2

" configure the color
highlight SCNvimEval guifg=black guibg=white ctermfg=black ctermbg=white
```

### Extras

```vim
" path to the sclang executable
" scnvim will look in some known locations for sclang, but if it can't find it use this variable instead
" (also improves startup time slightly)
let g:scnvim_sclang_executable = ''

" update rate for server info in status line (seconds)
" (don't set this to low or vim will get slow)
let g:scnvim_statusline_interval = 1

" set this variable if you don't want the "echo args" feature
let g:scnvim_echo_args = 0

" set this variable if you don't want any default mappings
let g:scnvim_no_mappings = 1

" set this variable to browse SuperCollider documentation in nvim (requires `pandoc`)
let g:scnvim_scdoc = 1

" pass flags directly to sclang - see help file for more details, caveats, and further examples
let g:scnvim_sclang_options = ['-u', 9999]
```

## Example configuration

See `:h scnvim` for all available options.

```vim
" vim-plug

call plug#begin()
  Plug 'davidgranstrom/scnvim'
  " (optional) for snippets
  Plug 'SirVer/ultisnips'
call plug#end()

" scnvim

" horizontal post window
let g:scnvim_postwin_orientation = 'h'

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
"       \ 'server_status': 'scnvim#statusline#server_status',
"       \ }
" 
" let g:lightline.active = {
"       \ 'left':  [ [ 'mode', 'paste' ],
"       \          [ 'readonly', 'filename', 'modified' ] ],
"       \ 'right': [ [ 'lineinfo' ],
"       \            [ 'percent' ],
"       \            [ 'server_status'] ]
"       \ }
```
