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
  - Select `python3`
  - Click the `Modify` button

## On Linux

#### Prerequisites
 - `apt install python3 git g++ gcc`

---

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
### Local config
You can override settings provided by the config from the repository with local values.

- `(py.exe|python3) openbuild.py --branch main --target windows-cl-msvc2022-x86_64 -config-override ./override.ini -- opencloud-desktop`

**override.ini**
```ini
[GeneralSettings]
# Use the system defaul keychain
CodeSigning/MacKeychainPath=${Env:HOME}/Library/Keychains/login.keychain
# Enable code signing
CodeSigning/Enabled=True
# Don't ask for a password for the keychain
CodeSigning/Protected=False

[BlueprintSettings]
opencloud/opencloud-desktop.revision=v3.0.3
opencloud/opencloud-desktop.buildNumber=2073
opencloud/opencloud-desktop.buildBeta=False
opencloud/opencloud-desktop.forceAsserts=False

[macos-clang-x86_64]
# Create .pkg packages instead of a .dmg
Packager/PackageType = MacPkgPackager

[macos-clang-arm64]
# Create .pkg packages instead of a .dmg
Packager/PackageType = MacPkgPackager
```

### Run the local build
A local build that is not packaged is not fully deployed yet, in order to execute it correctly you have to start it through Craft.
You can do that either by sourcing an environment:
- **Powershell** `./main/macos-clang-arm64/craft/craftenv.ps1`
- ***Shell script*** `. ./main/macos-clang-arm64/craft/craftenv.sh`
- and then start OpenCloud `opencloud -s`
 - on MacOS the binary path must be fully qualified: - `./Applications/KDE/OpenCloud.app/Contents/MacOS/OpenCloud -s`
or by asking Craft to run the application:
- `(py.exe|python3) openbuild.py --branch main -- --run opencloud -s`
