# [Vim](https://github.com/vim/vim)	和 [Neovim](https://github.com/neovim/neovim)(也习惯叫nvim)

Neovim比vim好用太多，推荐使用Neovim

Neovim完全兼容Vim，Neovim也完全支持用vimscript来写配置，它俩只是的配置文件名和放的目录位置不同。
由于Nvim是Vim的一个分叉，会定期从Vim合并补丁，所以基本功能几乎是一样的。有一些细微的差别，但这对初学者来说基本无关紧要。

nvim除了支持使用vimscript来写配置，从0.5版本开始，nvim还添加了对lua的支持。

# 终端问题
mac下一定不要使用系统自带的终端Terminal.app，不然颜色丰富的主题theme都不能正常显示。 推荐[Alacritty](https://github.com/alacritty/alacritty), 最后是[iTerm2](https://github.com/gnachman/iTerm2)也行。

## Alacritty 内存占用少,性能最好,缺点是不支持tab也没有默认配置.
安装Alacritty `brew cask install alacritty`

创建配置文件alacritty.yml。Alacritty 默认不会添加配置文件，要手动添加
```bash
mkdir ~/.config/alacritty
touch ~/.config/alacritty/alacritty.yml
```
我的配置 **alacritty.yml**
```
colors:

  primary:
    background: "#1e2127"
    # background: "#2E3440"
    foreground: "#D8DEE9"


  normal:
    black: "#3B4252"
    red: "#BF616A"
    green: "#A3BE8C"
    yellow: "#EBCB8B"
    blue: "#81A1C1"
    magenta: "#B48EAD"
    cyan: "#88C0D0"
    white: "#abb2bf"


  bright:
    black: "#5c6370"
    red: "#e06c75"
    green: "#98c379"
    yellow: "#d19a66"
    blue: "#61afef"
    magenta: "#c678dd"
    cyan: "#56b6c2"
    white: "#ECEFF4"

# background_opacity: 1.0
window.opacity: 1.0

# 设置字体
font:
  normal:
    family: "Hack Nerd Font"
    style: Regular
  bold:
    family: "Hack Nerd Font"
    style: Bold
  italic:
    family: "Hack Nerd Font"
    style: Italic
  bold_italic:
    family: "Hack Nerd Font"
    style: Bold Italic

  # 字大小
  size: 19.0 

  offset:
    x: 0
    y: 0
  glyph_offset:
    x: 0
    y: 0

window:
  padding:
    x: 2
    y: 2

scrolling:
# 回滚缓冲区中的最大行数,指定“0”将禁用滚动。
  history: 10000

  # 滚动行数 

  multiplier: 10

# 如果为‘true’，则使用亮色变体绘制粗体文本。
draw_bold_text_with_bright_colors: true

selection:
  semantic_escape_chars: ',│`|:"'' ()[]{}<>'
  save_to_clipboard: true

live_config_reload: true

key_bindings:
  - { key: V, mods: command, action: Paste }
  - { key: C, mods: command, action: Copy }

# alacritty在macOS电脑上，默认Option|Alt按键没起作用，这里需要重新映射，让Option|Alt按键生效 
# 映射格式如下，要用实际的按键代替下面的 [ALPHA_KEY]
#    - { key: [ALPHA_KEY],        mods: Alt,     chars: "\x1b[ALPHA_KEY]"   }
# 例如 下面就是映射 Alt + q 按键： 
#    - { key: Q,                  mods: Alt,     chars: "\x1bq"             }
# 完整的映射例子，参考： https://github.com/alacritty/alacritty/issues/62#issuecomment-347552058

  - { key: A,         mods: Alt,       chars: "\x1ba"                       }
  - { key: B,         mods: Alt,       chars: "\x1bb"                       }
  - { key: C,         mods: Alt,       chars: "\x1bc"                       }
  - { key: D,         mods: Alt,       chars: "\x1bd"                       }
  - { key: E,         mods: Alt,       chars: "\x1be"                       }
  - { key: F,         mods: Alt,       chars: "\x1bf"                       }
  - { key: G,         mods: Alt,       chars: "\x1bg"                       }
  - { key: H,         mods: Alt,       chars: "\x1bh"                       }
  - { key: I,         mods: Alt,       chars: "\x1bi"                       }
  - { key: J,         mods: Alt,       chars: "\x1bj"                       }
  - { key: K,         mods: Alt,       chars: "\x1bk"                       }
  - { key: L,         mods: Alt,       chars: "\x1bl"                       }
  - { key: M,         mods: Alt,       chars: "\x1bm"                       }
  - { key: N,         mods: Alt,       chars: "\x1bn"                       }
  - { key: O,         mods: Alt,       chars: "\x1bo"                       }
  - { key: P,         mods: Alt,       chars: "\x1bp"                       }
  - { key: Q,         mods: Alt,       chars: "\x1bq"                       }
  - { key: R,         mods: Alt,       chars: "\x1br"                       }
  - { key: S,         mods: Alt,       chars: "\x1bs"                       }
  - { key: T,         mods: Alt,       chars: "\x1bt"                       }
  - { key: U,         mods: Alt,       chars: "\x1bu"                       }
  - { key: V,         mods: Alt,       chars: "\x1bv"                       }
  - { key: W,         mods: Alt,       chars: "\x1bw"                       }
  - { key: X,         mods: Alt,       chars: "\x1bx"                       }
  - { key: Y,         mods: Alt,       chars: "\x1by"                       }
  - { key: Z,         mods: Alt,       chars: "\x1bz"                       }
  - { key: A,         mods: Alt|Shift, chars: "\x1bA"                       }
  - { key: B,         mods: Alt|Shift, chars: "\x1bB"                       }
  - { key: C,         mods: Alt|Shift, chars: "\x1bC"                       }
  - { key: D,         mods: Alt|Shift, chars: "\x1bD"                       }
  - { key: E,         mods: Alt|Shift, chars: "\x1bE"                       }
  - { key: F,         mods: Alt|Shift, chars: "\x1bF"                       }
  - { key: G,         mods: Alt|Shift, chars: "\x1bG"                       }
  - { key: H,         mods: Alt|Shift, chars: "\x1bH"                       }
  - { key: I,         mods: Alt|Shift, chars: "\x1bI"                       }
  - { key: J,         mods: Alt|Shift, chars: "\x1bJ"                       }
  - { key: K,         mods: Alt|Shift, chars: "\x1bK"                       }
  - { key: L,         mods: Alt|Shift, chars: "\x1bL"                       }
  - { key: M,         mods: Alt|Shift, chars: "\x1bM"                       }
  - { key: N,         mods: Alt|Shift, chars: "\x1bN"                       }
  - { key: O,         mods: Alt|Shift, chars: "\x1bO"                       }
  - { key: P,         mods: Alt|Shift, chars: "\x1bP"                       }
  - { key: Q,         mods: Alt|Shift, chars: "\x1bQ"                       }
  - { key: R,         mods: Alt|Shift, chars: "\x1bR"                       }
  - { key: S,         mods: Alt|Shift, chars: "\x1bS"                       }
  - { key: T,         mods: Alt|Shift, chars: "\x1bT"                       }
  - { key: U,         mods: Alt|Shift, chars: "\x1bU"                       }
  - { key: V,         mods: Alt|Shift, chars: "\x1bV"                       }
  - { key: W,         mods: Alt|Shift, chars: "\x1bW"                       }
  - { key: X,         mods: Alt|Shift, chars: "\x1bX"                       }
  - { key: Y,         mods: Alt|Shift, chars: "\x1bY"                       }
  - { key: Z,         mods: Alt|Shift, chars: "\x1bZ"                       }
  - { key: Key1,      mods: Alt,       chars: "\x1b1"                       }
  - { key: Key2,      mods: Alt,       chars: "\x1b2"                       }
  - { key: Key3,      mods: Alt,       chars: "\x1b3"                       }
  - { key: Key4,      mods: Alt,       chars: "\x1b4"                       }
  - { key: Key5,      mods: Alt,       chars: "\x1b5"                       }
  - { key: Key6,      mods: Alt,       chars: "\x1b6"                       }
  - { key: Key7,      mods: Alt,       chars: "\x1b7"                       }
  - { key: Key8,      mods: Alt,       chars: "\x1b8"                       }
  - { key: Key9,      mods: Alt,       chars: "\x1b9"                       }
  - { key: Key0,      mods: Alt,       chars: "\x1b0"                       }
  - { key: Space,     mods: Control,   chars: "\x00"                        } # Ctrl + Space
  - { key: Grave,     mods: Alt,       chars: "\x1b`"                       } # Alt + `
  - { key: Grave,     mods: Alt|Shift, chars: "\x1b~"                       } # Alt + ~
  - { key: Period,    mods: Alt,       chars: "\x1b."                       } # Alt + .
  - { key: Key8,      mods: Alt|Shift, chars: "\x1b*"                       } # Alt + *
  - { key: Key3,      mods: Alt|Shift, chars: "\x1b#"                       } # Alt + #
  - { key: Period,    mods: Alt|Shift, chars: "\x1b>"                       } # Alt + >
  - { key: Comma,     mods: Alt|Shift, chars: "\x1b<"                       } # Alt + <
  - { key: Minus,     mods: Alt|Shift, chars: "\x1b_"                       } # Alt + _
  - { key: Key5,      mods: Alt|Shift, chars: "\x1b%"                       } # Alt + %
  - { key: Key6,      mods: Alt|Shift, chars: "\x1b^"                       } # Alt + ^
  - { key: Backslash, mods: Alt,       chars: "\x1b\\"                      } # Alt + \
  - { key: Backslash, mods: Alt|Shift, chars: "\x1b|"                       } # Alt + |

```


## 终端[Tabby](https://github.com/Eugeny/tabby) ,默认配置很好，缺点是内存占用高, MacOS下Option|Alt按键估计也要重新映射才行
安装 `brew install tabby`




# 安装vim & nvim
- mac下安装Neovim	 ` brew install neovim ` 。有时brew的版本太低，可以直接从nvim的github官网下载最新版本
	1. 下载最新版本的二进制包： `nvim-macos.tar.gz`
	2. 在命令行下解压：`tar xzvf nvim-macos.tar.gz`
	3. 建立软连接 `ln -s ***完整的目录***/nvim-osx64/bin/nvim   /usr/local/bin/nvim`
    4. 运行 `nvim`
 
- (可选）替换默认的vim `nvim ~/.bashrc`
	```bash
	alias vim='nvim'
	alias vi='nvim'
	```
- mac下安装Vim		` brew install vim `

## 安装字体 nerd-font, 解决终端图标乱码
```bash
brew tap homebrew/cask-fonts     # 如果存在其它cask-fonts库，可以 brew untap  *仓库名** 删除重复的仓库 
brew install font-hack-nerd-font --cask
```
然后在终端里设置使用 Hack Nerd Font 字体


# 一些插件要安装系统依赖，mac的安装方式。
安装python支持，有一些好用的插件需要python3支持
```bash
brew install python3
pip3 install neovim --upgrade
```

ranger悬浮文件管理器，安装系统依赖

```bash
# macOS users please install ranger by `pip3 ranger-fm` instead of `brew install ranger`
pip3 install ranger-fm pynvim
```

vim-barbaric中文输入自动却换，安装系统依赖
```bash
curl -o /usr/local/bin/xkbswitch https://raw.githubusercontent.com/myshov/xkbswitch-macosx/master/bin/xkbswitch
```

模糊搜索telescope, 安装系统依赖

[ripgrep/rg](https://github.com/BurntSushi/ripgrep)  **文本搜索**神器grep最好代替者。

[fd](https://github.com/sharkdp/fd)  **文件搜索**find的最好替代

[sed](https://www.gnu.org/software/sed/) 一种在线编辑器，它一次处理一行内容, 用于 nvim-spectre 的全局字符串替换。

[ctags](https://github.com/universal-ctags/ctags) 用于LSP符号和标签的查看器和查找器
```bash
brew install ripgrep fd gnu-sed ctags
```



## 一些语言的 LSP language server依赖

### vim script  LSP Server
```
yarn global add vim-language-server
```

### python  LSP Server
```
pip3 install 'python-lsp-server[all]' pylsp-mypy pyls-isort

```



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

# 无需额外安装插件的基本配置
新建文件 `touch ~/.config/nvim/lua/basic.lua`
```lua
vim.cmd([[

" autocmd! bufwritepost .vimrc source ~/.vimrc	            	 "当 .vimrc 被修改时, 自动重新加载 
autocmd! bufwritepost basic.lua source ~/.config/nvim/lua/basic.lua   "当 lua/basic.lua 被修改时, 自动重新加载 

set encoding=UTF-8

let mapleader = " "	        "注意： 双引号里有个空格，这里把leader键映射成空格键

set tabstop=4               "tab 4个空格
set softtabstop=4
set shiftwidth=4
set shiftround		    	" 表示缩进列数对齐到 shiftwidth 值的整数倍
set expandtab			    " 转换tab为空格，按下Tab 键时，输入到的都是空格
set smarttab                " 表示插入 Tab 时使用 shiftwidth

set nu						"显示行号

set mouse=a                 "开启鼠标支持

autocmd InsertLeave,WinEnter * set cursorline    "高亮当前行
autocmd InsertEnter,WinLeave * set nocursorline  "插入模式，取消当前行高亮

set scrolloff=2	    		"jk移动时光标到底部时，光标上下方保留2行
set sidescrolloff=2

let g:vim_markdown_folding_disabled = 1  "设置md标题默认不折叠

]])
```
修改 **~/.config/nvim/init.lua** ，加载basic.lua文件
```lua
require('basic')		-- 基础设置, 加载文件 lua/basic.lua
```

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
  use 'mhinz/vim-startify'        -- 启动页列出最近打开的文件 
  use 'rlue/vim-barbaric'         -- 中文输入法自动切换，需要手动安装xkbswitch-macosx依赖，见下文

  use { 'plasticboy/vim-markdown', ft = {'markdown'},           --支持markdown编辑, 
        require = {'godlygeek/tabular'}   }                     -- vim-markdown依赖tabular插件
  use { 'iamcco/markdown-preview.nvim',  ft = {'markdown'},     -- 在md文件下运行 :MarkdownPreview 可实时预览
        run = function() vim.fn['mkdp#util#install']() end  }   -- 打开的文件类型是markdown文件时，才加载该插件

  <!-- use { 'tomtom/tcomment_vim' }  -- 注释插件   当前行 gcc or gc（选中模式） -->

  use { "vim-airline/vim-airline",          -- 状态栏美化插件
        requires = {
        "vim-airline/vim-airline-themes",
        "ryanoasis/vim-devicons" }}  --图标插件，支持vim-airline, lightline, vim-startify；要放在vim-airline后面

  use "kevinhwang91/rnvimr" --悬浮文件管理ranger, mac先安装系统依赖。hjkl ctrl-t新tab ctrl-x水平ctrl-v垂直打开文件

  use { "junegunn/fzf", run = function() vim.fn['fzf#install']() end }  --模糊查找神器: 内容，文件、Git分支、进程
  use 'junegunn/fzf.vim'
 
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
use 'rlue/vim-barbaric'     --中文输入法自动切换，这里使用packer.nvim插件管理器
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
    Plug 'lyokha/vim-xkbswitch'      "中文自动输入法切换插件, 记得重启vim然后执行 :PlugInstall
    ...
   call plug#end()
   
   let g:XkbSwitchEnabled = 1        "默认让vim-xkbswitch中文输入法自动切换生效
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
  
 ```vim
call plug#begin('~/.vim/plugged')  "这里同时也指定了插件的安装目录~/.vim/plugged

Plug 'scrooloose/nerdtree'
Plug 'mhinz/vim-startify' 
Plug 'tpope/vim-fugitive' 
Plug 'lfv89/vim-interestingwords'

call plug#end()
 ```

## 例子，配置nerdtree
- 在 .vimrc 配置文件`call plug#end()`的后面添加如下配置，用来设置`空格键 + n`快捷键来激活nerdtree:
  
  ```vim
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


## 用vim-plua安装Markdown
在.vimrc文件加入如下内容
```vim
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
```vim
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
```


## 快捷键定义or映射
```vim
let mapleader = " "	   			"注意： 双引号里有个空格，这里把leader键映射成空格键
inoremap jj <Esc>	   			"在插入模式下，连续输入jj可以退出插入模式

nmap sp :split<Return><C-w>w			"正常模式下，sp水平切分窗口
nmap vs :vsplit<Return><C-w>w			"正常模式下，vs垂直切分窗口
```



## 拆分窗口
	水平拆分 :sp
	垂直拆分 :vs    or  :vsp

## 交换当前行和下一行
	ddp

## 正常模式下，选中全部内容
	ggVG

## 回到上次编辑的地方
    g;

## 系统剪贴板clipboard
从vim复制到系统剪贴板复制 
```vim
"+y         注意前面的双引号"也要
"+2yy       复制两行
```

从系统剪贴板粘贴到vim

- 方法一：在 **输入模式**下，使用**Ctrl + v**  也能从系统剪贴板粘贴到vim
- 方法二： 
```vim
"+p				注意前面的双引号"也要
```
设置vim默认使用系统剪贴板。如果想y/p直接和系统剪贴板打通，可以在~/.vimrc中加上以下配置
```vim
set clipboard^=unnamed,unnamedplus    "其中unnamed代表*寄存器，unnamedplus代表+寄存器。
```

# nvim-tree 文件管理
packer.nvim安装
```lua
use { 'kyazdani42/nvim-tree.lua', requires = 'kyazdani42/nvim-web-devicons'}  -- 文件管理
```
nvim-tree 可以执行常见的 创建 、删除、拷贝、剪切 文件等操作
```
o 打开关闭文件夹
a 创建文件
r 重命名
x 剪切
c 拷贝
p 粘贴
d 删除
s 使用系统默认程序打开目录或文件
<Tab> 将文件添加到缓冲区，但不移动光标
<C-t> 在新tab中打开文件
<C-v> 垂直分屏打开文件
<C-x> 水平分屏打开文件
<C-]> 进入光标下的目录 相当 cd 目录
<C-r> 重命名目录或文件，删除已有目录名称
 - 返回上层目录
 R 刷新 
 / 搜索

```


# [vim-visual-multi](https://github.com/mg979/vim-visual-multi) 多光标插件or多选择插件 
用packer安装
```lua
use {'mg979/vim-visual-multi', branch = 'master'}
```

日常操作命令
```
ctrl-n 选中光标下的单词, 开始多选择操作

n/N 选中下一个/上一个匹配的单词

q 跳过当前匹配的单词or取笑当前匹配单词的选中状态, 并跳到下一个

i，a，I，A 启动插入模式
```


# [telescope](https://github.com/nvim-telescope/telescope.nvim)模糊查找神器,比fzf好用
用packer安装
```lua
use {
    "nvim-telescope/telescope.nvim",
    requires = {
        "nvim-lua/plenary.nvim", -- Lua 开发模块
        "BurntSushi/ripgrep", -- 文字查找
        "sharkdp/fd" -- 文件查找
    },
    config = function()  -- config 是每次插件加载完成后自动运行 lua/conf/telescope.lua 文件中的代码
        require("conf.telescope")
    end
}
```

在lua/conf/telescope.lua 文件中添加如下配置代码
```lua
-- telescope 需呀先手动安装依赖 fd 和 ripgrep

require("telescope").setup()

-- 查找文件: 在当面工作目录及子目录下查找. :pwd查看当前工作目录, :cd 可以进入新的工作目录
vim.keybinds.gmap("n", "<leader>ff", "<cmd>Telescope find_files theme=dropdown<CR>", vim.keybinds.opts)

-- 查找文件: 在打开过的文件中查找 file open rencend
vim.keybinds.gmap("n", "<leader>fr", "<cmd>Telescope oldfiles theme=dropdown<CR>", vim.keybinds.opts)

-- 查找文件: 在当前打开的缓冲区中查找
vim.keybinds.gmap("n", "<leader>fb", "<cmd>Telescope buffers theme=dropdown<CR>", vim.keybinds.opts)

-- 搜索光标下内容:  在当前工作目录及子目录下的文件中搜索
vim.keybinds.gmap("n", "<leader>fs", "<cmd>Telescope grep_string theme=dropdown<CR>", vim.keybinds.opts)

-- 搜索内容:  在当前工作目录及子目录下的文件中搜索
-- vim.keybinds.gmap("n", "<leader>fg", "<cmd>Telescope live_grep theme=dropdown<CR>", vim.keybinds.opts)


-- 查找 marks 标记
vim.keybinds.gmap("n", "<leader>fm", "<cmd>Telescope marks theme=dropdown<CR>", vim.keybinds.opts)

-- 查找帮助文档
vim.keybinds.gmap("n", "<leader>fh", "<cmd>Telescope help_tags theme=dropdown<CR>", vim.keybinds.opts)
```

- **`<leader>ff`** 查找文件: 在当面工作目录及子目录下查找. :pwd查看当前工作目录, :cd 可以进入新的工作目录
- **`<leader>fr`** 查找文件: 在打开过的文件中查找 file open rencent
- **`<leader>fb`** 查找文件: 在当前打开的缓冲区中查找
- **`<leader>fs`** 搜索光标下内容:  在当前工作目录及子目录下的文件中搜索

- **`<leader>fm`** 查找 marks 标记
- **`<leader>fh`** 查找帮助文档
```
ctrl-t 新tab中打开文件 
ctrl-x 水平分割窗口打开文件
ctrl-v 垂直分割窗口打开文件，可能要连续按2次

<Tab> 选中当前的搜索结果，可搭配 <CR> 一次性打开多个
<C-c> 退出搜索框
```
# [hop](https://github.com/phaazon/hop.nvim) 字词行快速定位跳转
使用packer安装
```lua
use {
    "phaazon/hop.nvim",
    config = function()
        require("conf.hop")  -- config 是每次插件加载完成后自动运行 lua/conf/hop.lua 文件中的代码
    end
}
```

在lua/conf/hop.lua加入下面的配置代码
```lua
require("hop").setup()
-- 搜索并跳转到字符
vim.keybinds.gmap("n", "<leader>hc", "<cmd>HopChar1<CR>", vim.keybinds.opts)
-- 搜索并跳转到单词
vim.keybinds.gmap("n", "<leader>hw", "<cmd>HopWord<CR>", vim.keybinds.opts)
```
- **`<leader>hc`** 输入1个字符,就可以快速跳转到给字符的位置


# LSP代码自动补全AutoComplete
Neovim内置支持LSP 客户端. 除了客户端,每种语言还需要相应的服务端 LSP Server. Neovim 是客户端，默认不包含 language server，需要自己安装。

[nvim-cmp](https://github.com/hrsh7th/nvim-cmp) 是补全核心插件，而 [vim-vsnip](https://github.com/hrsh7th/vim-vsnip) 是补全引擎，补全引擎有很多但我个人觉得 vim-vsnip 是最强大的，因为他可以直接调用 vscode 下的代码片段。

## lsp安装步骤
:h lsp 查看文档 QUICKSTART 里写了 4 步

1. 安装语言的LSP Client配置插件 [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig) ,该插件是nvim官方出品.
2. 安装语言的LSP server.  使用[nvim-lsp-installer](https://github.com/williamboman/nvim-lsp-installer) 可以自动安装语言的LSP Server。以前用nvim-lspinstall 现在已经被弃用.

3. 配置对应语言 require('lspconfig').xx.setup{…}
4. 检查LSP Client已经和当前缓冲区建立好链接 `:lua print(vim.inspect(vim.lsp.buf_get_clients()))`






# [ranger](https://github.com/ranger/ranger)悬浮文件管理

ranger只能逐级逐目录查找文件; 不能模糊、跨多个目录查找文件。

fzf.vim可以模糊搜索当前项目、或者当前目录和子目录中的文件、或者vim打开的第一个文件所在目录和子目录下的文件。在vim里可以用`:pwd` 查看当前目录  `:cd ***` 改变当前目录

安装系统依赖
```bash
# macOS users please install ranger by `pip3 ranger-fm` instead of `brew install ranger`
pip3 install ranger-fm pynvim
```
使用packer安装ranger的vim插件[rnvimr](https://github.com/kevinhwang91/rnvimr)
```
use "kevinhwang91/rnvimr"    --悬浮文件管理器ranger, mac下要先安装系统依赖。 使用hjkl 和 回车<CR>. ctrl-t新tab ctrl-x 水平 ctrl-v垂直打开文件
```
ranger文件管理器快捷键和基本设置（init.lua）
```vim
" 悬浮文件管理器ranger设置
let g:rnvimr_enable_ex = 1          " 让Ranger取代Netrw并成为文件浏览器
let g:rnvimr_enable_picker = 1      " 选择文件后隐藏
let g:rnvimr_ranger_cmd = 'ranger --cmd="set viewmode multipane"'  "使用multipane单列模式，可按~手动切换成多列
noremap <silent> <Leader>f :RnvimrToggle<CR>  “ranger逐级逐目录查找文件; 不能模糊、跨多个目录查找文件。
```

Ranger的基础键位如下
```
q 退出浮动窗口
jk 上下左右移动
h 表示进入上一级父目录
l或者回车<CR> 进入子目录或者打开文件

空格 选中一个文件，对选中的文件再按空格取消选中
v 选中全部文件

dd 剪切文件到剪切板
dD 彻底删除文件
yy 复制文件
pp 粘贴文件

a 修改名字

ctrl-t 新tab中打开文件 
ctrl-x 水平分割窗口打开文件
ctrl-v 垂直分割窗口打开文件，可能要连续按2次

g 可以快速进入不同目录，有提示
```

然后在终端运行，看看安装是否正确
```
nvim +'checkhealth rnvimr'
```

# [fzf.vim](https://github.com/junegunn/fzf.vim)模糊搜索神器, 文件、内容都可以搜索
使用packer安装fzf插件
```lua
use { "junegunn/fzf", run = function() vim.fn['fzf#install']() end }  --模糊查找神器: 内容，文件、Git分支、进程
use 'junegunn/fzf.vim'
```

fzf的基本配置（init.lua)
```vim
" ------ fzf 模糊搜索
" fzf的:Files模糊搜索当前项目、或者当前目录和子目录中的文件、或者vim打开的第一个文件所在目录和子目录下的文件 
" :pwd 查看当前目录  :cd *** 可以改变当前目录
nnoremap <silent> <Leader>pf :Files<CR>

" fzf模糊查找当前打开的文件（buffer）
nnoremap <silent> <Leader>b :Buffers<CR>

" fzf模糊查找打开过的历史文件
nnoremap <silent> <Leader>h :History<CR>

"fzf模糊搜索内容：当前项目、或者vim打开的第一个文件所在目录和子目录下所有文件的内容都可以搜索 
"buffer文件如果不属于 当前目录 则:Rg不会搜索；如果要搜索所有buffer的内容，就要用:Lines
nnoremap <silent> <Leader>ps :Rg<CR>

"fzf模糊搜索内容：在当前打开的所有文件(buffer)中搜索 
nnoremap <silent> <Leader>bs :Lines<CR>
```
fzf基本命令
```
<Esc> 退出浮动窗口
```


