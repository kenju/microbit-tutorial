# Create a Secret Dice

## Introduction @unplugged

First create a simple dice to roll in your game! 🎲

## Step One

Use the ``|led.plot|`` block to show rolling animations.

```blocks
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
})
```

## Step Two

Create a sprite with the ``||variables:set mySprite to||`` block.

```blocks
custom.makeRandomBackground()
// @highlight
let mySprite = sprites.create(img`
    . . . . . . . . . . b 5 b . . .
    . . . . . . . . . b 5 b . . . .
    . . . . . . . . . b c . . . . .
    . . . . . . b b b b b b . . . .
    . . . . . b b 5 5 5 5 5 b . . .
    . . . . b b 5 d 1 f 5 5 d f . .
    . . . . b 5 5 1 f f 5 d 4 c . .
    . . . . b 5 5 d f b d d 4 4 . .
    b d d d b b d 5 5 5 4 4 4 4 4 b
    b b d 5 5 5 b 5 5 4 4 4 4 4 b .
    b d c 5 5 5 5 d 5 5 5 5 5 b . .
    c d d c d 5 5 b 5 5 5 5 5 5 b .
    c b d d c c b 5 5 5 5 5 5 5 b .
    . c d d d d d d 5 5 5 5 5 d b .
    . . c b d d d d d 5 5 5 b b . .
    . . . c c c c c c c c b b . . .
`, SpriteKind.Player)
```

## Step Three

Add movement with the ``||controller:move mySprite with buttons||`` block.

```blocks
custom.makeRandomBackground()
let mySprite = sprites.create(img`
    . . . . . . . . . . b 5 b . . .
    . . . . . . . . . b 5 b . . . .
    . . . . . . . . . b c . . . . .
    . . . . . . b b b b b b . . . .
    . . . . . b b 5 5 5 5 5 b . . .
    . . . . b b 5 d 1 f 5 5 d f . .
    . . . . b 5 5 1 f f 5 d 4 c . .
    . . . . b 5 5 d f b d d 4 4 . .
    b d d d b b d 5 5 5 4 4 4 4 4 b
    b b d 5 5 5 b 5 5 4 4 4 4 4 b .
    b d c 5 5 5 5 d 5 5 5 5 5 b . .
    c d d c d 5 5 b 5 5 5 5 5 5 b .
    c b d d c c b 5 5 5 5 5 5 5 b .
    . c d d d d d d 5 5 5 5 5 d b .
    . . c b d d d d d 5 5 5 b b . .
    . . . c c c c c c c c b b . . .
`, SpriteKind.Player)
// @highlight
controller.moveSprite(mySprite)
```