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
