# [Vim](https://github.com/vim/vim)	和 [Neovim](https://github.com/neovim/neovim)(也习惯叫nvim)

Neovim比vim好用太多，推荐使用Neovim

Neovim完全兼容Vim，Neovim也完全支持用vimscript来写配置，它俩只是的配置文件名和放的目录位置不同。
由于Nvim是Vim的一个分叉，会定期从Vim合并补丁，所以基本功能几乎是一样的。有一些细微的差别，但这对初学者来说基本无关紧要。

nvim除了支持使用vimscript来写配置，从0.5版本开始，nvim还添加了对lua的支持。


# 安装
- mac下安装Neovim	 ` brew install neovim ` 。有时brew的版本太低，可以直接从nvim的github官网下载最新版本
	1. 下载最新版本的二进制包： `nvim-macos.tar.gz`
	2. 在命令行下解压：`tar xzvf nvim-macos.tar.gz`
	3. 建立软连接 `ln  ***完整的目录***/nvim-osx64/bin/nvim   /usr/local/bin/nvim`
 
- (可选）替换默认的vim `nvim ~/.bashrc`
	```bash
	alias vim='nvim'
	alias vi='nvim'
	```
- mac下安装Vim		` brew install vim `

# 配置文件

- Vim 的配置文件:  **`～/.vimrc`**  没有就新建一个`touch ~/.vimrc`

- Neovim 配置文件不是 **.vimrc**, 而是下面的**init.vim** 或者 **init.lua** 只能二选一，
	- **~/.config/nvim/init.lua** 默认使用lua语言。 在init.lua里也可以调用vimscript，见后面描述。
	- **~/.config/nvim/init.vim** 默认是用vimscript语言。在init.vim文件里也可以调用lua，见后面描述。
	
  没有就新建一个 `mkdir -p ~/.config/nvim  && touch ~/.config/nvim/init.lua`

- (几乎用不上）为了便于Neovim和Vim共享相同的配置，可以 **.vimrc** 文件里写配置，然后在Neovim的配置文件init.vim中直接引用，如：
  ```bash
  source $HOME/.vimrc
  ```

# 插件管理器[vim-plug](https://github.com/junegunn/vim-plug)


vim-plug是Vim和Neovim都可以使用的主流插件管理器

安装vim-plug
 ```bash
 # 为Vim安装插件管理器vim-plug, 默认安装在 (~/.vim/autoload)
 curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
 https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  
 # 为Neovim安装插件管理器vim-plug，默认安装在 (~/.local/share/nvim/site/autoload)
 curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs \
 https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim 
 ```

## 用vim-plug安装插件

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


# 只有Neovim可用的插件管理器[packer.nvim](https://github.com/wbthomason/packer.nvim)
安装**packer.nvim**
```bash
git clone --depth 1 https://github.com/wbthomason/packer.nvim\
 ~/.local/share/nvim/site/pack/packer/start/packer.nvim
```
packer.nvim会把插件安装到目录下： **~/.local/share/nvim/site/pack/packer**

创建配置文件 **` touch ~/.config/nvim/lua/plugins.lua`** 

```lua
--  ~/.config/nvim/lua/plugins.lua
return require('packer').startup(function()
  use 'wbthomason/packer.nvim'   -- Packer can manage itself

  -- 用use列出要安装的插件
  use 'mhinz/vim-startify'    -- 启动页列出最近打开的文件 
  use 'rlue/vim-barbaric'     -- 中文输入法自动切换

  -- 支持markdown编辑、预览, 在markdown文件下运行 :MarkdownPreview 就可以实时预览
  use {
      'plasticboy/vim-markdown', 
      require = {'godlygeek/tabular'}   }   -- vim-markdown依赖tabular插件
  use {
      'iamcco/markdown-preview.nvim',
      run = function() vim.fn['mkdp#util#install']() end, 
      ft = {'markdown'}  }  -- 打开的文件类型是markdown文件时，才加载该插件

  -- 用config配置插件

end)

```

修改 `init.lua` ，加载这个文件

```lua
" Packer插件管理
require('plugins')     -- 加载文件 lua/plugins.lua
```
但通常无论 **安装** 还是 **更新** 插件，每次修改plugins.lua文件后，只需要下边这一条命令就够了。

`:PackerSync`



## 在vimscript配置文件init.vim中执行lua

在`init.vim`文件里可以直接写 `lua`代码，这样
```
lua print('单行 lua')
```

多行调用
```
lua <<EOF
print('多行 lua')
print('多行 lua')
EOF
```

在init.vim 中加载其他 lua 文件
```
" 加载 lua/basic.lua 文件
lua require('basic')
```

## **init.lua**配置文件
### 一、在init.lua中执行vimscript代码，
使用 **`vim.cmd("set notimeout")`** 执行vimscript, 多行代码使用双方括号`[[...]]`来完成
```lua
-- 可能你已经使用了一些包管理器，比如vim-plug，当转向 Lua 时不需要更改它
-- 只需将整个插件列表包装在 vim.cmd 中并像以前一样继续使用它。
vim.cmd([[
set notimeout
set encoding=utf-8
]])
```

### 二、使用lua配置
- `vim.g.mapleader = ","` 等价于 `let g:mapleader = ','`； 注意**vim.g**对应的是 **let** 代表**全局变量**的表
- `vim.o.encoding="utf-8"` 等价于 `set encoding=utf-8`；其对应的是 **set** ，其中：
	- **vim.o** 用于全局设置
	- **vim.wo** 用于窗口设置
	- **vim.bo** 用于缓冲设置
- 把**init.vim** 的配置移动到**init.lua**大部分设置非常简单。你只需将 `set x = y` 替换为 `vim.o.x = "y"` 就可以了。
- 成对的布尔设置被合并为一个设置，例如，用 `vim.o.wrap = true` 和 `vim.o.wrap = false` 来代替 `set wrap` 和 `set nowrap`
- `HOME 目录` 问题： 在使用 **~** 作为对主目录的引用时遇到问题，所以可以通过编写 `HOME = os.getenv("HOME")` 来设置 HOME 变量
- 双反斜杠： 如果你想传递一个特殊字符 \t 给 Neovim，你需要在 Lua 中把它写成 "\\t"

### 三、lua键位映射
Lua API 具有将键映射到某些函数的功能。函数是 **vim.api.nvim_set_keymap(mode, keys, mapping, options)**
- mode 是指代表编辑器模式的字母（n 表示正常，i 表示插入等），就像在 nmap 或 imap 等原始 vim 函数中一样
- keys 是一个表示键组合的字符串
- mapping 是一个表示键映射到什么的字符串
- options 是一个表，你可以在其中传递一些附加设置。常用的两个是 `noremap = true` 和 `Silent = true`

举个例子, 下面这个函数等价于 `noremap <leader>a <cmd>Git blame<cr>`
```lua
vim.api.nvim_set_keymap(
  "n",
  "<leader>a",
  ":Git blame<cr>",
  { noremap = true }
 )
```
自己写了一些简单的函数，以避免每次都输入 **vim.api...** 
```lua
function map(mode, shortcut, command)
  vim.api.nvim_set_keymap(mode, shortcut, command, { noremap = true, silent = true })
end

function nmap(shortcut, command)
  map('n', shortcut, command)       -- 正常模式下映射
end

function imap(shortcut, command)
  map('i', shortcut, command)       -- 输入模式下映射
end
```
有了这些函数，上面的例子可以写成下面这样，可读性更好了
```lua
nmap("<leader>a", "<cmd>Git blame<cr>")     -- 等价于 noremap <leader>a <cmd>Git blame<cr>
```


## 一分钟的时间学会 Lua 语言
```lua
-- 这是一个注释
num = 22 -- 这是一个声明了number类型的全局变量
local num2 = 33 -- 本地变量

-- 定义字符串
str1 = 'this is a string'
str2 = "and so is this"
str3 = [[ and this is a string too ]]
str4 = "string " .. "concatenation"  --字符串连接使用 .. 运算符

val = true and not false -- 布尔和逻辑操作符

if str1 == 'something' then
  print("YES")
elseif str2 ~= 'is not equal' then
  print('Maybe')
else
  print('no')
end

function printText(text)
  print(text)
  return true
end

tab1 = { 'this', 'is, 'a', 'table' }   -- 一个数组
tab2 = { also = 'this is a table' }    -- 表是数组和词典类型的组合
tab2["new_key"] = "new value"

print(tab2["also"])

require('plugins') -- 加载lua目录下的plugins.lua文件并且执行它
```

# 我的配置init.lua

我的配置文件结构, 所在目录是 **~/.config/nvim/**。 后边章节会逐个介绍

```
├── init.lua                              入口文件，这里负责加载所有lua文件夹里的文件
└── lua                                   所有 lua 配置文件
    ├── basic.lua                         Neovim 的基础配置
    ├── keybindings.lua                   快捷键配置
    ├── lsp                               内置 LSP  (Language Server Protocol) 配置
    │   ├── diagnostic_signs.lua
    │   ├── language_servers.lua
    │   └── nvim-cmp-config.lua
    ├── plugin-config                     各个插件配置在这个文件夹
    │   ├── bufferline.lua
    │   ├── comment.lua
    │   ├── nvim-autopairs.lua
    │   ├── nvim-colorizer.lua
    │   ├── nvim-tree.lua
    │   ├── nvim-treesitter.lua
    │   ├── rust-tools.lua
    │   ├── surround.lua
    │   ├── telescope.lua
    │   └── which-key.lua
    └── plugins.lua                       插件安装管理
```


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

    " autocmd! bufwritepost .vimrc source ~/.vimrc	                      "当 .vimrc 被修改时, 自动重新加载 
    autocmd! bufwritepost basic.lua source ~/.config/nvim/lua/basic.lua   "当 lua/basic.lua 被修改时, 自动重新加载 

	set encoding=UTF-8

	set tabstop=4           "tab 4个空格
	set softtabstop=4
	set shiftwidth=4
	set shiftround			" 表示缩进列数对齐到 shiftwidth 值的整数倍
	set expandtab			" 转换tab为空格，按下Tab 键时，输入到的都是空格
	set smarttab            " 表示插入 Tab 时使用 shiftwidth

	set nu					"显示行号

    set mouse=a             "开启鼠标支持

	autocmd InsertLeave,WinEnter * set cursorline    "高亮当前行
	autocmd InsertEnter,WinLeave * set nocursorline  "插入模式，取消当前行高亮

	set scrolloff=4			"jk移动时光标到底部时，光标上下方保留4行
	set sidescrolloff=4


## 快捷键定义or映射

	let mapleader = " "	        			  "注意： 双引号里有个空格，这里把leader键映射成空格键
	inoremap jj <Esc>		    			"在插入模式下，连续输入jj可以退出插入模式

	nmap sp :split<Return><C-w>w			"正常模式下，sp水平切分窗口
	nmap vs :vsplit<Return><C-w>w			"正常模式下，vs垂直切分窗口



## 拆分窗口
	水平拆分 :sp
	垂直拆分 :vs    or  :vsp

## 交换当前行和下一行
	ddp

## 正常模式下，选中全部内容
	ggVG



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

