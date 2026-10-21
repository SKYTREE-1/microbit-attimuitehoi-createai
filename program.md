# microbit-attimuitehoi-createai 3
A guide to building an あっちむいてほい game with micro, using Create AI to recognize head movements.

> このページを開く [https://skytree-1.github.io/microbit-attimuitehoi-createai/program](https://skytree-1.github.io/microbit-attimuitehoi-createai/program)

## 手順

1. 機械学習のブロックが追加された makecode の画面で、JavaScriptモードにする。
2. 以下のコードをコピーして、貼り付ける（どこでもいいです .... 貼り付けたあと、勝手に位置が変わります）。
  
```{JavaScript}

let direction = 0

radio.setGroup(1)

// ① 自分の方向を決める
input.onGesture(Gesture.LogoUp, function () {
    direction = 0
    basic.showArrow(ArrowNames.North)
})

input.onGesture(Gesture.TiltRight, function () {
    direction = 1
    basic.showArrow(ArrowNames.East)
})

input.onGesture(Gesture.LogoDown, function () {
    direction = 2
    basic.showArrow(ArrowNames.South)
})

input.onGesture(Gesture.TiltLeft, function () {
    direction = 3
    basic.showArrow(ArrowNames.West)
})

// ② Aボタンで方向を送る
input.onButtonPressed(Button.A, function () {
    radio.sendNumber(direction)
})

// ③ 相手から受け取った方向を判定する
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        basic.showArrow(ArrowNames.North)

        if (input.isGesture(Gesture.LogoUp)) {
            basic.showIcon(IconNames.Happy)
        } else {
            basic.showIcon(IconNames.No)
        }

    } else if (receivedNumber == 1) {
        basic.showArrow(ArrowNames.West)

        if (input.isGesture(Gesture.TiltLeft)) {
            basic.showIcon(IconNames.Happy)
        } else {
            basic.showIcon(IconNames.No)
        }

    } else if (receivedNumber == 2) {
        basic.showArrow(ArrowNames.South)

        if (input.isGesture(Gesture.LogoDown)) {
            basic.showIcon(IconNames.Happy)
        } else {
            basic.showIcon(IconNames.No)
        }

    } else {
        basic.showArrow(ArrowNames.East)

        if (input.isGesture(Gesture.TiltRight)) {
            basic.showIcon(IconNames.Happy)
        } else {
            basic.showIcon(IconNames.No)
        }
    }
})
```
3. ブロックエディタにもどす。
4. 「無線で受信したとき」の中にある「もし〜なら」の条件のブロックのうちピンク色のもの（ロゴが上、左に傾けた、ロゴが下）を、機械学習のなかにある「MLが不明を検出したとき」にかえる。
5. 「不明」の部分を「ロゴが上」→「up」, 「左に傾けた」→「left」, 「ロゴが下」→「down」 となるように変更する。
6. あたりとはずれを音で知らせよう！
   micro:bitを頭につけると、画面を見ることができません。
   そこで、相手が選んだ方向を音で知らせるようにします。
   どの音をどの方向に割り当てるかは、自由に決めてかまいません。

例：あたり
```{javascript}
music.playTone(784, music.beat(BeatFraction.Eighth))
music.playTone(1047, music.beat(BeatFraction.Eighth))
```

例：はずれ
```{javascript}
music.playTone(262, music.beat(BeatFraction.Quarter))
```

7. 上下左右を音で知らせよう！
   micro:bitを頭につけると、画面を見ることができません。
   そこで、相手が選んだ方向を音で知らせるようにします。
   どの音をどの方向に割り当てるかは、自由に決めてかまいません。

    > 例
    > - ↑：低い音 → 高い音
    > - →：「ピン♪」のような音
    > - ↓：高い音 → 低い音
    > - ←：「ピピピ♪」のような3音

8. ここまでできたら、ダウンロードして実際にゲームしてみよう！

お疲れ様でした！
