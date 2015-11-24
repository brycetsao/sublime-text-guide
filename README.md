# Sublime Text 入坑指南

Sublime Text 是一套十分受歡迎的文字編輯器，
因爲有豐富的快速鍵功能，強大的套件庫，以及高度的可自訂性，它很適合作爲個人化的開發環境。
本文將爲大家介紹這個優秀的編輯器，並引導讀者在數分鐘之內將 Sublime Text 配置成爲個人化的 IDE。

## 安裝主程式

Sublime Text 是商業軟體，你可以在官方網站免費下載試用版，而試用期是**無限**的。
除了偶爾會在存檔時詢問你是否要購買，試用版與正式授權版並無任何分別。
目前一份授權的售價是 70 美元，可以到[這裏](http://www.sublimetext.com/buy)購買。

#### Windows/Mac OS X
到這裏下載：
http://www.sublimetext.com/3

#### Linux (Ubuntu/Mint)
建議用系統的套件管理來安裝，在 terminal 輸入：
``` shell
$ sudo apt-get install sublime-text
```

## 基本操作

### 基礎

### 快速鍵

## 安裝套件

### 安裝套件管理

依照官網的指示：https://packagecontrol.io/installation

翻譯如下：
> 複製下面的 Python code，然後在 Sublime Text 中按下 <kbd>Ctrl</kbd> + <kbd>\`</kbd> 打開 console（或者 `View > Show Console`）,貼上剛剛複製的 code，再按 <kbd>Enter</kbd>，就會執行安裝了。

安裝完成之後，請先重啓 Sublime Text。
用 <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> 叫出指令面板（或者 `Preference > Package Control`），
輸入「install package」即可瀏覽可用的套件，輸入欲安裝的套件名稱即可安裝。

### 套件推介

#### Alternate VIM Navigation

使用 <kbd>Alt</kbd> + <kbd>I</kbd> / <kbd>J</kbd> / <kbd>K</kbd> / <kbd>L</kbd> 來上下左右移動游標，
<kbd>Alt</kbd> + <kbd>H</kbd> / <kbd>;</kbd> 以將游標移動至行首 / 行尾，
在自動完成選單中也可以用這個方式在候選詞中上下移動，令右手不必再離開打字區。
亦可以搭配 <kbd>Shift</kbd> 選取文字、<kbd>Ctrl</kbd> 逐字移動等等。
筆者對這個套件的依賴已經到了沒裝它就不知如何移動游標的程度了。

#### AceJump

![AceJump](https://cloud.githubusercontent.com/assets/8056203/10858871/92069504-7f58-11e5-8593-e373121fd917.gif)

使用以下快速鍵瞬移到畫面中的任何位置：
* <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>;</kbd> 移動到目標字
* <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>'</kbd> 移動到目標字元 
* <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>.</kbd> 移動到目標行

更多說明請見[這裏](https://packagecontrol.io/packages/AceJump)。

#### All Autocomplete

內建的補完功能並沒有支援 STL 中一些常用的東西，好在 Sublime Text 會自動學習目前檔案中寫過的關鍵字。安裝了這個套件之後，不止編輯中的檔案，所有開啓中的檔案內用過的關鍵字都會被學習起來。

#### AdvancedNewFile

![AdvancedNewFile](https://cloud.githubusercontent.com/assets/9604053/11331052/4bb42544-91f0-11e5-9296-0edd78e503ca.png)

一個介面漂亮的檔案瀏覽器，將資料夾拖進側邊欄即可放入檔案櫃，更多說明請見[這裏](https://packagecontrol.io/packages/AdvancedNewFile)

## 將 Sublime Text 打造成爲 IDE

Sublime Text 本身只有文字編輯器，若要編譯程式碼，我們需要另行安裝編譯器。
Sublime Text 中提供了 Build System 這個功能，方便使用者自行整合想用的編譯器。
這部分將說明如何安裝 TDM-GCC 作爲 C++ 的編譯器，並示範用 Build System 來設定「編譯並執行」的功能。

### 安裝 GCC

GCC 是目前 C++ 最廣泛被使用的編譯器。Mac OS X 則已經內建了 GCC，所以不需再安裝。

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
但內建的 Build System 不是很好用，如果想要「編譯並執行」的功能，或加入自己想要的編譯參數，我們可以選擇 `Tools > Build System > New Build System` 來建立自訂的 Build System。

最後給出的是筆者使用的 Build System，其效果相當於執行以下的編譯指令，接着執行編譯完成的程式：
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
