## Microphone I2S

## Hardware
```sh
Supports all Raspberry Pi 
- Audio Amplifier: MAX98357A x 2
- Microphone: ICS-43432 x 2
- LED: Led APA102 x 12 (Control led: GPIO 5)
Button: 4 botton (GPIO 13, 22, 25 ,26)

```
## Setting:
```sh
echo "dtoverlay=googlevoicehat-soundcard" | sudo tee -a /boot/config.txt
sudo reboot
```

Done!


