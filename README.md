# Sublime Text 入坑指南

## 安裝主程式

#### Windows
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
#### AceJump
https://packagecontrol.io/packages/AceJump
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

