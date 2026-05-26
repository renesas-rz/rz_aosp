## 5. Handle Model Files

Assets bundled in the APK are compressed and cannot be accessed as regular files. The native code and TVM Runtime require actual file paths, so you must copy assets to internal storage on first run.

Implement a recursive copy function that checks each asset path. Android provides **getFilesDir()** for app-private storage that persists across app launches.

```java
File destDir = new File(getFilesDir(), "models");
if (!destDir.exists()) {
    AssetManager am = getAssets();
    // Copy recursively from assets to destDir
}
```

Store the absolute path to the copied model directory with something like `modelDir = new File(getFilesDir(), "yolov8n").getAbsolutePath();` and pass it to the TVM (pre)runtime. Check if files already exist before copying to avoid unnecessary copies after the first app launch. The internal storage path will be something like `/data/data/your.package/files/models/`, which can be passed directly to native code or Runtime.
