## Microphone I2S

## Hardware
```sh
Raspberry Pi compatible (supports Raspberry Pi Zero and Zero W, Raspberry PiB+, Raspberry Pi 2B, Raspberry Pi 3B, Raspberry Pi 3B+, Raspberry Pi3 A+ and Raspberry Pi 4B)
Audio Amplifier: MAX98357A x 2
Microphone: ICS-43432 x 2
LED: Led APA102 x 12
```
## Pinout (40-pin header)
```sh
       3.3V --> 1    2 <-- 5V
    I2C_SDA --> 3    4 <-- 5V
    I2C_SCL --> 5    6 <-- GND
                7    8
        GND --> 9   10
                11  12 <-- I2S_BCLK
                13  14 <-- GND
                15  16 <-- BUTTON_1(GPIO_23)
       3.3V --> 17  18
                19  20 <-- GND
                21  22
                23  24
        GND --> 25  26
     ID_SDA --> 27  28 <-- ID_SCL
                29  30 <-- GND
                31  32
                33  34 <-- GND
  I2S_LRCLK --> 35  36
                37  38 <-- I2S_DIN
        GND --> 39  40 <-- I2S_DOUT
```
## Setting:
```sh
echo "dtoverlay=googlevoicehat-soundcard" | sudo tee -a /boot/config.txt
```

Done!


