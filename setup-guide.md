# Setup guide

You need two things: a **host**, the PC that runs the games, and a **client**, the device you
play on. Norishine is the host and Norilight the client. Norilight also works with Apollo,
Vibepollo and Sunshine hosts, and Norishine with Moonlight, Artemis and other compatible
clients.

## 1. Install Norishine on the host

1. Download the Windows x64 installer from Norishine's
   [nightly release](https://github.com/Nori-Oppi/Norishine/releases/tag/nightly) and run it.
   If Apollo or Vibepollo is installed, the installer can replace it (copying its settings,
   apps and paired devices) or keep both.
2. Open the web UI at <https://localhost:47990> on the host. Your browser warns about the
   certificate the first time: Norishine makes its own, so continue to the page.
3. Follow the setup wizard: sign-in, host name, display and an encoder check. Details are in
   [Norishine's guide](https://github.com/Nori-Oppi/Norishine/blob/master/docs/GUIDE.md#first-start).

The host needs a GPU that encodes video in hardware: NVIDIA GeForce GTX 900 series or newer,
AMD Radeon RX 400 series or newer, or Intel HD Graphics 500 series or newer. Without one it
falls back to the CPU, which is much slower.

## 2. Install Norilight on the client

Download Norilight from its
[nightly release](https://github.com/Nori-Oppi/Norilight/releases/tag/nightly): the
`-Setup.exe` or the ZIP on Windows, the DMG on macOS. On first start it asks how you'll use
it and sets up a profile to match.

## 3. Pair

1. In Norilight, the host should appear by itself within a few seconds. If it doesn't, press
   **+** and enter the host's IP address (on the host: `ipconfig`, the IPv4 address).
2. Click the host. Norilight shows a 4-digit PIN.
3. On the host's web UI, open **Pairing**, type the PIN and press **Pair**. Then choose what
   the device may do; the first paired device may start apps and send input.

Click the host again to see its apps, and pick **Desktop** or an app to stream.

## The host doesn't show up, or pairing fails

- **Both on the same network?** Discovery only works on the local network. A guest Wi-Fi or
  a separate VLAN keeps them apart; add the host by IP address instead.
- **Firewall.** The Norishine installer allows the host through Windows Firewall. Other
  firewalls or security suites need the same: TCP 47984, 47989, 47990 (web UI) and 48010,
  UDP 47998 to 48000 and 48010. If Norishine runs next to another host, its ports start at
  48989 instead; add the host as `<address>:48989`.
- **Is the host running?** If <https://localhost:47990> doesn't open on the host, start
  Norishine from the Start menu, or start the Norishine service.
- **Pairing request not on the Pairing page?** Wait a few seconds and check that the
  client was pointed at the right PC. A PIN only works for its own request.

## Streaming over the internet

Streaming outside your home network works best through a VPN that puts both devices on one
network, such as [Tailscale](https://tailscale.com) or [ZeroTier](https://www.zerotier.com):
install it on both, then add the host in Norilight by its VPN address. This avoids opening
ports on your router. Forwarding the ports above on the router works too, but exposes the
host to the internet. Expect a lower bitrate than at home; Norishine adapts it to the
network by itself.

## Next

- Something wrong with the stream: [Troubleshooting](troubleshooting.md)
- Norilight's features: [Norilight's guide](https://github.com/Nori-Oppi/Norilight/blob/main/docs/GUIDE.md)
- Host settings, apps and devices: [Norishine's guide](https://github.com/Nori-Oppi/Norishine/blob/master/docs/GUIDE.md)
