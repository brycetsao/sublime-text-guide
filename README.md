# Sublime Text 入坑指南
本篇文向大家介紹 Sublime Text 這個優秀的編輯器，並引導讀者在數分鐘之內將 Sublime Text 配置成爲個人化的 IDE。

## 安裝主程式

#### Windows/Mac OS X
到這裏下載：
http://www.sublimetext.com/3

#### Linux (Ubuntu/Mint)
建議用系統的套件管理來安裝，在 terminal 輸入：
``` shell
$ sudo apt-get install sublime-text
```

## 安裝套件

### 安裝套件管理
依照官網的指示：https://packagecontrol.io/installation

翻譯如下：
> 複製下面的 Python code，然後在 Sublime Text 中按下 <kbd>Ctrl</kbd> + <kbd>\`</kbd> 打開 console（或者 `View > Show Console`）,貼上剛剛複製的 code，再按 <kbd>Enter</kbd>，就會執行安裝了。

安裝完成之後，請先重啓 Sublime Text。
用 <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> 叫出指令面板（或者 `Preference > Package Control`），
輸入「install package」,即可瀏覽可用的套件，輸入欲安裝的套件名稱即可安裝。

### 套件推介

#### Alternate VIM Navigation

使用 <kbd>Alt</kbd> + <kbd>I</kbd> / <kbd>J</kbd> / <kbd>K</kbd> / <kbd>L</kbd> 來上下左右移動游標，
<kbd>Alt</kbd> + <kbd>H</kbd> / <kbd>;</kbd> 以將游標移動至行首 / 行尾，
在自動完成選單中也可以用這個方式在候選詞中上下移動，令右手不必再離開打字區。
亦可以搭配 <kbd>Shift</kbd> 選取文字、<kbd>Ctrl</kbd> 逐字移動等等。
筆者對這個套件的依賴已經到了沒裝它就不知如何移動游標的程度了。

#### AceJump
https://packagecontrol.io/packages/AceJump

![AceJump](https://cloud.githubusercontent.com/assets/8056203/10858871/92069504-7f58-11e5-8593-e373121fd917.gif)

#### All Autocomplete
內建的補完功能並沒有支援 STL 中一些常用的東西，好在 Sublime Text 會自動學習目前檔案中寫過的關鍵字。安裝了這個套件之後，不止編輯中的檔案，所有開啓中的檔案內用過的關鍵字都會被學習起來。

#### AdvancedNewFile
https://packagecontrol.io/packages/AdvancedNewFile

## 將 Sublime Text 打造成爲 IDE

這個部分將說明如何安裝 TDM-GCC 作爲 C++ 的編譯器，並設定一鍵編譯。

### 安裝 GCC

GCC 是目前 C++ 最廣泛被使用的編譯器，因爲 Sublime Text 本身只是文字編輯器，我們需要另行安裝編譯器。
Mac OS X 則已經內建了 GCC，所以不需再安裝。

#### Windows

這裏推薦 Windows users 使用 TDM-GCC 而非 MinGW，因爲前者的安裝較爲簡單，不需經過繁複的設定。
（另外筆者也被 MinGW 的 bug 雷過）

到這裏下載：http://tdm-gcc.tdragon.net/download

#### Linux
一樣用系統的套件管理安裝，建議將 g++ 一併裝起來。
``` shell
$ sudo apt-get install g++
```

### 使用 Build System 建立編譯腳本

Build System 是編譯指令的腳本。
工具列中的 `Tools > Build System` 裏面已經內建了一些常用語言的 Build System。
但內建的 Build System 不是很好用，如果想要加入自己的編譯參數，我們可以選擇 `Tools > Build System > New Build System` 來建立自訂的 Build System。

以下是筆者所使用的 Build System，其效果相當於在 shell 執行以下的編譯指令，並執行編譯完成的程式，亦即「Compile & Run」：
``` shell
$ g++ -Wall -lm -lcrypt -O2 -std=c++11 -pipe -[檔案名稱]
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
            "shell_cmd": "g++ $file -Wall -lm -lcrypt -O2 -std=c++11 -pipe && gnome-terminal -x bash -c \"./a.out; read -p \\\"[Press any key]\\\"\""
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
