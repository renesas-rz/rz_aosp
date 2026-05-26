## **Remount filesystem**

By default, “/system” partition and “/vendor” partition are read-only even if you run “adb remount” command. If you want to access/modify these partitions, please operate as below.

```bash
# On Ubuntu Host PC, execute command:
$ adb root              # Access with root
$ adb disable-verity    # Disable verity
$ adb shell reboot      # Reboot your devices
$ adb root              # Access with root
$ adb remount           # Remount filesystem
```

After remounting, you can access and modify files under “/vendor”, “/system” partition. This step is useful for debugging purpose.

