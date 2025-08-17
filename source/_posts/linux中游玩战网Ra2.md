# 在linux安装战网平台

在这里我们给大家带来多平台支持的可能性来安装战网平台。

## 安装并设置wine

Wine（Wine Is Not an Emulator）是一个兼容层，让你能在 Linux（或 BSD、macOS）上运行 Windows 程序。

    Wine 版本选择：
    
        稳定版（stable）：适合日常使用
    
        开发版（devel）：功能更新更快
    
        Staging 版：开发版 + 额外补丁，适合游戏和测试
    
    架构：
    
        64 位前缀：默认，路径如 ~/.wine
    
        32 位前缀：某些老程序需要，需启用 32 位支持

## Debian / Ubuntu / Linux Mint / Pop!_OS

sudo dpkg --add-architecture i386  # 启用 32 位支持
sudo mkdir -pm755 /etc/apt/keyrings
sudo wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key

### 例 ubuntu 24.04
```bash
sudo dpkg --add-architecture i386  # 启用 32 位支持
sudo mkdir -pm755 /etc/apt/keyrings
sudo wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key

# 选择你的发行版版本，例如 ubuntu 24.04
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/noble/winehq-noble.sources

sudo apt update
sudo apt install --install-recommends winehq-stable

```

## fedora

```bash
sudo dnf config-manager --add-repo https://dl.winehq.org/wine-builds/fedora/$(rpm -E %fedora)/winehq.repo
sudo dnf install winehq-stable

```

## RHEL / CentOS / AlmaLinux / Rocky Linux

```bash
sudo dnf install epel-release
sudo dnf config-manager --add-repo https://dl.winehq.org/wine-builds/rhel/$(rpm -E %rhel)/winehq.repo
sudo dnf install winehq-stable

```

## Arch

```bash
sudo pacman -Syu wine
```

# 如果需要额外工具：
```bash
sudo pacman -S wine-mono wine-gecko winetricks
```

### openSUSE Tumbleweed / Leap

```bash
sudo zypper ar -cfp 95 https://dl.winehq.org/wine-builds/opensuse/tumbleweed/ winehq
sudo zypper ref
sudo zypper in winehq-stable

```

## gentoo

```bash
sudo emerge --ask app-emulation/wine
# 或者 Staging：
sudo emerge --ask app-emulation/wine-staging

```

### 确认您的wine已经正常安装。

```bash
wine --version
```

若您已经安装wine 那您只需要创建前缀并且使用新前缀来运行平台

```bash
export WINEPREFIX="$HOME/ra2"
wineboot
```

如果您觉得每次都要设置环境变量，推荐将其写入到.bashrc

```bash
echo 'export WINEPREFIX="$HOME/ra2"' >> ~/.bashrc
```



## 下载战网平台

https://www.ra2ol.com/在此处下载您的战网平台 并且在您的终端找到此文件地址

```bash
cd xxx
wine npxxx.xx
```

如您不能正常显示字体 请安装winetricks 具体安装步骤 每个发行版本不同。利用winetricks安装必须库以及字体：

```bash

winetricks -q directplay
winetricks -q d3dx9
winetricks -q vcrun2008
winetricks -q vcrun2010
winetricks -q vcrun2015
winetricks -q dotnet40
winetricks -q dxvk
winetricks -q allfonts
```

接下来设置winecfg的windows版本，最好为windows7，兼容性强一些。

若不能启动请先设置新的wine前缀，最好用Steam版本的proton版本运行安装程序。

接下来用wine运行你的战网程序

```bash
wine  wine HTplatform.exe 
```

剩下步骤基本和windows类似，这里有一个问题如果安装的时候提示你是否从网络下载红色警戒2尤里的复仇版本，若果您电脑有购买了steam版本的红色警戒您可以直接添加文件到战网平台，如果没有您可选从网络下载。下载之后目录类似这样：

```bash
wlmosv@wlmosv ~/g/rs> ls
args.bat        cookies.dat         HTEsport.Client.exe*  node.dll          rebuild.exe*    update/
avcodec.dll     dxbase.dll          HTEsport.Voice.exe*   OMCS.dll          Res/            vcomp140.dll
avutil.dll      ESBasic.dll         HTplatform.exe*       OraycnCodecs.dll  swresample.dll  vcruntime140.dll
BugReport.exe*  ExuiKrnln.dll       Logs/                 RA2/              Temp/           VoiceVer.txt
config.data     HPSocket4C.dll      msvcp140.dll          RANK.ini          unins000.dat    YURI/
Config.ini      HPSocket4C-SSL.dll  Newtonsoft.Json.dll   rebuild2.exe*     unins000.exe*   zlibwapi.dll
wlmosv@wlmosv ~/g/rs> cd YURI/
wlmosv@wlmosv ~/g/r/YURI> ls
7za.exe*  yuri/  yuri.7z.tmp
wlmosv@wlmosv ~/g/r/YURI> 



```

这里的yuri.7z.tmp您需要自行解压在此目录，防止下次打开时再次下载游戏文件。

之后选择设置兼容性。补丁为cncddraw就可以。



## 常见问题解答

- 为什么我总是一卡一卡？

关闭代理软件

- 为什么我进房间延迟那么高？

有的机器在wine创建前缀后不能完全模拟windows在ra2红警中的网络套件一般为100。但延迟没那么高 这个没有解决方法，但是不影响游戏。

- 我该怎么更新我的战网平台？

像windows一样

- 为什么有时候我进不去官方地图？

您可以使用测试版杜绝这种现象。