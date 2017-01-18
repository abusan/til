# chocolateyの使い方

## chocolateyとは
一言でいうと __Windowsで使えるapt-get__   

## インストール
公式サイトに書いてあるコマンドを、管理者権限で実行しているコマンドプロンプトで実行する。  
[Installation](https://chocolatey.org/install)  
More Install Options -> More Options -> Cmd.exeの項目にあるコマンド。Cmd.exeの横にあるアイコンをクリックするとコピーできる。  
```
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

### コマンドプロンプトを管理者権限で実行するには？
管理者権限で起動しないとchocolateyはインストールできない

+ タスクバーのWindowsボタンから
タスクバーのWindowsボタンを右クリック  
__コマンドプロンプト(管理者)__ をクリック

+ スタートメニューから  
Windows システムツール -> コマンドプロンプトで右クリック  
管理者として実行をクリック(Win10はその他の中にある)

## コマンド
chocolateyのコマンドは三種類  
+ chocolatey  
+ choco  
chocolateyのエイリアス
+ cinst  
chocolatey installのエイリアス

### ヘルプの表示
```
chocolatey /help
```

### インストール
```
cinst [パッケージ名]
```

### インストール(複数)
```
cinst [パッケージ名1] [パッケージ名2] ...
```

### インストール済みのパッケージリスト
```
choco list -lo
```

### インストールしたパッケージを全てアップデート
```
choco upgrade all -y
```

### 指定したパッケージをアップデート
```
choco upgrade [パッケージ名]
```

### パッケージのアンインストール
```
cuninst [パッケージ名]
```