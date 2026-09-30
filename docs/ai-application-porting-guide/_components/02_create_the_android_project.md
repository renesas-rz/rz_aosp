## 2. Create the Android Project

In Android Studio, select **"Native C++"** when creating a new project if you'll be using JNI. This automatically configures the NDK build system and creates the necessary folder structure.

Your project should follow this structure:
```
app/src/main/
├── assets/              # Model files and resources
├── cpp/                 # Native C++ code
│   ├── CMakeLists.txt
│   └── *.cpp
└── java/                # Android application code
```

Configure the **CMakeLists.txt** file to build your native code through Gradle. Link against required Android libraries like `log` for logging support.

```cmake
cmake_minimum_required(VERSION X.XX.X)
add_library(your_lib SHARED native_code.cpp)
target_link_libraries(your_lib android log)
```

Add the TVM Runtime library to your build by placing `drpruntime.aar` in the `app/libs/` folder and updating **build.gradle.kts**:
```gradle
dependencies {
    implementation(files("libs/drpruntime.aar"))
}
```
