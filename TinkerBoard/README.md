# The Board
- https://www.asus.com/us/Single-Board-Computer/Tinker-Board/

# TinkerOS
- https://tinkerboarding.co.uk/wiki/index.php/TinkerOS
- Image based on Debian 9
	- `https://dlcdnets.asus.com/pub/ASUS/mb/Linux/Tinker_Board_2GB/20190821-tinker-board-linaro-stretch-alip-v2.0.11.img.zip`

# Test On The Board
- FIXME

# Test In Emulator

#### Prepare QEMU booting files (zImage below is the booting kernel)
- `mkdir 20190821-tinker-board-linaro-stretch-alip-v2.0.11.img-qemu-boot-files`
- `sudo modprobe nbd max_part=16`
- `sudo qemu-nbd -c /dev/nbd0 20190821-tinker-board-linaro-stretch-alip-v2.0.11.img`
- `mkdir qemu-mounted`
- `sudo mount /dev/nbd0p1 ./qemu-mounted/`
- `cp ./qemu-mounted/zImage ./20190821-tinker-board-linaro-stretch-alip-v2.0.11.img-qemu-boot-files/`
- `sudo umount ./qemu-mounted`
- `rm -rf ./qemu-mounted`
- `sudo qemu-nbd -d /dev/nbd0`
- `sudo rmmod nbd`

#### Start QEMU with TinkerOS
- `qemu-system-arm -machine vexpress-a9 -m 256 20190821-tinker-board-linaro-stretch-alip-v2.0.11.img`

qemu-system-aarch64 -m 256 -machine virt -cpu cortex-a57 -bios /usr/share/qemu/edk2-aarch64-code.fd 20190821-tinker-board-linaro-stretch-alip-v2.0.11.img
