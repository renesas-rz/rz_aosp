## 1. Architecture Planning

Before starting, analyze your Linux application to determine what should be ported to Java and what stays in C++.

**Keep in C++ (via JNI):**
- CPU-intensive post-processing with heavy computation loops
- Complex algorithms that are difficult to rewrite
- Existing tested code with many dependencies
- Code that manipulates large data structures

**Port to Java:**
- Camera input and frame capture
- UI rendering and user interaction
- Application lifecycle and threading management
- TVM Runtime
- DRP-AI Driver calls (Use the Java driver HAL interface)

**Android Constraints:**

Android imposes several restrictions that differ from Linux environments. Thread stack size is limited to **1MB** by default, so large buffers must be allocated on the heap rather than the stack. File system access is sandboxed—applications cannot directly read files from arbitrary paths like `/home/user/`. Instead, resources must be bundled in the APK's assets folder and copied to internal storage. The camera is accessed through the Android HAL, which may require format conversions that weren't necessary with V4L2.
