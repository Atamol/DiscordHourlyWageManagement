![License](https://img.shields.io/badge/license-MIT-green)
![Python](https://img.shields.io/badge/python-3.x-blue)

# Discordによる時給・労働時間管理Bot
このBotはDiscordのスラッシュコマンドを用いて作業の開始・終了時刻を記録し，設定された時給に基づいて自動的に賃金を計算することができます．<br>
作業の一時停止や手動での時間修正などといった複雑な機能も備わっています．<br>
また，計算結果はすべて指定されたチャンネル内にログとして残すことでデータベースを形成するため，各データが可視化され，Discord上で管理が行えるようになります．

## 基本的な使い方
1. `/hourly_wage "任意の金額"`と入力して，時給を任意の金額に設定します（初回のみ）．
2. `/begin`を入力して作業を開始します．
3. `/rest`を使用して一時停止し，もう一度`/rest`を使用して再開します．
4. `/finish`を入力して作業を終了し，賃金を確認します．
5. `/sum`でこれまでの賃金の合計を表示します．

## コマンド一覧
- **時給の設定**: `/hourly_wage "任意の金額"`コマンドで時給をユーザーごとに設定します．Botがオフラインになるまでメモリに保存されるため，次回以降の設定は不要です．
- **作業開始**: `/begin`コマンドで作業時間の記録を開始します．
- **一時停止・再開**: `/rest`コマンドで作業時間の記録を一時停止し，再度同じコマンドで記録を再開します．
- **作業終了**: `/finish`コマンドで作業時間の記録を終了し，作業時間と賃金を計算します．
- **作業時間を手動修正**: `/fix`コマンドで，作業時間を手動で設定し，賃金を合計に加えます．オプションで`/finish`と`/fix`のメッセージリンクを添付することによってその投稿が削除され，不正な記録を修正することもできます．
- **指定した日時の合計作業時間と合計賃金を計算**: `/daily_sum`コマンドで，指定された日（年内のみ）の午前6:00からその翌日の午前5:59の間でデータを参照し，それらに含まれる作業時間と賃金の合計を計算します．
- **これまでの作業時間と賃金を計算**: `/sum`コマンドで，これまでのすべてのデータを参照して給料を計算し，これまでの作業時間と賃金の合計を表示します．
- **これまでの作業記録をリセット**: `/reset`コマンドで，これまでの作業記録（`/finish`と`/fix`のログ）をすべて削除し，リセットします．

## 実装の大まかな手順
1. `hourly_wage.py`をダウンロードします．
2. `discord.py`をインストールします．
3. コンソールからBotを起動します．

## その他
- 日付や時刻の操作に[datetime](https://docs.python.org/ja/3/library/datetime.html)というライブラリを使用しています．
- 正規表現マッチング操作に[re](https://docs.python.org/ja/3/library/re.html)というライブラリを使用しています．
- 作業記録を参照するコマンドは同一のチャンネルに投稿されたメッセージを認識することによって行われるため，作業記録コマンドは定めたチャンネルで使用するようにしてください．
- ユーザーやメッセージの識別にはメンションと特定の文字列を検出して判断するようにしているため，作業終了などのたびに各々が添付されます．
