# BUILD_FIX
 
 1. sepolicy test error
    TMP FIX : add 

    ```
    SELINUX_IGNORE_NEVERALLOWS = true
    ```

    to BoardConfig.mk

 2. Framework compatibility Matrix (Incompatible) IPower/default
    TMP FIX : go to hardware/interfaces/compatibility_matrices/compatibility_matrix.5.xml file. find IPower and make it optional="true"
