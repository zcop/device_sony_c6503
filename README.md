Copyright (C) Sony Mobile Communications 2013
=============================================

This is the Android device configuration for Xperia ZL.

To setup a tree and build images for the device do the following:

`repo init` as described by Google over at:
http://source.android.com/source/downloading.html

Put the following snippet in `.repo/local_manifests/c6503.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
<remote  name="sony" fetch="git://github.com/sonyxperiadev/" />
<remote  name="zcop" fetch="git://github.com/zcop/" />

<remove-project name="platform/hardware/qcom/display" />
<remove-project name="platform/hardware/qcom/keymaster" />
<remove-project name="platform/hardware/qcom/media" />
<remove-project name="platform/hardware/qcom/msm8960" />
<remove-project name="platform/hardware/qcom/power" />
<remove-project name="platform/hardware/qcom/sensors" />
<remove-project name="platform/hardware/invensense" />
<remove-project name="platform/hardware/akm" />

<project path="device/sony/lagan" name="device_sony_lagan" groups="device" remote="zcop" revision="android-4.3.1_r1" />
<project path="device/sony/c6503" name="device_sony_c6503" groups="device" remote="zcop" revision="android-4.3.1_r1" />
<project path="vendor/sony/c6503" name="vendor_sony_c6503" groups="device" remote="zcop" revision="android-4.3.1_r1" />
<project path="vendor/sony/lagan" name="vendor_sony_lagan" groups="device" remote="zcop" revision="android-4.3.1_r1" />
<project path="vendor/sony/dash" name="DASH" groups="device" revision="master" remote="sony" />
</manifest>
```

* `repo sync`
* `source ./build/envsetup.sh`
* `lunch full_c6503-userdebug`
* `make`

To flash the images produced make sure your device is unlocked, as described on
http://unlockbootloader.sonymobile.com/

Enter fastboot mode on the device by pressing volume up while inserting the USB
cable or execute `adb reboot bootloader`.

* `fastboot flash userdata out/target/product/c6503/userdata.img`
* `fastboot flashall`

Reflashing userdata is not necessary every time, but incompatibilities with
previous content might result in a device that doesn't boot. If this happens
try to reflash just the userdata again.
