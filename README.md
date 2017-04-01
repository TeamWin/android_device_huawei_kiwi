## TWRP device tree for Honor 5x (kiwi) ##
---------------

## Getting Started ##
---------------

To get started with OMNI sources to build TWRP, you'll need to get
familiar with [Git and Repo](https://source.android.com/source/using-repo.html).

To initialize your local repository using the OMNIROM trees to build TWRP, use a command like this:

`repo init --depth=1 -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-7.1`

or follow detailed instructions at [TWRP Git page](https://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni/tree/twrp-7.1).

## Build Intructions ##
---------------

Add to `.repo/local_manifests/kiwi.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
    <!-- device -->
    <project name="android_device_huawei_kiwi" path="device/huawei/kiwi" remote="TeamWin" revision="android-7.1" />
    <!-- kernel -->
    <!--<project name="LineageOS/android_kernel_huawei_kiwi" path="kernel/huawei/kiwi" remote="github" revision="cm-14.1" />-->
    <!-- cryptfs_hw -->
    <project name="LineageOS/android_vendor_qcom_opensource_cryptfs_hw" path="vendor/qcom/opensource/cryptfs_hw" remote="github" revision="cm-14.1" />
</manifest>
```

Then run `repo sync` to check it out.

To build:

```sh
. build/envsetup.sh
lunch omni_kiwi-eng
mka -j4 recoveryimage
```
