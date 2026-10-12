# CSOPESY Desktop OS Emulator

A minimal desktop-style OS shell built with **Dear ImGui**, **GLFW**, and **OpenGL 3**. It simulates a convincing desktop environment with a wallpaper, a real-time clock, a taskbar, placeholder apps, and a Task Manager. It is a visual mockup, not a functional operating system.

**Author:** Azzam Alonto
**Group:** 3
**Course:** CSOPESY (Semi-Major Output 2)

---

## Features

- **Desktop:** Full-window gradient wallpaper with a real-time clock in the top-right corner, updated every frame.
- **Taskbar:** Fixed panel at the bottom of the screen with three toggle buttons:
  - **Notes:** placeholder text screen
  - **Settings:** placeholder screen with checkboxes and a brightness slider
  - **Task Manager:** table of processes with CPU and memory columns (dummy values)
- **PWR button:** Closes the application through the normal exit path, so cleanup runs. It does not force-quit.

## Technologies

| Tool | Purpose |
|------|---------|
| C++ | Programming language |
| Visual Studio 2022 | IDE and compiler (x64, Debug) |
| GLFW 3.5.1 | Window creation, OpenGL context, and input |
| OpenGL 3.0 | Graphics rendering |
| Dear ImGui | Immediate-mode user interface |
| `imgui_impl_glfw` / `imgui_impl_opengl3` | ImGui backends for GLFW and OpenGL |

## Project Structure

CSOPESY-Desktop-OS/

├── main.cpp # Application entry point, UI logic, and main loop
└── imgui/ # Dear ImGui core and backend files

## Prerequisites

- Windows 10 or 11
- Visual Studio 2022 with the **Desktop development with C++** workload
- [Dear ImGui](https://github.com/ocornut/imgui) source (download the ZIP)
- [GLFW 64-bit Windows binaries](https://www.glfw.org/download.html) (pre-compiled, not the source package)

## Setup

1. **Get the libraries**
   - Extract the Dear ImGui ZIP.
   - Extract the GLFW Windows binaries to a permanent folder, for example `C:\Libraries\glfw`.

2. **Create the project**
   - In Visual Studio 2022, create a new **Empty Project (C++)**.
   - Set the Solution Platform to **x64**.

3. **Copy the files**
   - Create an `imgui` folder inside the project directory.
   - Copy the core ImGui files (`imgui.h`, `imgui.cpp`, `imgui_draw.cpp`, `imgui_tables.cpp`, `imgui_widgets.cpp`, `imconfig.h`, `imgui_internal.h`, `imstb_rectpack.h`, `imstb_textedit.h`, `imstb_truetype.h`) into `imgui/`.
   - From `backends/`, copy `imgui_impl_glfw.h/.cpp` and `imgui_impl_opengl3.h/.cpp`, `imgui_impl_opengl_loader.h` into `imgui/`.
   - Copy `main.cpp` from the ImGui example `examples/example_glfw_opengl3/` into the project folder, then replace it with this project's `main.cpp`.

4. **Add files to the project**
   - Add the `imgui` files to Solution Explorer under an **ImGui** filter.
   - Add `main.cpp` to **Source Files**.

5. **Configure the project** (Properties, **All Configurations**, **x64**)
   - **C/C++ → General → Additional Include Directories:**
  
 $(ProjectDir)imgui;C:\Libraries\glfw\include

      Use the path to your own GLFW `include` folder, the one that directly contains the `GLFW` folder.
   - **Linking:** Add the GLFW library in `main.cpp` with a pragma, so the Linker property pages are not needed:
```cpp
     #pragma comment(lib, "opengl32.lib")
     #pragma comment(lib, "C:\\Libraries\\glfw\\lib-vc2022\\glfw3.lib")
```
     Update the path to match your GLFW folder.

## Build and Run

1. Set the toolbar to **Debug** and **x64**.
2. Choose **Build → Rebuild Solution** (or press `Ctrl+Shift+B`).
3. Run with **Ctrl+F5** (Start Without Debugging) or **F5**.

To close the application, click the red **PWR** button on the taskbar.

## Usage

| Control | Action |
|---------|--------|
| **Notes** | Opens or closes the Notes window |
| **Settings** | Opens or closes the Settings window |
| **Task Manager** | Opens or closes the Task Manager table |
| **PWR** | Shuts down the application |

## How It Works

The program follows an **immediate-mode, event-driven** loop:

1. **Initialize:** Start GLFW, create the window and OpenGL 3.0 context, then set up ImGui and its backends.
2. **Each frame:**
   - Poll input events with `glfwPollEvents()`.
   - Draw the gradient wallpaper and clock on the background draw list.
   - Draw the taskbar and handle button clicks. Each button flips a boolean flag.
   - Draw any open window whose flag is `true`.
   - Render the draw data and swap buffers.
3. **Cleanup:** Shut down the backends, destroy the ImGui context and window, then terminate GLFW.

The UI is a function of program state, so no separate widget tree is kept.

## Known Limitations

- Buttons use text labels instead of image icons.
- The Task Manager shows dummy data, not real process information.
- Windows cannot be dragged or resized in the taskbar's fixed layout.

## Troubleshooting

| Error | Fix |
|-------|-----|
| `Cannot open include file: 'GLFW/glfw3.h'` | Check the Additional Include Directories path. It must end at the folder that contains `GLFW`, not inside it. |
| `Cannot open include file: 'imgui.h'` | Make sure the `imgui` folder is in the project directory and `$(ProjectDir)imgui` is in the include path. |
| `unresolved external symbol` | Check the `#pragma comment(lib, ...)` path to `glfw3.lib`, and confirm the platform is x64. |
| Window does not appear | Make sure the build is **x64** and the GLFW library matches your platform. |

## License

This project is for academic use. Dear ImGui and GLFW are licensed under their own terms (MIT). See their repositories for details.
