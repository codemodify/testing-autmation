# The Board
- https://www.raspberrypi.org/products/raspberry-pi-3-model-b-plus/

# Raspbian OS
- https://www.raspberrypi.org/downloads/raspbian/

# Test On The Board
- FIXME

# Test In Emulator (Raspbian Buster)

#### Prepare QEMU booting files
```shell
curl https://raw.githubusercontent.com/dhruvvyas90/qemu-rpi-kernel/master/kernel-qemu-4.19.50-buster \
    -o ./boot-helper-files/kernel-qemu-4.19.50-buster

curl https://raw.githubusercontent.com/dhruvvyas90/qemu-rpi-kernel/master/versatile-pb.dtb \
    -o ./boot-helper-files/versatile-pb.dtb

# Get Desktop
curl -O https://downloads.raspberrypi.org/raspbian/images/raspbian-2019-09-30/2019-09-26-raspbian-buster.zip
unzip 2019-09-26-raspbian-buster.zip

# OR Lite
curl -O https://downloads.raspberrypi.org/raspbian_lite/images/raspbian_lite-2019-09-30/2019-09-26-raspbian-buster-lite.zip
unzip 2019-09-26-raspbian-buster-lite.zip
```

#### Start QEMU with TinkerOS
```shell
qemu-system-arm -cpu arm1176 -m 256 \
    -kernel ./boot-helper-files/kernel-qemu-4.19.50-buster \
    -M versatilepb \
    -dtb ./boot-helper-files/versatile-pb.dtb \
    -no-reboot \
    -nographic \
    -append "dwc_otg.lpm_enable=0 root=/dev/sda2 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait" \
    -drive "file=2019-09-26-raspbian-buster-lite.img,index=0,media=disk,format=raw" \
    -net user,hostfwd=tcp::22222-:22 -net nic
```
- Login into R(aspbian) on Q(emu), then `sudo systemctl enable --now ssh`
- SSH from terminal into the RoQ `ssh -p 22222 pi@localhost`
  - `sudo apt-get update && sudo apt-get upgrade && sudo reboot` 
  - `sudo apt-get install connectd`
  - etc
