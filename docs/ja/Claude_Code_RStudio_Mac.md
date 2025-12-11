[ホーム](./)

# MacでRStudioとClaude Codeを使用する

MacにRStudioがR コードの実行用に、Claude CodeがAI搭載のコーディング支援用にインストールされています。このチュートリアルでは、同じプロジェクトファイルで両方のツールを一緒に使用する方法を説明します。Rプロジェクトを作成し、手動でコードを書いた後、ターミナルからClaude Codeを使用して可視化と分析を追加します。その間、RStudioを開いたままコードを実行してテストできます。

## 主要な概念

- **ターミナル** - Claude Codeが実行されるMacのコマンドラインインターフェース
- **共有ファイル** - RStudioとClaude Codeの両方がDocumentsフォルダ内の同じファイルで作業
- **ハイブリッドワークフロー** - RStudioがコードを実行し、Claude Codeがコードを書いて改善

## 必要なもの

- [MacにClaude Codeをインストール](./Install_Claude_Code_MacOS.md)ガイドの完了
- MacにインストールされたRStudio
- 20〜30分

## ステップ1: MacでRStudioを開く

- DockにあるLaunchpad（ドットのグリッドアイコン）をクリック
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
- **Open**をクリック
- **Create Project**をクリック
- RStudioがプロジェクトを作成して切り替えます

## ステップ3: 新しいRスクリプトを作成

- RStudioで、**File > New File > R Script**をクリック
- 左上のペインに新しい空のスクリプトが開きます
- **File > Save**をクリック（または**Command (⌘) + S**を押す）
- ファイル名を`iris.R`にする
- **Save**をクリック

## ステップ4: 手動で初期コードを書く

`iris.R`ファイルに次のコードを入力します:

```r
data(iris)
str(iris)
summary(iris)
```

- **File > Save**をクリックして変更を保存（または**Command (⌘) + S**を押す）
- コードを実行するには、すべての行を強調表示してから、スクリプトペインの右上にある**Run**ボタンをクリック
- Consoleペインにデータセットの構造と統計情報が表示されます

## ステップ5: ターミナルを開く

- キーボードで**Command (⌘) + Space**を押す
- 検索ボックスに`Terminal`と入力
- **Terminal**（黒い四角のアイコン）をクリック
- ターミナルウィンドウが開きます

## ステップ6: プロジェクトフォルダに移動

- ターミナルで、次のコマンドを入力:
  ```
  cd ~/Documents/test_claude
  ```
- 正しい場所にいることを確認するために入力:
  ```
  ls
  ```
- `iris.R`と`test_claude.Rproj`がリストされているはずです

**ヒント:** 正確なパスがわからない場合は、Finderからターミナルにフォルダをドラッグアンドドロップすると、フルパスが自動的に表示されます!

## ステップ7: Claude Codeを起動

- ターミナルで入力:
  ```
  claude
  ```
- Claude Codeが起動してウェルカムメッセージが表示されます
- 初回セッションの場合は認証が必要になる場合があります
- これでRプロジェクトのAI支援を使用する準備ができました

## ステップ8: Claudeに散布図を依頼

Claude Codeが遅い、または応答しない場合は、初期化されるまで待ちます。次に、このリクエストを入力します:

```
Add code to iris.R to create a scatter plot of sepal length vs. width, colored by species. Use ggplot2.
```
- Claude Codeが`iris.R`ファイルを読み取り、可視化コードを追加します
- 尋ねられたら、適切なオプションを選択してClaudeにiris.Rファイルの編集を許可します
- Claudeが完了するまで待ちます（確認メッセージが表示されます）


## ステップ9: RStudioで新しいコードを実行

- RStudioに戻る（RStudioウィンドウをクリックするか、**Command (⌘) + Tab**を押す）
- ファイルが変更されたというプロンプトが表示される場合があります - **Yes**をクリックして再読み込み
- プロンプトが表示されない場合は、**File > Reopen with Encoding > UTF-8**をクリック
- すべてのコードを強調表示して**Run**をクリック
- 右下の**Plots**ペインに散布図が表示されます
- ggplot2に関するエラーが出た場合は、Consoleペインで`install.packages("ggplot2")`と入力してインストール

## ステップ10: 散布図を改良

- ターミナルに切り替える（**Command (⌘) + Tab**を押すか、ターミナルウィンドウをクリック）
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

- ターミナルに切り替える
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

- ターミナルに切り替える
- 次のリクエストを入力:
  ```
  Review the entire script for correctness. Add comments when necessary.
  ```
- Claudeがコードをレビューし、包括的なコメントを追加します

## ステップ15: ClaudeにR Markdownの作成を依頼

- ターミナルに切り替える
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

- **RStudioでファイルの変更が表示されない** - **File > Reopen with Encoding > UTF-8**をクリックして手動でファイルを再読み込みするか、ファイルを閉じて再度開きます。
- **「claude: command not found」** - [インストールガイド](./Install_Claude_Code_MacOS.md)を完了したことを確認してください。新しいターミナルウィンドウを開いてみるか、ターミナルを完全に閉じて（**Command (⌘) + Q**）再度開きます。
- **プロットが表示されない** - ggplot2がインストールされていることを確認してください。必要に応じてRStudio Consoleで`install.packages("ggplot2")`を実行します。
- **「No such file or directory」** - ステップ6でパスを正しく入力したか確認してください。ドラッグアンドドロップのトリックを試してください: `cd `（スペース付き）と入力した後、Finderからターミナルにtest_claudeフォルダをドラッグします。
- **Claude Codeが最初のリクエストで遅い** - Claudeの初期化に30〜60秒待ちます。その後のリクエストは速くなります。

## Macキーボードショートカット

アプリ間の切り替えに便利なショートカット:
- **Command (⌘) + Tab** - 開いているアプリケーション間を素早く切り替え
- **Command (⌘) + `**（バッククォート） - 同じアプリケーションのウィンドウ間を切り替え
- **Command (⌘) + Space** - Spotlight検索を開く（アプリを開くため）
- **Command (⌘) + Q** - アプリケーションを完全に終了

## 次のステップ

- Claudeに統計検定（t検定、ANOVA）を分析に追加するよう依頼してみる
- Claudeにこのコードの**Pythonバージョン**を取得してQuartoドキュメントを準備するよう依頼
- ClaudeにRスクリプトの繰り返しタスク用の関数を作成するよう依頼
- Rコードが実行されないときにエラーメッセージをデバッグするためにClaudeを使用
- 遅いRコードのパフォーマンスを向上させるためにClaudeに最適化を依頼

## ワークフローの概要

このハイブリッドセットアップは、両方の世界のベストを組み合わせます:

- **RStudio（Mac）** - インタラクティブなRコンソール、即座のプロット表示、コード実行のための使い慣れたGUI
- **Claude Code（ターミナル）** - AI搭載のコード生成、レビュー、改善
- **共有ファイル** - 両方のツールがDocumentsフォルダ内の同じファイルで作業
- **反復的な改良** - 手動コードから始め、Claudeで強化し、RStudioでテストし、さらに改良
- **ドキュメント** - Claudeは分析のための包括的なレポートとコメントを生成できます

ワークフローはシンプルです: ターミナルでClaudeを使ってコードを書くか編集し、すぐにRStudioでテストして実行します。ファイルのコピーや手動同期は不要で、両方のアプリケーションがMac上で同じファイルにシームレスにアクセスします。

---

2024年12月11日に[Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/)によって作成されました。
