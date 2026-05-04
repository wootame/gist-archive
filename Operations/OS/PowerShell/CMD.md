# PowerShell コマンドリファレンス

## ファイル・ディレクトリ操作

**ディレクトリ配下をすべて削除**
```powershell
Remove-Item -Path "C:\path\to\dir\*" -Recurse -Force
```

**ディレクトリ配下を安全にすべて削除（隠し項目含む）**
```powershell
Get-ChildItem -Path "C:\path\to\dir" -Force | Remove-Item -Recurse -Force
```

**ディレクトリごと削除**
```powershell
Remove-Item -Path "C:\path\to\dir" -Recurse -Force
```

**ファイル名で検索**
```powershell
Get-ChildItem -Path "C:\path\to\dir" -Recurse -Filter "filename"
```

**拡張子で検索**
```powershell
Get-ChildItem -Path "C:\path\to\dir" -Recurse -Filter "*.txt"
```

**ディレクトリのみ検索**
```powershell
Get-ChildItem -Path "C:\path\to\dir" -Directory -Recurse
```

## パッケージ管理（winget）

**ソース一覧更新**
```powershell
winget source update
```

**パッケージアップグレード**
```powershell
winget upgrade
```

**すべてアップグレード**
```powershell
winget upgrade --all
```

**パッケージインストール**
```powershell
winget install <package_name>
```

**パッケージ削除**
```powershell
winget uninstall <package_name>
```

**パッケージ検索**
```powershell
winget search <keyword>
```

**インストール済みパッケージ一覧**
```powershell
winget list
```

**特定パッケージ確認**
```powershell
winget list | Select-String <package_name>
```

## システム情報

**OSバージョン確認**
```powershell
Get-ComputerInfo | Select-Object WindowsProductName, WindowsVersion, OsBuildNumber
```

```powershell
systeminfo | Select-String "OS Name","OS Version"
```

**カーネルバージョン相当（NTバージョン）確認**
```powershell
[System.Environment]::OSVersion.Version
```

**ディスク使用状況**
```powershell
Get-PSDrive -PSProvider FileSystem
```

**ディレクトリサイズ確認**
```powershell
(Get-ChildItem -Path "C:\path\to\dir" -Recurse -File | Measure-Object -Property Length -Sum).Sum
```

**サブディレクトリも表示**
```powershell
Get-ChildItem -Path "C:\path\to\dir" -Directory | ForEach-Object {
  $size = (Get-ChildItem -Path $_.FullName -Recurse -File | Measure-Object -Property Length -Sum).Sum
  [PSCustomObject]@{
    Directory = $_.FullName
    SizeMB = [math]::Round($size / 1MB, 2)
  }
}
```

**メモリ使用状況**
```powershell
Get-CimInstance Win32_OperatingSystem | Select-Object TotalVisibleMemorySize, FreePhysicalMemory
```

**CPU情報**
```powershell
Get-CimInstance Win32_Processor | Select-Object Name, NumberOfCores, NumberOfLogicalProcessors
```

## プロセス管理

**プロセス一覧**
```powershell
Get-Process
```

**特定プロセス検索**
```powershell
Get-Process | Where-Object { $_.ProcessName -like "*<process_name>*" }
```

**PIDで終了**
```powershell
Stop-Process -Id <PID>
```

**強制終了**
```powershell
Stop-Process -Id <PID> -Force
```

**プロセス名で終了**
```powershell
Stop-Process -Name <process_name>
```

## ネットワーク

**IPアドレス確認**
```powershell
Get-NetIPAddress
```

```powershell
ipconfig
```

**ポート使用状況**
```powershell
Get-NetTCPConnection -State Listen
```

```powershell
netstat -ano
```

**特定ポートを使用しているプロセス確認**
```powershell
Get-NetTCPConnection -LocalPort <port> | Select-Object LocalAddress, LocalPort, State, OwningProcess
```

## ユーザー・権限管理

**ファイル所有者変更**
```powershell
icacls "C:\path\to\file" /setowner "<user>"
```

**再帰的に変更**
```powershell
icacls "C:\path\to\dir" /setowner "<user>" /T
```

**ファイル権限変更（読み取りと実行を付与）**
```powershell
icacls "C:\path\to\file" /grant "<user>:(RX)"
```

**再帰的に変更（フルコントロールを付与）**
```powershell
icacls "C:\path\to\dir" /grant "<user>:(OI)(CI)F" /T
```

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