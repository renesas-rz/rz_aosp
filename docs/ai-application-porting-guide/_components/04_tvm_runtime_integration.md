## 4. TVM Runtime Integration

The TVM Runtime is provided as **drpruntime.aar** with Java wrapper classes. Unlike Linux where you directly link against `.so` files, Android requires binding to a HAL service that provides access to the hardware.

**Service Binding:**

The DRP-AI HAL exposes its functionality through Android's AIDL (Android Interface Definition Language) service. You must bind to this service before you can use PreRuntime or JniRuntime. This binding happens asynchronously, so initialize DRP-AI in the service connection callback.

```java
Intent intent = new Intent().setComponent(new ComponentName(
    "vendor.renesas.hal.drpai",
    "vendor.renesas.hal.drpai.HalBindService"));
bindService(intent, connection, BIND_AUTO_CREATE);

private final ServiceConnection connection = new ServiceConnection() {
    public void onServiceConnected(ComponentName name, IBinder binder) {
        halService = IRenesasDrpai.Stub.asInterface(binder);
        // Now initialize DRP-AI on a background thread
        drpaiHandler.post(() -> initializeDrpai());
    }
};
```

**Initialization Process:**

Once the service is bound, create PreRuntime and JniRuntime instances. The PreRuntime constructor now requires the HAL service interface as a parameter. Load your preprocessing configuration from the model directory, then obtain the DRP-AI memory address and load your inference model.

```java
preruntime = new PreRuntime(halService);
preruntime.Load(preprocessDir);
long drpaiMemAddr = preruntime.GetDrpaiStartAddress();

runtime = new JniRuntime();
runtime.LoadModel(modelDir, drpaiMemAddr);
```

**Running Inference:**

The inference flow is similar to Linux, but note that you must call **GetOutputBuffer()** after preprocessing to retrieve the result buffer. This buffer then becomes the input for the inference stage.

```java
// Create preprocessing parameter with input data
PreRuntime.SPreprocParam param = preruntime.CreatePreprocParam(inputSize);
param.inputBuffer.put(inputData);

// Run preprocessing
preruntime.Pre(param, outBuffer, outSize);
ByteBuffer prepOutput = preruntime.GetOutputBuffer();  

// Run inference
FloatBuffer floatInput = prepOutput.asFloatBuffer();
runtime.SetInput(0, floatInput);
runtime.Run(frequencyParam);

// Retrieve outputs
JniRuntime.OutputData output = runtime.GetOutput(index);
```

All DRP-AI operations should run on a dedicated background thread, never on the UI thread. If processing runs on the UI thread it can cause the app to freeze.
