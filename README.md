# Linux Graded Lab Assignment — Modules 1–4

**Submitted by:** Ujjwal Prakash  
**Date:** July 1, 2026  
**Course:** Linux Fundamentals  

---

## Overview

This repository contains the complete lab assignment for Modules 1–4, covering fundamental Linux concepts including environment verification, file permissions, filesystem links, I/O operations, and storage management.

All commands were executed on a macOS/Darwin system (ARM64 — Apple M1) running Darwin Kernel 25.0.0, which shares the same Unix/POSIX foundation as Linux.

---

## Repository Structure

```
Linux_Lab_Assignment/
│
├── Q1_Linux_Environment/
│   ├── Environment_Report.txt       ← Complete report with all command outputs
│   └── screenshots/                 ← Command execution screenshots
│
├── Q2_Secure_Workspace/
│   ├── Project_Workspace_Report.txt ← Workspace setup report
│   ├── ProjectWorkspace/            ← Actual workspace created during lab
│   │   ├── docs/
│   │   │   ├── plan.txt
│   │   │   └── requirements.txt
│   │   ├── scripts/
│   │   │   └── deploy.sh
│   │   ├── logs/
│   │   │   └── access.log
│   │   └── backup/
│   └── screenshots/
│
├── Q3_Link_Analysis/
│   ├── Link_Analysis_Report.txt     ← Full link experiment report
│   ├── hardlink.txt                 ← Hard link (original deleted)
│   ├── symlink.txt                  ← Symbolic link (now broken — expected)
│   └── screenshots/
│
├── Q4_IO_Investigation/
│   ├── IO_Investigation_Report.txt  ← I/O investigation report
│   ├── output.txt                   ← Created via output redirection
│   ├── error.txt                    ← Created via error redirection
│   ├── result.txt                   ← Combined stdout + stderr redirection
│   └── screenshots/
│
├── Q5_Storage_Assessment/
│   ├── Storage_Assessment_Report.txt ← Created using vi editor
│   └── screenshots/
│
└── README.md
```

---

## Questions Summary

### Q1 — Linux Environment Verification (4 Marks)
Verified user identity, group memberships, current shell, working directory, file listing, and network connectivity. Commands used: `whoami`, `id`, `groups`, `echo $SHELL`, `pwd`, `ls -la`, `ping`, `uname -a`.

**Key Finding:** User `ujjwalprakash` has admin group access. System running Darwin 25.0.0 on ARM64. Network stable with 10.7ms average latency to Google.

---

### Q2 — Secure Project Workspace Setup (4 Marks)
Created a multi-directory project workspace and configured layered permissions. Root workspace restricted to owner-only (chmod 700), with file-specific permissions for scripts (755) and sensitive docs (640).

**Key Finding:** Default umask 022 creates files with 644 permissions. Applying 700 to the root workspace blocks all unauthorized access at the directory level.

---

### Q3 — File System and Link Analysis (4 Marks)
Created original.txt, a hard link, and a symbolic link. Investigated inode sharing, demonstrated data synchronization through hard links, and showed symlink breakage upon original file deletion.

**Key Finding:** Hard link (inode 27939596) and original share the same inode — data persists after deletion. Symlink (inode 27939599) becomes broken ("No such file or directory").

---

### Q4 — File Access and I/O Investigation (4 Marks)
Used `lsof` to inspect open files, examined file descriptors (FDs 0,1,2), demonstrated stdout/stderr redirection, and inspected resource limits via `ulimit -a`.

**Key Finding:** The application logging issue was traced to missing `2>&1` — stderr was not being captured in the log file. Correct pattern: `./app >> /var/log/app.log 2>&1`.

---

### Q5 — Storage Health Assessment (4 Marks)
Assessed storage devices using `diskutil list`, `df -h`, `df -i`, and `du -sh`. Created the report file using **vi editor**. SMART status is verified (healthy). Data volume at 66% capacity.

**Key Finding:** Storage is healthy with 65 GB free. Inode utilization is < 0.3%. Recommend monitoring when usage exceeds 80%.

---

## Tools and Commands Used

| Category | Commands |
|----------|----------|
| Identity | `whoami`, `id`, `groups` |
| System Info | `uname -a`, `echo $SHELL`, `pwd` |
| File Operations | `ls -la`, `ls -li`, `touch`, `mkdir`, `echo`, `cat`, `rm` |
| Permissions | `chmod`, `umask`, `stat` |
| Links | `ln`, `ln -s` |
| I/O | `lsof`, `ulimit`, `>`, `>>`, `2>`, `2>&1` |
| Storage | `df -h`, `df -i`, `du -sh`, `diskutil list` |
| Network | `ping` |
| Editor | `vi` |

---

## Notes
- All commands were executed as user `ujjwalprakash` (non-root, with admin group access)
- The symbolic link in Q3 appears broken — this is **intentional and expected** as part of the experiment
- Screenshots of all command executions are included in the `screenshots/` folder of each question directory
