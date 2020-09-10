# osquery-packaging-docs
How to create Kolide launcher packages for Mac, Linux and Windows

## Pre-requisites 

These instructions were developed on a Mac with the `go` and `go-bindata` packages installed using Homebrew (brew.sh).

### *NIX

1. download the source code for package-builder at https://github.com/kolide/launcher/releases
2. unzip the source and chdir to that directory
3. run `make deps`
4. run `make package-builder`
5. change to the `build` directory
6. run `package-builder make --hostname fleet.example.com:443 --enroll_secret blahblah --update_channel stable -output_dir /Users/home/hilt/launcher/ -targets linux-systemd-deb` for linux packages
7. and `package-builder make --hostname fleet.example.com:443 --enroll_secret blahblah --update_channel stable -output_dir /Users/home/hilt/launcher/ for Mac packages

Note that in some cases I needed to specify package_version and also that you need docker to be able to build linux packages and the output, /tmp and /var/folders directory shared in the docker app for mac preferences.
