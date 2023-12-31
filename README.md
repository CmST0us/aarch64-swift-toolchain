# arm64-swift-toolchain
Swift Toolchian for arm64-linux-gnu

# Current support Swift version

* `5.9` (recommend)

# How to install in macOS host

Firstly you need to install official swift version `5.9`, download it from https://swift.org

Create `Destinations` folder in `/Library/Developer` if there is not exist.

Create `Runtimes` folder in `/Library/Developer` if there is not exist

`mkdir -p /Library/Developer/Destinations`
`mkdir -p /Library/Developer/Runtimes`

Copy destinations file
`cp Destinations/macos/arm-none-linux-gnueabihf-*.json /Library/Developer/Destinations`

Decompression file `swift-5.9-runtime-aarch64-none-linux-gnu` into `/Library/Developer/Runtimes` 

```
mkdir -p /Library/Developer/Runtimes/swift-5.9-runtime-aarch64-none-linux-gnu
tar xf swift-5.9-runtime-aarch64-none-linux-gnu.tar.gz -C /Library/Developer/Runtimes/swift-5.9-runtime-aarch64-none-linux-gnu
```

# How to install runtime in linux target

You need to upload runtime libraries into you arm64 linux device.
```
scp -r /Library/Developer/Runtimes/swift-5.9-runtime-aarch64-none-linux-gnu/usr/lib/swift/linux <username>@<target_host>:<install_path>

```

Login to your target device, add `<install_path>` to you ldconfig search path, than use `ldconfig` to update


# How to build

Create an example project

```
swift package init --type executable
swift build --destination /Library/Developer/Destinations/aarch64-none-linux-gnu-5.9.json
```

Build Static
```
swift package init --type executable
swift build --destination /Library/Developer/Destinations/aarch64-none-linux-gnu-5.9-static.json --static-swift-stdlib
```

After building success, you can upload binary to you target device, and run it.


# Cxx Support

**Cxx Support is disabled**



--------------
`Have fun and play with Swift!`
