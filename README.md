# 🛰️ Neo RTMP Server

**Stream from DJI Fly app to OBS Studio (Rust-based local RTMP relay)**

---

## ✨ Overview

**Neo RTMP Server** is a lightweight, Rust-based RTMP relay that allows you to receive the live stream sent from the **DJI Fly** app and view it directly in **OBS Studio** on your local network.

This tool runs as a single executable — no configuration files or dependencies required.

> 🎯 Ideal for DJI Neo, Avata 2, Mini 4 Pro, or any DJI drone that supports RTMP live streaming.

---

## 🚀 Key Features

* Single executable — no NGINX, no Docker, no setup scripts
* Works entirely **offline** within your local Wi-Fi network
* Supports **OBS Studio**, **ffplay**, and other RTMP clients
* Low latency (~1–2 seconds typical)
* Automatic relay between multiple clients (one publisher → many players)

---

## ⚙️ Installation

### 1. Install Rust

Download and install Rust toolchain from [https://rustup.rs](https://rustup.rs).
Supports Windows 11, macOS, and Linux.

### 2. Clone and run

```bash
git clone https://github.com/ychoi-kr/neo-rtmp-server.git
cd neo-rtmp-server
cargo run
```

You’ll see:

```
Neo RTMP server started → rtmp://<PC-IP>:1935/live/mystream
Play in OBS: rtmp://<PC-IP>:1935/live/mystream
```

---

## 📡 DJI Fly App Setup

> ⚠️ **Important:** Do *not* connect your phone directly to the drone’s Wi-Fi network.
> You must power on the **remote controller** and connect your phone to it **via USB cable**.
> Live streaming is only available in this configuration.

1. In DJI Fly, tap the **⋯ (three-dot)** menu on the top-right.
2. Go to **Transmission → Live Streaming Platform → RTMP**.
3. Enter:

   * **RTMP Address:** `rtmp://<PC-IP>:1935/live/mystream`
   * **Stream Key:** *leave blank*
4. Tap **Start Live** to begin streaming.

> 💡 PC IP Address can be found with `ipconfig` (Windows) or `ifconfig` (macOS/Linux).

If connection fails:

* Ensure Windows Firewall allows inbound connections on **port 1935**
* In DJI Fly settings → **Camera → Encoding Format**, select **H.264**

---

## 🎥 OBS Studio Setup

1. Open **OBS Studio**
2. Add **Source → + → Media Source**
3. Uncheck *Local File*, then enter:

   ```
   rtmp://localhost:1935/live/mystream
   ```
4. Confirm — the DJI stream will appear after a short buffer delay.

> ⏱️ The media source may take a couple of seconds to appear.
> To synchronize with your **webcam**, add a **“Video Delay (Async)”** filter to the webcam source and set **Delay (ms): 2000**.

---

## 🧠 Notes

* Actual end-to-end latency depends on your network (typically 1–2 seconds).
* Use the same Wi-Fi network for both PC and phone; 5 GHz is recommended.

---

## 🪶 License

MIT License © 2025 [ychoi-kr](https://github.com/ychoi-kr)

---

## 🌐 Links

* GitHub: [https://github.com/ychoi-kr/neo-rtmp-server](https://github.com/ychoi-kr/neo-rtmp-server)
* Demo Video: https://youtube.com/live/lC3U1t0mzxs?feature=share
