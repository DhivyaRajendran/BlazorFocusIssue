# BlazorFocusIssue

### Bug:

There is no event handler associated with this event. EventId: '29'

blazor.webassembly.js:1 Uncaught (in promise) Error: System.ArgumentException: There is no event handler associated with this event. EventId: '29'. (Parameter 'eventHandlerId')
   at Microsoft.AspNetCore.Components.RenderTree.Renderer.DispatchEventAsync(UInt64 eventHandlerId, EventFieldInfo fieldInfo, EventArgs eventArgs)
   at Microsoft.AspNetCore.Components.WebAssembly.Rendering.WebAssemblyRenderer.DispatchEventAsync(UInt64 eventHandlerId, EventFieldInfo eventFieldInfo, EventArgs eventArgs)
   at Microsoft.AspNetCore.Components.WebAssembly.Rendering.WebAssemblyRenderer.ProcessNextDeferredEventAsync()
    at Object.endInvokeDotNetFromJS (blazor.webassembly.js:1)
    at Object.invokeJSFromDotNet (blazor.webassembly.js:1)
    at Object.w [as invokeJSFromDotNet] (blazor.webassembly.js:1)
    at _mono_wasm_invoke_js_blazor (dotnet.5.0.4.js:1)
    at do_icall (<anonymous>:wasm-function[10596]:0x194e4e)
    at do_icall_wrapper (<anonymous>:wasm-function[3305]:0x79df9)
    at interp_exec_method (<anonymous>:wasm-function[2155]:0x44ad3)
    at interp_runtime_invoke (<anonymous>:wasm-function[7862]:0x12efff)
    at mono_jit_runtime_invoke (<anonymous>:wasm-function[7347]:0x118e5f)
    at do_runtime_invoke (<anonymous>:wasm-function[3304]:0x79d42)
    
### Replication Procedure:
    
Steps to reproduce the behavior:

    1. Clone the below repository and run the sample.

    2. Navigate to FetchData.

    3. Click the Date Column.
    
    4. Then press tab key to navigate to next cell
    
    5. Thrown an above mentioned exception.
    
### Sample description:
 
 In the blazor sample we have created a table and bind click, keydown and blur event for th(table header cell) element, In Keydown event based on the key(like tab) we get the corresponding cell(current or next cell) and applied tabIndex and className(tab index as 0 and class as "e-focused").
 
 Then call focusElement method through JSRuntime.InvokeVoidAsync method. In Js function we get the correpsonding element from document and call focus method for the th (cell) element. In blur event also we have updated the className and tabIndex(tab index as 1 and class as empty string).
 
 ### Expected behavior
 
 Resolve this exception (exception thrown only when bind onblur event with handler in WASM application)
 
 ### Additional context
```
.NET SDK (reflecting any global.json):
 Version:   5.0.104
 Commit:    ca6b6acadb

Runtime Environment:
 OS Name:     Windows
 OS Version:  10.0.18363
 OS Platform: Windows
 RID:         win10-x64
 Base Path:   C:\Program Files\dotnet\sdk\5.0.104\

Host (useful for support):
  Version: 5.0.4
  Commit:  f27d337295

.NET SDKs installed:
  2.1.617 [C:\Program Files\dotnet\sdk]
  2.2.202 [C:\Program Files\dotnet\sdk]
  3.1.113 [C:\Program Files\dotnet\sdk]
  5.0.100 [C:\Program Files\dotnet\sdk]
  5.0.104 [C:\Program Files\dotnet\sdk]

.NET runtimes installed:
  Microsoft.AspNetCore.All 2.1.23 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
  Microsoft.AspNetCore.All 2.1.24 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
  Microsoft.AspNetCore.All 2.1.26 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
  Microsoft.AspNetCore.All 2.2.3 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
  Microsoft.AspNetCore.All 2.2.8 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
  Microsoft.AspNetCore.App 2.1.23 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 2.1.24 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 2.1.26 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 2.2.3 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 2.2.8 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 3.1.2 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 3.1.9 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 3.1.13 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 5.0.0 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.AspNetCore.App 5.0.4 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
  Microsoft.NETCore.App 2.1.23 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 2.1.24 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 2.1.26 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 2.2.3 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 2.2.8 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 3.1.2 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 3.1.9 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 3.1.13 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 5.0.0 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.NETCore.App 5.0.4 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
  Microsoft.WindowsDesktop.App 3.1.2 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]
  Microsoft.WindowsDesktop.App 3.1.9 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]
  Microsoft.WindowsDesktop.App 3.1.13 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]
  Microsoft.WindowsDesktop.App 5.0.0 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]
  Microsoft.WindowsDesktop.App 5.0.4 [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]

To install additional .NET runtimes or SDKs:
  https://aka.ms/dotnet-download
  
  ```


