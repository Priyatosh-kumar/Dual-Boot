# How to Dual Boot Windows 11 Alongside Debian-Based Linux (Ubuntu/Linux Mint)


## Preliminary Checklist (Before You Start)

**1. Keep your BitLocker Recovery Key handy**

- If BitLocker is enabled on your system, you will need to disable it later.
- You can find your BitLocker key at: https://account.microsoft.com/devices/recoverykey

**2. Have access to your Microsoft account**

- This should be the same account used to log into your current Windows 11 installation.
- You may need it for BitLocker recovery or troubleshooting.

---

## Step-by-Step Instructions to Dual Boot Linux Mint/Ubuntu with Windows 11

### **Step 1: Create a Bootable Linux USB Drive**

1. Download the Linux ISO file:  
- [Linux Mint](https://www.linuxmint.com/edition.php?id=319)  
- [Ubuntu](https://ubuntu.com/download/desktop)  
2. Download [RUFUS](https://rufus.ie/en/)  
3. Plug in a USB drive (8GB or more).  
4. Open RUFUS:  
- Select your USB drive  
- Select the downloaded ISO file  
- Use GPT partition scheme (for UEFI)  
- Click **Start** to create the bootable Linux USB

---

### **Step 2: Disable BitLocker (if applicable)**

🔗 [Follow This Video Tutorial](https://www.youtube.com/watch?v=AU5nm7b1aT0)

**Or follow manually:**

1. Search **Manage BitLocker** from the Start Menu.  
2. If BitLocker is **ON**, click **Turn off BitLocker** for your Windows drive.  
3. Enter your **Microsoft account password** if prompted.  
4. Wait for the decryption process to finish *(this may take some time)*.

---

### **Step 3: Disable Secure Boot**

1. Press `Win + I` to open **Settings → System → Recovery**  
2. Under **Advanced startup**, click **Restart now**  
3. In the recovery environment, go to:  
- → **Troubleshoot**  
- → **Advanced options**  
- → **UEFI Firmware Settings**  
- → **Restart**  
4. Once in BIOS:  
- Find the **Secure Boot** option (usually under the **Boot** or **Security** tab)  
- Set it to **Disabled**  
- Save and Exit BIOS (usually by pressing `F10`)

---

### **Step 4: Boot from USB & Install Linux (Without Removing Windows)**

1. Plug in your bootable Linux USB drive.  
2. Restart your PC and open the boot menu  
   *(press **F12**, **Esc**, **Del**, or **F2**, depending on your computer's manufacturer)*.  
3. Select your USB drive from the boot options and press **Enter**.  
4. Boot into the Linux Mint/Ubuntu live environment, then click  
   **“Install Linux Mint”** or **“Install Ubuntu”**.

🔹 **At the "Installation Type" screen:**

- If you see **"Install Linux alongside Windows Boot Manager"**:  
  - ✅ **Recommended Option**  
  - Select this to automatically install Linux without deleting Windows.  
  - The installer will handle partitioning and dual boot setup.  
  - Use the slider to allocate space between Windows and Linux as needed.  

- If you see **"Erase disk and install Linux"**:  
  - ⚠️ **Do NOT choose this option** — it will delete Windows and all your data.

5. Click **Install Now**, follow the prompts, and complete the installation.

---

### ✅ **After Installation**

- Upon reboot, you’ll see a **GRUB menu** allowing you to choose between:
  - 🐧 **Linux**
  - 🪟 **Windows 11**
- Simply select the operating system you want to boot into.

---
### 🔴 **If “Install alongside Windows” is NOT Available**

➡️ **Boot Back into Windows & Create a Linux Partition**

---

### 🔄 **Step 4A: Create Unallocated Space from Windows**

1. Boot into **Windows 11**.  
2. Press `Win + X` → Select **Disk Management**.  
3. In the list of drives, find your **Windows (C:)** partition (usually the largest).  
4. Right-click it → Select **Shrink Volume**.  
5. In the popup:
   - Enter how much space to shrink .  
   - Click **Shrink**.  
6. You’ll now see **Unallocated space**.  

💡 *This will be used for the Linux installation.*

✅ **Do NOT** create any new partition in that unallocated space.  
Leave it **unformatted** so Linux can use it during installation.

### 🧩 **Manual Partitioning (Using “Something else” Option)**

1. Boot into the Linux USB again.  
2. Begin the installation and choose **“Something else”** when asked about the installation type.  
3. Locate the **free space** (unallocated space created from Windows).


#### 🔧 **Now, create the following partitions:**

####  a. Root Partition `/` – Required

- Select the free space → click **“+”**  
- **Size:** at least **20,000 MB** (20 GB)  
- **Type:** Primary  
- **File system:** ext4  
- **Mount point:** `/`

---

####  b. Swap Partition – Optional but Recommended

- Click **“+”**  
- **Size:** Equal to your **RAM size**  
  *(e.g., 4096 MB for 4 GB RAM)*  
- **Type:** Logical  
- **Use as:** Swap area

---

####  c. Home Partition `/home` – Optional

- Use **remaining space** if you want a separate partition for user files  
- **File system**

4. Click **Install Now** → **Confirm changes** → **Proceed with setup**

5. Set your region, username, and password → Wait for installation to complete.

---
---
---
# ❓ FAQs for Dual Booting Windows 11 & Linux (Simple Guide)

| **Question**                                      | **Answer**                                                                                                                                          |
|-------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| **Will I lose my Windows files when I install Linux?** | No. If you choose the option to install Linux alongside Windows, your files and Windows system will stay safe.                                       |
| **Do I need to backup my data before starting?**        | Yes, it’s always safest to back up important files before changing your system, just in case something goes wrong.                                  |
| **What if I accidentally delete Windows during install?** | If you select “Erase disk and install Linux,” Windows and all data will be deleted. Avoid this option if you want to keep Windows.                   |
| **How much space should I give to Linux?**                | At least 20 GB is recommended for Linux to run smoothly, but more space is better if you plan to install many apps or store files.                   |
| **What if my computer doesn’t boot from USB?**            | Check your BIOS settings to make sure USB boot is enabled, or try pressing a different key (like F12, Esc, F2 or *depending on your computer's manufacturer*) to open the boot menu.              |
| **Is it okay if I don’t disable BitLocker or Secure Boot?** | It might cause installation problems or prevent Linux from booting. Disabling them as described helps ensure smooth installation and operation.       |
| **What is the GRUB menu?**                                | GRUB is a simple menu that appears after rebooting, letting you choose whether to start Windows or Linux.                                            |
| **Can I remove Linux later if I don’t like it?**          | Yes, but removing Linux safely can be tricky and might require restoring the Windows bootloader. It’s best to follow a guide or ask for help.         |
| **Do I need to be online during Linux installation?**     | Not necessarily. You can install Linux offline, but being connected helps with updates and downloading additional software during setup.             |


---


## Beginner’s Troubleshooting

- **USB won’t boot?**  
  - Try different USB ports.  
  - Make sure USB boot is enabled in BIOS.  
  - Try a different key (F12, Esc, F2) during startup to access boot menu.

- **Linux install fails or freezes?**  
  - Check that Secure Boot and BitLocker are disabled.  
  - Try a different Linux USB or re-download the ISO.

- **Can’t see GRUB menu after install?**  
  - Sometimes Windows boots directly. Restart and try pressing **Shift** or **Esc** during boot.  
  - You may need to repair GRUB using a Linux live USB.

- **Forgot your Microsoft account password?**  
  - Visit [Microsoft Password Reset](https://account.live.com/password/reset) to recover it.

---
