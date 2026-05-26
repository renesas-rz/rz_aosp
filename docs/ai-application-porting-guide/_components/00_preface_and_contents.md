This guide walks through porting a Linux AI application to Android, covering the main architectural changes and platform-specific considerations.

## Contents

 - [1. Architecture Planning](#1-architecture-planning)
 - [2. Create the Android Project](#2-create-the-android-project)
 - [3. Camera Capture with Camera2](#3-camera-capture-with-camera2)
 - [4. TVM Runtime Integration](#4-tvm-runtime-integration)
 - [5. Handle Model Files](#5-handle-model-files)
 - [6. Post-Processing with JNI](#6-post-processing-with-jni)
 - [7. Visualization with OpenCV](#7-visualization-with-opencv)
 - [8. Threading and Lifecycle Management](#8-threading-and-lifecycle-management)
 - [Additional Considerations](#additional-considerations)
