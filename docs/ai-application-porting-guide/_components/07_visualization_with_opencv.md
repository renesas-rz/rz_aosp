## 7. Visualization with OpenCV

OpenCV on Android uses Java bindings instead of the C++ API. The method names and class hierarchy are similar but adapted to Java conventions.

**Initialization:**

Load OpenCV at application startup. The `OpenCVLoader.initLocal()` method loads the native OpenCV library from your APK. 

```java
import org.opencv.android.OpenCVLoader;

if (!OpenCVLoader.initLocal()) {
    // Handle initialization failure
}
```

**Drawing Operations:**

Convert Android Bitmaps to OpenCV Mat objects using the **Utils** class. Drawing functions are in the **Imgproc** class rather than directly on Mat. 

```java
import org.opencv.android.Utils;
import org.opencv.imgproc.Imgproc;
import org.opencv.core.Scalar;

Mat mat = new Mat();
Utils.bitmapToMat(bitmap, mat);

// Draw rectangle
Imgproc.rectangle(mat, 
    new Point(x1, y1), 
    new Point(x2, y2),
    new Scalar(255, 0, 0), 
    thickness);

// Draw text
Imgproc.putText(mat, text, new Point(x, y),
    Imgproc.FONT_HERSHEY_SIMPLEX, scale, color, thickness);

// Convert back to Bitmap
Utils.matToBitmap(mat, resultBitmap);
```

For best performance, pre-allocate Mat objects and reuse them across frames rather than creating new ones each time. Bitmaps should be recycled when no longer needed to free up memory, especially when processing video frames continuously.
