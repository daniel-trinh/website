---
out: Running.html
---

  [Hello]: Hello.html
  [Setup]: Setup.html
  [Triggered-Execution]: ../../docs/Triggered-Execution.html
  [Command-Line-Reference]: ../../docs/Command-Line-Reference.html

実行
----

このページではプロジェクトをセットアップした後の `sbt` の使い方を説明する。
君が[sbt をインストール][Setup]して、[Hello, World][Hello]か他のプロジェクトを作ったことを前提とする。

### インタラクティブモード

プロジェクトのベースディレクトリで、sbt を引数なしで実行する:

```
\$ sbt
```

sbt をコマンドライン引数なしで実行するとインタラクティブモードで起動する。
インタラクティブモードにはコマンドプロンプト（とタブ補完と履歴も！）がある。

例えば、`compile` と sbt プロンプトに入力する:

```
> compile
```

もう一度 `compile` するには、上矢印を押して、エンターキーを押す。

君のプログラムを実行するには、`run` と入力する。

インタラクティブモードを終了するには、`exit` と入力するか、Ctrl+D (Unix) か Ctrl+Z (Windows) を押す。

### バッチモード

sbt のコマンドを空白で区切られたリストとして引数に指定すると sbt をバッチモードで実行することができる。
引数を取る sbt コマンドの場合は、コマンドと引数の両方を引用符で囲むことで一つの引数として `sbt` に渡す。
例えば、

```
\$ sbt clean compile "testOnly TestA TestB"
```

この例では、`testOnly` は `TestA` と `TestB` の二つの引数を取る。
コマンドは順に実行される（この場合 `clean`、`compile`、そして `testOnly`）。

### 継続的ビルドとテスト

編集〜コンパイル〜テストのサイクルを速めるために、ソースファイルを保存する度
sbt に自動的に再コンパイルを実行させることができる。

ソースファイルが変更されたことを検知してコマンドを実行するには、コマンドの先頭に `~` をつける。
例えば、インタラクティブモードで、これを試してみよう:

```
> ~ compile
```

このファイル変更監視状態を止めるにはエンターキーを押す。

先頭の `~` はインタラクティブモードでもバッチモードでも使うことができる。

詳しくは、[Triggered Execution][Triggered-Execution] 参照。

### よく使われるコマンド

最もよく使われる sbt コマンドを紹介する。全ての一覧は [Command Line Reference][Command-Line-Reference] を参照。

<table>
  <tr>
    <td><tt>clean</tt></td>
    <td>（<tt>target</tt> ディレクトリにある）全ての生成されたファイルを削除する。</td>
  </tr>
  <tr>
    <td><tt>compile</tt></td>
    <td>
    （<tt>src/main/scala</tt> と <tt>src/main/java</tt> ディレクトリにある）
    メインのソースをコンパイルする。</td>
  </tr>
  <tr>
    <td><tt>test</tt></td>
    <td>全てのテストをコンパイルし実行する。</td>
  </tr>
  <tr>
    <td><tt>console</tt></td>
    <td>コンパイル済のソースと依存ライブラリにクラスパスを通して、Scala インタプリタを開始する。
  sbt に戻るには、<tt>:quit</tt> と入力するか、Ctrl+D (Unix) か Ctrl+Z (Windows) を押す。</td>
  </tr>
  <tr>
    <td><nobr><tt>run &lt;argument&gt;*</tt></nobr></td>
    <td><tt>sbt</tt> と同じ仮想マシン上で、プロジェクトのメインクラスを実行する。</td>
  </tr>
  <tr>
    <td><tt>package</tt></td>
    <td><tt>src/main/resources</tt> 内のファイルと <tt>src/main/scala</tt> と
    <tt>src/main/java</tt>
    からコンパイルされたクラスファイルを含む jar を作る。</td>
  </tr>
  <tr>
    <td><tt>help &lt;command&gt;</tt></td>
    <td>指定されたコマンドの詳細なヘルプを表示する。コマンドが指定されていない場合は、
  全てのコマンドの簡単な説明を表示する。</td>
  </tr>
  <tr>
    <td><tt>reload</tt></td>
    <td>ビルド定義（<tt>build.sbt</tt>、 <tt>project/*.scala</tt>、
    <tt>project/*.sbt</tt> ファイル）を再読み込みする。
  ビルド定義を変更した場合に必要。</td>
  </tr>
</table>

### タブ補完

インタラクティブモードには、空のプロンプトの状態を含め、タブ補完がある。
sbt の特殊な慣例として、タブを一度押すとよく使われる候補だけが表示され、
複数回押すと、より多くの冗長な候補一覧が表示される。

### 履歴コマンド

インタラクティブモードは、 sbt を終了して再起動した後でも履歴を覚えている。
履歴にアクセスする最も簡単な方法は矢印キーを使うことだ。以下のコマンドも使うことができる:

<table>
  <tr>
    <td><tt>!</tt></td>
    <td>履歴コマンドのヘルプを表示する。</td>
  </tr>
  <tr>
    <td><tt>!!</tt></td>
    <td>直前のコマンドを再実行する。</td>
  </tr>
  <tr>
    <td><tt>!:</tt></td>
    <td>全てのコマンド履歴を表示する。</td>
  </tr>  
  <tr>
    <td><tt>!:n</tt></td>
    <td>最後の <tt>n</tt> コマンドを表示する。</td>
  </tr>
  <tr>
    <td><tt>!n</tt></td>
    <td><tt>!:</tt> で表示されたインデックス <tt>n</tt> のコマンドを実行する。</td>
  </tr>
  <tr>
    <td><tt>!-n</tt></td>
    <td><tt>n</tt>個前のコマンドを実行する。</td>
  </tr>
  <tr>
    <td><tt>!string</tt></td>
    <td>'string' から始まる最近のコマンドを実行する。</td>
  </tr>
  <tr>
    <td><tt>!?string</tt></td>
    <td>'string' を含む最近のコマンドを実行する。</td>
  </tr>
</table>
