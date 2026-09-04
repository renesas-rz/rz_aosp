## **Change SELinux mode**

SELinux mode is set "enforcing" mode as default. If you face any failure related to SELinux, try with "permissive" mode permanent by the following procedure.

1)  Turn on device and interrupt autoboot.

2)  Edit bootargs.

    => editenv bootargs

    # Add "androidboot.selinux=permissive" to bootargs as below example.

    Example:

    bootargs: init_time=xxxxxxxxxx androidboot.selinux=permissive

    => saveenv

If you only want to set SELinux mode temporary to "permissive" mode to run your application, we recommend using below commands:

*  On Ubuntu host PC, execute command:

```bash
adb root
adb shell setenforce 0	#Disable SELinux
adb shell setenforce 1	#Enable SELinux
```
{: .dollar }
