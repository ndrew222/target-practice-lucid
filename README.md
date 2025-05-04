# Introduction

So the game I implemented on the Alchitry Io board is based on the toy _Bop It! Smash_. Its simple design and interactiveness were what got me to choose this particular game for the project.

# How to play

So the setup is very simple. When you power on the device, the game is in the `INIT` state.
Pressing any of the face buttons will initiate the `GAMESTART` state. In this state, the LED will be oscillating from left to right and vice versa.
The goal is to press any button during the instant that the LED is located in the middle (the spot where the LED is constantly on). The button press is registered the moment the circuit is closed, so long button presses will not be treated any differently.

On hit, the game will enter the `SUCCESS` state, where your score will be displayed to you. After a brief timeout to avoid accidentally skipping out of the screen, pressing any button will result in `GAMESTART` being entered again. There is an LED on the Alchitry Au board to indicate if the timeout period has passed (bottom LED).

This is repeated until you miss the glowing LED, after which the `FAIL` state is entered[^1].
There, your score is once again displayed, but hitting any button will bring your game back to the `INIT` state.

# Some notable limitations

When you are playing the game, as the buttons are on the right side of the device, your hand blocks the debug LEDs. These LEDs display the state, and also whether the timeout has passed. While not essential for playing the game, does make it slightly frustrating when the timeout indicator is obstructed.

There can occasionally be a weird bug where either the LED runs off the screen, or just doesn't appear. If that happens, the device needs to be rebooted by unplugging it and plugging it back in.

There is this other weird bug which have not been able to find the cause of where the LED does not start in the same place whenever the game is started. While this is not game breaking, has been extremely frustrating on the development side, as I can't seem to find the cause of it.

[^1]: The game score indicator only counts up to 9, as there was insufficient time to implement multiple digits in the seven segment display. The game's difficulty is tweaked to account for that, and also once you reach 9 points, the next hit is guaranteed to fail. On testing, it has been observed that one is statistically more likely to fail as the score increases.
