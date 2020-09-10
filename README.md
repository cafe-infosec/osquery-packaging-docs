# osquery-packaging-docs
How to create Kolide launcher packages for Mac, Linux and Windows

## Pre-requisites 

These instructions were developed on a Mac with the `go` and `go-bindata` packages installed using Homebrew (brew.sh).

### *NIX

1. `git clone https://github.com/kolide/launcher.git`
2. `cd launcher`
3. run `make deps`
4. run `make package-builder`
5. change to the `build` directory
6. run `package-builder make --hostname fleet.example.com:443 --enroll_secret blahblah --update_channel stable -output_dir /Users/home/hilt/launcher/ -targets linux-systemd-deb` for linux packages
7. and `package-builder make --hostname fleet.example.com:443 --enroll_secret blahblah --update_channel stable -output_dir /Users/home/hilt/launcher/ for Mac packages

Note that in some cases I needed to specify package_version and also that you need docker to be able to build linux packages and the output, /tmp and /var/folders directory shared in the docker app for mac preferences.

### Windows

(this was copied from Just A Larry on the osquery slack, circa March 2020)

#### setup working dir

Using Chocolatey install additional packages
choco install wixtoolset
choco install make
choco install git
choco install golang

Copy the contents of C:\Program Files (x86)\WiX Toolset v3.11\bin to C:\wix311

Add C:\Program Files\Git\cmd to the Path system environment variable
setx path "%path%";"C:\Program Files\Git\cmd"

Add directory path for the git source code
cd C:\Go\src
mkdir \github.com\kolide

#### Clone Github Repo
cd github.com\kolide
git clone https://github.com/kolide/launcher.git

#### Compile launcher source
cd launcher
make deps
make generate
make

#### Test launcher
c:\Go\src\github.com\kolide\launcher\build\launcher -help
Compile package-builder source
cd c:\Go\src\github.com\kolide\launcher
make deps
make package-builder

#### Test package-builder
c:\Go\src\github.com\kolide\launcher\build\package-builder.exe make --help

#### Using package-builder.exe
cd c:\Go\src\github.com\kolide\launcher\build
package-builder make --hostname=your_kolide_url_here:443 --enroll_secret=<enroll_secret_here>
