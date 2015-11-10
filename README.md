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
#### AceJump
#### All Autocomplete
#### AdvancedNewFile

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
                    "&&", "echo", "Compilation", "completed.",
                    "&&", "start", "cmd", "/k", "a"
               ]
          }
     ]
}
```

#### Linux
``` json
{
    "shell_cmd": "g++ \"${file}\" -o \"${file_path}/${file_base_name}\"",
    "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
    "working_dir": "${file_path}",
    "selector": "source.c, source.c++",

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

