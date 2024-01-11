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