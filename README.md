# trimui-brick-dropbear-server.pak

A TrimUI Brick app wrapping [`dropbear`](https://matt.ucc.asn.au/dropbear/dropbear.html), an ssh server.

## Requirements

- Rust (for building)

## Building

> [!NOTE]
> TODO: Build this in docker. It currently uses the `dropbear` binary as distributed by the `Trimui_EX` project, but using that as a base isn't great.

```shell
make build
```

## Installation

> [!IMPORTANT]
> The dropbear binary **must** first be built for the TrimUI Brick.

1. Mount your TrimUI Brick SD card.
2. Create a folder in your SD card with the full-path of `/Tools/tg3040/Toggle SSH Server.pak`.
3. Copy `launch.sh`, `bin` and `res` to that SD card folder, ensuring it is still executable.
4. Unmount your SD Card and insert it into your TrimUI Brick.

## Usage

> [!NOTE]
> Due to not knowing the default root password, only `passwordless-root` mode works at this time.

### daemon-mode

To run dropbear in daemon mode, create a file named `daemon-mode` in the pak folder.

### passwordless-root

> [!WARNING]
> This app currently removes the root password on the device completely when running in `passwordless-root` mode. The password is not subsequently reset.

> [!TODO]
> This should instead use `mount -o` or something on `/etc/passwd` and `/etc/group`
> See this [commit](https://github.com/OnionUI/Onion/commit/175eb8278e7ec953405c4186535980b6abba9dc6#diff-d4c880409fa3390f8eb4c351c55b29767d309eea10ed79d9d206eee760f51c3c) for more details.

To allow access to the root user without specifying a password, create a file named `passwordless-root` in the pak folder.

### password

> [!NOTE]
> TODO: Implement me. Tina Linux does not come with `useradd` so we will potentially need to manipulate `/etc/passwd` and `/etc/shadow` directly.

Creating a file named `password` will result in the contents of that file being used as the password for the `trimui` user. If not specified, the password is set to `trimui`.