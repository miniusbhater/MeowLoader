# MeowLoader
# <img width="128" height="128" alt="Untitled (4)" src="https://github.com/user-attachments/assets/8be4412f-9727-4682-956e-d154385fd573" />


### MeowLoader is a plugin loader built in C++
<img width="579" height="427" alt="image" src="https://github.com/user-attachments/assets/f39a0066-2ad4-41a0-bb20-07efddf53dcb" />

#### Supported plugin languages:
 - C++
 - C# (With MeowSharpBridge)
 - C
 - Rust
 - Anything that compiles to a native DLL and can export a C ABI function

   
## Using MeowLoader
<details>
  <summary><b>Injecting</b></summary>

  Open MeowInjector.exe and then enter the process name of any running program (without .exe on the end)

  If it was successful you should be presented with the MeowLoader window and see this in the injector
  <img width="565" height="322.5" alt="image" src="https://github.com/user-attachments/assets/f0c85c18-b595-45af-a652-c7ec7424e0e3" />

  

  </details>



## Creating plugins

<details>
  <summary><b>C++</b></summary>

Below is a very simple C++ plugin which logs when it is loaded and when it is unloaded
```
#include "pch.h"
#include "MeowPlugin.h"

class PluginTemplate : public MeowPlugin
{
public:
    PluginInfo infoData =
    {
        L"My Plugin",         // name
        L"1.0.0",             // version
        L"MeowLoader Plugin"  // description
    };


    PluginTemplate()
    {
        info = &infoData;
    }

    void OnLoad() override
    {
        // code here runs when the plugin is loaded    
    }

    void OnTick() override
    {
      // code here runs every tick
    }

    void OnEnable() override
    {
        // code here runs when the plugin is enabled
    }

    void OnDisable() override
    {
        // code here runs when the plugin is disabled
    }

    void OnShutdown() override
    {     
        // code here runs when the plugin is unloaded
    }
  
};

extern "C" __declspec(dllexport)
MeowPlugin* CreatePlugin()
{
    return new PluginTemplate();
}

```
</details>

