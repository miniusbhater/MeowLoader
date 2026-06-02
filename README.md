# MeowLoader
### MeowLoader is a C++ plugin loader
<img width="577" height="428" alt="image" src="https://github.com/user-attachments/assets/6e9d89e8-08ae-4b5f-911b-3e8fe507a7a7" />

#### Supported languages:
 - C
 - C++
 - Rust
 - Zig
 - D
 - Anything that compiles to a native DLL and can export a C ABI function

## Creating plugins

### C++
Below is a very simple C++ plugin which logs when it loads and when it is unloaded
```#include "pch.h"
#include "MeowPlugin.h"

class PluginTemplate : public MeowPlugin
{
public:
    PluginInfo infoData =
    {
        L"My Plugin",                 // name
        L"1.0.0",                     // version
        L"MeowLoader Plugin Template" // description
    };

    PluginTemplate()
    {
        info = &infoData;
    }

    void OnLoad() override
    {
        LogMsg(L"Plugin loaded");           
    }

    void OnTick() override
    {
      
    }

    void OnShutdown() override
    {    
        LogMsg(L"Shutdown received");
    }
};

extern "C" __declspec(dllexport)
MeowPlugin* CreatePlugin()
{
    return new PluginTemplate();
}```
