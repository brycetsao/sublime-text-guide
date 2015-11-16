# Sublime Text 入坑指南

## 安裝主程式

#### Windows / Mac OS X
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
https://packagecontrol.io/packages/Alternate%20VIM%20Navigation

可以用 <kbd>Alt</kbd> + <kbd>I</kbd><kbd>J</kbd><kbd>K</kbd><kbd>L</kbd> 來上下左右移動游標，
<kbd>Alt</kbd> + <kbd>H</kbd> / <kbd>;</kbd> 以將游標移動至行首 / 行尾。

#### AceJump
https://packagecontrol.io/packages/AceJump

![AceJump](https://cloud.githubusercontent.com/assets/8056203/10858871/92069504-7f58-11e5-8593-e373121fd917.gif)

#### All Autocomplete
https://packagecontrol.io/packages/All%20Autocomplete

#### AdvancedNewFile
https://packagecontrol.io/packages/AdvancedNewFile

## 將 Sublime Text 打造成爲 IDE

### 安裝 GCC

#### Windows
http://tdm-gcc.tdragon.net/download

#### Linux
```shell
$ sudo apt-get install gcc
```

### 使用 Build System 建立編譯腳本

#### Windows
```json
{
     "variants":
     [
          {   
               "name": "Run",
               "shell": true,
               "cmd": 
               [
                    "g++", "-Wall", "-lm", "-O2", "-std=c++11", "-pipe", "$file",
                    "&&", "start", "cmd", "/k", "a"
               ]
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
            "shell_cmd": "g++ \"${file}\" -lm -lcrypt -O2 -std=c++11 -pipe;
            gnome-terminal -x bash -c \"./a.out; read -p \\\"[Press anykey]\\\"\""
        }
    ]
}
```

