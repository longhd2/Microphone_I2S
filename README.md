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
ssh vào pi
![image](https://github.com/longhd2/Microphone_I2S/assets/43842525/8f03b8be-271c-4e4f-bbb9-c9465eb33fb5)

Sau đó gõ lệnh
```sh
sudo nano /usr/share/alsa/alsa.conf
```
tìm đến dòng số 14 "~/.asoundrc" và thêm # vào đầu để tắt .asoundrc
![image](https://github.com/longhd2/Microphone_I2S/assets/43842525/ca1c2de4-11de-46ba-8096-25cafe1e0121)
Sau đó bấm Ctr + Y + để lưu lại

Sau đó
```sh
echo "dtoverlay=googlevoicehat-soundcard" | sudo tee -a /boot/config.txt

```
![image](https://github.com/longhd2/Microphone_I2S/assets/43842525/4dc3bae1-6cd2-4f90-946b-783b4f90ebe8)

Sau đó cài đặt cho tệp âm thanh
```sh
sudo nano /etc/asound.conf
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
Sau đó reboot để khởi động lại:
```sh
sudo reboot
```
Chúc bạn thành công!
