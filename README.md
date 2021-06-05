# VRMNXファイル連携システム

## 概要
「VRMNXファイル連携システム」（VRMNX File linkege System：VRMNX FLS）は「[鉄道模型シミュレーターNX](http://www.imagic.co.jp/hobby/products/vrmnx/ "鉄道模型シミュレーターNX")」（VRMNX）のビュワーオブジェクトを外部から制御するためのシステムです。  
タイマーイベント(既定は0.1秒毎)でレイアウトファイルと同階層にある「read」フォルダ内のファイルを読み込み、テキストで記述されている命令をVRMNXで実行します。

![vrmnxfls-about](https://user-images.githubusercontent.com/66538961/107119739-e9334300-68cc-11eb-8f29-7ed26ccc383b.png)

## ダウンロード
- [vrmnxfls.py](https://raw.githubusercontent.com/CaldiaNX/vrmnxfls/main/vrmnxfls.py)

## 利用方法
レイアウトファイルと同じフォルダ階層に「vrmnxfls.py」ファイルと「read」「read_end」フォルダを配置します。  

フォルダ構成：
```
C:\VRMNX（一例）
├ \read
├ \read_end
├ \send (任意) 起動時 レイアウト情報 出力用
├ vrmnxfls.py
└ VRMNXレイアウトファイル.vrmnx
```

対象レイアウトのレイアウトスクリプトに以下の★内容を追記します。  

```py
#LAYOUT
import vrmapi
import vrmnxfls # ★インポート

def vrmevent(obj,ev,param):
    vrmnxfls.vrmevent(obj,ev,param) # ★メイン処理
    if ev == 'init':
        dummy = 1
    elif ev == 'broadcast':
        dummy = 1
    elif ev == 'timer':
        dummy = 1
    elif ev == 'time':
        dummy = 1
    elif ev == 'after':
        dummy = 1
    elif ev == 'frame':
        dummy = 1
    elif ev == 'keydown':
        dummy = 1
```

ファイル読み込みに成功すると、ビューワー起動時のスクリプトログに

```
load VRMNXファイル連携システム Ver.x.x
```

が表示されます。  

## 動作内容
「read」フォルダにシステム仕様に準拠した命令の記述されたテキストファイルを置くことで、ビュワーを操作します。  
読み込んだファイルは「read_end」フォルダへ移動します。  
対応命令は下記のリファレンスを参照ください。

## 関連資料
- [VRMNXファイル連携システム リファレンス](REFERENCE.md)
- [VRMNXネットワークコントローラー](vrmnxflsNetController.md)
- [VRMNXネットワークコントローラー対応レイアウト](vrmnxflsSampleLayout.md)

## 履歴
- 2021/06/05 v1.6
  - 呼び出し方法を変更。※既存レイアウトは修正が必要
  - 細部の記述を修正
- 2020/11/14 v1.5
  - 複数分岐操作で負数の場合に逆方向とする機能を追加
- 2020/10/24 v1.4
  - 編成の電源を制御する「setPower」「setPowerAll」追加
- 2020/09/27 v1.3
  - アンダーバー区切りによるポイント一括設定に対応
- 2020/09/23 v1.2
  - レイアウト情報出力「sendSettingFile」追加
- 2020/09/14 v1.1
  - 方向転換「Turn」命令追加
- 2019/12/29 v1.0
  - 公開

## 本システムを使って実現したいこと
- VRMNXとは異なるプログラムでの運転盤や自動運転システムとの連携
- DCCコントローラを使った運転（シリアル通信・命令変換）
- レイアウト同士を連携させた疑似オンライン運転会

## 今後の実装予定
- VRMNX側からの出力対応
- 命令チェックとエラー制御
- 対象オブジェクト・命令セットの拡充
- イベントドリブン（SetEvent～）の追加
