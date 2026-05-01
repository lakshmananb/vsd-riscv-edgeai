# Running Notes for Hands-On Trial during the Workshop (May 1st to 10th, 2026)
## Author:  Lakshmanan B (https://github.com/lakshmananb)
## Created:  1st May 2026, 17:30 IST
## Updated:  1st May 2026, 19:03 IST

# VSD RISC-V Edge-AI Workshop — SiFive FreedomStudio on local computer
### Problem encountered - 1:  Not able to have access for the downloaded archive.  
   <img width="1419" height="274" alt="image" src="https://github.com/user-attachments/assets/28e95cb6-175f-47dd-86e0-81dd1073aced" />
   ### Resolution: Working after redownload.  Installation underway.

# VSD RISC-V Edge-AI Workshop — SiFive FreedomStudio on GitHub Codespaces

This repository provides a complete cloud-based environment for the **RISC-V Edge-AI Workshop** using **SiFive FreedomStudio 3.1.1**.
Participants can compile, debug, and explore RISC-V applications directly from their browsers using GitHub Codespaces.
No local installation or hardware setup is required.

---

## 1. Launch Codespace

1. Go to the repository:
   [https://github.com/vsdip/vsd-riscv-edgeai](https://github.com/vsdip/vsd-riscv-edgeai)
2. Click the green **Code ▼** button and open the **Codespaces** tab.
3. Select **Create codespace on main**.
   ![Codespace creation](images/1.jpg)

GitHub will automatically start a new Codespace workspace configured for FreedomStudio.

---

## 2. Access the noVNC Desktop

1. Once the Codespace has launched, go to the **PORTS** tab next to the terminal.
   ![Ports tab](images/2.jpg)
2. Wait until **Port 6080** (labeled *noVNC Desktop*) appears.
   Then click the **globe icon** under “Forwarded Address.”
   ![Port view](images/3.jpg)
3. A new browser tab will open showing a directory listing.
   Click **vnc.html** to launch the full graphical desktop.
   ![Directory listing](images/4.jpg)

### Problem encountered - 2:  Every few minutes the noVNC Desktop is getting disconnected.
   <img width="1484" height="711" alt="image" src="https://github.com/user-attachments/assets/0bf0a7fe-9d51-4619-bfaf-61c9300da233" />

---

## 3. Start SiFive FreedomStudio

1. Inside the noVNC desktop, open a terminal window (Applications → Terminal).

2. Check that FreedomStudio is available on the Desktop and launch it:

   ```bash
   cd ~/Desktop/FreedomStudio-3-1-1
   ./FreedomStudio-3-1-1
   ```

   ![Terminal launch](images/5.jpg)

### Problem encountered - 3:  Encountering the following error upon (step 3.2) invocation of FreedomStudio-3-1-1.
   <img width="817" height="418" alt="image" src="https://github.com/user-attachments/assets/a966ff8f-c53b-4ce3-a842-31ef01f85d5a" />
   ### Resolution:  Ignored.
   
3. When prompted for a workspace, use the default:

   ```
   /home/vscode/Desktop
   ```

   Then click **Launch**.
   ![Workspace dialog](images/6.jpg)

   ### Problem encountered - 4:  Creation of workspace (Step:  3.4), default workspace path is not as specified in the notes / README.
      <img width="779" height="363" alt="image" src="https://github.com/user-attachments/assets/43fe7ea4-1783-4e06-8268-ca26508e50de" />
   
      <img width="1099" height="179" alt="image" src="https://github.com/user-attachments/assets/35f3bd5d-c2be-430e-b14e-1d7d7098a71f" />
      ### Resolution:  Manually provided the path as available in the VNC under /home/vscode/ insead of /home/vsduser/.

---

## 4. FreedomStudio Setup Wizard

After startup, FreedomStudio will display the **Welcome to SiFive Freedom Studio** dialog.
You can explore available tools and debuggers such as **OpenOCD**, **QEMU**, or **openFPGALoader**, then select
**“I’m done here, take me to the Workbench.”**

![FreedomStudio Welcome](images/7.jpg)

This opens the main Eclipse-based IDE interface for RISC-V software development.

---

## 5. Explore and Build RISC-V Projects

Inside the IDE:

1. Go to **Sifive Tools -> Create Software Example Project -> Create a new Validation Project**.
2. Select any example RISC-V or Edge-AI project folder.
### Problem encountered - 5:  Not able to build, as it seems the target has to be specified.  Which target among the list to be selected for this workshop is not specified.
<img width="1346" height="949" alt="image" src="https://github.com/user-attachments/assets/3df6d569-948b-47cd-9c77-4080184efe84" />

3. Build using the hammer icon or by pressing `Ctrl+B`.
### Problem encountered - 6:  Not able to build.  I can't see any hammer icon.  Refer to the screenshot above.
   ### Resolution:  Tried selecting freedom-e310-arty as the target and sifive-welcome as an example.  Still cannot see any hammer icon or able to build.

### Problem encountered - 7:  But once the target and example are selected the pop-up grows beyond the screen size even on a fullscreen mode, and there is no scroller available to see action buttons below.  
   ### Resolution:  I had to try many things and figured out to resize the window to see the action buttons, but once resized, there is no way to validate the user entries in the absence of scroller option.  But now, I can see the "Next" and "Finish" buttons (but not any hammer icon), and able to start building by clicking on Finish button.  However, the build failed with 4 errors.
   <img width="1299" height="928" alt="image" src="https://github.com/user-attachments/assets/d65da668-8d92-4ac8-8f1a-8138f0573210" />

 ### Problem encountered - 8:  Build failed with 4 errors.
   ### Resolution:  Followed steps as in the last video #29 under "QEMU based simulations" in the course dashboard https://vsdiat.vlsisystemdesign.com/dashboard/13.  Changed target to qemu_sifive_e31 & changing the bsp/settings.mk to set compatible RISCV_ARCH as below.
   ```
   RISCV_ARCH = rv32imac_zicsr_zifencei
   ```

   ### Problem encountered - 9:  Build passes.  Not able to debug due to environments issues (bc notfound and echo having I/O error).
   <img width="1117" height="753" alt="image" src="https://github.com/user-attachments/assets/caeef623-392a-4a43-bb0e-2866031f8381" />

4. Run and debug using **QEMU** for software-level testing.

---

## 6. Environment Details

* Operating System: Ubuntu 22.04
* Desktop Environment: XFCE (served via noVNC)
* IDE: SiFive FreedomStudio 3.1.1
* Access Port: 6080 (auto-forwarded by GitHub Codespaces)
* FreedomStudio is downloaded and extracted automatically during setup (`.devcontainer/setup.sh`)

If FreedomStudio does not appear after Codespace creation, you can re-run manually:

```bash
cd ~/Desktop/FreedomStudio-3-1-1
./FreedomStudio-3-1-1
```

---

## 7. Tips for Smooth Operation

* Use a Chromium-based browser (Chrome or Edge) for better VNC responsiveness.
* Avoid closing the Codespace tab while FreedomStudio is running.
* All files in `/home/vscode/Desktop` persist while the Codespace is active.
* If the desktop view appears blank, refresh the noVNC tab once after the Codespace boots.

---

## 8. Troubleshooting

| Issue                                | Solution                                                            |
| ------------------------------------ | ------------------------------------------------------------------- |
| Port 6080 does not appear            | Wait for setup to complete (~2–3 min). Refresh PORTS tab.           |
| noVNC window is blank                | Refresh browser tab or reopen from PORTS list.                      |
| FreedomStudio not found              | Run setup manually or restart Codespace.                            |
| Workspace prompt reappears each time | Select "Use this as default and do not ask again" before launching. |

---

### Maintained by

**VLSI System Design (VSD)**
[https://www.vlsisystemdesign.com](https://www.vlsisystemdesign.com)

