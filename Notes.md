# MDL-SDK AMDGPU/LLVM Build Notes

## Steps Taken
- Copied the `AMDGPU` folder from the `llvm-project` branch `llvmorg-12.0.1`.

## Requirements
- Clang compiler (version 12.0.1):  
  [LLVM 12.0.1 Release](https://github.com/llvm/llvm-project/releases/tag/llvmorg-12.0.1)

## Build Recommendations
- **Always use out-of-source compilation** to avoid build failures.

## Example CMake Configuration
```cmake
-Dclang_PATH=D:/Sandbox/LLVM-src/12.0.1/from_inst/bin/clang.exe   # Path to Clang from LLVM installer
-DMDL_BUILD_DOCUMENTATION=OFF
-DDXC_DIR=C:/dxc_shader_compiler/dxc_2025_02_20                   # https://github.com/microsoft/DirectXShaderCompiler/releases/tag/v1.8.2502
-DQt5_Dir=C:/Qt/5.15.2/winrt_x64_msvc2019/lib/cmake/Qt5
```

## TODO

- Add ROCm 6.4 for Windows (for final IR compilation).
- Adjust the MDL LLVM backend to support different targets.
  - This requires enabling several additional LLVM libraries:
    - LLVMCoroutines
    - LLVMHelloNew
    - LLVMMIRParser
    - LLVMAMDGPUCodeGen
    - LLVMAMDGPUDesc
    - LLVMAMDGPUInfo
    - LLVMAMDGPUUtils
    - LLVMPasses
- Review the `_LLVM_LIB_NAMES` variable:
  - See `src/mdl/jit/llvm/CMakeLists.txt`
  - See `cmake/dependencies/add_llvm.cmake`
  - This set currently compiles.
- Note: There is also `_LLVM_EXCLUDE` which prevents some libraries from being compiled (see `src/mdl/jit/llvm/CMakeLists.txt`).
- Start with `example_compilation` to generate outputs for different backends.