# BUILD_FIX
 
 1. sepolicy test error
    TMP FIX : add 

    ```
    SELINUX_IGNORE_NEVERALLOWS = true
    ```

    to BoardConfig.mk

 2. Framework compatibility Matrix (Incompatible) IPower/default
    TMP FIX : go to hardware/interfaces/compatibility_matrices/compatibility_matrix.5.xml file. find IPower and make it optional="true"

 3. Not building zip file after build succesfull (Android 11)

    ```
    . build/envsetup.sh && lunch {your_target}
    ```
    ```
    mkdir dist_output
    ```
    ```
    make dist DIST_DIR=dist_output
    ```
    then
    ```
    make dist
    ```
    if zip not builded automatically

4. cannot find symbol error in xdroid caf 11
   
   # clone packages_services_Telecomm from PixelExperience first
   
   then

    ```
     replace RingtoneFactory in packages/services/Telecomm/src/com/android/server/telecom/RingtoneFactory.java with included file inside repo
    ```

5. Dex2Oat failed to compile
   ```
   ERROR: Dex2oat failed to compile a boot image.It is likely that the boot classpath is inconsistent.Rebuild with ART_BOOT_IMAGE_EXTRA_ARGS="--runtime-arg -verbose:verifier" to see verification errors.   
   ```
   So after some digging AOSP code I've came up with this workaround. Note that I don't think its a solution - just a workaround. Basically it figures out that WITH_DEXPREOPT is overriden in build scripts. In my AOSP version it was in
   build/core/board_config.mk

   Workaround:

   In build/core/board_config.mk set WITH_DEXPREOPT to false build/core/board_config.mk
   Silence the error in build/core/dex_preopt_config.mk by removing 
   ```
   $(call pretty-error, DEXPREOPT must be enabled for user and userdebug builds) 
   ```
   build/core/dex_preopt_config.mk

6. fix JVM target error
   ```
   error: cannot inline bytecode built with JVM target 11 into bytecode that is being built with JVM target 1.8. Please specify proper '-jvm-target' option
   ```
   edit android/build/soong/java/kotlin.go and find "func kotlinCompile" then change
   ```
   "kotlinJvmTarget":   flags.javaVersion.StringForKotlinc(),
   ```
   To
   ```
   "kotlinJvmTarget": "11",
   ```
