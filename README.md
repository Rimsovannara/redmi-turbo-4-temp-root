# Temporary Root Guide for Redmi Turbo 4 (Codename: `rodin`)

This repository provides a step-by-step guide for achieving temporary root access on the **Redmi Turbo 4** without unlocking the bootloader.

> **Note:** This guide assumes that the required `preload.so` payload is compatible with your specific device/software version.

---

## ⚠️ Disclaimer

> Modifying device software carries risks. Proceed with caution. The authors and contributors are not responsible for bricked devices, data loss, security issues, or voided warranties.

---

## 📋 Prerequisites

Before starting, make sure you have:

1. **KernelSU Manager** installed on your device.
2. A terminal emulator such as **Termux**.
3. **Wireless Debugging** enabled in **Developer Options**.
4. The required `preload.so` payload file.
5. `preload.so` placed in your internal storage, for example:
   - `/sdcard/preload.so`
   - `/storage/emulated/0/preload.so`

---

# 🛠️ Method 1: Manual Method via ADB

## Step 1: Install ADB Tools

Open **Termux** and install the required Android tools:

```bash
pkg update && pkg install android-tools
```

---

## Step 2: Pair Wireless Debugging

1. Open:

   **Settings → Developer Options → Wireless Debugging**

2. Enable **Wireless Debugging**.

3. Select **Pair device with pairing code**.

4. Keep the pairing screen visible. Using split-screen or a floating window can make this easier.

5. In Termux, run:

```bash
adb pair <IP_ADDRESS>:<PAIRING_PORT>
```

6. When prompted, enter the **6-digit pairing code** shown on your device.

### Example

```bash
adb pair 192.168.1.100:37123
```

> Replace the IP address and port with the values displayed on your device.

---

## Step 3: Connect via ADB

After pairing, return to the main **Wireless Debugging** screen.

Find the device's active **IP address and port**, then run:

```bash
adb connect <IP_ADDRESS>:<ADB_PORT>
```

### Example

```bash
adb connect 192.168.1.100:42567
```

Verify the connection:

```bash
adb devices
```

You should see your device listed.

---

## Step 4: Push the Payload

Push `preload.so` to the temporary directory:

```bash
adb push /sdcard/preload.so /data/local/tmp/preload.so
```

You can verify that the file was transferred:

```bash
adb shell ls -l /data/local/tmp/preload.so
```

---

## Step 5: Execute the Payload

Run the payload using:

```bash
adb shell "LD_PRELOAD=/data/local/tmp/preload.so /system/bin/toybox id"
```

If the payload successfully triggers the intended exploit, the command should execute with the privileges provided by the payload.

> **Important:** The exact output and behavior may vary depending on the Redmi Turbo 4 firmware version and the compatibility of `preload.so`.

---

## Step 6: Verify Root Access

Open **KernelSU Manager** and check the root status.

You can also verify the current shell identity with:

```bash
adb shell id
```

If the temporary root method was successful, the resulting privileges should reflect the access provided by the exploit.

---

# 🚀 Method 2: One-Click Application

For an automated setup, you can use the **GhostLock** application if it is compatible with your device and firmware.

### Steps

1. Download and install the latest `ghostlock-release.apk`.
2. Open the application.
3. Follow the instructions provided by the application.
4. Trigger the temporary-root process.
5. Open **KernelSU Manager** and verify the result.

> **Warning:** Only install APK files from a source you trust. Verify the APK and its release information before installing it.

---

# 🔄 Temporary Root

This method provides **temporary** root access.

A reboot may remove the temporary root state, meaning the process may need to be repeated after restarting the device.

---

# ❗ Troubleshooting

## `adb: command not found`

Install Android platform tools in Termux:

```bash
pkg update
pkg install android-tools
```

---

## `failed to connect`

Make sure:

- Wireless Debugging is enabled.
- Your phone and computer/Termux environment can communicate with each other.
- You are using the correct ADB port.
- The device has been paired first.

Check connected devices:

```bash
adb devices
```

---

## `adb push` cannot find `preload.so`

Check whether the file exists:

```bash
ls -l /sdcard/preload.so
```

or:

```bash
ls -l /storage/emulated/0/preload.so
```

If necessary, use the full path:

```bash
adb push /storage/emulated/0/preload.so /data/local/tmp/preload.so
```

---

## KernelSU does not show root

Make sure:

- The payload is compatible with your firmware.
- `preload.so` was transferred successfully.
- The payload executed without errors.
- You are checking KernelSU after running the trigger command.

Different firmware versions may require different payloads or methods.

---

# 📱 Device Information

| Property | Value |
|---|---|
| Device | Redmi Turbo 4 |
| Codename | `rodin` |
| Root Method | Temporary Root |
| Bootloader Unlock | Not required |
| Root Manager | KernelSU |
| Payload | `preload.so` |
| Terminal | Termux |
| Connection | ADB Wireless Debugging |

---

# 🤝 Credits & Acknowledgments

- Original method shared via **CoolApk**.
- **GhostLock Project** for the one-click automation tool.
- **KernelSU Project** for the root management solution.

---

# ☕ Support

If this guide was helpful and you would like to support the project, donations are appreciated.

**BEP20 Address:**

```text
0x53e9ff85f4543c1df0cb70aec6c38d8b52843dd3
```

---

# ⚠️ Final Notes

This project is provided for educational and research purposes.

Always make sure that the payload and rooting method are intended for your exact device and firmware version.

**Device:** Redmi Turbo 4  
**Codename:** `rodin`
