[ホーム](./)

# WindowsでWSLとRStudioを使ってClaude Codeを使用する

WindowsにRコード実行用のRStudioと、AI搭載のコーディング支援用のWSL内のClaude Codeがあります。このチュートリアルでは、同じプロジェクトファイルで両方のツールを一緒に使用する方法を説明します。Windowsでプロジェクトを作成し、手動でコードを書いた後、UbuntuターミナルからClaude Codeを使用して可視化と分析を追加します。その間、RStudioを開いたままコードを実行してテストできます。

## 主要な概念

- **WSL（Windows Subsystem for Linux）** - Windows内でUbuntu Linuxを実行し、Claude Codeがインストールされています
- **ファイルパス変換** - `C:\Users\YourName\Documents`のようなWindowsパスは、WSLでは`/mnt/c/Users/YourName/Documents`になります
- **ハイブリッドワークフロー** - RStudio（Windows）がコードを実行し、Claude Code（WSL）がコードを書いて改善

## 必要なもの

- [WindowsにClaude Codeをインストール](./Install_CLAUDE_Code_Win.md)ガイドの完了
- WindowsにインストールされたRStudio
- 20〜30分

## ステップ1: WindowsでRStudioを開く

- **Windowsスタートボタン**をクリック
- 検索ボックスに`RStudio`と入力
- **RStudio**をクリックして開く
- RStudioウィンドウが複数のペインで開きます

## ステップ2: 新しいRプロジェクトを作成

- RStudioで、トップメニューから**File**をクリック
- **New Project...**をクリック
- **New Directory**を選択
- **New Project**を選択
- **Directory name**に`test_claude`と入力
- 「Create project as subdirectory of:」の横にある**Browse**をクリック
- **Documents**フォルダに移動
- **Select Folder**をクリック
- **Create Project**をクリック
- RStudioがプロジェクトを作成して切り替えます

## ステップ3: 新しいRスクリプトを作成

- RStudioで、**File > New File > R Script**をクリック
- 左上のペインに新しい空のスクリプトが開きます
- **File > Save**をクリック（または保存アイコン）
- ファイル名を`iris.R`にする
- **Save**をクリック

## ステップ4: 手動で初期コードを書く

`iris.R`ファイルに次のコードを入力します:

```r
data(iris)
str(iris)
summary(iris)
```

- **File > Save**をクリックして変更を保存
- コードを実行するには、すべての行を強調表示してから、スクリプトペインの右上にある**Run**ボタンをクリック
- Consoleペインにデータセットの構造と統計情報が表示されます

## ステップ5: Ubuntuターミナルを開く

- **Windowsスタートボタン**をクリック
- 検索ボックスに`Ubuntu`と入力
- **Ubuntu**（オレンジ色の円形アイコン）をクリック
- Ubuntuターミナルが開きます

## ステップ6: プロジェクトフォルダに移動

- Ubuntuターミナルで、次のコマンドを入力（`YourUsername`を実際のWindowsユーザー名に置き換えてください）:
  ```
  cd /mnt/c/Users/YourUsername/Documents/test_claude
  ```
- ユーザー名を見つけるには、`ls /mnt/c/Users/`と入力してフォルダ名を探します
- 正しい場所にいることを確認するために入力:
  ```
  ls
  ```
- `iris.R`と`test_claude.Rproj`がリストされているはずです

## ステップ7: Claude Codeを起動

- Ubuntuターミナルで入力:
  ```
  claude
  ```
- Claude Codeが起動してウェルカムメッセージが表示されます
- 再度ログインが必要な場合があります。前のチュートリアルを参照してください。
- これでRプロジェクトのAI支援を使用する準備ができました

## ステップ8: Claudeに散布図を依頼

Claude Codeが遅い、または応答しない場合は、初期化されるまで待ちます。次に、このリクエストを入力します:

```
Add code to iris.R to create a scatter plot of sepal length vs. width, colored by species. Use ggplot2.
```
- Claude Codeが`iris.R`ファイルを読み取り、可視化コードを追加します
- 尋ねられたら、2を選択してClaudeにiris.Rファイルの編集を許可します
- Claudeが完了するまで待ちます（確認メッセージが表示されます）


## ステップ9: RStudioで新しいコードを実行

- RStudioに戻る（RStudioウィンドウをクリック）
- ファイルが変更されたというプロンプトが表示される場合があります - **Yes**をクリックして再読み込み
- プロンプトが表示されない場合は、**File > Reopen with Encoding > UTF-8**をクリック
- すべてのコードを強調表示して**Run**をクリック
- 右下の**Plots**ペインに散布図が表示されます
- ggplot2に関するエラーが出た場合は、Consoleペインで`install.packages("ggplot2")`と入力してインストール

## ステップ10: 散布図を改良

- Ubuntuターミナルに切り替える
- 次のリクエストを入力:
  ```
  Remove title. Change marker type by species. Change to the classic theme.
  ```

## ステップ11: 改良されたプロットを表示

- RStudioに切り替える
- プロンプトが表示されたらファイルを再読み込み
- 更新されたコードを強調表示して**Run**をクリック
- プロットは現在、タイトルなしで表示され、種ごとに異なるマーカー形状があり、クラシックテーマを使用しているはずです


## ステップ12: ClaudeにPCAプロットを依頼

- Ubuntuターミナルに切り替える
- 次のリクエストを入力:
  ```
  Add code to perform PCA on the numeric variables and plot the samples using the first two principal components.
  ```

## ステップ13: PCA分析を実行

- RStudioに切り替える
- プロンプトが表示されたらファイルを再読み込み
- すべてのコードを強調表示して**Run**をクリック
- PC1とPC2に投影されたサンプルを示すPCAプロットが表示され、種ごとに色分けされます

## ステップ14: Claudeにレビューとコメントを依頼

- Ubuntuターミナルに切り替える
- 次のリクエストを入力:
  ```
  Review the entire script for correctness. Add comments when necessary.
  ```
- Claudeがコードをレビューし、包括的なコメントを追加します

## ステップ15: ClaudeにR Markdownの作成を依頼

- Ubuntuターミナルに切り替える
- 次のリクエストを入力:
  ```
  Create a new R Markdown file for this analysis. Save as iris_report.Rmd
  ```
- Claudeがこのファイルの作成許可を求めます
- Claudeがプロジェクトフォルダに新しい`.Rmd`ファイルを作成します


## ステップ16: R Markdownファイルをニット

- RStudioに切り替える
- **File > Open File...**をクリック
- `iris_report.Rmd`を選択して**Open**をクリック
- スクリプトペインの上部にある**Knit**ボタン（毛糸玉のアイコン）をクリック
- RStudioがHTMLレポートを生成します
- 完全な分析とナラティブテキストを示すレポートが新しいウィンドウで開きます
- HTMLファイルはプロジェクトフォルダに保存されます

## トラブルシューティング

- **WSLからWindowsファイルにアクセスする際の「Permission denied」** - `C:/`ではなく`/mnt/c/`を使用していることを確認してください。パス内のユーザー名が正しいか確認してください。
- **RStudioでファイルの変更が表示されない** - **File > Reopen with Encoding > UTF-8**をクリックして手動でファイルを再読み込みします。
- **「claude: command not found」** - インストールガイドを完了したことを確認してください。新しいUbuntuターミナルウィンドウを開いてみてください。
- **プロットが表示されない** - ggplot2がインストールされていることを確認してください。必要に応じてRStudio Consoleで`install.packages("ggplot2")`を実行します。
- **エラー: 「cannot change working directory」** - Windowsパスにスペースが含まれています。ステップ6で、パスを引用符で囲みます: `cd "/mnt/c/Users/Your Name/Documents/test_claude"`
- **Claude Codeが最初のリクエストで遅い** - Claudeの初期化に30〜60秒待ちます。その後のリクエストは速くなります。

## 次のステップ

- Claudeに統計検定（t検定、ANOVA）を分析に追加するよう依頼してみる
- Claudeにこのコードの**Pythonバージョン**を取得してQuartoドキュメントを準備するよう依頼
- ClaudeにRスクリプトの繰り返しタスク用の関数を作成するよう依頼
- Rコードが実行されないときにエラーメッセージをデバッグするためにClaudeを使用
- 遅いRコードのパフォーマンスを向上させるためにClaudeに最適化を依頼

## ワークフローの概要

このハイブリッドセットアップは、両方の世界のベストを組み合わせます:

- **RStudio（Windows）** - インタラクティブなRコンソール、即座のプロット表示、コード実行のための使い慣れたGUI
- **Claude Code（WSL）** - AI搭載のコード生成、レビュー、改善
- **共有ファイル** - 両方のツールがWSLの`/mnt/c/`マウントポイントを通じて同じファイルで作業
- **反復的な改良** - 手動コードから始め、Claudeで強化し、RStudioでテストし、さらに改良
- **ドキュメント** - Claudeは分析のための包括的なレポートとコメントを生成できます

ワークフローはシンプルです: UbuntuターミナルでClaudeを使ってコードを書くか編集し、すぐにRStudioでテストして実行します。ファイルのコピーや手動同期は不要で、WSLとWindowsはシームレスに同じファイルを共有します。

---

2024年12月11日に[Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/)によって作成されました。
