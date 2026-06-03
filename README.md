# MeowLoader <img width="32" height="32" alt="Logo" src="https://github.com/user-attachments/assets/2834de85-a703-4864-8c48-0b8f91245583" />


### MeowLoader is a plugin loader built in C++
<img width="579" height="427" alt="image" src="https://github.com/user-attachments/assets/f39a0066-2ad4-41a0-bb20-07efddf53dcb" />

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
```
#include "pch.h"
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
}
```
