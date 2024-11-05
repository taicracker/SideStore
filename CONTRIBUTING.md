# Contributing to SideStore

Thank you for your interest in contributing to SideStore! SideStore is a community driven project, and it's made possible by people like you.

By contributing to this Project (SideStore), you agree to the Developer's Certificate of Origin found in [CERTIFICATE-OF-ORIGIN.md](CERTIFICATE-OF-ORIGIN.md). Any contributions to this project after the addition of the Developer's Certificate of Origin are subject to its policy.

There are many ways to contribute to SideStore, so if you aren't a developer, there are still many other ways you can help out:

-   [Writing documentation](https://github.com/SideStore/SideStore-Docs)
-   [Submitting detailed bug reports and suggesting new features](https://github.com/SideStore/SideStore/issues/new/choose)
-   Helping out with support
    -   [Discord](https://discord.gg/sidestore-949183273383395328)
    -   [GitHub Discussions](https://github.com/SideStore/SideStore/discussions)

However, this guide will focus on the development side of things. For now, we will only have setup information here, but you can [join our Discord](https://discord.gg/RgpFBX3Q3k) if you need help
after setup.

## Requirements

This guide assumes you:

-   are on a Mac
-   have Xcode installed
-   have basic command line knowledge (know how to run commands, cd into a directory)
-   have basic Git knowledge ([GitHub Desktop](https://desktop.github.com) is a great tool for beginners, and greatly simplifies working with Git)
-   have basic Swift/iOS development knowledge

## Setup

1. Fork the SideStore repo on GitHub.
2. Clone the fork: `git clone https://github.com/<your github username>/SideStore.git --recurse-submodules`

    If you are using GitHub Desktop, refer to
    [this guide](https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/adding-and-cloning-repositories/cloning-and-forking-repositories-from-github-desktop).

3. Copy `CodeSigning.xcconfig.sample` to `CodeSigning.xcconfig` and fill in the values.
4. **(Development only)** Change the value for `ALTDeviceID` in the Info.plist to your device's UDID. Normally, SideServer embeds the device's UDID in SideStore's Info.plist during installation. When
   running through Xcode you'll need to set the value yourself or else SideStore won't resign (or even install) apps for the proper device. You can achieve this by changing a few things to be able to
   build and use SideStore.
5. Finally, open `AltStore.xcodeproj` in Xcode.

Next, make and test your changes. Then, commit and push your changes using git and make a pull request.

## Prebuilt binary information

minimuxer and em_proxy use prebuilt static library binaries built by GitHub Actions to speed up builds and remove the need for Rust to be installed when working on SideStore.
[`Dependencies/fetch-prebuilt.sh`](./Dependencies/fetch-prebuilt.sh) will be run before each build by Xcode, and it will check if the downloaded binaries are up-to-date once every 6 hours. If you want
to force it to check for new binaries, run `bash ./Dependencies/fetch-prebuilt.sh force`.

## Building an IPA for distribution

You can use the Makefile: `make build fakesign ipa`

This will create SideStore.ipa.

> **Warning**
>
> The binary created will contain paths to Xcode's DerivedData, and if you built minimuxer on your machine, paths to $HOME/.cargo. This will include your username. If you want to keep your user's
> username private, you might want to get GitHub Actions to build the IPA instead.

## Developing minimuxer alongside SideStore

Please see [minimuxer's README](https://github.com/SideStore/minimuxer) for development instructions.
