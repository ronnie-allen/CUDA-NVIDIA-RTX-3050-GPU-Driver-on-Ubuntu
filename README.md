
## 🚀 README: Installing NVIDIA RTX 3050 GPU Driver on Ubuntu

This guide helps you set up the **NVIDIA RTX 3050 GPU** on **Ubuntu** the proper way, disabling Nouveau and installing the recommended official driver. Works 100% ✅

----------

### 📌 Requirements

-   Ubuntu 20.04 / 22.04 / newer
    
-   NVIDIA RTX 3050
    
-   Internet connection
    
-   Basic terminal access (`sudo` rights)
    

----------

### 🧱 STEP 1: Update Your System

```bash
sudo apt update && sudo apt upgrade -y

```

Reboot if necessary:

```bash
sudo reboot

```

----------

### 🚫 STEP 2: Disable Nouveau Driver

Ubuntu comes with **Nouveau**, an open-source NVIDIA driver that conflicts with the official one. We need to disable it.

#### 2.1 Create blacklist file:

```bash
sudo nano /etc/modprobe.d/blacklist-nouveau.conf

```

Paste this inside:

```
blacklist nouveau
options nouveau modeset=0

```

Save:

-   `Ctrl + O` → Enter
    
-   `Ctrl + X` to exit
    

#### 2.2 Update initramfs:

```bash
sudo update-initramfs -u

```

#### 2.3 Reboot:

```bash
sudo reboot

```

----------

### 🔍 STEP 3: Check Available NVIDIA Drivers

```bash
ubuntu-drivers devices

```

You’ll see a list like this:

```
driver : nvidia-driver-570 - third-party non-free recommended

```

Take note of the **recommended** one (e.g., `nvidia-driver-570`).

----------

### 💾 STEP 4: Install the NVIDIA Driver

Example (replace `570` if your recommended version is different):

```bash
sudo apt install nvidia-driver-570 -y

```

Once installed:

```bash
sudo reboot

```

----------

### ✅ STEP 5: Verify Installation

After reboot, run:

```bash
nvidia-smi

```

You should see output like this:

```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 570.xx    Driver Version: 570.xx    CUDA Version: 12.x          |
| GPU       Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr.|
| 0     NVIDIA RTX 3050      Off      | 00000000:01:00.0  On |                  |
+-----------------------------------------------------------------------------+

```

Congrats! You're running NVIDIA RTX 3050 successfully on Ubuntu 🎉

----------

### ⚡ (Optional) Install CUDA Toolkit

```bash
sudo apt install nvidia-cuda-toolkit -y

```

Check version:

```bash
nvcc --version

```

----------

### 🧠 Notes

-   To **check GPU status anytime**: `nvidia-smi`
    
-   To check driver info: `nvidia-settings` (GUI app)
    
-   If using ML frameworks (PyTorch, TensorFlow), verify CUDA compatibility
    

----------
#### Made with 🫶🏻 by Ronnie Allen
