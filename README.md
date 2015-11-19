# Sublime Text 入坑指南
本篇文除了介紹 Sublime Text 這個優秀的編輯器，也能幫助讀者在數分鐘之內將 Sublime Text 配置成個人化的 IDE。

## 安裝主程式

#### Windows/Mac OS X
http://www.sublimetext.com/3

#### Linux (Ubuntu/Mint)
``` shell
$ sudo apt-get install sublime-text
```

## 安裝套件

### 安裝套件管理
https://packagecontrol.io/installation

### 套件推介

#### Alternate VIM Navigation
[詳細說明](https://packagecontrol.io/packages/Alternate%20VIM%20Navigation)

可以用 <kbd>Alt</kbd> + <kbd>I</kbd><kbd>J</kbd><kbd>K</kbd><kbd>L</kbd> 來上下左右移動游標，
<kbd>Alt</kbd> + <kbd>H</kbd> / <kbd>;</kbd> 以將游標移動至行首 / 行尾。可搭配 <kbd>Shift</kbd> 選取文字、<kbd>Ctrl</kbd> 逐字移動。

#### AceJump
https://packagecontrol.io/packages/AceJump

![AceJump](https://cloud.githubusercontent.com/assets/8056203/10858871/92069504-7f58-11e5-8593-e373121fd917.gif)

#### All Autocomplete
https://packagecontrol.io/packages/All%20Autocomplete

#### AdvancedNewFile
https://packagecontrol.io/packages/AdvancedNewFile

## 將 Sublime Text 打造成爲 IDE

這個部分將說明如何安裝 TDM-GCC 作爲 C++ 的編譯器，並設定一鍵編譯。

### 安裝 GCC

GCC 是目前 C++ 最廣泛被使用的編譯器，因爲 Sublime Text 本身只是文字編輯器，我們需要另行安裝編譯器。
Mac OS X 則已經內建了 GCC，所以不需再安裝。

#### Windows

這裏推薦 Windows users 使用 TDM-GCC 而非 MinGW，因爲前者的安裝較爲簡單，不需經過繁複的設定。
下載：http://tdm-gcc.tdragon.net/download

#### Linux
``` shell
$ sudo apt-get install gcc
```

### 使用 Build System 建立編譯腳本

Build System 是編譯指令的腳本。
工具列中的 Tools > Build System 裏面已經內建了一些常用語言的 Build System。
但內建的 Build System 不是很好用，如果想要加入自己的編譯參數，我們可以選擇 Tools > Build System > New Build System 來建立自訂的 Build System。

以下是筆者所使用的 Build System，其效果相當於在 shell 以下編譯指令，並執行編譯完成的執行檔，亦即「Compile & Run」：
``` shell
$ g++ -Wall -lm -O2 -std=c++ -pipe -[file_name]
```

#### Windows
``` json
{
    "variants":
    [
        {
            "name": "Run",
            "shell_cmd": "g++ $file -Wall -lm -O2 -std=c++11 -pipe && start cmd /k a"
        }
    ]
}
```

#### Linux
``` json
{
    "variants":
    [
        {
            "name": "Run",
            "shell_cmd": "g++ $file -Wall -lm -lcrypt -O2 -std=c++11 -pipe && gnome-terminal -x bash -c \"./a.out; read -p \\\"[Press anykey]\\\"\""
        }
    ]
}
```

#### Mac OS X
``` json
{
    "variants":
    [
        {
            "name": "Run",
            "shell_cmd": "g++ $file -Wall -lm -O2 -std=c++11 -pipe && open -a Terminal ./a.out"
        }
    ]
}

```
