# Fixing hardware decoding problems

Norilight decodes the stream on this device's GPU. When no GPU decoder works, it falls back
to the CPU, which adds latency and often can't keep up above 1080p or 60 FPS. Norilight
warns about this at start-up.

## Windows

1. **Update the GPU driver** from the GPU maker rather than Windows Update:
   [NVIDIA](https://www.nvidia.com/Download/index.aspx),
   [AMD](https://www.amd.com/en/support) or
   [Intel](https://www.intel.com/content/www/us/en/download-center/home.html). This fixes
   most cases.
2. **Remote Desktop sessions** have no GPU decoder. Run Norilight on the PC itself.
3. **Laptops with two GPUs**: let Norilight use the stronger one (Windows Settings, System,
   Display, Graphics).
4. **"N" editions of Windows** lack the Media Feature Pack; add it under Windows Settings,
   Optional features.
5. **Older GPUs** can't decode HEVC or AV1. Set **Compression format (codec)** to H.264
   (Settings, Video decoding).

## macOS

Every Mac Norilight supports decodes H.264 and HEVC in hardware. If the warning appears,
update macOS, and check that Norilight isn't running in a virtual machine.

## Linux

Norilight needs VA-API (Intel, AMD) or VDPAU or NVDEC (NVIDIA) and the matching driver
packages, for example `intel-media-driver` or `mesa-va-drivers`. `vainfo` lists what the
driver decodes. Hardware decoding doesn't work under XWayland: start Norilight with
`QT_QPA_PLATFORM=wayland`, or use an X11 session.

## Checking the result

**Settings › Video decoding › Decode video using** is **Automatic** by default. Set it to
**Hardware only (GPU)** to see whether a stream starts on the GPU at all; the error then
says why it doesn't. The performance stats (Ctrl+Alt+Shift+S) name the decoder in use.
**Software only (CPU)** is a last resort for when the GPU decoder shows corrupt video.

If none of this helps, open an [issue](https://github.com/Nori-Oppi/Norilight/issues) with
Norilight's log (`Norilight-<time>.log` in the temp folder).
