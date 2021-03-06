# TacOS
Tokuyama advanced educational computer's Operating System
---

TacOSは徳山高専で開発した教育用のオペレーティングシステムです。
受講者にソースコードを読んでもらうことを第１の目的にしています。
ソースコードとして読めるだけでなく実機で動作する
本物のオペレーティングシステムでもあります。

## 動作環境
TacOSはTaC(Tokuyama Advanced Educational Computer)と
呼ばれる実機上で動作します。
TaCはFPGA(Xilinx Spartan-6)に組み込まれた原始的なパーソナルコンピュータです。
USBまたはBlutooth経由のシリアル接続で端末を接続し，
ハードディスク代わりのマイクロSDカードを準備することで
1980年代前半の8bitパソコン程度（？）の能力を発揮します。
詳しくは，[TeC7のマニュアル](https://github.com/tctsigemura/TeC7/raw/master/Manual/manual.pdf)
をご参照下さい．

TaCのCPUは、49MHzで動作する、
メモリ空間64KiBのオリジナル16bitCPUです。
8bit版のTeCとアセンブリ言語レベルではそっくりになっているので、
TeCで機械語の勉強をした人はすぐに理解することが可能です。

TaCはマイクロSDカードにインストールしたTacOSをブートすることが可能です。

### TaCの入手
TaCは[竹上電気商会](http://www.e-takegami.jp/)で
販売しているTeC7の16bitモードのことです。
TeC7に
[最新の設計データ](https://github.com/tctsigemura/TeC7)
を書き込む必要があります。

### TaCの設計図
VHDLで記述されたTaCの設計図（？）は、
[tctsigemura/TeC7](https://github.com/tctsigemura/TeC7)で公開しています。

## できること
### オペレーティングシステムの勉強
公開中のOSの教科書
（[オペレーティングシステム](https://github.com/tctsigemura/OSTextBook)）
の中で、TacOSのソースコードが実装例として参照されています。

### ソースコードの勉強
TacOSのソースコードを読んで勉強することができます。
TacOSは、
マイクロカーネル方式の読みやすい構造を持っています。
TacOSは、
[C--言語](https://github.com/tctsigemura/C--)で
記述されています。
ビルドするとメモリマップがファイルに出力されます。
TaCのコンソールパネルからブレークポイントを設定したり、
ステップ実行させたりしながらOSの内部をトレースできます。

### アプリケーションの実行
TacOSのアプリケーションプログラムは
[C--言語](https://github.com/tctsigemura/C--)で記述します。
C--言語の開発環境はMacやLinuxで動作します。
C--言語で記述したアプリケーションは、
FAT16マイクロSDカードに書き込んでTaCで実行することができます。

### アプリケーションの開発
近い将来、
[C--言語](https://github.com/tctsigemura/C--)の
言語処理系がTacOSに移植される予定です。
移植が完了したら、TaC上でTaCのアプリケーションを開発する
ことが可能になります。

### 組込みアプリケーションの開発
os/app ディレクトリで組み込み用のアプリケーションを開発できます．
LCDとMP3デコーダボードを追加した
TeC7用のMP3プレーヤアプリのサンプルが含まれています．

### ディレクトリ構成

```
+ README.md     このファイル
|
+ os  +         kernel のソースプログラム
|     |
|     + kernel  マイクロカーネル
|     |
|     + fs      FAT16ファイルシステム・サーバ
|     |
|     + mm      メモリマネージャ・サーバ
|     |
|     + pm      プロセスマネージャ・サーバ
|     |
|     + tty     ターミナル
|     |
|     + sio     シリアル入出力・ドライバ
|     |
|     + app     組込版のアプリの例（簡単なmp3プレーヤ）
|     |
|     + util    C--スタートアップとユーティリティルーチン
|
+ usr +         TacOS上で実行されるユーティリティのソースプログラム
|     |
|     + ar      アーカイバ
|     |
|     + cat     テキストファイル表示
|     |
|     + cp      ファイルコピー
|     |
|     + dump    ファイルの16進ダンプ表示
|     |
|     + echo    コマンド行引数を表示
|     |
|     + edit    テキストエディタ（ラインエディタ）
|     |
|     + env     環境変数の表示と環境変数を操作した上でコマンド実行
|     |
|     + fsize   ファイルサイズを表示
|     |
|     + head    テキストファイルの先頭だけ表示
|     |
|     + hello   デモプログラム
|     |
|     + in      I/Oポートを読んで値を表示
|     |
|     + ls      ファイル一覧
|     |
|     + mkdir   ディレクトリ作成
|     |
|     + mv      ファイルの移動
|     |
|     + out     I/Oポートに値を書き込む
|     |
|     + printenv 環境変数の表示
|     |
|     + pwd     カレントディレクトリの表示
|     |
|     + rm      ファイルを削除
|     |
|     + rmdir   ディレクトリを削除
|     |
|     + shell   コマンドインタプリタ
|     |
|     + spitest オプションのLCD・MP3デコーダボードの動作テスト
|     |
|     + sr      シリアルからファイル受信（TaC側）
|     |
|     + ss      シリアルにファイル送信（PC側）
|     |
|     + touch   ファイルを作成
|     |
|     + ...
|
+ uSD +         TacOSのインストールイメージ（マイクロSDに書き込む内容）
      |
      + kernel.bin  汎用版のカーネル
      |
      + kernel0.bin 組込版のカーネル（アプリがリンクされている）
      |
      + bin     ユーティリティの実行形式を格納したディレクリ
```
