# Vim 和 NeoVim

 Neovim完全兼容Vim，Neovim也完全支持用vimscript来写配置，它俩只是的配置文件名和放的目录位置不同。

# 安装

- mac下安装[Vim](https://github.com/vim/vim)
  
  ```bash
  brew install vim
  ```

- mac下安装[Neovim](https://github.com/neovim/neovim)
  
  ```bash
  brew install neovim
  ```

# 配置文件

- Vim 的配置文件:  **～/.vimrc**  没有就新建一个`touch ~/.vimrc`

- Neovim的配置文件: **~/.config/nvim/init.vim**  没有就新建一个 `touch ~/.config/nvim/init.vim`

- 为了便于Neovim和Vim共享相同的配置，可以 **.vimrc** 文件里写配置，然后在Neovim的配置文件init.vim中直接引用，如：
  
  ```bash
  source $HOME/.vimrc
  ```

# 插件管理器

- 目前Vim和Neovim主流主的插件管理器是 [vim-plug](https://github.com/junegunn/vim-plug)

- Vim默认把vim-plug安装在 **~/.vim/autoload** 目录下

- NeoVim默认把vim-plug安装在 **~/.local/share/nvim/site/autoload** 目录下
  
  ```bash
  # Vim (~/.vim/autoload)
  curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  
  # Neovim (~/.local/share/nvim/site/autoload)
  curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim 
  ```

# 安装插件

- 在vim的配置文件.vimrc（neovim是init.vim)里，把要安装的插件放在`call plug#begin(PLUGIN_DIRECTORY)` 和 `call plug#end()` 之间 ; PLUGIN_DIRECTORY 是占位符，要用实际的插件安装目录代替。 vim插件一般安装在`~/.vim/plugged`。Neovim的插件也可以安装在这里。

- 安装插件就是告诉插件管理器插件的地址(以下地址均是来自 github, 地址使用作者名/仓库名即可)
  
  ```bash
  call plug#begin('~/.vim/plugged')  "这里同时也指定了插件的安装目录~/.vim/plugged
  
  Plug 'scrooloose/nerdtree'
  Plug 'mhinz/vim-startify' 
  Plug 'tpope/vim-fugitive' 
  Plug 'lfv89/vim-interestingwords'
  
  call plug#end()
  ```

## 例子，配置nerdtree

- 在 .vimrc 配置文件`call plug#end()`的后面添加如下配置，用来设置`,n`快捷键来激活nerdtree:
  
  ```bash
  let mapleader = ","  
  nnoremap <silent> <leader>n :NERDTreeToggle<CR>
  "n 表示这个映射只在普通(normal)模式下生效，
  "nore 表示这个映射是非递归的，
  ```

- 重新运行vim, 然后手动执行`:PlugInstall` 插件就会自行安装

- 更新插件使用 :PlugUpdate

- 更新 vim-plug 插件自己 :PlugUpgrade

- 移除插件，移除配置文件的地址，执行 :PlugClean 命令即可。

- 关闭插件执行界面是快捷键 q

# Mac系统，Vim的输入和正常模式下，解决恼人的中文输入法的切换

## [解决办法1](https://jdhao.github.io/2021/02/25/nvim_ime_mode_auto_switch/)使用 [vim-barbaric](https://github.com/rlue/vim-barbaric), 貌似这个更好用
vim-barbaric 是一款帮助用户自动设置输入法模式的插件。

1. 需要先安装 [xkbswitch-macosx](https://github.com/myshov/xkbswitch-macosx)
```bash
	curl -o /usr/local/bin/xkbswitch https://raw.githubusercontent.com/myshov/xkbswitch-macosx/master/bin/xkbswitch
```
2. 然后安装vim-barbaric插件即可, 该插件开箱即用，无需额外设置。
```bash
	Plug 'rlue/vim-barbaric'   " 这里使用vim-plug插件管理器安装
```



## [解决办法](https://zhuanlan.zhihu.com/p/49411224)使用[Vim-xkbswitch](https://github.com/lyokha/vim-xkbswitch), 具体步骤

1. 拷贝xkbswitch 到 /usr/local/bin
   
   ```bash
   git clone https://link.zhihu.com/?target=https%3A//github.com/myshov/xkbswitch-macosx
   cp xkbswitch-macosx/bin/xkbswitch /usr/local/bin
   ```

2. 拷贝 libxkbswitch.dylib 到 /usr/local/lib/
   
   ```bash
   git clone https://github.com/myshov/libxkbswitch-macosx
   cp libxkbswitch-macosx/bin/libxkbswitch.dylib /usr/local/lib/
   ```

3. 安装vim-xkbswitch 插件。下面示例使用vim-plug，在.vimrc文件中添加如下内容
   
   ```bash
   call plug#begin('~/.vim/plugged')
    ...
    Plug 'lyokha/vim-xkbswitch'  "中文自动输入法切换插件, 记得重启vim然后执行 :PlugInstall
    ...
   call plug#end()
   
   let g:XkbSwitchEnabled = 1    "默认让xkbs输入法自动切换生效
   ```

# 把插入模式下的光标改成闪烁的竖线(Neovim默认是可以的)

```bash
 "在不同的终端下，配置不同
 let &t_SI = "\e[5 q"
 let &t_EI = "\e[2 q"

 "  不同数字表示不同的光标形状
 "  1 -> blinking block
 "  2 -> solid block 
 "  3 -> blinking underscore
 "  4 -> solid underscore
 "  5 -> blinking vertical bar
 "  6 -> solid vertical bar`
```
