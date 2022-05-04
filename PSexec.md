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



