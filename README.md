# MeowLoader
# <img width="128" height="128" alt="Untitled (4)" src="https://github.com/user-attachments/assets/8be4412f-9727-4682-956e-d154385fd573" />


### MeowLoader is a plugin loader built in C++
<img width="579" height="427" alt="image" src="https://github.com/user-attachments/assets/f39a0066-2ad4-41a0-bb20-07efddf53dcb" />

#### Supported plugin languages:
 - C++
 - C
 - Rust
 - Anything that compiles to a native DLL and can export a C ABI function

   
## Using MeowLoader
<details>
  <summary><b>Injecting</b></summary>

  ## Injecting MeowLoader

Open `MeowInjector.exe` and then enter the executable name of any running program (without `.exe` on the end).

If it was successful you should be presented with the MeowLoader window and see this in the injector:

<img width="565" height="322.5" alt="image" src="https://github.com/user-attachments/assets/f0c85c18-b595-45af-a652-c7ec7424e0e3" />

## Troubleshooting

If you enter a program that isn't running or enter the incorrect executable name, the injection will fail.

For example, in this case `obs` was entered instead of `obs64`.

To find the correct executable name:

1. Open **Task Manager**.
2. Find the program you want to inject into.
3. Right-click the program.
4. Click **Open file location**.
5. Use the executable name shown there (without the `.exe` extension).

<img width="565" height="322.5" alt="image" src="https://github.com/user-attachments/assets/bea068e1-75fa-47bb-8942-33286a7f47ac" />

</details>

<details>
  <summary><b>Loading plugins</b></summary>
  
## Loading Plugins

Plugins can be placed inside the **Plugins** folder - located in the same directory as `MeowInjector.exe`.

If a plugin is placed here MeowLoader will automatically attempt to load it and you should be able to see it's name, title and description in the log.

You can have as many plugins as you want inside of the plugins folder.

You can also load plugins after MeowLoader is injected by clicking **Load Plugin** in MeowLoader and then selecting the plugin in the file explorer window that pops up.

## Loaded Plugins

Plugins that are loaded will log their info the the MeowLoader log and you should see something like this:

<img width="275" height="163" alt="image" src="https://github.com/user-attachments/assets/699175e7-dd0f-40ad-ae79-531c295e34bc" />

## Managing Plugins

Plugins can also be Enabled, Disabled, Unloaded and Reloaded by clicking the **Plugins** tab then selecting the plugin you want.

<img width="275" height="163" alt="image" src="https://github.com/user-attachments/assets/14c163dc-b3c2-4b0a-a419-0f84a83e5006" />

  </details>


<details>
  <summary><b>Errors</b></summary>

  | Error | Meaning |
|----------|-------------|
| `No plugins found` | No plugins were found in the `Plugins` folder |
| `Already loaded` | The plugin that tried to load is already loaded |
| `Missing CreatePlugin export` | The plugin that tried to load is missing its `CreatePlugin` export |
| `Failed to load plugin` | The plugin that tried to load failed |
| `Invalid plugin` | The plugin that tried to load is missing its metadata |
| `Cannot reload: source path unknown` | The plugin that tried to reload no longer exists in its original directory |
| `Exeption in OnLoad` | The plugin that tried to load has an issue in its OnLoad method |
| `Exeption in OnTick` | The plugin that tried to load has an issue in its OnTick method |
| `Exeption in OnShutdown` | The plugin that tried to load has an issue in its OnShutdown method |
| `Exeption in OnEnable` | The plugin that tried to load has an issue in its OnEnable method |
| `Exeption in OnDisable` | The plugin that tried to load has an issue in its OnDisable method |

  </details>


## Creating plugins

<details>
  <summary><b>Basic info</b></summary>

 ## Lifecycle methods

| Method | Description |
|----------|-------------|
| `OnLoad()` | Called when the plugin is loaded |
| `OnTick()` | Called every 16ms |
| `OnEnable()` | Called when the plugin is enabled with the enable button |
| `OnDisable()` | Called when the plugin is disabled with the disable button |
| `OnShutdown()` | Called when the plugin is unloaded |

## Plugin info

Every plugin must provide metadata through a PluginInfo structure.  
Example (C++):

```cpp
PluginInfo infoData =
    {
        L"My Plugin",         // name
        L"1.0.0",             // version
        L"MeowLoader Plugin"  // description
    };
```

## Logging

Plugins can write messages to the log.  
Example (C++):

```cpp
LogMsg(L"This is a log :3");
```

## Creating a plugin

Create a class that derives from `MeowPlugin`.  
Example (C++):

```cpp
class MyPlugin : public MeowPlugin
{
public:
    void OnLoad() override
    {

    }
};
```

Export a factory function.  
Example (C++):

```cpp
extern "C" __declspec(dllexport)
MeowPlugin* CreatePlugin()
{
    return new MyPlugin();
}
```

## Final notes

- Plugins must export `CreatePlugin()`.
- All strings use UTF-16.
  </details>

#### Code Templates
<details>
  <summary><b>C++</b></summary>

Below is a very simple C++ plugin which logs when it is loaded and when it is unloaded
```cpp
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

