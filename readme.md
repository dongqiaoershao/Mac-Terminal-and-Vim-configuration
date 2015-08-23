

# Mac上的vim各种配置方法
## 网上教程：http://www.vpsee.com/2013/09/use-the-solarized-color-theme-on-mac-os-x-terminal/
## Solarized是目前最完整的Terminal/Editor/IDE配色项目，要在 Mac OS X 终端里舒服的使用命令行（至少）需要给3个工具配色，terminal、vim 和 ls。这里不得不提和Terminal相同功能的工具iTerm2。
### 1）下载Solarized：
    
    $ git clone git://github.com/altercation/solarized.git
    
### 2）Mac OS X 自带的 Terminal 和免费的 iTerm2 都是很好用的工具，iTerm2 可以切分成多窗口，更方便一些。如果你使用的是 Terminal 的话，在solarized/osx-terminal.app-colors-solarized 下双击 Solarized Dark ansi.terminal 和 Solarized Light ansi.terminal 就会自动导入两种配色方案 Dark 和 Light 到 Terminal.app 里。如果你使用的是 iTerm2 的话，到 solarized/iterm2-colors-solarized 下双击 Solarized Dark.itermcolors 和 Solarized Light.itermcolors 两个文件就可以把配置文件导入到 iTerm 里。

### 3）vim的配色最好和终端一致
    
    $ cd solarized
    $ cd vim-colors-solarized/colors
    $ mkdir -p ~/.vim/colors
    $ cp solarized.vim ~/.vim/colors/
    $ vi ~/.vimrc
    ``
        输入以下内容：
        syntax on
        set background=dark
        colorscheme solarized
    ``
    
### 4）ls
    ``
    MacOSX是基于FreeBSD的，所以一些工具ls,top等都是BSD那一套，ls不是GNU ls，所以即使Terminal/iTerm2配置了颜色，
    但是在Mac上敲入ls命令也不会显示高亮，可以通过安装coreutils来解决（brew install coreutils），不过如果对ls颜色
    不挑剔的话有个简单办法就是在.bash_profile里输出CLICOLOR=1：
    ``
    
    $ vi ~/.bash_profile
    ``
        输入以下内容
        export CLICOLOR=1
    ``

### 5）ls高亮设置
    $ sudo brew install xz coreutils
    $ gdircolors --print-database > ~/.dir_colors
    $ vim ~/.bash_profile 添加以下代码
    ``
        输入以下内容：
        if brew list | grep coreutils > /dev/null ; then
            PATH="$(brew --prefix coreutils)/libexec/gnubin:$PATH"
            alias ls='ls -F --show-control-chars --color=auto'
            eval `gdircolors -b $HOME/.dir_colors`
        fi
    ``

### 6）grep高亮设置
    $ vim ~/.bash_profile 添加以下代码
    ``
        输入以下内容：
        alias grep='grep --color'
        alias egrep='egrep --color'
        alias fgrep='fgrep --color'
    ``


### 7）增强命令行命令行工具：添加ll、l、la指令
    $ vim ~/.bash_profile 添加以下内容即可
    ``
        输入以下内容
        alias ll='ls -alF'
        alias la='ls -A'
        alias l='ls -CF'
    ``

### 8）mac电脑安装brew
    $ curl -LsSf http://github.com/mxcl/homebrew/tarball/master | sudo tar xvz -C/usr/local --strip 1


#### 补充：也可以玩一下 Terminal+Tmux、zsh+oh-my-zsh+powerline一套。



