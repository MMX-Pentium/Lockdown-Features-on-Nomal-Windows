# 免責事項
この改造を行った場合に発生した損害を筆者は一切の責任を負いません。  
この改造は元に戻す方法が見つかっていなかったり正常に機能しなかったり未確認なところが沢山あります。  
  
# 概念
Windows 10 IoTには組み込みシステム向けのロックダウン機能があり、それらの機能を通常のWindowsエディションで使えるようにしようという試みと言う名の私の暇つぶし。  

# カスタムログオンを有効にする方法(現時点では元に戻せないので注意)
以下をbatファイルとして実行

```bash
cd /d %~dp0

openfiles > NUL 2>&1
if NOT %ERRORLEVEL% EQU 0 goto USER_PROC

dir /b %SystemRoot%\servicing\Packages\Microsoft-Windows-Embedded-EmbeddedLogon-Package~3*.mum >List.txt
for /f %%i in ('findstr /i . List.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"
exit

:USER_PROC
powershell start-process %~nx0 -verb runas
```
