# 📖 User Manual — Dedupe & Organize

This guide is for **absolute beginners** — no Python or command-line experience needed.

It will walk you through:
1. **Installing Python** (if you don’t have it yet)
2. **Downloading this tool**
3. **Running it safely**
4. **Cleaning up duplicates**
5. **Organizing your files**

We cover **Windows**, **macOS**, and **Linux** separately.

---

## 1️⃣ Step 1 — Install Python

### **Windows**
1. Go to [https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/).
2. Click the yellow **"Download Python"** button.
3. Run the installer.
4. ✅ **Important**: Check the box **“Add Python to PATH”** before clicking Install.

To check if it worked:
1. Press `Windows + R`, type `cmd`, press Enter.
2. Type:
   ```powershell
   python --version
   ```
   You should see something like:
   ```
   Python 3.11.6
   ```

---

### **macOS**
1. Open **Terminal** (press `Command + Space`, type `Terminal`, press Enter).
2. Type:
   ```bash
   python3 --version
   ```
3. If you get `command not found`:
   - Install **Homebrew** (copy-paste in Terminal):
     ```bash
     /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
     ```
   - Then install Python:
     ```bash
     brew install python
     ```

---

### **Linux (Ubuntu/Debian)**
1. Open **Terminal**.
2. Run:
   ```bash
   sudo apt update
   sudo apt install python3 python3-pip
   ```
3. Check version:
   ```bash
   python3 --version
   ```

---

## 2️⃣ Step 2 — Get the tool

1. Go to the GitHub repository page in your browser.
2. Click **Code → Download ZIP**.
3. Extract the ZIP file somewhere easy (e.g., Desktop).

---

## 3️⃣ Step 3 — Open a terminal in the tool's folder

### **Windows**
1. Open the folder where you extracted the tool.
2. **Right-click → Open in Terminal** (or "Open PowerShell here").

### **macOS**
1. Open Terminal.
2. Type `cd ` (with a space after it).
3. Drag the folder into the Terminal window.
4. Press Enter.

### **Linux**
1. Right-click in the folder → **Open Terminal here**.

---

## 4️⃣ Step 4 — Install optional helpers

This tool works without extras, but two add-ons make it nicer:
- **tqdm** → progress bars
- **send2trash** → safe “send to Trash” instead of deleting

In your terminal:
```bash
# Windows
pip install tqdm send2trash

# macOS / Linux
python3 -m pip install tqdm send2trash
```

---

## 5️⃣ Step 5 — Run the tool (safe mode)

By default, the tool does **nothing permanent** — it just shows what it *would* do.

**Example:**
```bash
# Windows
python dedupe_and_organize.py "C:\Users\YourName\Downloads"

# macOS / Linux
python3 dedupe_and_organize.py ~/Downloads
```

You’ll see lines like:
```
Hash: 67ff41b9d45c KEEP: /home/user/Downloads/file1.jpg
[DRY] TRASH /home/user/Downloads/file1_copy.jpg
```
`[DRY]` means **no changes made yet**.

---

## 6️⃣ Step 6 — Actually remove duplicates (safe Trash mode)

To send duplicates to your **Recycle Bin / Trash**:
```bash
# Windows
python dedupe_and_organize.py "C:\Users\YourName\Downloads" --apply --duplicate-action trash

# macOS / Linux
python3 dedupe_and_organize.py ~/Downloads --apply --duplicate-action trash
```

---

## 7️⃣ Step 7 — Move duplicates to a folder

To keep duplicates in a special folder for review:
```bash
# Windows
python dedupe_and_organize.py "C:\Users\YourName\Downloads" --apply --duplicate-action move --duplicates-dir "C:\Users\YourName\Duplicates"

# macOS / Linux
python3 dedupe_and_organize.py ~/Downloads --apply --duplicate-action move --duplicates-dir ~/Duplicates
```

---

## 8️⃣ Step 8 — Organize kept files

### **By year/month**
```bash
# Windows
python dedupe_and_organize.py "C:\Users\YourName\Photos" --apply --organize kept --org-mode yyyymm --organize-root "C:\Users\YourName\Organized"

# macOS / Linux
python3 dedupe_and_organize.py ~/Photos --apply --organize kept --org-mode yyyymm --organize-root ~/Organized
```
Creates:
```
Organized/
  2024/
    01/
      file1.jpg
      file2.jpg
```

### **By file extension**
```bash
# Windows
python dedupe_and_organize.py "C:\Users\YourName\Photos" --apply --organize kept --org-mode ext --organize-root "C:\Users\YourName\Organized"

# macOS / Linux
python3 dedupe_and_organize.py ~/Photos --apply --organize kept --org-mode ext --organize-root ~/Organized
```
Creates:
```
Organized/
  _by_ext/
    jpg/
    mp4/
```

---

## 9️⃣ Step 9 — Extra tips

- Always **test without `--apply`** first.
- Use `--workers 8` for faster scanning on multi-core computers.
- Skip tiny files:
  ```bash
  --min-size 1048576   # only files >= 1 MB
  ```
- Save reports:
  ```bash
  --report-csv report.csv --report-json report.json
  ```

---

## 🔄 How to undo changes

- **Trash mode** → open your system Trash/Recycle Bin and restore files.
- **Move mode** → duplicates are in the `--duplicates-dir` you chose; move them back manually.
- **Delete mode** → cannot be undone.

---

## ✅ You’re done!

Now you know how to:
- Install Python
- Download and open the tool
- Run safe previews
- Clean up duplicates without losing anything important
- Organize your files automatically
