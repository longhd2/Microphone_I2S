# Microphone I2S cho Raspberry Pi

![image](https://github.com/longhd2/Microphone_I2S/assets/43842525/9aa7127b-9fc9-406e-baad-6c8b14ff37de)


**Microphone I2S cho Raspberry Pi** là một phần mở rộng đa chức năng cho Raspberry Pi, được thiết kế để mở rộng khả năng thu âm và phát lại âm thanh của thiết bị. Hỗ trợ cho tất cả các phiên bản của Raspberry Pi cùng với LED APA102 và 4 phím bấm cảm ứng nó là một sự bổ sung tuyệt vời cho các dự án Raspberry Pi của bạn.

## Đặc Điểm Chính

- **Hỗ Trợ Tất Cả Các Phiên Bản Raspberry Pi:** Sản phẩm này tương thích với tất cả các phiên bản của Raspberry Pi, từ Raspberry Raspberry Pi Zero đến Raspberry Pi 4.

- **Chất Lượng Âm Thanh Tối Ưu:** Được trang bị hai microphone ICS-43434 kỹ thuật số chất lượng cao, và 2 bộ khuếch đại âm thanh Streo 3W cho chất lượng âm thanh với độ chính xác và chi tiết tối ưu.

- **Hệ Thống LED APA102:** Với 12 đèn LED APA102 tích hợp, bạn có thể tạo ra các hiệu ứng ánh sáng sáng tạo và thú vị.

- **Điều Khiển LED Dễ Dàng:** Microphone I2S được trang bị một cổng GPIO 5 để điều khiển hệ thống LED APA102.

- **Tích Hợp Nút Bấm Cho Điều Khiển Thuận Tiện:** Với bốn nút bấm cảm ứng được kết nối vào các cổng GPIO 13, 22, 25 và 26 thuận tiện cho việc điều khiển thiết bị

## Hardware

- **Hỗ trợ cho tất cả các phiên bản Raspberry Pi**
- **Microphone:** ICS-43434 x 2
- **Bộ khuếch đại âm thanh:** MAX98357A x 2
- **LED:** Led APA102 x 12 (Control led: GPIO 5)
- **Button:** 4 button (GPIO 13, 22, 25, 26)

## Setting

### SSH vào Raspberry Pi Image

1. Bật Raspberry Pi và kết nối vào nó thông qua SSH.

2. Gõ lệnh sau để chỉnh sửa tệp cấu hình âm thanh:

   ```sh
   sudo nano /usr/share/alsa/alsa.conf
   ```

   Tìm đến dòng số 14 `~/.asoundrc` và thêm dấu "#" vào đầu để tắt `.asoundrc`. Sau đó, bấm `Ctrl + O` để lưu lại, sau đó nhấn `Enter`, cuối cùng bấm `Ctrl + X` để thoát khỏi trình soạn thảo nano.

3. Tiếp theo, gõ lệnh sau để thêm dtoverlay vào tệp cấu hình:

   ```sh
   echo "dtoverlay=googlevoicehat-soundcard" | sudo tee -a /boot/config.txt
   ```

4. Gõ lệnh sau để cài đặt cho tệp âm thanh:

   ```sh
   sudo nano /etc/asound.conf
   ```

   Trong cửa sổ nano, paste nội dung sau:

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

5. Lưu và đóng tệp cấu hình bằng cách nhấn `Ctrl + O`, sau đó nhập "Y" để xác nhận và "Enter" để lưu.

6. Cuối cùng, gõ lệnh sau để khởi động lại Raspberry Pi:

   ```sh
   sudo reboot
   ```

## Liên Hệ

Nếu bạn có bất kỳ câu hỏi hoặc ý kiến phản hồi, vui lòng liên hệ với chúng tôi qua email vipiteam@gmail.com hoặc fanfage https://www.facebook.com/groups/285131860062315/.


