# VPNer
## 0. AppleScriptからアプリケーションを実行する準備
  システム環境設定>アクセシビリティ(ユニバーサルアクセス)  
  `補助装置にアクセスできるようにする` をチェック  

## 1. Automatorに新しいAppleScriptを記述する
  ファイル>新規  
  サービスを選択  
  中央の項目からライブラリ>AppleScriptを実行  
  selectで以下の設定  
  「サービスは以下の項目を受け取ります」=>"入力なし"  
  「検索対象」=>"すべてのアプリケーション"  
  コードに以下を記述  
    
    tell application "System Events"
        --現在focusされているApplicationの名前を取得
        set theName to name of the first process whose frontmost is true
    end tell
    --------この部分をVPNにする
    --------現在はsample
    beep 3
    --------ここまで

    tell application theName
        --現在選択されているApplicationにfocus
        activate
    end tell

## 2. VPN用のコードを----の間に記述
    tell application "System Events"
        tell current location of network preferences
            set VPNservice to service "VPN SERVICE" -- name of the VPN service
            set isConnected to connected of current configuration of VPNservice
            if isConnected then
                disconnect VPNservice
            else
                connect VPNservice
            end if
        end tell
    end tell

## 3. ショートカットキーの設定
  システム環境設定>キーボード>キーボードショートカット  
  最下部の`一般`の項目からAutomatorのworkflowファイル名に適当なショートカットを入れる  

## 4. 実際に動くコード
    tell application "System Events"
        --現在focusされているApplicationの名前を取得
        set theName to name of the first process whose frontmost is true
    end tell

    tell application "System Events"
        tell current location of network preferences
            set VPNservice to service "VPN (test)" -- name of the VPN service
            set isConnected to connected of current configuration of VPNservice
            if isConnected then
                disconnect VPNservice
            else
                connect VPNservice
            end if
        end tell
    end tell

    tell application theName
        --現在選択されているApplicationにfocus
        activate
    end tell  
  このコードを0 ~ 3の手順で設定する
