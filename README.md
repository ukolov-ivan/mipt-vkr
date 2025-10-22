# Lax-Friedrichs Continuity Equation Solver

This project implements a numerical solver for the 1D continuity equation
using the Lax-Friedrichs finite difference method. It leverages Eigen for
efficient numerical computations and VTK for visualizing the simulation results.
Vcpkg is used for package management.

## Equation Solved

The solver addresses the 1D continuity equation:
$\frac{\partial \rho}{\partial t} + \frac{\partial (u\rho)}{\partial x} = 0$
where $\rho$ is the density and $u$ is the velocity.
For this template, a constant velocity $u$ is assumed, simplifying it to a
linear advection equation.

## Features

*   **Lax-Friedrichs Method:** Stable first-order accurate numerical scheme.
*   **Eigen Integration:** Efficient array and matrix operations for numerical data.
*   **VTK Visualization:**
    *   Generates `.vti` files (VTK Image Data) for visualization in tools like Paraview.
    *   (Optional) Interactive visualization window for real-time viewing.
*   **Vcpkg Package Management:** Easy setup of dependencies.

## Prerequisites

*   C++17 compatible compiler (e.g., GCC, Clang, MSVC)
*   CMake (version 3.10 or higher)
*   Git
*   Vcpkg

## Setup and Build Instructions

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/your-username/lax_friedrichs_continuity.git
    cd lax_friedrichs_continuity
    ```

2.  **Install Vcpkg (if you don't have it):**
    ```bash
    git clone https://github.com/microsoft/vcpkg.git
    cd vcpkg
    ./bootstrap-vcpkg.sh # Or bootstrap-vcpkg.bat on Windows
    ./vcpkg integrate install
    cd .. # Back to lax_friedrichs_continuity
    ```
    *Note: You can also use a system-wide vcpkg installation.*

3.  **Install Dependencies using Vcpkg:**
    Ensure you are in the `lax_friedrichs_continuity` directory.
    ```bash
    # For a Windows MSVC 64-bit build
    vcpkg install eigen3:x64-windows vtk[opengl2]:x64-windows

    # For a Linux/macOS build
    vcpkg install eigen3 vtk[opengl2]
    ```
    The `[opengl2]` feature for VTK is required if you want interactive visualization. If you only plan to output `.vti` files, `vtk` without `[opengl2]` might suffice, but `opengl2` is generally a safe default.

4.  **Configure and Build with CMake:**

    ```bash
    mkdir build
    cd build
    # If using local vcpkg:
    cmake .. -DCMAKE_TOOLCHAIN_FILE=../vcpkg/scripts/buildsystems/vcpkg.cmake

    # If using a system-wide vcpkg:
    # You might need to specify the path to your vcpkg toolchain file
    # cmake .. -DCMAKE_TOOLCHAIN_FILE="/path/to/your/vcpkg/scripts/buildsystems/vcpkg.cmake"
    # Or if 'vcpkg integrate install' was used, CMake might find it automatically.

    cmake --build .
    ```

## Running the Application

After a successful build, you can run the executable from the `build` directory:

```bash
cd build
./LaxFriedrichsContinuity
