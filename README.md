# 土の中のつながり ── 土壌生態系のアクターネットワーク模擬

Soil Ecosystem ANT Simulator — a teaching model, not a measurement

公開先：https://mitsulab-soil.github.io/Soil-Ecosystem-ANT-Simulator/

## これは何か

土の中の生き物と物 ── 細菌・菌類・線虫・原生生物・ミミズ・植物の根・有機物・水・酸素 ── を色のついた粒として平面の上で動かし、近づいた粒どうしのやりとり（分解・捕食・助け合い・競争・運ぶ）を線で結んで、その網の目（ネットワーク）を数で見る学習用の模擬（シミュレーション）です。生き物と物を同じ「粒」として並べる点で、アクターネットワーク理論（ANT）の考え方を借りています。

A browser-based, agent-based teaching model: nine kinds of particles interact when they come close, and the resulting network is summarised with simple graph metrics.

## データの性質（必ず読んでください）

- **測ったデータは使っていません。** ふるまいの規則と係数は、動きが分かりやすくなるよう決めた値です。
- 粒の数・大きさ・速さ・寿命・時間の進み方は、実物と対応していません（以前の版にあった「1 ステップ＝60 秒の実時間」の対応は根拠が示せないため外しました）。
- 画面に出る数値（密度・クラスター係数・多様度・まとまり指数）は、この模擬の中の粒について計算したものです。本物の土の状態を表すものではありません。
- 「まとまり指数 S」は、均等度・密度・偏りの少なさを決めた重みで足したこのモデル独自の目安です。生態学でいう「安定性」を測るものではありません。
- 「いまの様子」（分解者がふえる／食う・食われるが目立つ／ならされてくる）は、粒の数と均等度の簡単な条件で自動で付ける名前です。

## 使い方

`index.html` をブラウザで開くだけで動きます。スマホでも使えます。

| 操作 | 動き |
|---|---|
| ⏸ 止める／▶ 動かす | 一時停止と再開 |
| ↺ はじめから | 粒を置き直して最初から |
| つなぎ役を表示 | 多くとつながる菌類・水・有機物の粒に輪を付ける |
| 速さ | 1 フレームに進めるステップ数（1〜10） |
| 粒に触れる・押す | 説明を出す／押した粒を追いかける |

## モデルのしくみ（要点）

- 近さ s = 1 − 距離／届く範囲（0〜1）。捕食では食べる側が α·s を得て、食べられる側が β·α·s を失う。分解では分解者が α·s を得て、有機物が β·s·E·0.04 を失う。食う・食われるの関係で数が増減する考え方（ロトカ＝ヴォルテラ型）を、粒ごとの規則に置き換えたもので、方程式そのものを解いてはいません。
- 生き物の粒はエネルギーが尽きるか寿命が来ると消え、有機物の粒になります。エネルギーが一定を超えると一定の確率でふえます。
- 雨（200 ステップごと）・落ち葉（150 ステップごと）・根のまわりで細菌がふえる（300 ステップごと）を決まった間隔で起こします。
- 網の目の数値：n＝粒の数、m＝つながっている組の数（同じ組は一本）。ρ = 2m / n(n−1)、k̄ = 2m / n、C＝二つ以上とつながる粒について、隣どうしもつながっている割合の平均。H′・J′ は 9 種類の粒の数の割合から計算（水・酸素・有機物も一種類として数える）。

## 本物の土とのちがい

- 平面の上だけで動きます。本物の土は、すき間や団粒が立体に入り組んでいます。
- 温度・pH・土の種類・季節は入っていません。
- 「菌類」は、腐生菌と菌根菌をまとめた一つの粒です。本物では役割の違う別のなかまです。
- ミミズの通り道で空気が入る様子を、酸素の粒を足して表しています。ミミズや根が酸素をつくるわけではありません。

## 参考にした資料

- Bardgett, R. D. & van der Putten, W. H. (2014) Belowground biodiversity and ecosystem functioning. *Nature* 515: 505–511. https://doi.org/10.1038/nature13855
- Coleman, D. C., Crossley, D. A. & Hendrix, P. F. (2004) *Fundamentals of Soil Ecology*, 2nd ed. Academic Press.
- Callon, M. (1986) Some elements of a sociology of translation. In J. Law (ed.) *Power, Action and Belief*. Routledge.
- Latour, B. (2005) *Reassembling the Social: An Introduction to Actor-Network-Theory*. Oxford University Press.
- Watts, D. J. & Strogatz, S. H. (1998) Collective dynamics of 'small-world' networks. *Nature* 393: 440–442.

## 関連

- 前の版：[土壌微生物ネットワークの可視化](https://github.com/mitsulab-soil/Visualization-of-soil-microbial-networks)
- note：[【mitsulab】土壌生態系シミュレーター（Ver1.0）開発](https://note.com/mitsu32_lab/n/nd04af75e5c24)

## ライセンス

プログラムは MIT License です。外部のライブラリは使っていません。文字は Noto Sans JP・Shippori Mincho・JetBrains Mono（SIL Open Font License、Google Fonts）。

## 更新の記録

- 2026-10-01：中身を点検して改訂。測った値ではないことを画面と説明に明記し、「1 ステップ＝60 秒」の実時間対応・「安定性」「小世界構造」などの根拠のない言い方を外した。網の目の密度の計算で同じ組を重ねて数えることがあった誤り、ミミズの分解が二重に計算されていた誤り、、時系列グラフが H′ でなく J′ を描いていた食い違いを直した。「菌根菌」の粒を「菌類」（腐生菌と菌根菌をまとめたもの）に改め、根が酸素の粒を出す規則と、効果のない「団粒ができる」記録を外した。スマホで使えるように画面の割り付けと文字の大きさを直した。同梱していた論文形式の PDF は、検証できない記述や実物と合わない数値を含むため、このリポジトリから外した。

---

© 2026 mitsulab ／ https://mitsulab.jp

## 著作権 ／ Copyright

© 2026 mitsulab. 文章と図の著作権は mitsulab にあります（All rights reserved）。プログラムは上に書いたとおり MIT License です。文章と図の無断の転載と、AI の学習・生成への利用はお断りします（テキスト・データマイニングの権利を留保します）。くわしくは [利用規約](https://mitsulab.jp/terms/#ai)。

Text and figures © 2026 mitsulab, all rights reserved; the program is under the MIT License as stated above. Reposting the text and figures without permission, and using them for AI training or generation, are not permitted; text and data mining rights are reserved. See the [Terms of Service](https://mitsulab.jp/terms/#ai-en).
