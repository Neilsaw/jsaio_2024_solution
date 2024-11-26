# 第5回 日本眼科AI学会総会 AIコンテスト 解法

テーマ: 眼底写真を用いたメタボリックシンドローム推定  
http://www.jsaio.jp/meeting/soukai/contest/index.html

---

## 解法概要
- 2種類の画像分類モデルによるメタボ有無の推論
- 50個のモデルによる単純加算平均で決定

## 使い方

1. config/config.json のdatasetファイルパスを環境に合わせて変更
2. 1_preprocess
    - 眼底画像の眼底部分のみで切り抜く (黒部分を除外する)
    - 320x320の画像に変換
3. 2_train_seed_ensemble
    - 配下のnotebookをそれぞれ実行
      - exp040: maxvit_tiny_tf_224.in1k
      - exp042: seresnext50_32x4d.racm_in1k
    - 2 model * 5 seed * 5 fold = 50 個のモデルを作成
4. 3_inference
    - 500 枚の testに対して推論実施
    - 1枚当たり 50 model * 3 TTA = 150 個の出力の平均で推論

## 謝辞

本研究に使用した臨床情報と眼底写真は、日本眼科AI学会と国立情報学研究所の共同研究により提供され、Japan Ocular Imaging Registry により管理されたものです。

【引用文献】 Miyake M, Akiyama M, Kashiwagi K, Sakamoto T, Oshika T. Japan Ocular Imaging Registry: a national ophthalmology real-world database. Jpn J Ophthalmol. 2022 Nov;66(6):499-503. doi: 10.1007/s10384-022-00941-0.
