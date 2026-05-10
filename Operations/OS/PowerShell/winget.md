# パッケージ管理（winget）

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


