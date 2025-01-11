# Installing clangd on KISS

I use neovim with mason to manage my lsp servers. The issue is that there is no clangd prebuilt for musl...

The issue affect Void and Alpine also, but they have a nice clang-tools-extra package to avoid needing to compile everything. 

Here in KISS Linux we are doomed to compile everything. Sit back and relax, we are going on a very long compilation adventure !

## How to do ?

- `git clone https://github.com/llvm/llvm-project.git`
- `cd llvm-project && mkdir build && cd build`
- `cmake -DCMAKE_BUILD_TYPE=Release -DLLVM_ENABLE_PROJECTS="clang;clang-tools-extra" ../llvm`
- Wait for something like 8-9h... Or less if you computer is not a 4 core i5 @ 2.8GHz.
- `make install`

## Ok fine, now what ?

Simply add this line at the end of your neovim config :

`require'lspconfig'.clangd.setup{}`

And you are (finally) good to go !
