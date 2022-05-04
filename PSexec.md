[程式人生 > > PSTools工具使用方法](https://www.796t.com/content/1545698596.html)
[PSTools工具使用方法](https://www.twblogs.net/a/5c21e798bd9eee16b4a762e8)
[psTool Suit使用方法](https://itman.pixnet.net/blog/post/28315565)

## PsTool PsExec 常用遠端指令

### 遠端變更電腦名稱.bat
```
@ECHO OFF      
SET /P ComputerName1=舊電腦名稱:
SET /P ComputerName2=新電腦名稱:
SET /P DomainID=網域管理者Domain\Admin:
SET /P DomainPWD=網域管理者密碼:

PsExec.exe "\\%ComputerName1%" -i -d -u %DomainID% -p %DomainPWD% wmic ComputerSystem where Name="%ComputerName1%" call Rename Name="%ComputerName2%"

pause
```

### 遠端執行程式.bat
```
@ECHO OFF      
SET /P ComputerName1=目標電腦名稱:
SET /P DomainID=網域管理者Domain\Admin:
SET /P DomainPWD=網域管理者密碼:

PsExec.exe "\\%ComputerName1%" -i -d -u %DomainID% -p %DomainPWD% "\\Server\Folder\update.exe"

pause
```

### 列出幾個常用的指令
```
@強制關機
start /min psshutdown -f \\192.168.1.112 -u administrator -p 123456 -t 1
@關機
start /min psshutdown -k \\192.168.1.112 -u administrator -p 123456 -t 1
@重新啟動電腦
start /min psshutdown -r \\192.168.1.112 -u administrator -p 123456 -t 1
@關機
start /min psshutdown -s \\192.168.1.112 -u administrator -p 123456 -t 1
```

### 預設的原始目錄為 %SystemRoot%（C:\windows）
### 語法：
psexec [\\computer[,computer2[,...] | @file] [-u user [-p psswd]]][-n s][-l][-s|-e][-x][-i [session]][-c [-f|-v]][-w directory][-d][-<priority>][-a n,n,... ] cmd [arguments]
### 參數（部份）：
+ -c：將指定的程式複製到遠端系統以執行。如果省略這個選項，則應用程式必須在遠端系統上的系統路徑中。
+ -d：請勿等候應用程式終止。僅使用這個非互動式應用程式的選項。
+ -f：即使檔案已經存在於遠端系統內，還是將指定的程式複製到遠端系統。
+ -i：執行此程式，才能夠讓它與遠端系統中指定的工作階段的桌上型電腦互動。如果沒有指定的工作階段，則處理序在主控台工作階段中執行。
+ -l：以限制使用者的身分執行處理序（刪除系統管理員群組，且只允許使用者群組指派的權限）。在 Windows Vista 中，使用低整合性執行處理序。
+ -p：指定選擇性使用者名稱密碼。如果省略這個動作，則會出現輸入隱藏密碼的提示。
+ -u：指定選擇性使用者名稱以登入遠端電腦。
+ -w：設定處理序的工作目錄（相對於遠端電腦）。
@file：導入 PsExec 以執行每個電腦（指定的文字檔中所列示）的命令。

###  範例：
```
@執行遠端電腦上的IE
psexec -u domain\user -p password \\192.168.0.24 -d -l -i "X:\Program Files\Internet Explorer\iexplore.exe"
@開啟遠端電腦上的檔案(shutdown.bat)
psexec -u domain\user -p password \\192.168.0.24 -d -w c:\sch -i notepad shutdown.bat
@顯示遠端電腦的連線狀態（會跳出輸入密碼的提示）
psexec -u domain\user \\192.168.0.24  netstat -na
@啟動遠端電腦上的互動式命令提示（會跳出輸入密碼的提示，user 要為 Administrators 群組成員）
psexec -u domain\user \\192.168.0.24 cmd
@複製檔案(cpuz.exe)到遠端電腦上（會跳出輸入密碼的提示）
psexec -u domain\user \\192.168.0.24 -c cpuz.exe
```
