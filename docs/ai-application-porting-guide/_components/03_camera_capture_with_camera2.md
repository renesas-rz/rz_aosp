## 3. Camera Capture with Camera2

Replace V4L2 with Android's Camera2 API. The fundamental difference is that V4L2 provides direct hardware access with minimal abstraction, while Camera2 routes everything through the Android Camera HAL. This means format negotiation works differently, and you may not get the exact pixel format your preprocessing expects. Depending on the camera, it might be possible to access the camera through a more low-level API if necessary. 

Start by obtaining a **CameraManager** to enumerate available cameras. USB cameras typically appear with the `LENS_FACING_EXTERNAL` characteristic. Once you've identified the correct camera, open it asynchronously using a **StateCallback** that runs on a thread.

```java
CameraManager manager = (CameraManager) getSystemService(CAMERA_SERVICE);
manager.openCamera(cameraId, stateCallback, backgroundHandler);
```

Use **ImageReader** to capture frames from the camera. Unlike V4L2's direct buffer access, Camera2 delivers frames through callbacks. Configure the ImageReader with your desired resolution and format, then register a listener:

```java
imageReader = ImageReader.newInstance(width, height, ImageFormat.YUV_420_888, 2);
imageReader.setOnImageAvailableListener(reader -> {
    Image image = reader.acquireLatestImage();
    // Process image
    image.close();  
}, backgroundHandler);
```

**Format Conversion Requirements:**

The Camera2 API typically outputs **YUV_420_888** regardless of what the camera hardware natively supports. If your pipeline expects a different format (like YUYV), you must implement a conversion layer. This adds overhead but is unavoidable when using the standard Android camera stack.

The conversion involves reading the Image's planar YUV data and repacking it into the interleaved format your preprocessing requires. Extract the Y, U, and V planes from the Image object, then interleave them according to your target format's specification. This typically adds a few ms per frame.
