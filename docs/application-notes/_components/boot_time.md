## **Optimize boot time**

!!! note 
    The command in the box above will be executed on the **Board u-boot's console**.

In this release, we provide some tips that help you to reduce the boot time. Please follow the steps below to reduce boot time:

* Disable console log (user won’t see console log when booting):

    ```bash
    editenv bootargs
    edit: loglevel=0
    ```
    {: .diamond2}

* Disable boot animation

    ```bash
    editenv bootargs
    edit: loglevel=0 androidboot.nobootanimation=1
    ```
    {: .diamond2}

* Reduce boot delay

    ```bash
    setenv bootdelay 1
    ```
    {: .diamond2}

* Save changes

    ```bash
    saveenv
    ```
    {: .diamond2}

With the above changes, boot time will be reduced by around 10 seconds.
