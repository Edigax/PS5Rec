# PS5Rec 🎮📹

**PS5Rec** is a native PlayStation 5 payload by [**Edigax**](https://github.com/Edigax) that captures gameplay and screen output directly into standard **MP4** container files with **synchronized 48 kHz stereo AAC-LC audio**, saving directly to the console's internal storage (`/data/pbs/recordings/`).

Built on top of the original hardware screen capture research by **Seregonwar** ([PBS-Payload](https://github.com/seregonwar/PBS-Payload)), **PS5Rec** integrates native in-payload audio encoding (VisualOn AAC-LC) and standalone container muxing (minimp4). No capture card, external PC recording, or post-processing wrapping is required!

---

## ✨ Features

- **Direct MP4 Container Output**: Muxes raw H.264 video and stereo audio directly into universally playable `.mp4` video files on the console.
- **Synchronized Game Audio**: Real-time 48 kHz stereo audio capture through `sceAvcap2OpenAudio` encoded directly to 128 kbps stereo AAC-LC.
- **Embedded Web Dashboard**:
  - Live low-latency screen streaming preview in your PC or mobile browser.
  - One-click Start / Stop recording controls with real-time frame and audio bitrate stats.
  - Built-in video player with audio playback for all recorded clips.
  - Instant browser download of `.mp4` recordings directly from internal storage.
  - Auto-scanning web server: binds to port **`9999`** by default (and automatically falls back to **`10000`** if 9999 is busy).
- **Multi-Resolution Support**: Configurable resolution modes (720p, 1080p, 1440p, 2160p) according to display and firmware capability.
- **Wide Firmware Compatibility**: Supports PlayStation 5 system firmwares **3.20 through 13.60**.
- **Self-Contained Binary**: Single precompiled ELF payload (`ps5rec.elf`).

---

## 🚀 How to Use

### 1. Download the Payload
Download the latest `ps5rec.elf` directly from this repository:
- [`ps5rec.elf`](ps5rec.elf) (or from the [Releases](https://github.com/Edigax/PS5Rec/releases) page)

### 2. Send to Your PlayStation 5
Make sure your PS5 is running an ELF loader (e.g., via WebKit exploit, Lapse, or etaHEN):

```bash
# Using netcat to port 9020 (standard WebKit exploit loader):
nc -w 3 <YOUR_PS5_IP> 9020 < ps5rec.elf

# Using netcat to port 9021 (standard SDK elfldr):
nc -w 3 <YOUR_PS5_IP> 9021 < ps5rec.elf
```

Once loaded, an on-screen notification will appear on your TV:
```
PS5Rec by Edigax
Screen & Audio Recorder (MP4 + AAC Edition)
Based on PBS by Seregonwar
Streaming and web dashboard ready on port 9999
```

### 3. Open Web Dashboard & Record
1. Open any web browser on your computer or phone and visit:
   ```text
   http://<YOUR_PS5_IP>:9999
   ```
   *(If port 9999 was busy from a previous session, visit `http://<YOUR_PS5_IP>:10000`)*
2. Click **Start Recording** to begin capturing gameplay with audio.
3. Click **Stop Recording** when done.
4. Recordings are saved to `/data/pbs/recordings/` on your PS5. Preview them in the browser or click **Download** to save the `.mp4` file to your computer.

---

## 📜 Credits & Acknowledgments

- **[Edigax](https://github.com/Edigax)**: PS5Rec maintainer, MP4 container integration, live 48 kHz AAC audio encoding pipeline, and binary releases.
- **[Seregonwar](https://github.com/seregonwar)**: Original [PBS-Payload](https://github.com/seregonwar/PBS-Payload) and the initial PS5/PS4 hardware screen capture reverse-engineering.
- **[ps5-payload-dev](https://github.com/ps5-payload-dev)** team: `ps5-payload-sdk` and toolchain.
- **[lieff](https://github.com/lieff/minimp4)**: Lightweight `minimp4` MP4 container muxer.
- **VisualOn**: Open-source `vo-aacenc` AAC-LC audio encoder.
- Community testers: **stonedmodder**, **zer0day**, **nexgen999**, **NSTG**, and **ONE Jailbreak**.

---

## ⚖️ License

This project is licensed under the **GNU General Public License v3.0** (GPL-3.0) in accordance with the original PBS-Payload license. See [LICENSE](LICENSE) for details.
