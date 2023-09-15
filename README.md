# Microphone I2S cho Raspberry Pi

![Microphone I2S](link-to-your-image.png)

**Microphone I2S cho Raspberry Pi** là một phần mở rộng đa chức năng cho Raspberry Pi, được thiết kế để mở rộng khả năng thu âm và ánh sáng của thiết bị. Với sự hỗ trợ cho tất cả các phiên bản của Raspberry Pi, âm thanh chất lượng cao và tích hợp LED APA102, nó là một sự bổ sung tuyệt vời cho các dự án Raspberry Pi của bạn.

## Đặc Điểm Chính

- **Hỗ Trợ Tất Cả Các Phiên Bản Raspberry Pi:** Sản phẩm này tương thích với tất cả các phiên bản của Raspberry Pi, từ Raspberry Pi 3 đến Raspberry Pi Zero.

- **Chất Lượng Âm Thanh Tối Ưu:** Được trang bị hai microphone ICS-43434 chất lượng cao, sản phẩm này bắt lấy âm thanh với độ chính xác và chi tiết tối ưu.

- **Hệ Thống LED APA102:** Với 12 đèn LED APA102 tích hợp, bạn có thể tạo ra các hiệu ứng ánh sáng sáng tạo và thú vị.

- **Điều Khiển LED Dễ Dàng:** Microphone I2S được trang bị một cổng GPIO 5 để điều khiển hệ thống LED APA102.

- **Tích Hợp Nút Bấm Cho Điều Khiển Thuận Tiện:** Với bốn nút bấm được kết nối vào các cổng GPIO 13, 22, 25 và 26.

## Hardware

- **Hỗ trợ cho tất cả các phiên bản Raspberry Pi**
- **Bộ khuếch đại âm thanh:** MAX98357A x 2
- **Microphone:** ICS-43432 x 2
- **LED:** Led APA102 x 12 (Control led: GPIO 5)
- **Button:** 4 button (GPIO 13, 22, 25, 26)

## Setting

- Bật Raspberry Pi và mở ứng dụng thu âm.
- Sử dụng nút bấm để điều khiển chức năng của Microphone I2S.
- Tận hưởng âm thanh chất lượng cao và hiệu ứng ánh sáng độc đáo.




### SSH vào Raspberry Pi Image

1. Bật Raspberry Pi và kết nối vào nó thông qua SSH.

2. Gõ lệnh sau để chỉnh sửa tệp cấu hình âm thanh:

   ```sh
   sudo nano /usr/share/alsa/alsa.conf

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

## Liên Hệ

Nếu bạn có bất kỳ câu hỏi hoặc ý kiến phản hồi, vui lòng liên hệ với chúng tôi qua [địa chỉ email hoặc trang web của bạn].

```
Chúc bạn thành công!
