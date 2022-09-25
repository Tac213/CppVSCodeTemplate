# CppVSCodeTemplate

A C++ template repository for VSCode, based on clang tool chain, with code linting and formatting enabled.

## Prerequisites

- Git
- CMake 3.19 (or more recent)

## Quick start

> If you don't have a tool chain, just skip this part.

1. Clone or download this repository, open it with VSCode.
2. Click `Yes` when VSCode ask you whether to install the recommended extensions.
3. Select a kit(tool chain), by clicking the button on the VSCode status bar, or pressing `Ctrl + Shift + P` and typing in `CMake: Select a Kit`.
4. Build the project, by clicing the button on the VSCode status bar, or pressing `F7`.
5. Open `main.cpp`, add a breakpoint, then press `F5`. The program should be run and the breakpoint should be hit.

## Best usage

### Install clang as tool chain

On Windows, download a build version of LLVM in [this website](https://github.com/brechtsanders/winlibs_mingw/releases/). Extract the downloaded file to any folder you like, for example `C:\softwares`, then you should get the `C:\softwares\mingw64` folder. Then add `C:\softwares\mingw64\bin` to `$PATH`.

On MacOS, install Xcode.

On Ubuntu, run following command lines.

```bash
wget https://apt.llvm.org/llvm.sh
chmod +x llvm.sh
sudo ./llvm.sh <version number> all  # for example, to install clang-13, run: sudo ./llvm.sh 13 all
```

With `llvm.sh`, clang should be install as clang-x, for example, clang-13. You can also set alias for convenience.

```bash
alias clang='clang-13'
alias clang++='clang++-13'
alias clangd='clangd-13'
alias clang-tidy='clang-tidy-13'
alias clang-format='clang-format-13'
```

### Install recommended extensions

Install the following extensions:

- [llvm-vs-code-extensions.vscode-clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd)
- [vadimcn.vscode-lldb](https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb)
- [ms-vscode.cmake-tools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools)
- [twxs.cmake](https://marketplace.visualstudio.com/items?itemName=twxs.cmake)

These extensions have been written in `.vscode/extensions.json`, you can also click `Yes` when VSCode ask you whether to install the recommended extensions, which makes it easier to install all the above extensions.

### Build and run

1. Select kit: press `Ctrl + Shift + P` and typing in `CMake: Select a Kit`, select clang as kit.
2. Configure project: press `Ctrl + Shift + P` and typing in `CMake: Configure`.
3. Build project: press `F7`.
4. Run and debug project: add breakpoints, then press `F5`.

You can also skip step 3. Just press `F5` to run, the project should be built before running.

## The configurables

### Code linting and formatting behavior

Just simply modify the `.clang-tidy` and `.clang-format` file in the root folder.

### Build directory

Default build directory is `${workspaceFolder}/build/${cmake:buildType}`. If you wanna change this configuration, open `.vscode/settings.json`, change the following 2 fields.

```json
{
  "cmake.buildDirectory": "${workspaceFolder}/build/${buildType}",
  "clangd.arguments": [
    "--compile-commands-dir=${workspaceFolder}/build/Debug",
    "--completion-style=detailed",
    "--header-insertion=never",
    "--background-index",
    "-j=12",
    "--clang-tidy"
  ]
}
```
