# Create a Secret Dice

## Introduction @unplugged

First create a simple dice to roll in your game! 🎲

## Step One

Use the ``|led.plot|`` block to show rolling animations.

```blocks
let plot: number[] = []
let plots: number[][] = []
function showRolling () {
    plots = [
    [0, 0],
    [0, 1],
    [0, 2],
    [0, 3],
    [0, 4],
    [1, 4],
    [2, 4],
    [3, 4],
    [4, 4],
    [4, 3],
    [4, 2],
    [4, 1],
    [4, 0],
    [3, 0],
    [2, 0],
    [1, 0]
    ]
    for (let j = 0; j <= plots.length - 1; j++) {
        plot = plots[j]
        led.plot(plot[0], plot[1])
        basic.pause(50)
        led.unplot(plot[0], plot[1])
    }
}
input.onGesture(Gesture.Shake, function () {
    // show dice rolling animation
    basic.clearScreen()
    for (let index = 0; index < 2; index++) {
        showRolling()
    }
    // TODO: show dice numbers later
})
```

## Step Two

Let's send secret messages!

```blocks
radio.setGroup(99)
input.onButtonPressed(Button.A, function () {
    radio.sendString("showMax")
})
input.onButtonPressed(Button.B, function () {
    radio.sendString("showMin")
})
```

## Step Three

Let's set the secret flag on receiving secret messages!

```blocks
let secretFlag = ""
secretFlag = "random"
radio.onReceivedString(function (receivedString) {
    // set secretFlag based on received radio message
    if (receivedString == "showMax") {
        secretFlag = "showMax"
    } else if (receivedString == "showMin") {
        secretFlag = "showMin"
    } else {
        secretFlag = "random"
    }
})
```

## Step Four

Now is the time to roll your dice!

```blocks
let diceNum = 0
input.onGesture(Gesture.Shake, function () {
    // show dice rolling animation
    basic.clearScreen()
    for (let index = 0; index < 2; index++) {
        showRolling()
    }
    // inject secretFlag
    if (secretFlag == "showMax") {
        diceNum = 6
    } else if (secretFlag == "showMin") {
        diceNum = 1
    } else {
        diceNum = randint(1, 6)
    }
    // reset secret flag
    secretFlag = "random"
    // flash dice number
    for (let index = 0; index < 4; index++) {
        basic.clearScreen()
        basic.pause(100)
        basic.showNumber(diceNum)
    }
})
```
