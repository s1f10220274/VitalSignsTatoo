# Vital Signs Tattoo Shader & Prefab

OSC対応、細かくカスタマイズが可能なバイタルタトゥーのシェーダーとprefabのセットです。

OSC送信ツールは付属していませんが、おめが試作制作局様のOSC HeartRateSender
([https://booth.pm/ja/items/3687355](https://booth.pm/ja/items/3687355)) に標準で対応しています。
OSC対応についての詳細は下の方に記載してあります。

---

## 導入方法

既存のメッシュにマテリアルを貼り付けるタイプと
(VitalSignsTattoo_prefab)、
既に平面にセットアップされているためより導入が簡単なタイプ
(VitalSignsTattoo_quad_prefab) があります。
それぞれ導入方法を説明します。

### 既存のメッシュに直接貼り付ける場合

1. 先に最新版のModular Avatarを導入しておいてください。
   [https://modular-avatar.nadena.dev/ja/](https://modular-avatar.nadena.dev/ja/)
2. prefab -> MA Merge Animator -> 相対的パスのルート
   (Relative Path Root) を貼り付け対象
   (顔だったらBodyなど) に変更してください。
   (*Modular Avaterが最新版でないと相対的パスのルートが設定できません。)
3. Tools(ツール)タブのVitalSignsTatooを開き、
   適用したいオブジェクトとサブメッシュを選択して
   Applyを押してください。

**注意**
貼り付け対象のサブメッシュ構造によっては、
意図した部分に貼れない可能性があります。

### 平面をアバターに追従させる場合

1. 先に最新版のModular Avatarを導入しておいてください。
   [https://modular-avatar.nadena.dev/ja/](https://modular-avatar.nadena.dev/ja/)
2. Armature内部の追従させたいボーン直下に置いて、
   位置と大きさを調整してください。

---

## シェーダー設定項目詳細

カスタマイズできるマテリアルの設定項目です。
アニメーションに関する知識があれば動かすこともできます。

* **Language**
  EnglishとJapaneseのみ対応しています。

* **Texture**
  好きな文字や模様をタトゥーにすることが出来ます。
  意図した発色にならない可能性がありますので、
  必ず白のみの透過PNGを入れてください。

* **Main Color**
  下地の色です。

* **Sync Main Color With Light**
  チェックを付けるとMain Colorが無視され、
  全体が光の色と同期します。

* **Light Low**
  BPMがLight Range Min以下の時の光の色です。

* **Light High**
  BPMがLight Range Max以上の時の光の色です。

* **Light Range Min**
  BPMで入力してください。
  心拍数の場合、最も落ち着いている時の数値を入れると
  いい感じになります。

* **Light Range Max**
  BPMで入力してください。
  心拍数の場合、有酸素運動をしている時の数値を入れると
  いい感じになります。

* **Texture Scale**
  テクスチャを「何分割するか」の設定です。
  数値が大きくなるほど小さく表示されることに注意してください。

* **Texture Offset**
  右上隅を基準(X:0,Y:0)としたテクスチャの貼り付け位置です。
  正の値でX:左、Y:下に動きます。

* **Texture Rotation**
  テクスチャの傾きです。

* **BPM**
  BPMを入力する項目です。
  この項目を動的に変更することで速度を変えるアニメーションを
  作ることが出来ます。

* **Light Intensity**
  光の強さです。
  光度を上げると二値に近づきます。

* **Light Frequency**
  光の周波数(光の頻度)です。

* **Wave Amplitude**
  波の振幅(強さ)です。

* **Wave Frequency**
  波の周波数(細かさ)です。
  上げるとより小刻みに波打ちます。

* **Phase Offset**
  波の位相オフセットです。

* **Hide Material**
  マテリアルのオンオフ用の項目です。
  有効にすると完全に透明になって見えなくなります。

---

## OSC対応について

おめが試作制作局様のOSC HeartRateSender
([https://booth.pm/ja/items/3687355](https://booth.pm/ja/items/3687355)) に標準で対応していますが、
Parameterの名前を変更することでお手持ちのOSC送信ツールと
対応させることが可能です。
デフォルトで入っているアニメーションを活用してください。

以下に少しだけ詳しい説明を書きます。

OSC対応は、アニメーションの進行度をFloat値で同期させる
Motiontime方式を採用しています。
デフォルトでは心拍数BPMの0-255を
HeartRateFloat01の0.0-1.0に対応させていますが、
個人の心拍数の範囲やOSC送信ツールによって
カスタマイズしてください。

HeartRateFloat01の名称を
OSC送信ツールから送信されるparameterの名称に変更することで
アニメーションを同期させることが出来ます。

Motiontime方式以外を使用している場合のサポートは出来ませんが、
VitalSignsShaderのBPMやその他の設定項目は
アニメーションから制御することが可能です。
心拍数以外の使用用途(楽曲のBPMと同期など)の場合も、
こちらをアニメーションから制御する形になるかと思います。

---

## FAQ

### Q. どのサブメッシュに貼られたか分からない / 貼ったマテリアルが見つからない

**A.**
Texture Scaleを0.5にすると二倍の大きさになります。
またTexture Offsetは右上隅を基準(X:0,Y:0)とした
テクスチャの貼り付け位置です。
正の値でX:左、Y:下に動きます。

きちんと貼られているか不安な場合は
TestTextureをマテリアルに貼り付けて確認してみてください。
適用されているサブメッシュの部分が真っ白になります。

---

### Q. Expression Menuがない

**A.**
「相対的パスのルート」がちゃんと設定されているか
確認してください。

prefab -> MA Merge Animator ->
相対的パスのルート(Relative Path Root)を
貼り付け対象(顔だったらBodyなど)に変更してください。

該当項目がない場合は最新版でないことが原因です。
最新版のModular Avatarを導入するか、
MAコンポーネントをすべて該当メッシュに移植してください。

---

### Q. 自分でカスタマイズしたテクスチャを使用したい

**A.**
推奨しています。
必ず白のみの透過PNGを使用し、
インポート設定のm_AlphaIsTransparencyをオンにしてください。

白以外がテクスチャ内にある場合、
意図した発色にならない可能性があります。

---

## 使用素材・ツール

* **使用フォント**
  ふゆいろスクリプト(きんいろ書体シリーズ)
  [http://getsuren.com/kiniro_series.html](http://getsuren.com/kiniro_series.html)

* **補助ツール**
  Modular Avatar
  [https://modular-avatar.nadena.dev/ja/](https://modular-avatar.nadena.dev/ja/)

* **OSC送信ツール**
  OSC HeartRateSender
  [https://booth.pm/ja/items/3687355](https://booth.pm/ja/items/3687355)

* **SubMeshInspectorWindow**
  (Blend Shape Builderが前提となります)
  [https://gist.github.com/flammpfeil/18bb0b5f41588c6530500375d1a273f6](https://gist.github.com/flammpfeil/18bb0b5f41588c6530500375d1a273f6)

* **Blend Shape Builder**
  [https://github.com/unity3d-jp/BlendShapeBuilder?tab=readme-ov-file#blend-shape-builder--vertex-tweaker](https://github.com/unity3d-jp/BlendShapeBuilder?tab=readme-ov-file#blend-shape-builder--vertex-tweaker)

---

## License

このプロジェクトはMITライセンスに準拠しています。
This project is licensed under the MIT License,
see the LICENSE.txt file for details

---

## Copyright

Copyright © 2024-2025 Konoha
