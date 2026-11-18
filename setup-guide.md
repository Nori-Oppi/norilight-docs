# Setup guide

Adapted for Norilight and Norishine from Moonlight's
[Setup Guide](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide), by the
Moonlight Game Streaming Project.

* [Quick setup](#quick-setup)
* [Streaming over the Internet](#streaming-over-the-internet)
* [Firewall setup](#firewall-setup)
* [Client setup](#client-setup)
* [Additional requirements for HDR streaming](#additional-requirements-for-hdr-streaming)
* [Keyboard, mouse and gamepad input](#keyboard-mouse-and-gamepad-input)
* [Adding programs](#adding-programs)
* [Streaming your entire desktop](#streaming-your-entire-desktop)
* [Troubleshooting](troubleshooting.md)

***

**Host gaming PC requirements**

For Norishine:
* Any modern GPU from AMD, NVIDIA or Intel
* Windows 10 or 11 (Windows 7 and 8 are *not* supported). Linux and macOS aren't supported yet.
* 5 Mbps or higher upload speed (only needed for streaming outside your house)

Norilight also streams from [Apollo](https://github.com/ClassicOldSong/Apollo),
[Vibepollo](https://github.com/Nonary/Vibepollo) and
[Sunshine](https://github.com/LizardByte/Sunshine) hosts. Norishine's own features (host
management, adaptive bitrate, Tuning) need Norishine.

There are [additional host PC requirements](#additional-requirements-for-hdr-streaming) for
streaming HDR content.

## Quick setup

### Using Norishine

More detail is in [Norishine's guide](https://github.com/Nori-Oppi/Norishine/blob/master/docs/GUIDE.md).

1. On your gaming PC, install the latest Norishine from its
   [nightly release](https://github.com/Nori-Oppi/Norishine/releases/tag/nightly). If Apollo or
   Vibepollo is installed, the installer can replace it (keeping its settings, apps and paired
   devices) or keep both. Your PC may need a reboot after installation to finish setup and for
   controller emulation to work.

2. Open the web UI at <https://localhost:47990/>, or with **Open Norishine** in the tray menu.
   Your browser shows a "this page is not secure" warning that you can safely ignore: Norishine
   makes its own certificate. (With Apollo or Vibepollo kept next to it, Norishine uses
   <https://localhost:48990/> instead.)

3. The first time, Norishine asks you to create an account to secure access to the web UI.
   This is important, as anyone with access to it can add new clients that control your
   computer remotely. The [setup wizard](https://github.com/Nori-Oppi/Norishine/blob/master/docs/GUIDE.md#first-start)
   follows: an optional import from Apollo or Vibepollo, the host name, virtual display or
   monitor, and an encoder check.

4. Start Norilight and make sure your client is on the same network as your PC. In most cases
   your gaming PC shows up in the PC list after a few seconds. You can also add a computer
   by its IP address with the **+** button if it doesn't show up or you're pairing over the
   Internet.

5. Click the PC in the list to start pairing. Norilight shows a PIN. On the host, the wizard's
   **First device** step (or the web UI's **Pairing** page later) lists the request: enter the
   PIN and press **Pair**, then choose what the device may do. If you get an error after
   entering the PIN, try the [troubleshooting steps](troubleshooting.md).

6. Try streaming a game or app to make sure everything works. If you run into problems, try
   the [troubleshooting steps](troubleshooting.md).

7. Norishine comes with Desktop and Steam Big Picture. You can
   [add other games and apps](#adding-programs) on the web UI's **Apps** page.

## Streaming over the Internet

### Automatic configuration

Norishine has a UPnP option that forwards the ports needed for streaming over the Internet:
in the web UI, open **Settings**, turn on **Show advanced settings**, and under **Network and
pairing** turn on **Open ports on the router automatically (UPnP)**. Your router must allow
UPnP.

For the easiest setup, **first pair Norilight with your gaming PC while on your home
network**, then try it over the Internet. For iOS and tvOS users of other Moonlight clients,
[you _must_ pair while on the same network](https://github.com/moonlight-stream/moonlight-ios/issues/417)
to comply with Apple guidelines.

#### Having trouble?

* Make sure UPnP is on in your router's settings, and delete any older port forwarding
  entries for Moonlight or another host.
* Try streaming from a different network. Some corporate or public Wi-Fi networks block
  streaming applications. If that happens, ZeroTier, Tailscale or NordVPN Meshnet (below) may
  work.
* If your router is behind a Carrier-Grade NAT or a second router, port forwarding can't
  work; use one of the options below.

### ZeroTier

[ZeroTier](https://www.zerotier.com/) is a service that acts like a VPN, but with better
performance in most cases.

It also lets you stream from several PCs that share one Internet connection. However, it
needs software on your hosts and clients that must be running and connected to stream over
the Internet, unlike the other options.

Use ZeroTier if:
* UPnP doesn't work because you're behind a Carrier-Grade NAT, you have two routers connected
  together, or it otherwise fails and you can't fix it yourself.
* You have several gaming PCs on your network that you'd like to stream from over the
  Internet.
* Streaming is blocked on the network you want to use.

To set it up:
1. [Create an account](https://my.zerotier.com/login) on the ZeroTier website. The free service
   is fine for Norilight.
2. Download the Windows version from the [Downloads page](https://www.zerotier.com/download/)
   and install it on your host gaming PC.
3. Install ZeroTier on your client device.
    * For Norilight on a PC or Mac, download and install it from the
      [Downloads page](https://www.zerotier.com/download/).
    * For Artemis or Moonlight on Android or iOS, the apps are in the
      [Google Play Store](https://play.google.com/store/apps/details?id=com.zerotier.one) and
      [Apple App Store](https://itunes.apple.com/us/app/zerotier-one/id1084101492).
4. Go to the [Networks tab](https://my.zerotier.com/network) and create a new network.
    * Uncheck all checkboxes in the "IPv6 Auto-Assign" section (if checked).
    * Under "IPv4 Auto-Assign", make sure "Auto-Assign from Range" is checked, click "Easy",
      then choose "10.147.17.*".
5. Copy the Network ID from that page and type it into the ZeroTier app's Join Network dialog
   (or use the e-mail invite system).
    * If Windows asks for the network type or location, choose Private or Home network to
      avoid firewall problems.
6. After joining the network on each device (_including the client running Norilight!_), go
   back to the ZeroTier Network page and **check the Auth checkbox for each member** so the
   devices can connect to each other. ZeroTier should show as connected on all devices.
7. With ZeroTier connected on the client and host, open Norilight, press **+**, and type the
   "Managed IP" of your host PC from the ZeroTier Network page.

To connect more clients or hosts, install ZeroTier on the device, then do steps 5 to 7.

Don't forget to connect to your ZeroTier network when you want to stream over the Internet!

### Tailscale

[Tailscale](https://tailscale.com) connects all your devices into a private network called a
Tailnet. Once a device is logged into your Tailscale account, it finds the most efficient way
to reach your other devices using
[NAT traversal](https://tailscale.com/blog/how-nat-traversal-works), then creates a secure
WireGuard tunnel between them, so they talk directly without extra latency.

1. **Create a free account:**
   [Sign up](https://login.tailscale.com/start) with an address from a public service like
   Gmail, Microsoft, GitHub or Apple. This makes you a
   [personal user](https://tailscale.com/pricing?plan=personal), free on up to 100 devices.
   Other e-mail domains may be treated as a company account with more restrictions.

2. **Install Tailscale on your devices:**
   [Download](https://tailscale.com/download) and install Tailscale on both the host and the
   client, and log in to the same account on each. They then show up on the
   [Machines page](https://login.tailscale.com/admin/machines), each with a `100.x.x.x` IP
   address, an IPv6 address and a DNS name.

3. **Test the connection:**
   On the host, open a Command Prompt and type `tailscale status` to list the devices in your
   Tailnet. For example, with "my-pc" and "my-laptop", the last column shows a dash (-) until
   the devices have talked to each other.
   ```sh
   > tailscale status
   100.xx.xx.xx   my-pc          email.account@ windows -
   100.xx.xx.xx   my-laptop      email.account@ windows -
   ```
   Then type `tailscale ping my-laptop` (or your device's name). Watch the ping times and
   whether the connection is direct or goes through a relay (DERP server). The first pings may
   use a relay while Tailscale sets up a direct connection; after a few seconds the devices
   should connect directly, with faster pings. A single reply means it was already direct.

   A successful direct connection:
   ```sh
   > tailscale ping my-laptop
   pong from my-laptop (100.xx.xx.xx) via DERP(nyc) in 28ms
   pong from my-laptop (100.xx.xx.xx) via DERP(nyc) in 25ms
   pong from my-laptop (100.xx.xx.xx) via 192.168.2.93:57324 in 0ms
   ```

   Rarely, a direct connection isn't possible and Tailscale keeps using a relay. Then you
   can't stream between these devices: Tailscale's relays are shared and rate-limited, and
   pushing a stream through them is rude and may get your device or account blocked.

4. **Connect with Norilight:**
   Once the devices connect directly, add the host in Norilight by its Tailscale `100.x.x.x`
   address or its ts.net name (`my-pc.tail12345.ts.net`) with **+**. Norilight links the
   address to the host's existing entry and shows it online. On a Norishine host the bitrate
   follows the network by itself; on a mobile network you may still want a lower resolution.

5. **Stay connected anywhere:**
   Some mobile networks block or disturb WireGuard's UDP packets (T-Mobile in the US has been
   known to), which can stop the connection.

6. **Other features:**
   Tailscale also offers custom subdomains, exit nodes and subnet routing. Subnet routing is
   for advanced users: another Tailscale node on your home network passes the packets between
   a PC without Tailscale and an outside client.

### NordVPN Meshnet

[Meshnet](https://nordvpn.com/meshnet/) is a feature of the NordVPN app that links devices on
different networks into a private network, so they connect as if they were on the same LAN.

It avoids port forwarding, works behind a Carrier-Grade NAT, and lets you stream from several
gaming PCs that share one Internet connection.

First, turn on Meshnet on your host gaming PC:
1. Create a free account on the [Nord Account sign-up page](https://nordaccount.com/signup). A
   NordVPN subscription isn't needed.
2. On your gaming PC, install the
   [NordVPN app](https://support.nordvpn.com/hc/en-us/articles/19472023025169-Installing-and-using-NordVPN-on-Windows-10-and-11).
3. Log in to NordVPN with your Nord account.
4. On the left, choose "Devices in Meshnet".
5. Turn on Meshnet.

You now see your gaming PC's Nord name and Meshnet IP address; either works in Norilight.

Then link your client device(s):
1. Install the NordVPN app on the client.
2. Log in to your Nord account.
3. [Turn on Meshnet](https://meshnet.nordvpn.com/getting-started/how-to-start-using-meshnet).

Your gaming PC now appears in the list of peer devices.

Finally, pair in Norilight:
1. In the NordVPN app, copy the Nord name of your gaming PC.
2. Open Norilight and press **+**.
3. Paste the Nord name and choose **OK**.

You can now pair and stream over the Internet. Meshnet must be on for this to work!

### Manual port forwarding (advanced)

If UPnP doesn't work, forward these ports on your router to your host gaming PC's IP address:
* **TCP** 47984, 47989, 48010
* **UDP** 47998, 47999, 48000, 48002, 48010

If Norishine runs next to Apollo or Vibepollo, its ports are 1000 higher (48984, 48989,
49010 and so on). Don't forward 47990 (the web UI) unless you know you need it.

If your router has separate "internal port" and "external port" options, set both to the same
value. For example, the forward for TCP 47989 has internal port 47989 and external port 47989.

To check the basic forwarding, visit https://www.canyouseeme.org/ and test ports 47984 and
47989; both should report "Success". The other ports are only open while streaming, so only a
stream can test them.

If Norilight already found your gaming PC on the same network, it connects over the Internet
without further steps. If not, open https://www.whatsmyip.org/ on your gaming PC and add the
address it shows in Norilight. If you don't get an error, you're all set. Also see
[Static DHCP reservation](#static-dhcp-reservation).

### Static DHCP reservation

On many routers you also need a static DHCP reservation, so the host always gets the same
address and the forwarded ports keep pointing at the right PC. Some routers do this by
themselves when you forward ports, many don't. Routers call it different things (static IP,
reservation, fixed IP) and put it in different places, often the DHCP settings, the client
list or the NAT/LAN settings. You're looking for a way to give one device a fixed address, by
its MAC address or from the client list.

### IPv6 (advanced, certain ISPs only)

If your host gaming PC has native IPv6, you can stream over IPv6 instead. This is only
recommended if you're comfortable with network administration.

1. Open http://test-ipv6.com/ on both your host PC and client to check their IPv6 scores.
    * If your host scores 0/10, look for an IPv6 option in your router settings. Make sure it's
      on and set to "Native", "Automatic", "DHCPv6" or similar; avoid "6to4" and "Teredo".
      Restart the router and test again. If you can't find the option or it doesn't work, ask
      your ISP whether they support IPv6.
    * If your host can't reach 10/10, you can't use this method with your ISP.
    * If your client scores below 10/10 but your host doesn't, the
      [Cloudflare 1.1.1.1 app](https://1.1.1.1/) with the free WARP feature can give the client
      IPv6 on networks that lack it.
2. In Norishine's web UI, open **Settings**, turn on **Show advanced settings**, and under
   **Network and pairing** turn on **IPv6**. Restart Norishine.
3. If your router has an IPv6 firewall, allow TCP ports 47984 to 48010 and UDP ports 47998 to
   48010 to your host PC through it. This is the most likely reason an IPv6 connection fails.
4. If Norilight already found your gaming PC on the same network, it connects over IPv6
   without further steps. Otherwise press **+** and type the host's IPv6 address.

## Firewall setup

If you can't stream even on the same network as your gaming PC, a firewall may be blocking it.
First, turn off the firewall on your gaming PC for a moment (usually Windows Firewall or one
built into your antivirus) to confirm that's the problem.

### Windows Firewall

Norishine's installer creates the Windows Firewall rules. If they don't work, create rules for
the streaming ports:
1. Open a Command Prompt or PowerShell window as administrator.
2. Run these 2 commands:
```
netsh advfirewall firewall add rule name="GameStream UDP" dir=in protocol=udp localport=5353,47998-48010 action=allow
netsh advfirewall firewall add rule name="GameStream TCP" dir=in protocol=tcp localport=47984,47989,48010 action=allow
```
3. Check that your PC now shows as online in Norilight.

### Other firewall software

For other firewalls, follow their instructions to allow these ports:
* **TCP** 47984, 47989, 48010
* **UDP** 5353, 47998, 47999, 48000, 48002, 48010

## Client setup

**Norilight**

* Windows 10 or 11 (x64): the installer or the ZIP from the
  [nightly release](https://github.com/Nori-Oppi/Norilight/releases/tag/nightly).
* macOS (Apple Silicon and Intel): the DMG from the same release. Nightlies are unsigned, so
  right-click the app and choose **Open** the first time, and allow Local Network access.
* Linux keeps Moonlight's build code but isn't built or tested yet.

Your PC should decode H.264 in hardware, or it has to decode on the CPU. Most PCs made since
around 2010 work fine, though older ones may not keep up with 60 FPS. On first start Norilight
asks how you'll use it and sets up a profile to match.

**Other clients**

Norishine works with any Moonlight-compatible client:
[Artemis](https://github.com/ClassicOldSong/moonlight-android) on Android (with Apollo and
Norishine extras), and Moonlight on Android, iOS, tvOS, ChromeOS and others.

**Network requirements**

For a good experience you need a mid to high-end router with a good wireless connection to
your client (5 GHz Wi-Fi 5 (802.11ac) or Wi-Fi 6 (802.11ax) strongly recommended), and a good
connection from your host PC to the router (Ethernet strongly recommended).

## Additional requirements for HDR streaming

HDR10 streaming works when the following hardware and software requirements are met. If they
aren't, the HDR option in the client may be grayed out or missing.

Known issues with HDR streaming:
- Some games and applications may show flashing color artifacts with HDR on.
- You may see scaling artifacts if the stream resolution doesn't match the host display's.
  With a virtual display, Norishine matches it to the client.
- If HDR is already on at the host when streaming starts, you may need to turn HDR off and on
  again on the host for the stream to switch to HDR.

**Host PC requirements**
- A Windows host with an NVIDIA, AMD or Intel GPU that can encode HEVC Main 10 (or AV1 10-bit)
- An HDR-capable display, an EDID emulator dongle, or Norishine's virtual display

The setup wizard's encoder check says whether your host can stream HDR.

**Windows client requirements (Norilight)**
- Windows 10 1703 (Creators Update) or later
- HDR10-compatible display
- A GPU that decodes HEVC Main 10 and outputs HDR10
  - Intel: 7th-generation (Kaby Lake) iGPUs and later
  - NVIDIA: 1000-series (Pascal) GPUs and later
  - AMD: RX 400-series (Polaris) GPUs and later
- HDR turned on in Windows for streaming in a window

With **Tuning: Quality**, Norilight turns HDR on by itself when the display has HDR on and both
PCs can do it.

**macOS client requirements (Norilight)**
- macOS Catalina or later
- See [Apple's documentation](https://support.apple.com/en-us/HT210980) for further
  requirements and recommendations

**Other clients**
- Android: Android 7.0 or later, an HEVC Main 10 hardware decoder and an HDR10 display
- iOS and Apple TV: iOS/tvOS 11.3 or later and an HDR10 display (on iOS, devices with "XDR"
  displays; on Apple TV, a TV that supports HDR10)

## Keyboard, mouse and gamepad input

**Norilight**

Norilight supports keyboard, mouse and touchscreen input and up to 4 game controllers (with
mappings for most common gamepads included; see [Gamepad mapping](gamepad-mapping.md)).
**Settings › Shortcuts** lists every keyboard and controller shortcut:

* Ctrl+Alt+Shift+Q: end the stream (the game keeps running on the host)
* Ctrl+Alt+Shift+E: end the stream and close Norilight
* Ctrl+Alt+Shift+Z: release the mouse and keyboard, or capture them again
* Ctrl+Alt+Shift+X: switch between fullscreen and a window
* Ctrl+Alt+Shift+D: minimize the stream window
* Ctrl+Alt+Shift+S: show or hide performance stats
* Ctrl+Alt+Shift+M: turn remote desktop mouse on or off
* Ctrl+Alt+Shift+C: show or hide this PC's cursor (remote desktop mouse)
* Ctrl+Alt+Shift+L: keep the cursor inside the stream window, or let it out
* Ctrl+Alt+Shift+K: send system keys like Alt+Tab to the host, or keep them here
* Ctrl+Alt+Shift+V: type this PC's clipboard text on the host
* Ctrl+Alt+Shift+R: list Apollo and Norishine server commands (1 to 9 runs one, Esc closes)

What a device may send (controller, keyboard, mouse, touch, pen) is set per device on the
host: in Norishine's web UI, open **Devices** and click the device.

**Touchscreen controls**

On a touchscreen, there are two modes: one uses the screen as a trackpad, the other passes
touches straight through.

Trackpad mode:
* Move the cursor: swipe across the screen.
* Left click: tap with one finger.
* Right click: hold one finger down and tap a second finger.
* Click and drag: hold one finger for about half a second, then drag.
* Scroll: drag 2 fingers vertically.

Touchscreen mode:
* Move the cursor and left click: tap where you want to click.
* Right click: hold where you want to right click.
* Click and drag: tap a spot and drag your finger across the screen.

**Other clients**

Artemis and Moonlight for Android, and Moonlight for iOS and tvOS, have their own controller
and mouse options; see the
[Moonlight Setup Guide](https://github.com/moonlight-stream/moonlight-docs/wiki/Setup-Guide#keyboardmousegamepad-input-options).

## Adding programs

You can stream almost any game or app by adding it on Norishine's **Apps** page: press
**Add app**, set **Command** to the program (quotes around a path with spaces), and optionally pick
an image or press **Find cover**. Details are in
[Norishine's guide](https://github.com/Nori-Oppi/Norishine/blob/master/docs/GUIDE.md#apps).
Norilight with **Manage** permission can add and edit apps too (gear on the host's tile ›
**Manage host**).

The next time the client shows the app list, the new app is there, ready to stream.

If quitting the game doesn't end the stream, press *Ctrl+Alt+Shift+Q* in Norilight to end it,
then right-click the app and choose **Quit Game** to close it on the host.

## Streaming your entire desktop

Norishine has a built-in **Desktop** app: pick it to see your whole desktop and run whatever
you want. An app with an empty **Command** streams the desktop too. With
**A virtual display** chosen in the setup wizard, the desktop opens on its own screen that
matches your client.

***
