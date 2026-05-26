## **Optimize boot time**

In this release, we provide some tips that help you to reduce the boot time. Please follow the steps below to reduce boot time:

* Disable console log (user won’t see console log when booting):

    ```bash
    => editenv bootargs
    edit: loglevel=0
    ```

* Disable boot animation

    ```bash
    => editenv bootargs
    edit: loglevel=0 androidboot.nobootanimation=1
    ```

* Reduce boot delay

    ```bash
    => setenv bootdelay 1
    ```

* Save changes

    ```bash
    => saveenv
    ```

With the above changes, boot time will be reduced by around 10 seconds.

<span style="color:red">**Note:**</span> The command in the box above will be executed on the **Board u-boot's console**.
