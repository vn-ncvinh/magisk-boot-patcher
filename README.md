# Run patch boot locally

That's how we can run Magisk's `boot_patch.sh` on Linux x86 or x64 and patch a boot image for an ARM device

> Tested with Magisk v25.2 with FP3

* Get Magisk `.apk`
* Extract it

Keep in the same folder:
```bash
mkdir output
cp assets/boot_patch.sh ./output/boot_patch.sh
cp assets/util_functions.sh ./output/util_functions.sh
cp assets/stub.apk ./output/stub.apk
cp lib/x86_64/libmagiskboot.so ./output/magiskboot
cp lib/armeabi-v7a/libmagisk32.so ./output/magisk32
cp lib/arm64-v8a/libmagisk64.so ./output/magisk64
cp lib/arm64-v8a/libmagiskinit.so ./output/magiskinit
```
You can delete all the rest.

In util_functions.sh:
* Change function `ui_print()` to only contain `echo "$1"`
* Change every `getprop` command, to `adb shell getprop`, to go run it on device rather than locally.

You can now run:
`sh boot_patch.sh boot.img`

The outpout file `new-boot.img` has the exact same sha256 hash as the `magisk_patched-*.img`, so we can consider it works :)