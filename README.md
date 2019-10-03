(Work in progress)

# Camel LSP client for Vim

This is a short instruction on how to integrate your Vim editor with [Camel LSP server](https://github.com/camel-tooling/camel-language-server).

## Prerequisites

This instruction requires the following plugins:

- [vim-lsp](https://github.com/prabirshrestha/vim-lsp)
- [asyncomplete.vim](https://github.com/prabirshrestha/asyncomplete.vim)

It assumes those plugins below are already installed in `~/.vimrc`:

```vim
Plug 'prabirshrestha/asyncomplete.vim'
Plug 'prabirshrestha/async.vim'
Plug 'prabirshrestha/vim-lsp'
Plug 'prabirshrestha/asyncomplete-lsp.vim'
```

Here we use [vim-plug](https://github.com/junegunn/vim-plug) but you can use a plugin manager of your choice: pathogen.vim, Vundle, NeoBundle, dein.vim, etc.

## Download LSP jar

```sh
mkdir -p ~/lsp/camel-lsp-server
cd ~/lsp/camel-lsp-server
curl -L https://oss.sonatype.org/content/repositories/snapshots/com/github/camel-tooling/camel-lsp-server/1.1.0-SNAPSHOT/camel-lsp-server-1.1.0-20190930.170258-135.jar -O
```

## Install Camel LSP to your vim

Add following to `~/.vimrc`:

```vim
if executable('java') && filereadable(expand('~/lsp/camel-lsp-server/camel-lsp-server-1.1.0-20190930.170258-135.jar'))
  au User lsp_setup call lsp#register_server({
    \ 'name': 'camel',
    \ 'cmd': {server_info->[
    \   'java',
    \   '-jar',
    \   expand('~/lsp/camel-lsp-server/camel-lsp-server-1.1.0-20190930.170258-135.jar')
    \ ]},
    \ 'whitelist': ['java', 'xml']
    \ })
endif
```
