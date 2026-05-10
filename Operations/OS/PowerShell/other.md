# その他の操作

## Clipboard

**Clipboard に登録**
```
Set-Clipboard
```

**Clipboard の内容取得**
```
Get-Clipboard
```
※終了方法
Ctrl + Z → Enter

## 圧縮・解凍

**tar.gz 作成**
```powershell
tar -czf archive.tar.gz C:\path\to\dir
```

**tar.gz 解凍**
```powershell
tar -xzf archive.tar.gz
```

**zip 作成**
```powershell
Compress-Archive -Path "C:\path\to\dir\*" -DestinationPath "archive.zip"
```

**zip 解凍**
```powershell
Expand-Archive -Path "archive.zip" -DestinationPath "C:\path\to\out"
```
