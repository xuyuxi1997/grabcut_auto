# キャラクターイラストの顔パーツ自動分割
Live2Dを制作するためには、キャラクターイラストの目、口、髪の毛、などのパーツを予め別レイヤーに分割して用意しておかなくてはいけません。しかし、レイヤー分けしていない既存の画像をLive2Dに取り込んで動かしたい場合には、手作業でパーツごとにレイヤー分けをする必要があります。その作業はとても時間がかかり、面倒であるため、このツールでは、対話的前景領域抽出のgrabcutのアルゴリズムとアニメ画像の顔認識のプログラムをベースとして、目、鼻、口などの顔パーツを認識し、切り取りをすることができます。

# 各ファイルについて
〇grabcut_auto - [grabcutのプログラム](https://github.com/opencv/opencv/blob/master/samples/python/grabcut.py) をベースとして、以下の機能を追加しました。
・顔認識のプログラムから前景領域抽出をする範囲を自動で選択
・抽出後の出力画像をパーツごとにクロップして透過保存
・目の切り取りを選択後、白目部分も切り取り可能に
・鼻の自動切り取り

〇landmark.py - [アニメ顔用のランドマーク検出プログラム](https://github.com/kanosawa/anime_face_landmark_detection) をベースとして、検出した顔ランドマークの座標をもとに、それぞれのパーツごとの座標設定を追加しました。

# 使い方
