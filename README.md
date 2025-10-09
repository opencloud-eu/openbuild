# About
This repository contains a helper script to make it easier to setup a OpenCloud build environment.


# Required dependencies
- https://community.kde.org/Craft#Setting_up_Craft
## On Windows
### Visual Studio 2022
 - Start `Visual Studio Installer`
  - Select `Modify`
  - Select `Desktop development with C++`
  - Go to `Individual Components`
  - Select `git`
  - Select `python2`
  - Select `python3`
  - Click the `Modify` button

# Get started
- `(py.exe|python3) openbuild.py opencloud-desktop`

## Build a specific branch configuration
This will only affect the version of the dependencies, without providing `--branch` the `main` branch is used.
- `(py.exe|python3) openbuild.py --branch main -- opencloud-desktop`

## Build a specific client tag
- `(py.exe|python3) openbuild.py --branch stable-3.0 -- --set revision=v3.0.2 opencloud-desktop`
- `(py.exe|python3) openbuild.py --branch stable-3.0 -- opencloud-desktop`

## Use special craft commands
- `(py.exe|python3) openbuild.py --branch main -- --package opencloud-desktop`
- `(py.exe|python3) openbuild.py --branch main -- --run .\main\windows-cl-msvc2022-x86_64-debug\bin\opencloud.exe`


## Appendix
### Run with a specific target configuration
- `(py.exe|python3) openbuild.py --branch main --target windows-cl-msvc2022-x86_64`
### Query available targets
- `(py.exe|python3) openbuild.py --branch main --target help`


## On Linux

#### Prerequisites
 - `apt install python3 git g++ gcc`
 
### Build the client with opencloud dependencies

- `python3 ./openbuild.py --branch main --target linux-64-gcc opencloud-desktop`
- When built, start the client like this: `./main/linux-64-gcc/bin/opencloud -s`


