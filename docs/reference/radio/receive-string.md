# Receive String

Find the next string sent by `radio` from another micro:bit.

```sig
radio.receiveString()
```

### Returns

* the first [string](/reference/types/string) that was sent. If no
  string was sent, then this function returns an empty (blank) string.

### Simulator

This function only works on the micro:bit, not in browsers.

### Example: Simple receiver

Show the string sent by another micro:bit.

```blocks
radio.onDataReceived(() => {
    basic.showString(radio.receiveString());
});
```

### Example: Two-way radio

If you load this program onto two or more micro:bits, you can send a code word from one of them to the others by pressing button `A`.
The other micro:bits will receive the code word and then show it.

```blocks
input.onButtonPressed(Button.A, () => {
    radio.sendString("Codeword: TRIMARAN")
    basic.showString("SENT");
})

radio.onDataReceived(() => {
    basic.showString(radio.receiveString());
});
```

### ~hint

A radio that can both transmit and receive is called a _transceiver_.

### ~

### Example: Mood radio

This is a simple program to send whether you are happy or sad over ```radio```.
Use the `A` or `B` button to select an emotion.

This program will also receive your friend's mood.

```blocks
let data: string = "";
input.onButtonPressed(Button.A, () => {
    radio.sendString("H");
});
input.onButtonPressed(Button.B, () => {
    radio.sendString("S");
});
radio.onDataReceived(() => {
    data = radio.receiveString();
    if ("H" == data) {
        basic.showLeds(`
            . . . . .
            . # . # .
            . . . . .
            # . . . #
            . # # # .
            `);
    } else if ("S" == data) {
        basic.showLeds(`
            . . . . .
            . # . # .
            . . . . .
            . # # # .
            # . . . #
            `);
    } else {
        basic.showString("?");
    }
});
```

### See also

[send string](/reference/radio/send-string), [on data received](/reference/radio/on-data-received)

```package
microbit-radio
```