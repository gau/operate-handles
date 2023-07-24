# README

パスオブジェクトのハンドルを操作するIllustratorのスクリプト（jsx）です。図入りの詳しい説明は[noteの記事](https://note.com/gautt/n/nc5094a367dc5)をご覧ください

## 更新履歴

- **0.5.13：テキストフレーム取得時にエラーが出るのを修正**
- 0.5.12：複合パス、テキストパスに対応
- 0.5.11：対象オブジェクトやポイントが多い場合の警告にて、選択したボタンと逆の挙動になっていたのを修正
- 0.5.10：option（Alt）キーを押しながら実行したときの設定項目を、［角度：0°］、［距離：100％］、オプション［既存のハンドルのみ操作］のみオンに変更
- 0.5.9：option（Alt）キーを押しながら実行したとき設定項目を初期値にする機能を実装
- 0.5.8：スクリプト名と一部の内部処理を変更
- 0.5.7：既存のハンドルの長さが0のとき元の位置に戻ってしまう不具合を修正／オプションの表現を変更
- 0.5.6：未選択で実行したときのレイヤー取得エラーを修正
- 0.5.5：オプションの表現を変更
- 0.5.4：既存のハンドルを変更しないオプション選択時は既存のハンドルを破棄して新規に置き換えオプションを無効
- 0.5.3：既存のハンドルを変更しないオプションを追加
- 0.5.2：上下キーでテキストフィールドの数値の増減に対応
- 0.5.1：対象オブジェクトや対象ポイントが多すぎるときに警告を表示するように変更
- 0.5.0：新規作成

## 検証バージョン

* Illustrator 2019〜2023

## インストール方法

1. ダウンロードしたファイルを解凍します。
2. 所定の場所に「数値でハンドルを操作する.jsx」をコピーします。Windows版ではお使いのIllustratorの種類によって保存する場所が異なりますのでご注意ください。
3. Illustratorを再起動します。
4. `ファイル > スクリプト > 数値でハンドルを操作する`と表示されていればインストール成功です。

#### ファイルをコピーする場所

| OS | バージョン | フォルダの場所 |
|:-----|:-----|:-----|
| Mac | 全 | /Applications/Adobe Illustrator *(ver)*/Presets/ja_JP/スクリプト/ |
| 32bit Win | CS5まで | C:\Program Files\Adobe\Adobe Illustrator *(ver)*\Presets\ja_JP\スクリプト\ |
| 64bit Win | CS5, CS6（32bit版） | C:\Program Files (x86)\Adobe\Adobe Illustrator *(ver)*\Presets\ja_JP\スクリプト\ |
| 64bit Win | CS6（64bit版）以降 | C:\Program Files\Adobe\Adobe Illustrator *(ver)* (64 Bit)\Presets\ja_JP\スクリプト\ |

- *(ver)*にはお使いのIllustratorのバージョンが入ります
- 本スクリプトは、2022以前では動作を検証しておりません

## どのようなスクリプトか

選択したアンカーポイントやセグメントのハンドル（方向点／方向線）を数値で動かします。［角度］と［長さ］を数値で指定することで、手動では難しい正確な曲線を作成する助けになります。また、対象のハンドルすべてを連動して動かすことができるため、幾何学的な形を作ることも可能です。

## 使い方

1. 対象となるパスオブジェクトやアンカーポイント、セグメントを選択します。（複数可）
2. `ファイル > スクリプト > 数値でハンドルを操作する`を選択します。
3. ［角度］と［長さ］のスライダーでハンドルを操作します。
4. ［実行］をクリックします。

## 角度について

基準となるアンカーポイントからハンドルの先（方向点）までの角度です。`-180°`〜`180°`までの`360°`を指定できます。

## 角度の基準

### A. ハンドルを新しく作る場合

隣り合うアンカーポイント同士を直線でつないだラインを`0°`とした角度です。つまり、`0°`にすればセグメントは直線になります。

### B. 既存のハンドルを使う場合

もともとのハンドルの角度を`0°`とします。つまり、`0°`にすればもとのハンドルと同じ角度になります。ただし、あとで説明する［[既存のハンドルをすべて新規に置き換え](#既存のハンドルをすべて新規に置き換え)］オプションがオンの場合、既存のハンドルはリセットされるため「A. ハンドルを新しく作る場合」と同じになります。

## 長さについて

基準となるアンカーポイントからハンドルの先（方向点）までの距離を相対的に表す値です。`0％`〜`200％`までを指定できます。

## 長さの基準

### A. ハンドルを新しく作る場合

隣り合うアンカーポイント同士を直線でつないだラインを`100％`とした相対的な長さです。つまり、`0％`にすればハンドルはなくなり、`100％`にすれば隣り合うアンカーポイントまでの距離と等しくなります。

### B. 既存のハンドルを使う場合

もともとのハンドルの長さを`100％`とします。つまり、`0％`にすればハンドルはなくなり、`100％`でもとのハンドルと同じ長さ、`200％`で2倍の長さになります。ただし、あとで説明する［[既存のハンドルをすべて新規に置き換え](#既存のハンドルをすべて新規に置き換え)］オプションがオンの場合、既存のハンドルはリセットされるため「A. ハンドルを新しく作る場合」と同じになります。

## オプションについて

ハンドルの動き方や操作の対象となる範囲を調整するいくつかのオプションを利用できます。少しややこしいので、自分のイメージする操作ができるようにオンオフを切り替えつつ試してみてください。

### 既存のハンドルをすべて新規に置き換え

もともとセグメントにハンドルが存在している場合、すべてのハンドルをリセットして新規に作成しなおします。もともとのハンドルの有無に関わらず、すべての角度と長さを連動させて同じにしたいときオンにします。逆に、もともとのハンドルを基準に操作したいときはオフにします。

### 既存のハンドルのみ操作

実行前に存在しているハンドルだけを対象に操作します。ハンドルが存在しないセグメントに新しくハンドルが追加されることはありません。

### 既存のハンドルを変更しない

実行前に存在しているハンドルは操作の対象から外します。［[既存のハンドルのみ操作](#既存のハンドルのみ操作)］がオフのときのみ有効です。

### 選択されたアンカーポイントのハンドルだけ操作

選択されたアンカーポイント（選択の表示が塗りつぶされたアンカーポイント）から出ているアンカーポイントだけを操作の対象とします。特定のアンカーポイントのハンドルだけを狙って操作したいときオンにします。逆に、選択したセグメントを対象としたい場合はオフにするといいでしょう。

### 隣り合うハンドルの動きを反転

オフの場合は、隣り合うハンドルは鏡写しのように角度が反転されます。この動きを逆にしたいときオンにしましょう。

## 便利機能

- option（Alt）キーを押しながらスクリプトを実行すると、［角度：0°］、［距離：100％］、オプション［既存のハンドルのみ操作］のみオンの状態でダイアログが開きます。既存のハンドルのみを編集したいときはこの状態で開くと分かりやすいです
- 数値フィールドでキーボードの上下キーを押すと、値を1ずつ増減できます

## 注意

- 実行前にドキュメントを保存しておくことをお勧めします
- 必要なオブジェクトが見つからないとき、選択が不適切な場合は処理を中断します
- 複合シェイプには対応していません
- オブジェクトの種類や構造によって意図しない結果になる可能性もゼロではありません

## 免責事項

- このスクリプトを使って起こったいかなる現象についても制作者は責任を負えません。すべて自己責任にてお使いください。
- OSのバージョンやその他の状況によって実行できないことがあるかもしれません。もし動かなかったらごめんなさい。

## ライセンス

- ハンドルを操作する.jsx
- Copyright (c) 2023 Toshiyuki Takahashi
- Released under the MIT license
- [http://opensource.org/licenses/mit-license.php](http://opensource.org/licenses/mit-license.php)
- Created by Toshiyuki Takahashi ([Graphic Arts Unit](http://www.graphicartsunit.com/))
- [Twitter](https://twitter.com/gautt)
