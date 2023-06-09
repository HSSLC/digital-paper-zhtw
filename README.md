## Sony Digital Paper App 與 Fujitsu Digital Paper PC App 及 QUADERNO PC App 繁體中文翻譯
鑒於Sony Digital Paper App在繁體中文環境下還是會以簡體中文顯示，以及Fujitsu Digital Paper PC App（一代）和QUADERNO PC App（二代）沒有繁體中文的翻譯，此處翻譯了一份繁體中文翻譯檔供大家使用。  
__本儲存庫不會提供修改好的二進位檔案，請自行按照步驟修改__  

（以下通稱各版本軟體為Digital Paper App）  

### 螢幕截圖

<table>
  <tr>
    <td><img src="screenshots/sony.png" alt="Screenshot of Sony"></td>
    <td><img src="screenshots/fujitsu.png" alt="Screenshot of Fujitsu"></td>
    <td><img src="screenshots/quaderno.png" alt="Screenshot of Quaderno"></td>
  </tr>
</table>

### 切換語言
如果只是要切換語言的話，可以將主程式啟動的捷徑參數手動指定`--lang`參數。  
內建的語言：
* Sony Digital Paper App
  * en
  * ja
  * zh（簡體）
  * zh-CN（簡體）
  * zh-TW（預設內容也是簡體，導致繁體使用者也會看到簡體而非fallback的英文）
* Fujitsu Digital Paper PC App
  * en
  * en-US（內容較en少了一點）
  * ja
  * zh-CN
* Quaderno PC App
  * en
  * en-US（內容較en少了一點）
  * ja
  * zh-CN

例如：
```
DigitalPaperApp.exe --lang=en
```

### 修改方式

如果需要新增繁體中文至Digital Paper App，需要手動修改程式資源，可以照著以下步驟修改：  
需要先安裝[node.js](https://nodejs.org/)環境以使用asar包裝工具。  
接下來要安裝[asar包裝工具](https://github.com/electron/asar#install)，請照著裡面的指示安裝。  
然後下一步請找到Digital Paper App的程式檔，是以asar格式包裝的網頁，通常位於以下位置： 

#### Sony Digital Paper App：

```
C:\Program Files (x86)\Sony\Digital Paper App\DigitalPaperApp\resources\app.asar
```

#### Fujitsu Digital Paper PC App

```
C:\Program Files (x86)\Fujitsu\Digital Paper PC App\DigitalPaperPCApp\resources\app.asar
```

#### QUADERNO PC App

```
C:\Program Files\Fujitsu\QUADERNO PC App\QUADERNO_PCApp\resources\app.asar
```

請將其複製到其他地方以供拆解。  
接下來用node.js執行asar工具，安裝完的asar主程式通常會以下位置
```
%USERPROFILE%\node_modules\@electron\asar\bin\asar.js
```  

接下來執行以下拆解指令：
```
node %USERPROFILE%\node_modules\@electron\asar\bin\asar.js extract app.asar app
```

記得將檔案名稱與位置自行替換成自己的。  
然後將這個repo中對應各Digital Paper App版本的`messages.zh-TW.json`下載並複製到`app\res\locales\messages.zh-TW.json`  
再來將這些檔案打包回去，考慮以下指令：
```
node %USERPROFILE%\node_modules\@electron\asar\bin\asar.js pack app app.asar
```
檔案名稱與路徑也記得換成自己的，接下來就將修改完的`app.asar`複寫回原本拿出來的地方，舊版的記得備份，免得損毀。

### 翻譯

用openCC翻譯+轉換詞彙，再人工修正，Fujitsu和QUADERNO是用Sony版直接diff+merge，有可能會有轉換錯誤或是沒被轉換的漏網之魚，歡迎丟issues或是發pr進來。  
目前提供的翻譯檔案適用於以下版本，其他版本不保證可以完全相容：
* Digital Paper App 1.4.6.00008版（Sony）
* Digital Paper PC App 1.1.1.09250版（Fujitsu）
* QUADERNO PC App 2.1.1.06290（Fujitsu二代）

在原英文中有Software跟Firmware不精確地混用的情況，已經在繁體中文中盡量修正了，如果有漏修的歡迎回報。

### 聲明

本翻譯僅供學術研究參考用途。