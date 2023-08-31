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
sudo nano /usr/share/alsa/alsa.conf
```
tìm đến dòng số 14 "~/.asoundrc" và thêm # vào đầu để tắt .asoundrc
```sh
echo "dtoverlay=googlevoicehat-soundcard" | sudo tee -a /boot/config.txt
```


Lệnh Thống kê ID của Mic USB và Loa
```sh
arecord -l
aplay -l
```
Chạy lệnh sau
```sh
sudo nano /home/pi/.asoundrc
```
Cửa sổ nano hiện lên, paste dòng sau

```sh
options snd_rpi_googlemihat_soundcard index=0

pcm.softvol {
    type softvol
    slave.pcm dmix
    control {
        name Master
        card sndrpigooglevoi
    }
}

pcm.micboost {
    type route
    slave.pcm dsnoop
    ttable {
        0.0 30.0
        1.1 30.0
    }
}

pcm.!default {
    type asym
    playback.pcm "plug:softvol"
    capture.pcm "plug:micboost"
}

ctl.!default {
    type hw
    card sndrpigooglevoi
}


```
Coppy cấu hình âm thanh vào etc:
```sh
sudo cp /home/pi/.asoundrc /etc/asound.conf
sudo reboot
```
