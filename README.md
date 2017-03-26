# android_device_huawei_kiwi

To build recovery for Honor 5x device (kiwi), follow these steps:

You will need minimal manifest, we will use omni sources https://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni

First initialize the repo (we will use twrp-7.1 branch):

repo init -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-7.1


Next you will need the device tree in order to compile the recovery, https://github.com/TeamWin/android_device_huawei_kiwi

To automate the process, you can creat kiwi.xml manifest and place it in .repo/local_manifests directory.

copy the following code to kiwi.xml file:

<?xml version="1.0" encoding="UTF-8"?>
<manifest>
    <project name="TeamWin/android_device_huawei_kiwi" path="device/huawei/kiwi" remote="github" revision="android-7.1" />
    <project name="LineageOS/android_kernel_huawei_kiwi" path="kernel/huawei/kiwi" remote="github" revision="cm-14.1" />
    <project name="LineageOS/android_vendor_qcom_opensource_cryptfs_hw" path="vendor/qcom/opensource/cryptfs_hw" remote="github" revision="cm-14.1" />
</manifest>

When you use repo sync, all the sources needed for building will be downloaded automatically for you!

This device tree uses prebuilt kernel and dt images with f2fs support for kiwi.

Backported stable 3.10.y f2fs changes were pulled from:

https://github.com/LineageOS/android_kernel_cyanogen_msm8916/commit/16a2a86b1869fb3c7e9502b7cb5593258516f64c


If you choose to have the kernel compiled and images built at the time the recovery is created you will need to uncomment,

TARGET_USES_UNCOMPRESSED_KERNEL := true
TARGET_KERNEL_CONFIG := kiwi-64_defconfig

in device/huawei/kiwi/BoardConfig.mk. To proceed with compilation of the recovery image issue:

mka recoveryimage or mka -jX recoveryimage where X is the number of jobs (cpu cores you want to use to speedup compile time).


Good luck and happy building!