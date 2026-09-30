## 8. Threading and Lifecycle Management

Android requires explicit thread management and proper cleanup to prevent resource leaks and crashes. Android applications must respond to lifecycle events and perform operations on appropriate threads.

**Background Thread Setup:**

Create dedicated **HandlerThread** instances for different tasks. The camera callback, inference processing, and DRP-AI operations should each run on separate background threads. Only UI updates should happen on the main thread.

```java
HandlerThread cameraThread = new HandlerThread("Camera");
cameraThread.start();
Handler cameraHandler = new Handler(cameraThread.getLooper());

HandlerThread inferenceThread = new HandlerThread("Inference");
inferenceThread.start();
Handler inferenceHandler = new Handler(inferenceThread.getLooper());
```

Post work to these handlers instead of running it directly. This prevents blocking the UI thread and allows Android to manage thread priorities appropriately.

```java
inferenceHandler.post(() -> {
    // Run inference
    Results results = processFrame(input);
    
    // Update UI on main thread
    runOnUiThread(() -> displayResults(results));
});
```

**Resource Cleanup:**

Implement proper cleanup in **onDestroy()** to release all resources when the application exits. This includes closing camera sessions, stopping background threads, releasing DRP-AI resources, and unbinding from services.

Close camera-related objects first, then stop threads by calling **quitSafely()** and waiting for them to finish with **join()**. Release PreRuntime and any native objects you created. Finally, unbind from the DRP-AI HAL service.

```java
@Override
protected void onDestroy() {
    // Close camera
    if (imageReader != null) imageReader.close();
    if (cameraDevice != null) cameraDevice.close();
    
    // Stop threads
    if (inferenceThread != null) {
        inferenceThread.quitSafely();
        try { inferenceThread.join(); } catch (InterruptedException e) {}
    }
    
    // Release preruntime
    if (preruntime != null) preruntime.close();
    
    // Release native resources
    if (nativeHandle != 0) nativeCleanup(nativeHandle);
    
    // Unbind service
    unbindService(halServiceConnection);
    
    super.onDestroy();
}
```
