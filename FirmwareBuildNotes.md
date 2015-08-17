Follow tutorial to get source and tools:
http://forum.xda-developers.com/showthread.php?t=1490886

~/src/yinlips
  * android - Android system source
  * kitchen - firmware build environment
  * lichee - kernel source
  * lost+found - src/yinlips is actually a separate emulated disk
  * `_*` - extracted from old firmware and/or files for new
  * `*.fex` - these are mostly text source files to be compiled into `*.bin`
  * `_extract/*.fex` - partition images are not fex files, but are named `*.fex` apparently to prevent them from being encrypted (according to original developer of this kitchen).

TODO:
  * `joydev.ko` and Gamepad IME
  * `_bootfs_src/script.txt` - resize partitions
  * new kernel from source
  * new android from source
  * Full spoof as SGS2 (GT-I9100) for better GameLoft / EA compatibility
  * what does MarketEnabler do?  can i delete it?
  * Remove Google Music, any other Google apps that can be installed from market
  * resize partitions
  * install voice recorder?
  * setcpu?
  * adb not running

DONE:
  * rm emus
  * rm SKGameExplore
  * rm games
  * rm ireader
  * tweak build.prop
  * update Adobe Flash

Possibly Useful Things:
  * mkbootimg --kernel boot.img-kernel --ramdisk ramdisk-new.gz --cmdline 'console=ttyS0,115200 rw init=/init loglevel=8' --base 0x40000000 -o boot.img
  * http://android-dls.com/wiki/index.php?title=HOWTO:_Unpack%2C_Edit%2C_and_Re-Pack_Boot_Images
  * Reports model "crane\_e602", kernel "2.6.36-android/skkzk@freeman-desktop #8", build "crane\_e602-eng 2.3.4 GRJ22 eng.skkzk.20120419.114758 test-keys", internal flash free 2.72G, internal storage free 423M.
  * This is reported by their 20120531 update.
  * If debugging enabled, usb=18d1:0002; if disabled, usb=1f3a:efe8
  * Smart Bench 2011:
    * with no dexopt line:  Prod=862, Game=2020
    * with dalvik.vm.dexopt-flags=v=n,o=a,u=y: Prod=833, Game=1802

Boot Process:
  * The boot process (for Linux on the A10):
    * http://rhombus-tech.net/allwinner_a10/a10_boot_process/
  * brom->boot0->boot1->boot.axf->bImage
    * boot0 reads COMMON\_SYS\_CONFIG; defines basic hardware
    * (later stage) reads script.bin; similar looking file defines remaining hardware
  * COMMON\_SYS\_CONFIG:
    * partition defs start at part\_num
    * file->part "download" defs start at down\_num
    * pkt\_name is content for partition; verify\_file is checksum
    * BOOTFS/VBOOTFS
    * LROOTFS/BROOTFS
    * LSYSTEMFS/VSYSTEMFS
    * LRECOVERYFS/VRECOVERYFS
    * DISKFS/-

To install a ROM:
  * Shut down your 18A, unplug USB.
  * Copy LiveSuit to a new directory, double-click to unpack and install driver.
  * Run LiveSuit, click No.
  * Click cube icon, select img file.
  * Hold R&U button, plug in.  Keep holding til beeps and "Tips: Does mandatory format?" window.
    * R&U is labeled - it's the little button next to the DC power port.
  * Release R&U, click Yes, Yes.
  * Wait patiently.