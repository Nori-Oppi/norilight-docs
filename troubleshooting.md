# Troubleshooting

Start with the error message: most say what failed. Then find the closest problem below. If
nothing helps, open an issue on
[Norilight](https://github.com/Nori-Oppi/Norilight/issues) or
[Norishine](https://github.com/Nori-Oppi/Norishine/issues) with both logs (see [Logs](#logs)).

## The stream doesn't start

- **"Permission denied"** when starting an app: the host only lets this device watch. On the
  host's web UI, open **Devices**, click the device and choose **Play** or **Full control**.
- **The connection times out**, or Norilight reports blocked ports: a firewall drops the
  stream. Allow the ports from the [setup guide](setup-guide.md#the-host-doesnt-show-up-or-pairing-fails),
  on the host and on any firewall between the two.
- **"An app is already running"**: another device's stream, or a stream that didn't end
  cleanly. Quit the app from Norilight (right-click it, **Quit Game**) or use **Close the running
  app** on the host's Troubleshooting page.
- **Black screen, then the stream ends**: the host couldn't capture its display. Usually the
  display is off or asleep, or a virtual display couldn't be created. Restart Norishine from
  its Troubleshooting page, and check its log for the capture error.
- **Nothing works after a host update or a crash**: restart the host (Troubleshooting page,
  **Restart Norishine**).

## The stream stutters or lags

1. Turn on the performance stats in Norilight (Ctrl+Alt+Shift+S) and look at what's high:
   - **Frames dropped by the network** or a high round-trip time: the network. Use a cable
     instead of Wi-Fi for at least one of the two, use 5 GHz Wi-Fi, or lower the bitrate.
     On a Norishine host the bitrate already follows the network; **Host bitrate** shows it.
   - **Host busy**: the host's GPU or CPU can't keep up. Lower the resolution or frame rate,
     or close what else runs on the host.
   - **Decoder busy** or a high decode time: this device can't keep up. See
     [Fixing hardware decoding problems](hardware-decoding.md), or choose a lower
     resolution or the H.264 codec.
2. Try **Tuning: Performance** in the profile (Settings, Video quality). It picks settings
   for the lowest latency.
3. With V-Sync off, motion can look uneven; turn on V-Sync and frame pacing for smoother
   motion at a little more latency.

## The picture looks wrong

- **Blurry or blocky**: the bitrate is too low for the resolution, often because the
  network forced it down. Raise the bitrate in the profile, or improve the network.
- **Washed-out or too dark with HDR**: HDR has to be on in Windows on both PCs, and the
  client display must support it. Turn HDR off in the profile to compare.
- **Wrong resolution or black bars**: set the resolution in the profile, or give the device
  a fixed **Display mode** on the host (Devices, the device, Display). With a virtual
  display the host follows the client's resolution by itself.

## Sound

- **No sound**: check the audio device the host plays to (Norishine's audio settings) and
  the volume on both PCs. Some apps only pick their audio device when they start, so
  restart the app.
- **Crackling**: usually the network or a busy host, as with stutter above.

## Input

- **Mouse or keyboard doesn't work**: the device may not be allowed to send it (host's
  Devices page, **Fine-tune**). Ctrl+Alt+Shift+Z captures the mouse and keyboard again.
- **Controller isn't seen or its buttons are wrong**: see [Gamepad mapping](gamepad-mapping.md).
- **Input stops in some games or on the sign-in screen**: Windows keeps input from programs
  that aren't running as administrator away from these. The installed Norishine runs as a
  service, so this works; a host started by hand has to run as administrator too.

## Logs

- **Norilight**: `Norilight-<time>.log` in the temp folder (`%TEMP%` on Windows), or next to
  `Norilight.exe` for the ZIP version.
- **Norishine**: the Troubleshooting page in the web UI shows the log; **Download** saves it.

## Starting over

Both can be reset without losing anything: the settings move to a dated backup and the
first-start wizard opens again. Clients have to pair again afterwards.

- Norilight: **Settings › Network & diagnostics › Reset Norilight**, see
  [Resetting Norilight](https://github.com/Nori-Oppi/Norilight/blob/main/docs/GUIDE.md#resetting-norilight).
- Norishine: **Troubleshooting › Reset Norishine**, see
  [Resetting Norishine](https://github.com/Nori-Oppi/Norishine/blob/master/docs/GUIDE.md#resetting-norishine).
