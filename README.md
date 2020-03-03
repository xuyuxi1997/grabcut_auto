# キャラクター画像の顔パーツ自動分割

## 概要
Live2D制作の前準備である、キャラクター画像の"顔パーツをそれぞれのレイヤーに分割する"という作業を効率化するためのツールを作成しました。

## 目的
Live2Dを制作するためには、キャラクターイラストの目、口、髪の毛、などのパーツを予め別レイヤーに分割して用意しておかなくてはいけません。しかし、レイヤー分けしていない既存の画像をLive2Dに取り込んで動かしたい場合には、手作業でパーツごとにレイヤー分けをする必要があります。その作業はとても時間がかかり、面倒であるため、このツールにより、対話的前景領域抽出のgrabcutのアルゴリズムとアニメ画像の顔認識のプログラムをベースとして、目、鼻、口などの顔パーツを認識し、自動で切り取りを行うことを目的としました。

## 機能一覧
- grabcut_auto - [grabcutのプログラム](https://github.com/opencv/opencv/blob/master/samples/python/grabcut.py) をベースとして、以下の機能を追加しました。    
    - 顔パーツ(右目、左目、鼻、口、前髪、顔)を顔認識によって認識し、前景領域抽出を行う機能  
    - マウスで描写することによって、前景領域と背景領域を選択する機能  
    - 出力画像をクロップして、それぞれのパーツごとに名前を付けて透過で保存する機能  
    - 目の切り取りを選択後、白目部分も切り取り可能に  
    - 鼻の自動切り取り  

- landmark.py - [アニメ顔用のランドマーク検出プログラム](https://github.com/kanosawa/anime_face_landmark_detection) をベースとして、検出した顔ランドマークの座標をもとに、それぞれのパーツごとの座標設定を追加しました。

## デモリールと使い方
#### デモリール
![grabcutauto_demo](https://user-images.githubusercontent.com/61644695/75748092-0200b380-5d62-11ea-9dcf-58dcea4ffeb9.gif)
#### 出力結果：パーツごとにクロップして保存されたファイル
<img src="cropped_file1.png" width="450" height=250px > <img src="cropped_file2.png" width="400" height=300px > 
#### 使い方
コマンドラインにて以下を入力します。抽出する顔パーツは"right_eye", "left_eye", "nose", "mouth", "face", "bangs"のうちのどれかを選んで入力します。    
    `python grabcut_auto.py <画像ファイル名> <抽出する顔パーツ>`   
    
    1.入力ウィンドウと出力ウィンドウが開きます。  
    2.入力ウィンドウ上で、抽出する顔パーツが矩形で囲まれます。  
    3.'n'を数回押すことによって前景抽出を行います。  
    4.以下のキーを入力し、前景領域と背景領域をマウスによる描写で選択し、'n'を押すことで抽出したい部分を調整することができます。  

Key '0' - 明確な背景領域をマウスで描写  
Key '1' - 明確な前景領域をマウスで描写  
Key '2' - 曖昧な背景領域をマウスで描写  
Key '3' - 曖昧な前景領域をマウスで描写  
key '4' - 白目を前景抽出する  
key '5' - "nose"を選択して鼻を前景抽出する  
Key 'n' - 前景抽出をアップデートする  
Key 'r' - リセット  
Key 's' - 出力を保存  
key 'q' - 終了

## 使用言語、環境
- python 3.7.6  
- Visual Studio 2017  
- Windows 10    

## 必要条件  
- opencv-python  
- torch-python
- [checkpoint_landmark_191116.pth.tar](https://drive.google.com/file/d/1NckKw7elDjQTllRxttO87WY7cnQwdMqz/view)(顔検出の為のカスケードファイル)

## 制作期間、担当箇所など
研究室仮配属の制作課題にて3人チームで作成しました。
- 制作期間
    - 約2か月
- 主な担当箇所
    - 鼻、前髪、顔の座標設定、切り取り
    - key'5'により鼻の前景領域を自動で抽出し、クロップして保存する機能
    - 主な保存機能（透過保存、出力画像の保存、マスクの保存など）
    - 使用したイラストの制作
    - Live2Dの制作
