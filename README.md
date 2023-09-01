# Wallpunch 3C: Cross-Platform VPN Client Monorepo

Wallpunch 3C (the "Common C Core") is a single repository containing basic VPN client projects for iOS, Mac, Android, and Windows[^1] which share a custom, cross-platform VPN protocol implemented in C. This repo is intended as a simple working example to share the overall framework with the community. *It DOES NOT contain the actual Wallpunch protocol or UI source code.*

## Motivation

As a single developer creating a new VPN for several different platforms, my key motivators for structuring the code in this fashion were 1) to maximize the amount of code I could reuse across clients and 2) to minimize the manual effort needed to build a new version of the clients for all platforms.

During the development process I spent a lot of time searching for and reading through guides and example implementations for each platform. However, all of the resources I found were extremely outdated and required considerable reworking to run on modern IDEs. I hope by publishing this repo and the associated client development guides I can save future VPN developers the pain and suffering of figuring out basic system interfaces and let them focus on the interesting aspects of VPN development - creating more robust protocols and more effective UIs.

Putting together the simplified repo and guides also helped me improve the framework and deepened my understanding of the underlying concepts. Plus if it becomes popular some extra traffic to the Wallpunch site won't hurt! If you're in China and need a VPN [please give Wallpunch a try ;)](https://wallpunch.net)

## Host (Development) Platform

This repo was created on an Intel Mac running Monterey (12.6.7). It won't work on Windows/Linux and may not even work on the newer Apple silicon Macs. As far as I know Xcode can only run on Mac so it isn't possible to create a functioning monorepo with iOS/Mac clients on any other platform anyway.

## Target (Client) Platforms

- `iOS` - iOS >=14.0. Xcode 14.1 is used for building/publishing.
- `Mac` - macOS >=11.0. Xcode 14.1 is used for building/publishing.
- `Android` - Android API level >=26. Android Studio Dolphin (2021.3.1) is used for building/publishing.
- `Windows` - Windows 10 and 11. Building/publishing is done via Visual Studio 2022 on a VM running Windows 10.

## Usage

- Use `make` to propagate any changes in the core protocol code to the client projects.
- Client projects should open and build in their respective IDEs[^2] directly out of the box but may require some tweaking if your development environment is different than mine.

## 3C VPN Protocol

:warning: **A VERY simple protocol is implemented to demonstrate functionality only and is not suitable for any sort of real-world use. It contains no encryption, authentication, or authorization!**

Clients are initialized from the UI with a server IP address and port number. The client creates a VPN interface, reads packets from the device, discards any non-IPv4 packets, and sends them via UDP to the server. The server receives the packets, opens a raw socket, sends out the packets, and sends back any replies. The client then writes the return packets to the VPN interface.

## More Information

Detailed guides explaining the overall framework architecture and specific client implementations can be found on the Wallpunch website:
- Wallpunch 3C Overview (Coming Soon...)
- iOS Client Guide (Coming Soon...)
- Mac Client Guide (Coming Soon...)
- Android Client Guide (Coming Soon...)
- Windows Client Guide (Coming Soon...)

[^1]: I will make a Linux version eventually but it is low priority for me because almost none of my potential customers use Linux.
[^2]: I would love to hear ideas on how to further automate things so no manual IDE operation is required for building/publishing.
