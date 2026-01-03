How to Build App for QEMU:

   cd /workspace/apps/<test folder>
   west build -p always -b esp32s3_devkitc/esp32s3/procpu -- -DDTC_OVERLAY_FILE=boards/esp32s3_devkitc.overlay

   Next, create a 4 MB binary from your compiled binary file and pad the end with zeros:

   dd if=/dev/zero of=build/zephyr/zephyr_4mb.bin bs=1M count=4
   dd if=build/zephyr/zephyr.bin of=build/zephyr/zephyr_4mb.bin conv=notrunc

   Finally, run the application in QEMU:

   qemu-system-xtensa -nographic -machine esp32s3 -drive file=build/zephyr/zephyr_4mb.bin,if=mtd,format=raw

How to Stop program running on QEMU:
   1. Press Ctrl + A (press and hold Ctrl, then press A, then release both keys).
   2. Press the X key (lowercase x, no Shift).