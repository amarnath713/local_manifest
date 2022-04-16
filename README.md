# local_manifest
 
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
<remote name="xenxynon"
                fetch="https://github.com/xenxynon" />
        <remote name="XS"
                fetch="https://github.com/XenStuff" />
        <remote name="prpr"
                fetch="https://github.com/ImPrashantt" />
 <!-- device trees -->
  <project path="device/xiaomi/lavender" name="device_xiaomi_lavender-p" remote="XS" revision="aosp" />
        <project path="vendor/xiaomi/lavender" name="vendor_xiaomi_lavender-p" remote="XS" revision="12" />
        <remove-project name="vendor_aosp" /> <project path="vendor/aosp" name="vendor_aosp" remote="XS" revision="one" />
        <project path="vendor/aosp" name="vendor_aosp" remote="XS" revision="twelve-plus" /> 
 <!-- kernel -->
  <project path="kernel/xiaomi/lavender" name="android_kernel_xiaomi_lavender-LTO" remote="prpr" revision="eas-caf" clone-depth="1" />

 </manifest>
 Build.Sh
# sync rom
repo init --depth=1 --no-repo-verify -u https://github.com/PixelExperience/manifest -b twelve -g default,-mips,-darwin,-notdefault
git clone https://github.com/XenStuff/manifest --depth=1 -b pe3 .repo/local_manifests
repo sync -c --no-clone-bundle --no-tags --optimized-fetch --prune --force-sync -j8
 # build rom
source build/envsetup.sh
lunch aosp_lavender-userdebug
export TZ=Asia/Kolkata #put before last build command
mka bacon
 
