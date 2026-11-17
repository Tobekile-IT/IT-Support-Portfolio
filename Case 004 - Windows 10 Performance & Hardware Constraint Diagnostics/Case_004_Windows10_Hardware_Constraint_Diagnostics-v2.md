# Case 004: Windows 10 Performance & Hardware Constraint Diagnostics

**Technician:** Tobekile Mazula | ZuluTech – Computer Repairs & IT Support  
**Device:** Acer Aspire Laptop  
**Operating System:** Windows 10  
**Primary Issue:** Intermittent system slowness and freezing during everyday student workloads  

---

## 1. Executive Summary
A student client reported intermittent freezing and sluggish performance on an Acer Aspire laptop running Windows 10. A structured hardware and software diagnostic revealed that the system runs on **4 GB of soldered RAM (`1 of 1` slots used)** and **eMMC flash storage**, making a physical memory upgrade impossible. After verifying the system was completely free of malware (**200,515 items scanned, 0 threats found**), targeted resource optimization was performed—reducing idle CPU load from **70% to 11%**, dropping disk activity from **56% to 0%**, and freeing **300 MB of critical RAM** without unnecessary hardware expenditure.

---

## 2. Initial Assessment & Hardware Discovery
Using **Task Manager** and **CrystalDiskInfo**, the baseline system metrics and hardware architecture were evaluated:

* **CPU Load:** `70%` at idle (`1.93 GHz`)
* **Memory (RAM):** `3.2 / 3.8 GB` (`84%` utilized; `1 of 1` slots used — **permanently soldered, non-upgradable**)
* **Storage (`Disk 0`):** `56%` active time; identified as **SD / eMMC flash storage** (lacking S.M.A.R.T. reporting sensors for CrystalDiskInfo)

![Before Optimization - Task Manager Baseline](images/01_before_task_manager.png)

---

## 3. Troubleshooting & Optimization Actions

### Step 1: Startup Application Audit
Inspected **Task Manager > Startup apps** and identified high-impact background services loading automatically at boot alongside Windows 10:
* Disabled **Microsoft Copilot** and **Google Chrome** background startup processes while preserving **Windows Security (`SecurityHealthSystray`)**.

![Startup Apps Before](images/02_startup_apps_before.png)

![Startup Apps Disabled](images/03_startup_apps_disabled.png)

### Step 2: Malware & Adware Verification
Executed a full system scan using **Malwarebytes** from a portable technician diagnostic toolkit to rule out hidden adware or malicious background tasks:
* **Items Scanned:** `200,515`
* **Threats Detected:** `0`
* Uninstalled the temporary scanner post-audit to prevent background trial services from consuming limited RAM.

![Malwarebytes Clean Scan](images/04_malwarebytes_scan_clean.png)

### Step 3: Background App & Visual Performance Tuning
* Navigated to **Settings > Apps > Installed apps** and set **Background app permissions** to **Never** for resource-heavy applications (including **WhatsApp**).
* Adjusted Windows visual performance settings (**Adjust for best performance**, retaining font smoothing and thumbnails) to reduce GPU/CPU animation overhead.

---

## 4. Before & After Results

| Metric | Before Optimization | After Optimization | Improvement |
| :--- | :--- | :--- | :--- |
| **Idle CPU Usage** | `70%` | `11%` | **-59% load reduction** |
| **Memory (RAM) In Use** | `3.2 GB (84%)` | `2.9 GB (76%)` | **300 MB freed** |
| **Disk Active Time** | `56%` | `0%` | **Storage thrashing eliminated** |
| **Malware Status** | Unverified | `0 threats (200,515 scanned)` | **Verified clean** |

![After Optimization - Task Manager Results](images/05_after_task_manager.png)

---

## 5. Client Recommendation & Takeaways
* **Honest Hardware Guidance:** Advised the client against purchasing aftermarket RAM modules due to the soldered `1 of 1` motherboard configuration, saving unnecessary hardware costs.
* **Usage Best Practices:** Recommended limiting simultaneous browser tabs and utilizing lightweight browser sleeping tabs to keep memory usage below saturation during study sessions.
