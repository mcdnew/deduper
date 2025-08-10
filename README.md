# 📦 Dedupe & Organize

A safe, cross-platform Python tool to **find and handle duplicate files** by content (SHA-256 hash), **keep the newest copy**, and optionally **organize the kept files** into tidy folders.

By default, it’s **safe**: runs in **dry-run mode** and makes **no changes** until you add `--apply`.

---

## ✨ Features
- Works with **any file type** and on **Linux, macOS, and Windows**
- **Keeps the newest copy** (by modification time)
- Safe actions: **Move**, **Trash/Recycle Bin**, or **Delete**
- Optional **organize** step for kept files (by Year/Month or Extension)
- **Multithreaded hashing** for speed
- **Progress bars** with [`tqdm`](https://pypi.org/project/tqdm/)
- **Hash cache** for fast re-runs
- Detailed **CSV/JSON reports** for auditing

---

## ⚠️ Safety Model
- **Dry-run by default**: No files are changed unless you add `--apply`.
- **Keep latest**: The most recent file is preserved in each duplicate set.
- **Reversible options**:
  - `--duplicate-action trash` → send duplicates to system Trash/Recycle Bin
  - `--duplicate-action move` → move duplicates to a folder
- **Permanent deletion** only if you explicitly choose `--duplicate-action delete`

---

## 📦 Requirements
- Python **3.8+**
- Optional (recommended):
  - [`tqdm`](https://pypi.org/project/tqdm/) → pretty progress bars
  - [`send2trash`](https://pypi.org/project/Send2Trash/) → safe Trash/Recycle Bin support

Install extras:
```bash
# macOS / Linux
python3 -m pip install --upgrade pip
python3 -m pip install tqdm send2trash

# Windows (PowerShell)
py -m pip install --upgrade pip
py -m pip install tqdm send2trash
```

---

## 🚀 Quick Start

### Safe preview (dry-run)
**Linux/macOS**
```bash
python3 dedupe_and_organize.py ~/Downloads
```
**Windows**
```powershell
py .\dedupe_and_organize.py "$HOME\Downloads"
```

---

### Apply changes safely

#### Send duplicates to Trash/Recycle Bin (recommended)
```bash
python3 dedupe_and_organize.py ~/Downloads --apply --duplicate-action trash
```

#### Move duplicates to a folder
```bash
python3 dedupe_and_organize.py ~/Downloads --apply --duplicate-action move --duplicates-dir ~/Duplicates
```

#### Permanently delete duplicates (**dangerous**)
```bash
python3 dedupe_and_organize.py ~/Downloads --apply --duplicate-action delete
```

---

## 📂 Organize Kept Files

**By year/month**
```bash
python3 dedupe_and_organize.py ~/Photos --apply --organize kept --org-mode yyyymm --organize-root ~/Organized
```
Creates `~/Organized/YYYY/MM/...`

**By extension**
```bash
python3 dedupe_and_organize.py ~/Photos --apply --organize kept --org-mode ext --organize-root ~/Organized
```
Creates `~/Organized/_by_ext/jpg/`, `.../mp4/`, etc.

---

## ⚡ Performance
- Use `--workers N` to speed up hashing:
```bash
python3 dedupe_and_organize.py ~/BigFolder --workers 8
```
- Install `tqdm` for nice progress bars
- Large datasets benefit greatly from caching

---

## 💾 Hash Cache
Avoid re-hashing unchanged files.

- Default cache: `.dedupe_cache.json` in current folder
- Custom cache:
```bash
python3 dedupe_and_organize.py ~/Downloads --cache-file ~/.cache/dedupe_hashes.json
```
- Force re-hash:
```bash
python3 dedupe_and_organize.py ~/Downloads --refresh-cache
```
- Disable cache:
```bash
python3 dedupe_and_organize.py ~/Downloads --no-cache
```

---

## 📊 Reporting
Generate CSV/JSON reports:
```bash
python3 dedupe_and_organize.py ~/Downloads   --report-csv report.csv --report-json report.json
```

---

## 🛠 Command Reference
```
python3 dedupe_and_organize.py PATH [PATH2 PATH3 ...]
  --apply                         # perform actions; default is dry-run
  --duplicate-action {move,trash,delete}
  --duplicates-dir DIR            # for move action
  --organize {none,kept}
  --org-mode {yyyymm,ext}
  --organize-root DIR
  --workers N                     # hashing threads (0=auto)
  --min-size BYTES
  --follow-symlinks
  --report-csv FILE
  --report-json FILE
  --cache-file FILE
  --no-cache
  --refresh-cache
  --no-color
```

---

## 🧩 How duplicates are detected
- Files are grouped by **size** and **SHA-256 hash**
- Filenames and locations are irrelevant
- The newest file by modification time is kept

---

## 🔄 Recovery & Rollback
- **Trash mode**: restore from system Trash/Recycle Bin
- **Move mode**: files are in `--duplicates-dir`
- **Delete mode**: irreversible — use with extreme caution

---

## 🛡 Best Practices
- Always start with a **dry-run**
- Prefer **Trash** or **Move** for your first runs
- Keep cache in a persistent location for large datasets
- Adjust `--workers` for speed on big datasets

---

## ❓ FAQ

**Q: Will this change file contents?**  
A: No, only moves, trashes, or deletes duplicates.

**Q: What if two files have the same content but different timestamps?**  
A: The newest (highest mtime) is kept.

**Q: Does it follow symlinks?**  
A: Not by default; add `--follow-symlinks`.

**Q: Can I skip tiny files?**  
A: Yes, with `--min-size`.

---

## 📝 License
MIT License — free to use, modify, and share.
