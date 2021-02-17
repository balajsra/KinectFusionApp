# KinectFusionApp

This is a sample application using the [KinectFusionLib](https://github.com/chrdiller/KinectFusionLib). It implements 
cameras (for data acquisition from recordings as well as from a live depth sensor) as data sources. The resulting fused volume 
can then be exported into a pointcloud or a dense surface mesh.

## Dependencies

- **GCC**
  - Arch
    - `sudo pacman -S gcc`

- **CUDA 8.0** or higher. In order to provide real-time reconstruction, this library relies on graphics hardware. Running it exclusively on CPU is not possible.
  - Arch
    - `sudo pacman -S cuda`

- **OpenCV 3.0** or higher. This library heavily depends on the GPU features of OpenCV that have been refactored in the 3.0 release. Therefore, OpenCV 2 is not supported. Make sure you compile opencv with CUDA support.
  - Arch (AUR)
    - Install the `nvidia-sdk` package by following the instructions in the pinned comment on the [AUR page](https://aur.archlinux.org/packages/nvidia-sdk/).
    - `paru -S opencv-cuda`

- **Eigen3** for efficient matrix and vector operations.
  - Arch
    - `sudo pacman -S eigen`

- **OpenNI2** for data acquisition with a live depth sensor.
  - Arch (AUR)
    - `paru -S openni2`

- **RealSense**
    - Arch (AUR)
      - `paru -S librealsense`

- **cmake** for build system
  - Arch
    - `sudo pacman -S cmake`

## Prerequisites

- Adjust CUDA architecture: Set the CUDA architecture version to that of your graphics hardware. See [this](https://arnon.dk/matching-sm-architectures-arch-and-gencode-for-various-nvidia-cards/) for reference.
  - NVIDIA GeForce GTX 970
    ```cmake
    SET(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS};-O3 -gencode arch=compute_52,code=sm_52)
    ```
  - NVIDIA GeForce GTX 1070
    ```cmake
    SET(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS};-O3 -gencode arch=compute_61,code=sm_61)
    ```
- Tested with a nVidia GeForce 970, compute capability 5.2, maxwell architecture

- Set custom opencv path (if built from source):
    ```cmake
    SET("OpenCV_DIR" "/opt/opencv/usr/local/share/OpenCV")
    ```

## Build

- `git clone ...`
- `git submodule init`
- `git submodule update`
- `mkdir build`
- `cd build`
- `cmake ../`
- `make clean all`

## Usage

Copy data source to computer and setup data sources in `KinectFusionApp/config.toml`.
The full path to the rgbd images and parameters is: `data_path` + source/ + `recording_name`.

In the top level `KinectFusionApp` directory, run the binary and point it to the location of the config file: `./bin/KinectFusionApp -c KinectFusionApp/config.toml`.

Use the following keys to perform actions:
- `p` Export all camera poses known so far
- `m` Export a dense surface mesh
- ` ` Export nothing, just end the application
- `a` Save all available data

## License

This library is licensed under MIT.

## Acknowledgements

Original implementation of `KinectFusionApp` and `KinectFusionLib` done by [Christian Diller](https://github.com/chrdiller).
