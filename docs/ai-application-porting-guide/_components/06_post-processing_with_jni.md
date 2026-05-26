## 6. Post-Processing with JNI

For performance-critical post-processing code, use JNI to call existing C++ implementations rather than rewriting in Java. This is particularly beneficial for preprocessing or postprocessing operations, like NMS or coordinate transformation, that involve loops over large datasets.

**Java Declaration:**

Declare native methods in your Java class and load the shared library. Create wrapper methods that prepare data for the native call and handle results. Here is a simple example function.

```java
public class ProcessingHelper {
    static {
        System.loadLibrary("your_native_lib");
    }
    
    private native float[] nativePostProcess(
        float[] modelOutput, 
        int outputSize,
        int imgWidth, 
        int imgHeight);
}
```

**Native Implementation:**

In your C++ code, implement the JNI function with the full mangled name that follows Java's package structure. Extract data from Java arrays using i.e **GetFloatArrayElements**, process it, and return results as Java objects.

```cpp
extern "C" {
JNIEXPORT jfloatArray JNICALL
Java_com_package_ProcessingHelper_nativePostProcess(
        JNIEnv *env, jobject thiz,
        jfloatArray input, jint size, jint width, jint height) {
    
    jfloat *inputData = env->GetFloatArrayElements(input, nullptr);
    
    float *results = new float[resultSize];
    
    // Process data...
    
    // Release Java array
    env->ReleaseFloatArrayElements(input, inputData, JNI_ABORT);
    
    // Create and return Java array
    jfloatArray outputArray = env->NewFloatArray(resultSize);
    env->SetFloatArrayRegion(outputArray, 0, resultSize, results);
    
    delete[] results;
    return outputArray;
}
}
```

**Memory Management Critical Points:**

Android's thread stack limit of 1MB will cause crashes if you allocate large arrays on the stack, so allocate them on the heap. Always release Java elements using i.e. **ReleaseFloatArrayElements** to prevent memory leaks. The JNI_ABORT flag tells the JVM you haven't modified the array, avoiding an unnecessary copy back.

For objects that persist across multiple frames (like pre-allocated buffers), consider creating them once and passing a handle (cast to `jlong`) between Java and C++. This eliminates per-frame allocation overhead.
