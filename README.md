# PhotoShop-ThumbNails

## Complete Thumbnail Fix Toolkit - All-in-One Solution

Here's a comprehensive batch script + manual steps combined into ONE toolkit to resolve all TIF/PSD preview issues.

---

## Part 1: Automated Fix Script

**Create this batch file:** `Fix_Thumbnails_Complete.bat`

```batch
@echo off
echo ========================================
echo  Complete TIF/PSD Thumbnail Fix Toolkit
echo ========================================
echo.

REM Step 1: Kill Explorer
echo [1/6] Stopping Windows Explorer...
taskkill /f /im explorer.exe

REM Step 2: Clear Thumbnail Cache
echo [2/6] Clearing thumbnail cache...
cd %localappdata%\Microsoft\Windows\Explorer
del thumbcache*.db /f /q
del iconcache*.db /f /q

REM Step 3: Clear Disk Cleanup Thumbnails
echo [3/6] Running disk cleanup for thumbnails...
cleanmgr /sagerun:1

REM Step 4: Registry - Increase Cache Size
echo [4/6] Increasing thumbnail cache size...
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer" /v ThumbnailCacheSize /t REG_DWORD /d 500 /f

REM Step 5: Registry - Reduce Hover Time
echo [5/6] Reducing preview hover delay...
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer" /v ThumbnailLivePreviewHoverTime /t REG_DWORD /d 500 /f

REM Step 6: Registry - Enable Large Cache
echo [6/6] Enabling large cache mode...
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /v LargeCache /t REG_DWORD /d 1 /f

REM Step 7: Restart Explorer
echo.
echo [Complete] Restarting Windows Explorer...
start explorer.exe

echo.
echo ========================================
echo  Script Complete! 
echo  Next: Run manual steps below
echo ========================================
pause
```

**Save as:** `Fix_Thumbnails_Complete.bat`  
**Run as:** Administrator (right-click → Run as administrator)

---

## Part 2: Manual Steps (Do After Script)

### **Step 1: Install Adobe Camera Raw Codec**
- Google: "Adobe Camera Raw download"
- Download latest version from Adobe
- Install it
- Restart PC

### **Step 2: Disable Slow Shell Extensions**
- Download: **ShellExView** (Nirsoft - free)
- Run it
- Sort by "Type" column
- Disable these (right-click → Disable Selected Items):
  - Adobe Bridge context menu
  - Adobe Acrobat context menu  
  - OneDrive/Dropbox handlers (if not needed)
  - WinRAR/7zip extra context menus
- **DO NOT disable:**
  - Adobe PSD Shell Extension (thumbnail provider)
  - TIFF handlers
  - Windows Imaging Component

### **Step 3: Optimize Photoshop Save Settings**
Open Photoshop:
- Edit → Preferences → File Handling
- **Image Previews:** Set to "Always Save"
- **File Compatibility:** Set to "Always"
- **Icon/Thumbnail:** Check "Always Save"
- Click OK

For TIF files:
- When saving: Use **LZW compression** (not ZIP)
- Check "Save Image Pyramid"
- Check "Embed Fast Preview"

### **Step 4: Optimize Folders for Pictures**
For each folder with TIF/PSD:
- Right-click folder → Properties
- Go to "Customize" tab
- "Optimize this folder for:" → Select **Pictures**
- Check "Also apply this template to all subfolders"
- Apply → OK

### **Step 5: Adjust Performance Settings**
- Right-click "This PC" → Properties
- Advanced system settings → Performance Settings
- **Keep these checked:**
  - Show thumbnails instead of icons ✓
  - Smooth edges of screen fonts ✓
- **Uncheck these:**
  - Show preview handlers in preview pane (major lag source)
  - Animate windows when minimizing/maximizing

---

## Part 3: Optional Advanced Fixes

### **If Still Slow - Install Better Thumbnail Handler**

**Option A: SageThumbs (Free)**
- Google: "SageThumbs download"
- Install it
- Supports PSD/TIF with layers
- Much faster than Windows default

**Option B: MysticThumbs (Paid - $30)**
- Best performance
- Handles all Adobe formats
- Worth it for professionals

### **If Working from Network/External Drive**

Add this registry setting:
```
Win+R → regedit
Navigate: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced
Create DWORD: DisableThumbsDBOnNetworkFolders
Value: 0
```

---

## Part 4: Weekly Maintenance Script

**Create:** `Weekly_Cache_Cleanup.bat`

```batch
@echo off
echo Cleaning thumbnail cache...
taskkill /f /im explorer.exe
del %localappdata%\Microsoft\Windows\Explorer\thumbcache*.db /f /q
start explorer.exe
echo Done! Cache cleaned.
timeout /t 3
```

Run this once a week to keep thumbnails fast.

---

## Complete Checklist

**Run in this order:**

✅ **1. Run Fix_Thumbnails_Complete.bat** (as Admin)  
✅ **2. Install Adobe Camera Raw**  
✅ **3. Download ShellExView** → Disable slow context menus  
✅ **4. Configure Photoshop save settings**  
✅ **5. Optimize folders for Pictures**  
✅ **6. Adjust Windows Performance settings**  
✅ **7. (Optional) Install SageThumbs or MysticThumbs**  
✅ **8. Restart PC**

---

## Project Estimate for Client

**Complexity:** Medium

**Why Medium?**
- Multiple layers: Registry tweaks, codec installation, shell extension cleanup
- Requires system optimization across Windows + Photoshop
- Some steps need testing and verification
- May need third-party tool installation

**How to Tackle:**
- Run automated script first (saves 30 mins)
- Install proper codecs and handlers
- Disable conflicting shell extensions
- Optimize Photoshop and folder settings
- Test with client's actual files
- Document settings for future reference

**Timeline & Budget:**

**Minimum:**
- **Days:** 1 day (3 hours)
- **Cost:** $9 USD / ₹765 INR
- Basic script + codec installation

**Realistic (Recommended):**
- **Days:** 1.5 days (4-5 hours)
- **Cost:** $12-15 USD / ₹1,020-1,275 INR
- Full toolkit implementation + testing + documentation

**Includes:**
- Custom batch scripts
- Registry optimization
- Shell extension cleanup
- Photoshop configuration
- Testing with actual files
- Weekly maintenance script setup

This is a complete solution that addresses ALL common causes of slow TIF/PSD previews.
