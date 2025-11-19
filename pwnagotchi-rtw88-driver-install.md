<h1 align="center">⚡ Pwnagotchi + rtw88 ⚡</h1>
<p align="center"><b>Pwnagotchi driver installation guide for enabling external Wi-Fi adapters—such as the TP-Link AC600 Archer T2U Plus—that use the rtw88 driver.</b></p>

---

## ✅ Requirements

| Component          | Details                                      |
|--------------------|----------------------------------------------|
| Firmware           | Pwnagotchi running **Jayofelony image** (https://github.com/jayofelony/pwnagotchi)     |
| Connectivity       | Wi‑Fi + SSH access to the unit               |
| Wi‑Fi Adapter      | External adapter supported by `rtw88`        |
| User               | Comfortable with terminal + basic editing    |

---

## 🧠 Why this resource exists

The instructions for installing the rtw88 driver for Pwnagotchi—specifically—did not exist. Once a user installs the driver, there are other adjustments that must be addressed for proper functionality. Those issues include:

- Random freezes  
- Reboot loops  
- Wi‑Fi never fully initializing  
- Pwnagotchi services fighting each other  

This guide:

1. Installs the `rtw88` driver and firmware.  
2. Disables onboard Wi‑Fi via `/boot/firmware/config.txt`.  
3. Disables the `fix_services` plugin so it stops interfering.  

---

## ‼️ Do this first

Install Raspberry Pi kernel headers and build essentials.

```bash
sudo apt install -y raspberrypi-kernel-headers build-essential git
```

**Do not update or upgrade!**

## 🔧 Install — rtw88

All commands below are run on the Pwnagotchi via SSH.

### 1. SSH into your Pwnagotchi

```bash
ssh pi@<PWNAGOTCHI_IP>
```

Replace `<PWNAGOTCHI_IP>` with your Pwnagotchi’s IP. (Usually 10.0.0.2)

---

### 2. Clone the rtw88 driver

```bash
git clone https://github.com/lwfinger/rtw88
```

---

### 3. Change directory to rtw88

```bash
cd rtw88
```

---

### 4. Build and install the driver + firmware

```bash
make
sudo make install
sudo make install_fw
```

---

### 5. Apply modprobe config

```bash
sudo cp rtw88.conf /etc/modprobe.d/
```

---

### 6. Clean up the source folder

```bash
cd ..
sudo rm -R rtw88
```

---

## 🛜 Disable onboard Wi‑Fi

Open /boot/firmware/config.txt:

```bash
sudo nano /boot/firmware/config.txt
```

Find the section for your Pi model (for example `pi0`) and look for:

```ini
#dtoverlay=disable-wifi
```

Remove the **hashtag** (#) so it looks like this:

```ini
dtoverlay=disable-wifi
```

Save & exit out of nano:

- Press <kbd>Ctrl</kbd> + <kbd>X</kbd>  
- Press <kbd>Y</kbd> to confirm save  
- Press <kbd>Enter</kbd> to exit  

---

## 🚨 Critical Step — disable <code>fix_services</code>

If you skip this, your Pwnagotchi will likely reboot/freeze repeatedly and interfere with other plugins and functions.

1. Open the **Pwnagotchi Web UI** in your browser. (http://10.0.0.2:8080)  
2. Go to the **Plugins** tab.  
3. Find the plugin named `fix_services`.  
4. Disable it.  

---

## 🔁 Reboot

```bash
sudo reboot
```

After reboot, your `rtw88` driver compatible external Realtek adapter should work efficiently.

---

## 🩻 Common issues

- **Driver not loading**  
  - `dtoverlay=disable-wifi` was not set correctly in `config.txt`.  
- **Boot loops or freezing**  
  - `fix_services` plugin is still enabled.  
- **Build errors on \`make\`**  
  - Kernel headers were not installed.

---

## 🕶 References

- Developer @jayofelony is responsible for developing the Pwnagotchi image—the foundational firmware of this project.
- The team that developed and may still be developing the rtw88 driver: https://github.com/lwfinger/rtw88
- Special thanks to @ruslyn (R4TKN) - https://github.com/rusyln - https://ko-fi.com/r4tkn
  - Created the inspiration behind this project via social media and provided guidance/advice for issues with installing the driver.
- Special thanks to @wpa-2 (wpa_2 on Reddit)
  - Provided guidance/advice to disable the `fix_services` plugin.

---

### If you would like to support me, you can donate via the button below 😊
[![BuyMeACoffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black)](https://buymeacoffee.com/ghostech) 
