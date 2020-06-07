Various tips and tricks for scnvim!

Many tips are presented in `autocmd` fashion so you can just copy and paste them to your `init.vim`. If you don't want to use `autocmd` for configuration [look here instead](#afterftpluginsupercollidervim).

Use an `augroup` to avoid `autocmd` build up.

**Example `augroup`**

```vim
" NOTE: the augroup called scnvim is reserved by the plugin
augroup scnvim_settings
  autocmd FileType supercollider setlocal ...
augroup END
```

## Settings

**Indendation**

```vim
autocmd FileType supercollider setlocal tabstop=4 softtabstop=4 shiftwidth=4
```

**Wrap the post window output**

```vim
autocmd FileType scnvim setlocal wrap
```

## Mappings

**Map any piece of SuperCollider code to a key**
```vim
autocmd FileType supercollider nnoremap <silent><buffer> <F2> :call scnvim#sclang#send('100.rand')<CR>
```

**Map any piece of SuperCollider code to a key (silent version)**
```vim
autocmd FileType supercollider nnoremap <silent><buffer> <F3> :call scnvim#sclang#send_silent('100.rand')<CR>
```

**Custom mapping for block evaluation**
```vim
autocmd FileType supercollider nmap <Space> <Plug>(scnvim-send-block)
```

---

### `after/ftplugin/supercollider.vim`

First get the location of your config directory.

```vim
:echo stdpath('config')
```

In your shell, `cd` to that directory and create `after/ftplugin/supercollider.vim` then add settings using `setlocal`.