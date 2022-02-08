# Vim 和 NeoVim(也习惯叫nvim)

Neovim完全兼容Vim，Neovim也完全支持用vimscript来写配置，它俩只是的配置文件名和放的目录位置不同。
由于Nvim是Vim的一个分叉，会定期从Vim合并补丁，所以基本功能几乎是一样的。有一些细微的差别，但这对初学者来说基本无关紧要。

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

- Neovim的配置文件: **~/.config/nvim/init.vim**  没有就新建一个 `mkdir -p ~/.config/nvim  && touch ~/.config/nvim/init.vim`

- 为了便于Neovim和Vim共享相同的配置，可以 **.vimrc** 文件里写配置，然后在Neovim的配置文件init.vim中直接引用，如：
  
  ```bash
  source $HOME/.vimrc
  ```

# 插件管理器

- 目前Vim和Neovim主流主的插件管理器是 [vim-plug](https://github.com/junegunn/vim-plug)
 ```bash
 # 为Vim安装插件管理器vim-plug, 默认安装在 (~/.vim/autoload)
 curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
 https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  
 # 为Neovim安装插件管理器vim-plug，默认安装在 (~/.local/share/nvim/site/autoload)
 curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs \
 https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim 
 ```

# 用vim-plug安装插件

- 在vim的配置文件.vimrc（neovim是init.vim)里，把要安装的插件放在`call plug#begin(PLUGIN_DIRECTORY)` 和 `call plug#end()` 之间 ; PLUGIN_DIRECTORY 是占位符，要用实际插件的安装目录代替。 vim插件一般安装在`~/.vim/plugged`。Neovim的插件也可以安装在这里。

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


- 在 .vimrc 配置文件`call plug#end()`的后面添加如下配置，用来设置`空格键 + n`快捷键来激活nerdtree:
  
  ```bash
  let mapleader = " "  "注意： 双引号里有个空格，这里把leader键映射成空格键
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

## 优先用这个[解决办法1](https://jdhao.github.io/2021/02/25/nvim_ime_mode_auto_switch/)使用 [vim-barbaric](https://github.com/rlue/vim-barbaric), 貌似这个更好用
vim-barbaric 是一款帮助用户自动设置输入法模式的插件。

1. 需要先安装 [xkbswitch-macosx](https://github.com/myshov/xkbswitch-macosx)
```bash
curl -o /usr/local/bin/xkbswitch https://raw.githubusercontent.com/myshov/xkbswitch-macosx/master/bin/xkbswitch
```
2. 然后安装vim-barbaric插件即可, 该插件开箱即用，无需额外设置。
```bash
Plug 'rlue/vim-barbaric'   " 这里使用vim-plug插件管理器安装
```



## [解决办法2](https://zhuanlan.zhihu.com/p/49411224)使用[vim-xkbswitch](https://github.com/lyokha/vim-xkbswitch), 具体步骤

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


# Markdown
在.vimrc文件加入如下内容
```bash
    call plug#begin('~/.vim/plugged')
        ...
        "markdown support
        Plug 'godlygeek/tabular'
        Plug 'plasticboy/vim-markdown'

        " markdown preview
        Plug 'iamcco/markdown-preview.nvim', { 'do': { -> mkdp#util#install() }, 'for': ['markdown', 'vim-plug']}
        ...
    call plug#end()
    let g:vim_markdown_folding_disabled = 1  "设置md标题默认不折叠

```
在vim里运行 **`一次`** 下面的命令
```bash
	:source %
	:PluginInstall
	:call mkdp#util#install()
```
以后只要在vim的md文件下运行 `:MarkdownPreview` 命令就可以一边编辑，一边在浏览器里面预览了，而且两边保持同步。

# 把插入模式下的光标改成竖线| (Neovim默认是可以的)

```bash
 "在不同的终端下，配置不同
 let &t_SI.="\e[5 q" "SI = INSERT mode
 let &t_SR.="\e[4 q" "SR = REPLACE mode
 let &t_EI.="\e[1 q" "EI = NORMAL mode (ELSE)

 "  不同数字表示不同的光标形状
 "  1 -> blinking block
 "  2 -> solid block 
 "  3 -> blinking underscore
 "  4 -> solid underscore
 "  5 -> blinking vertical bar
 "  6 -> solid vertical bar`
```


# vim常用命令or操作
## 基本配置

	autocmd! bufwritepost .vimrc source ~/.vimrc		"当 .vimrc 被修改时, 自动重新加载 

	autocmd InsertLeave,WinEnter * set cursorline    "高亮当前行
	autocmd InsertEnter,WinLeave * set nocursorline  "插入模式，取消当前行高亮

	set tabstop=4           “tab 4个空格
	set softtabstop=4
	set shiftwidth=4

	set nu									"显示行号

	autocmd InsertLeave,WinEnter * set cursorline    "高亮当前行
	autocmd InsertEnter,WinLeave * set nocursorline  "插入模式，取消当前行高亮

## 快捷键定义or映射

  let mapleader = " "							  "注意： 双引号里有个空格，这里把leader键映射成空格键
	inoremap jj <Esc>									 "在插入模式下，连续输入jj可以退出插入模式

	nmap ss :split<Return><C-w>w			"正常模式下，ss水平切分窗口
	nmap sv :vsplit<Return><C-w>w			"正常模式下，sv垂直切分窗口


## 拆分窗口
	垂直拆分 :vsp
	水平拆分 :sp

## 交换当前行和下一行
	ddp

## 正常模式下，选中全部内容
	ggvG



## 系统剪贴板clipboard
从vim复制到系统剪贴板复制 

	"+y         注意前面的双引号"也要
	"+2yy       复制两行

从系统剪贴板粘贴到vim

- 方法一：在输入模式下 Ctrl + v  也能从系统剪贴板粘贴到vim
- 方法二： 

		"+p				注意前面的双引号"也要

设置vim默认使用系统剪贴板。如果想y/p直接和系统剪贴板打通，可以在~/.vimrc中加上以下配置
```bash
set clipboard^=unnamed,unnamedplus    "其中unnamed代表*寄存器，unnamedplus代表+寄存器。
```

