# システム管理

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