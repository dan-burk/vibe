[ホーム](./)

# WSLを使ってWindowsにClaude Codeをインストール

このガイドでは、Windows Subsystem for Linux（WSL）を使ってWindowsにClaude Codeを導入する手順を最初から最後まで説明します。WSLはWindows上でLinuxを動かす仮想環境です。Claude CodeはWindowsでも動作しますが、多くの開発コマンドをそのまま使えるLinux環境の方が高速で安定します。

## 概要

- WSLをインストール
- Ubuntu Linuxをセットアップ
- Node.jsをインストール
- Claude Codeをインストール
- APIキー（またはサブスクリプション）を設定
- Claude Codeを使って作業開始

## 用意するもの

- Windows 10（バージョン2004以降）またはWindows 11 PC
- インターネット接続
- 管理者権限のあるアカウント
- Claude Pro/MaxサブスクリプションまたはAnthropic APIキー
- 作業時間の目安：15〜20分

## ステップ1：仮想化が有効か確認

WSLを使うには、PCで仮想化が有効になっている必要があります。

1. タスクバー（画面下部）を右クリックし、**タスクマネージャー**を開く
2. コンパクト表示の場合は左下の**詳細**をクリック
3. 上部の**パフォーマンス**タブを開き、左の**CPU**を選択
4. 右下にある **仮想化:** の表示を確認
   - **「有効」** と表示 → 次のステップへ
   - **「無効」** と表示 → PCのBIOSで仮想化（Intel VT-x / AMD-V / SVMなど）を有効にしてから再起動

## ステップ2：管理者権限でPowerShellを開く

1. **Windowsスタートボタン**をクリックし、`PowerShell`と入力
2. 検索結果の **Windows PowerShell** を右クリック
3. **管理者として実行** を選択し、UACの確認は **はい** をクリック
4. 白文字の青いウィンドウ（管理者PowerShell）が起動します

## ステップ3：WSLをインストール

**インストール済みか確認：**
```powershell
wsl --list --verbose
```
- `Ubuntu` が `Running` / `Stopped` 状態で表示 → すでにインストール済みなのでステップ4へ
- エラーや「ディストリビューションがありません」と表示 → 次のインストール手順へ

**WSLとUbuntuをまとめてインストール：**
```powershell
wsl --install
```
- 「Installing: Windows Subsystem for Linux」「Installing: Ubuntu」などの表示が出ます
- 完了メッセージが出たら、スタート > 電源アイコン > **再起動** を選択
- 再起動後、2〜5分ほどでUbuntuウィンドウが自動で開き、セットアップが続行されます
  - もし自動で開かない場合は、後述の手順でUbuntuを手動起動すれば問題ありません

> **補足：** コマンドが認識されない場合は、Windowsのバージョンが古い可能性があります。Windows UpdateでWindows 10 バージョン2004以降、またはWindows 11に更新してください。

## ステップ4：Ubuntuの初期設定（初回のみ）

再起動後に表示されるUbuntuターミナル、またはスタートメニューから起動したUbuntuで以下を実行します。

1. `Enter new UNIX username:` が表示されたら、小文字と数字のみのユーザー名を入力（例：`myname`）
2. `New password:` が表示されたらパスワードを入力（画面には表示されません）
3. `Retype new password:` に同じパスワードを再入力
4. `Installation successful!` などのメッセージが出れば完了

> このユーザー名とパスワードはUbuntu内でコマンドを実行する際に必要なので、必ず控えておきましょう。

## ステップ5：Ubuntuを最新に更新

```bash
sudo apt update
sudo apt upgrade -y
```
- パスワード入力を求められたら、先ほど設定したUbuntuのパスワードを入力（表示されなくてもOK）
- 更新とアップグレードには5〜10分ほどかかる場合があります

## ステップ6：Node.jsをインストール

Claude CodeにはNode.js 18以上が必要です。nvm（Node Version Manager）を使うと管理が簡単です。

1. nvmインストーラーをダウンロード：
   ```bash
   wget https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh --no-check-certificate
   ```
2. インストーラーを実行：
   ```bash
   cat install.sh | bash
   ```
3. 現在のシェルにnvmを読み込む：
   ```bash
   \. "$HOME/.nvm/nvm.sh"
   ```
4. Node.js 24をインストール：
   ```bash
   nvm install 24
   ```
5. 動作確認：
   ```bash
   node --version
   ```
   `v24.x.x` と表示されれば成功です

## ステップ7：Claude Codeをインストール

```bash
curl -fsSL https://claude.ai/install.sh | bash
claude --version
```
- 2〜5分で完了します。黄色や赤の警告は情報表示である場合がほとんどです。
- `claude --version` でバージョン番号が表示されればOKです。

## ステップ8：Anthropic APIに接続

### オプションA：Claude Pro/Maxサブスクリプションを使う

```bash
claude
```
- Claudeがブラウザを自動で開こうとします。開かない場合は、ターミナルに表示された長いURLを **Ctrl + クリック** するかコピーしてブラウザに貼り付けます。
- Claude.aiにログインし、**Authorize** をクリック
- 表示されたコードで **Copy Code** をクリックし、ターミナルに戻って右クリック > **貼り付け**（または **Ctrl + Shift + V**）
- 成功メッセージが出れば接続完了です。

### オプションB：Anthropic APIキーを使う

1. [Anthropic Console](https://console.anthropic.com/) でAPIキーを取得
2. Ubuntuターミナルで以下を実行（`your-api-key-here`を実際のキーに置き換え）：
   ```bash
   export ANTHROPIC_API_KEY="your-api-key-here"
   ```
3. 毎回設定したくない場合は、`~/.bashrc` に追記：
   ```bash
   echo 'export ANTHROPIC_API_KEY="your-api-key-here"' >> ~/.bashrc
   ```
4. ターミナルを閉じて再起動すると設定が反映され、Claude CodeがAPIキーを自動で読み込みます。

> **重要：** Claude Pro/Maxサブスクリプションを使っている場合は `ANTHROPIC_API_KEY` を設定しないでください。サブスクリプションの利用枠が優先され、予期しないAPI課金を避けられます。

### オプションC：Azure（Microsoft Foundry）経由でAnthropic APIを使う

AzureでAnthropicモデルを使っている場合は、以下の環境変数を設定します：
```
# Microsoft Foundry統合を有効化
export CLAUDE_CODE_USE_FOUNDRY=1
# Azureリソース名（例: myfoundry-eastus2）
export ANTHROPIC_FOUNDRY_RESOURCE=xxx-eastus2
# リソースにデプロイしたモデル名
export ANTHROPIC_DEFAULT_OPUS_MODEL=claude-opus-4-5
export ANTHROPIC_DEFAULT_SONNET_MODEL=claude-sonnet-4-5
export ANTHROPIC_FOUNDRY_API_KEY=your_full_api_key
```
`xxx-eastus2` と `your_full_api_key` をAzureポータルの値で置き換えてください。

## ステップ9：Claude Codeを試してみる

```bash
claude
```
- 動作確認として「量子コンピューティングについて説明して」などの質問を投げてみましょう。

## ステップ10：Windows側のプロジェクトで作業する

```bash
cd /mnt/c/Users/YourUserName/Documents/YourProject
claude
```
- `YourUserName` と `YourProject` を自分の環境に合わせて置き換えます。
- Windows上のファイルでも、`/mnt/c/...` 経由で開けばUbuntuから直接編集できます。
- まずは「このコードベースの概要を教えて」と聞き、状況を把握しましょう。その後、変更の依頼やテストを繰り返します。

## Ubuntuターミナルを再度開くには

1. Windowsスタートボタンをクリック
2. `Ubuntu` と入力
3. オレンジ色のアイコンの **Ubuntu** アプリをクリック
4. これで新しいUbuntuターミナルが開きます

## トラブルシューティング

### 「Please enable the Virtual Machine Platform ...」と表示される
- 仮想化が無効です。ステップ1の手順に従ってBIOSで有効にしてから再度 `wsl --install` を実行してください。

### `wsl --install` が失敗する
- PowerShellを管理者権限で開いているか確認
- Windows 10 バージョン2004以降／Windows 11であるか確認
- `wsl --update` を先に実行し、その後 `wsl --install` を再実行

### 再起動後にUbuntuが自動で開かない
- スタートメニューで `Ubuntu` を検索し、アプリを手動で起動してください

### `sudo: apt: command not found`
- WSLが壊れている可能性があります。
  ```powershell
  wsl --unregister Ubuntu
  wsl --install
  ```
  を管理者PowerShellで再実行します。

### Node.jsのインストールに失敗する
- 先に `sudo apt update` を実行したか確認
- コマンドを入力し直し、タイポがないかチェック

### Claude Codeコマンドが見つからない
- インストール完了メッセージが出たか確認
- Ubuntuターミナルを閉じて再起動
- もう一度 `curl -fsSL https://claude.ai/install.sh | bash` を実行

## サポートリソース

- WSL全般：[Microsoft WSLドキュメント](https://docs.microsoft.com/en-us/windows/wsl/)
- Claude Code全般：[Claude Code GitHub](https://github.com/anthropics/claude-code)
