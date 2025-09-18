# Pwnagotchi Custom Plugins Installation

This guide explains how to install specific **custom plugins** from this repository into a **Jayofelony Pwnagotchi build**. These steps will download the plugins directly from GitHub, place them into the correct directory, and enable them via the Web UI.

---

## Plugins Included

- `aircrackonly_ng.py`  
- `aircrackonly.py`  
- `hulk.py`  
- `instattack.py`  

---

## Installation Steps

### 1. SSH into your Pwnagotchi

Open a terminal on your computer and run:

```bash
ssh pi@<pwnagotchi-ip>
```

> Replace `<pwnagotchi-ip>` with your Pwnagotchi’s IP address. (It is usually 10.0.0.2)

---

### 2. Navigate to the custom plugins directory

```bash
cd /usr/local/share/pwnagotchi/custom-plugins
```

---

### 3. Download all plugin files from GitHub

```bash
sudo wget -r -np -nH --cut-dirs=3 -R "index.html*" https://github.com/GhosTech-IT/pwnagotchi/raw/main/plugins/
```

**Explanation of the command:**

- `sudo` → ensures proper permissions to write to the directory.  
- `wget -r` → recursively download all files in the folder.  
- `-np` → do not traverse to parent directories.  
- `-nH` → do not create a host directory.  
- `--cut-dirs=3` → flatten the directory structure so files go directly into `custom-plugins`.  
- `-R "index.html*"` → ignore GitHub-generated index pages.  

---

### 4. Reboot the Pwnagotchi

```bash
sudo reboot
```

---

### 5. Enable the plugins via Web UI

1. Open a browser and navigate to:  
   ```
   http://<pwnagotchi-ip>:8080
   ```  
2. Go to the **Plugins** section.  
3. Toggle on the new plugins:  
   - `aircrackonly_ng`  
   - `aircrackonly`  
   - `hulk`  
   - `instattack`  
4. Save changes.  

> After enabling, the plugins will be active on the next reboot.

---

### Notes

- This guide assumes you are using the **Jayofelony Pwnagotchi build**, which already contains the `custom-plugins` directory.  
- Only the plugin files in this repository will be downloaded — no other files will be affected.
