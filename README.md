# 🚀 Full Guide: Installing NVIDIA RTX 4050, CUDA 12.8 & cuDNN 8.9.7 on Ubuntu 22.04

This guide ensures your system is ready for **deep learning**, **GPU acceleration**, and **high-performance computing** using the **NVIDIA RTX 4050**.

----------

### 📋 Prerequisites

-   Ubuntu 22.04 (or newer)
    
-   RTX 4050 GPU
    
-   Internet connection
    
-   Terminal access (`sudo`)
    
-   Charger plugged in (for laptops)
    

----------

## ✅ STEP 1: Update Your System

```bash
sudo apt update && sudo apt upgrade -y

```

🔍 **Why?**  
To ensure all existing packages are up to date, reducing the chance of version conflicts during driver or CUDA installation.  
👉 Think of it like cleaning your desk before setting up a new PC build.

Optional (if prompted or just to be safe):

```bash
sudo reboot

```

----------

## 🚫 STEP 2: Disable the Nouveau Driver (Default Open-Source NVIDIA Driver)

Ubuntu uses Nouveau by default, but it **conflicts** with NVIDIA’s proprietary driver, so we need to **blacklist** it.

### 2.1 Create a Blacklist File

```bash
sudo nano /etc/modprobe.d/blacklist-nouveau.conf

```

Paste this into the file:

```
blacklist nouveau
options nouveau modeset=0

```

Save and exit:

-   `Ctrl + O`, `Enter` → Save
    
-   `Ctrl + X` → Exit
    

### 2.2 Update initramfs

```bash
sudo update-initramfs -u

```

🔍 **Why?**  
Rebuilds the initial RAM filesystem with the new kernel module settings, so Nouveau stays disabled.

### 2.3 Reboot

```bash
sudo reboot

```

----------

## 📦 STEP 3: Install the Official NVIDIA Driver

### 3.1 Check Available Drivers

```bash
ubuntu-drivers devices

```

🔍 **Why?**  
Shows the best driver recommended for your GPU (e.g., `nvidia-driver-570`). You avoid guesswork.

### 3.2 Install Recommended Driver

```bash
sudo apt install nvidia-driver-570 -y

```

### 3.3 Reboot Again

```bash
sudo reboot

```

🔍 **Why?**  
So the system starts using the new NVIDIA driver instead of the disabled Nouveau.

### 3.4 Verify GPU is Working

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

Congrats! You're running NVIDIA RTX 4050 successfully on Ubuntu 🎉


🔍 **Why?**  
Confirms that your RTX 3050 is detected and functioning correctly with the installed driver.

----------

## 💻 STEP 4: Install CUDA Toolkit 12.8

> You need this for GPU-based computations in ML, AI, and data science tasks.

### 4.1 Download `.deb (local)` from the official [CUDA site](https://developer.nvidia.com/cuda-downloads)

Then install it:

```bash
sudo dpkg -i cuda-repo-ubuntu2204-12-8-local_*.deb
sudo cp /var/cuda-repo-*/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt update
sudo apt install cuda -y

```

🔍 **Why?**  
Adds the NVIDIA CUDA repo and installs the CUDA dev kit — including compiler (`nvcc`), runtime libraries, and more.

### 4.2 Add CUDA to Path

Open `.bashrc`:

```bash
nano ~/.bashrc

```

Add these lines at the bottom:

```bash
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH

```

Then apply the changes:

```bash
source ~/.bashrc

```

🔍 **Why?**  
So your terminal knows where to find CUDA tools and libraries.

### 4.3 Verify CUDA

```bash
nvcc --version

```

🔍 **Why?**  
To confirm CUDA installed correctly and the version is available.

----------

## ⚙️ STEP 5: Install cuDNN 8.9.7 (for Deep Learning Acceleration)

> cuDNN boosts ML frameworks like PyTorch & TensorFlow by giving GPU-based neural net performance.

### 5.1 Download `.deb` from [cuDNN Archive](https://developer.nvidia.com/rdp/cudnn-archive)

Install it:

```bash
sudo dpkg -i cudnn-local-repo-ubuntu2204-8.9.7.29_1.0-1_amd64.deb
sudo cp /var/cudnn-local-repo-*/cudnn-*-keyring.gpg /usr/share/keyrings/
sudo apt update
sudo apt install libcudnn8 libcudnn8-dev libcudnn8-samples -y

```

🔍 **Why?**

-   `libcudnn8`: Runtime for deep learning
    
-   `libcudnn8-dev`: Headers for compiling models
    
-   `libcudnn8-samples`: Sample models to test
    

----------

## 🧪 STEP 6: Test cuDNN Installation

```bash
cat /usr/include/cudnn_version.h | grep CUDNN_MAJOR -A 2

```

🔍 **Why?**  
Checks the installed cuDNN version.

Run a sample test:

```bash
cp -r /usr/src/cudnn_samples_v8/ ~/cudnn_samples
cd ~/cudnn_samples/mnistCUDNN
make
./mnistCUDNN

```

✅ Output should say: `Test Passed!`  
🔍 **Why?**  
Confirms everything (CUDA + cuDNN) is correctly set up.

----------

## 🧠 STEP 7: Verify GPU with Python (PyTorch / TensorFlow)

### For PyTorch:

```python
import torch
print(torch.cuda.is_available())        # Should return True
print(torch.cuda.get_device_name(0))    # NVIDIA RTX 3050

```

### For TensorFlow:

```python
from tensorflow.python.client import device_lib
print(device_lib.list_local_devices())

```

🔍 **Why?**  
To confirm your ML code can now access the GPU for training or inference.

----------

## 🔌 Pro Tip: Keep Charger Plugged In

Laptop GPUs like RTX 4050 may **disable themselves** on battery to save power.  
👉 Always keep the **charger connected** during GPU-intensive tasks.

----------

## 🎉 That’s it!

You now have a complete setup with:

-   ✅ Official NVIDIA Driver
    
-   ✅ CUDA 12.8
    
-   ✅ cuDNN 8.9.7
    
-   ✅ Fully GPU-enabled deep learning environment
    

----------

#### Made with 🫶🏻 by Ronnie Allen
