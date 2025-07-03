# VehicleScan AOSP Android 15 (based on raspberry-vanilla aosp for pi 4)


This project is built upon Android 15.0.0_r32 and the Raspberry Pi Vanilla project for the Raspberry Pi 4. It is developed as a final project for the AOSP course at ITI Embedded Systems Track Intake 45.

## How to build (Ubuntu 22.04 LTS):

1. Establish [Android build environment](https://source.android.com/docs/setup/start/requirements).

2. Install additional packages:

```bash
sudo apt-get install dosfstools e2fsprogs fdisk kpartx mtools rsync
```

3. Initialize repo with Raspberry Pi Vanilla manifest and add VehicleScan custom manifest:

```bash
repo init -u https://android.googlesource.com/platform/manifest -b android-15.0.0_r32 --depth=1
curl -o .repo/local_manifests/manifest_brcm_rpi.xml -L https://raw.githubusercontent.com/raspberry-vanilla/android_local_manifest/android-15.0/manifest_brcm_rpi.xml --create-dirs
curl -o .repo/local_manifests/manifest_vehiclescan.xml -L https://raw.githubusercontent.com/VehicleScan/android_local_manifest/main/manifest_vehiclescan.xml
```

4. Sync source code:

```bash
repo sync
```

5. Setup Android build environment:

```bash
. build/envsetup.sh
```

6. Select the device and build target:

```bash
lunch aosp_rpi4_car-bp1a-userdebug
```

7. Compile:

```bash
make bootimage systemimage vendorimage -j$(nproc)
```

8. Make flashable image for the device:

```bash
./rpi4-mkimg.sh
```
