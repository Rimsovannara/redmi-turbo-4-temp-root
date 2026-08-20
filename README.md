# Temporary Root Guide for Redmi Turbo 4 (Codename: `rodin`)

This repository provides a step-by-step guide on how to achieve temporary root access on the **Redmi Turbo 4** without unlocking the bootloader.

---

## ⚠️ Disclaimer

> Modifying device software carries risks. Proceed with caution. The authors and contributors are not responsible for bricked devices, data loss, or voided warranties.

---

## 📋 Prerequisites & Downloads

Before starting, ensure you have downloaded the necessary files:

* **[All-in-One Tools Package](https://xdaforums.com/attachments/kernelsu_v3-2-5-apk-4-rar-zip.6364025/)** *(Includes: Termux, KernelSU, MT Manager, and `preload.so`)*

**Preparation:**
1. Install the **KernelSU Manager** and **Termux** (or another terminal emulator) from the downloaded package.
2. Extract the `preload.so` payload file and place it in the root of your internal storage (`/sdcard/` or `/storage/emulated/0/`).
3. Enable **Wireless Debugging** in your device's Developer Options.

---

## 🛠️ Method 1: Manual Method via ADB (Termux)

### Step 1: Install ADB Tools
Open **Termux** and install the necessary Android tools:
```bash
pkg update && pkg install android-tools
```

### Step 2: Pair Wireless Debugging
1. Open Settings > Developer Options > Wireless Debugging.
2. Select **Pair device with pairing code** (using split-screen or floating window is recommended).
3. In Termux, run:
```bash
adb pair <IP_ADDRESS>:<PORT>
```
4. Enter the 6-digit pairing code when prompted.

### Step 3: Connect via ADB
Check the main Wireless Debugging screen for the active port number and connect:
```bash
adb connect <IP_ADDRESS>:<PORT>
```

### Step 4: Push the Payload
Copy the `preload.so` file to the temporary directory:
```bash
adb push /sdcard/preload.so /data/local/tmp/preload.so
```

### Step 5: Execute the Payload
Run the following command in Termux:
```bash
adb shell "LD_PRELOAD=/data/local/tmp/preload.so /system/bin/toybox id"
```

### Step 6: Verify Root Access
Open the **KernelSU** application to confirm that temporary root status is active.

---

## 🚀 Method 2: One-Click Application (Recommended)

For an automated setup that does not require manual ADB pairing, you can use the GhostLock app.

1. **[Download the GhostLock APK](https://xdaforums.com/attachments/ghostlock-release-apk.6374784/)**
2. Install the APK on your device.
3. Open the application and tap the trigger button to activate temporary root.
4. Verify root status within the KernelSU app.

*(Source code available at the [GhostLock GitHub Repository](https://github.com/YuKongA/ghostlock-app))*

---

## 🤝 Credits & Acknowledgments

* **XDA-Developers**: [Original XDA Guide for K80 Ultra / Redmi Turbo 4](https://xdaforums.com/t/guide-temporary-root-for-k80-ultra-redmi-turbo-4-no-bootloader-unlock-needed.4795161/) *(Originally sourced from CoolApk)*.
* **[YuKongA / GhostLock](https://github.com/YuKongA/ghostlock-app)** for the one-click automation tool.

---

## ☕ Support

If this guide was helpful, donations are appreciated:

**BEP20 Address:** `0x53e9ff85f4543c1df0cb70aec6c38d8b52843dd3`
