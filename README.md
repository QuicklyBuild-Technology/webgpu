# webgpu

This is a WebGPU API for native JavaScript, based on a [Fork](https://github.com/maierfelix/dawn-ray-tracing) of Chromium's [Dawn Project](https://dawn.googlesource.com/dawn/).

### Platforms:

This project comes with pre-built N-API binaries for the following platforms:

|       OS      |     Status    |
| ------------- | ------------- |
| <img src="https://i.imgur.com/FF3Ssp6.png" alt="" height="16px">  Windows       | ‌‌ ‌‌ ‌‌ ‌‌ ‌‌ ‌‌ ✔ ‌‌ ‌‌ ‌‌ ‌‌ ‌‌ ‌‌|
| <img src="https://i.imgur.com/bkBCY7V.png" alt="" height="16px">  Linux         | ‌‌ ‌‌ ‌‌ ‌‌ ‌‌ ‌‌ ‌‌ X ‌‌ ‌‌ ‌‌ ‌‌ ‌‌ ‌‌|
| <img src="https://i.imgur.com/iPt4GHz.png" alt="" height="16px">  MacOS         | ‌‌ ‌‌ ‌‌ ‌‌ ‌‌ ‌‌ ‌‌ X ‌‌ ‌‌ ‌‌ ‌‌ ‌‌ ‌‌|

## Installation
````
npm install webgpu
````

## Examples
````
cd examples & npm install & cd ..
node --experimental-modules examples/interactive-triangle.mjs
````

## TODOs
 - Add CTS
 - Get a build setup similar to Dawn?
 - Compile for Linux and MacOS
 - Rework GPUBuffer, mainly the mapping part
 - Research for a better Error callback system
 - Cleanup the code generator for descriptor decoding
 - Add ArrayBuffer neutering to GPUBuffer on unmapping ([this issue](https://github.com/nodejs/node-addon-api/issues/541) previously blocked me to add it)

## Building

You have to build [dawn](https://dawn.googlesource.com/dawn) as a shared library.
After building dawn, create a file named `PATH_TO_DAWN` in this project's root, containing the path to dawn.

Now in order to generate the bindings and build this project, run:
````
npm run all --dawnversion=0.0.1
````

### Windows

Follow dawn's initial setup instructions, but instead of the standard build, do the following:

To generate the project as a shared library using MSVS:
````
gn gen out/Shared --ide=vs --target_cpu="x64" --args="is_component_build=true is_debug=false is_clang=false"
````
It's important that you build using MSVS and **not** clang, as otherwise you will potentially get linking errors.

To build the project run:
````
ninja -C out/Shared
````

### Linux // TODO

### MacOS // TODO
