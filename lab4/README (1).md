# Lab 4 — Linux VM Operations & Forensics

**Name:** Lujain Zia  
**Roll no:** 2023-BSE-034  
**Date:** October 16, 2025  

---

## Task 1 – Verify VM Resources in VMware

**Goal:** Confirm the VM resources that were allocated in Lab 1.

**Steps:**
- Open VMware Workstation and locate the Ubuntu Server VM.
- Inspect VM settings for: VM name, RAM, CPU, disk, and network adapter.
- 📸 Screenshot: `vm_settings.png`

---

## Task 2 – Start VM and Login via Host Terminal

**Steps:**
- Start or resume the VM in VMware.
- Connect using SSH:  
  `ssh student@<vm-ip-address>`
- 📸 Screenshot: `vm_login.png`
- Run:
  ```bash
  whoami
  pwd
  ```
- 📸 Screenshot: `whoami_pwd.png`

---

## Task 3 – Filesystem Exploration and Dotfiles

**Commands & Screenshots:**

- `ls -la /` → `ls_root.png`
- `ls -la /bin` → `ls_bin.png`
- `ls -la /sbin` → `ls_sbin.png`
- `ls -la /usr` → `ls_usr.png`
- `ls -la /opt` → `ls_opt.png`
- `ls -la /etc` → `ls_etc.png`
- `ls -la /dev` → `ls_dev.png`
- `ls -la /var` → `ls_var.png`
- `ls -la /tmp` → `ls_tmp.png`
- `ls -la ~` → `home_ls.png`

**Short Paragraph:**
- Open with: `nano ~/answers.md`
- Write and save a 3–5 sentence explanation on:
  - `/bin`, `/usr/bin`, `/usr/local/bin`
- 📸 Screenshot: `answers_md.png`

---

## Task 4 – Essential CLI Tasks (Navigation & File Ops)

**Workspace Creation:**
```bash
mkdir -p ~/lab4/workspace/python_project
cd ~/lab4/workspace/python_project
pwd
```
📸 Screenshots:
- `mkdir_workspace.png`
- `cd_workspace.png`
- `pwd_workspace.png`

**File Creation:**
```bash
nano README.md        # Add: Lab 4 README
nano main.py          # Add: print("hello lab4")
nano .env             # Add: ENV=lab4
```
📸 Screenshots:
- `nano_readme.png`
- `nano_main.png`
- `nano_env.png`

**List Files:**
```bash
ls -la
```
📸 Screenshot: `workspace_ls.png`

**File Operations:**
```bash
cp README.md README.copy.md      # → cp_readme.png
mv README.copy.md README.dev.md  # → mv_readme.png
rm README.dev.md                 # → rm_readme.png
```

**Directory Copy:**
```bash
mkdir -p ~/lab4/workspace/java_app
cp -r ~/lab4/workspace/python_project ~/lab4/workspace/java_app_copy
ls -la ~/lab4/workspace
```
📸 Screenshots:
- `mkdir_java_app.png`
- `cp_recursive.png`
- `copy_verify.png`

**History and Autocomplete:**
```bash
history
```
📸 Screenshot: `history.png`

Use `Tab` to auto-complete a command.
📸 Screenshot: `tab_completion.png`

---

## Task 5 – System Info & Processes

**Commands:**
```bash
uname -a                   # → uname.png
cat /proc/cpuinfo          # → cpuinfo.png
free -h                    # → meminfo.png
df -h                      # → diskinfo.png
cat /etc/os-release        # → os-release.png
ps aux                     # → processes.png
```

---

## Task 6 – Users & Account Verification (No sudo group)

**Create and Verify User:**
```bash
sudo adduser lab4user                # → adduser_lab4user.png
getent passwd lab4user              # → lab4user_passwd.png
su - lab4user                       # → su_lab4user.png
sudo whoami                         # → sudo_whoami.png
exit                                # → exit_back.png
sudo deluser --remove-home lab4user # (Optional) deluser.png
```

---

## Task 7 – Bonus: Demo Script

**Script Creation:**
```bash
nano ~/lab4/workspace/run-demo.sh
# Add:
# #!/bin/bash
# echo "Lab 4 demo: current user is $(whoami)"
# echo "Current time: $(date)"
# uptime
# free -h
```
📸 Screenshot: `nano_run_demo.png`

**Make Executable and Run:**
```bash
chmod +x ~/lab4/workspace/run-demo.sh    # → chmod_run_demo.png
~/lab4/workspace/run-demo.sh             # → run_demo_output.png
sudo ~/lab4/workspace/run-demo.sh        # (Optional) run_demo_output_sudo.png
```

---

# Exam Evaluation Questions

## Q1: Remote Access Verification

📸 Screenshots:
- `Q1_remote_connection.png`
- `Q1_user_verification.png` (via `whoami`, `pwd`)
- `Q1_host_confirmation.png` (via `hostname`)

---

## Q2: Filesystem Forensics

📸 Screenshots:
- `Q2_root_listing.png` (`ls -la /`)
- `Q2_os_version.png` (`cat /etc/os-release`)
- `Q2_directory_evidence.png` (for `/bin`, `/sbin`, `/usr`, `/opt`, etc.)
- `Q2_hidden_files.png` (`ls -la ~`)
- `Q2_report_file.png` (`nano Q2_report.md`)

---

## Q3: Evidence Handling

📸 Screenshots:
- `Q3_workspace_created.png` (`mkdir -p ~/analysis_lab/...`)
- `Q3_files_created.png` (manual creation via `nano`)
- `Q3_backup_handling.png` (copy, rename, delete)
- `Q3_workspace_backup.png` (`cp -r ~/analysis_lab ~/evidence_backup`)
- `Q3_command_history.png` (`history`)
- `Q3_autocomplete.png` (using `Tab`)

---

## Q4: System Profiling

📸 Screenshots:
- `Q4_system_info.png` (`uname -a`)
- `Q4_resource_info.png` (`free -h`, `df -h`)
- `Q4_process_list.png` (`ps aux`)

---

## Q5: User Audit & Privilege Escalation

📸 Screenshots:
- `Q5_user_created.png` (`adduser lab4user`)
- `Q5_user_verified.png` (`getent passwd lab4user`)
- `Q5_user_login.png` (`su - lab4user`)
- `Q5_permission_denied.png` (`sudo whoami`)
- `Q5_switch_back.png` (`exit`)
- `Q5_authlog_analysis.png` (`cat /var/log/auth.log`)
- `Q5_user_removed.png` (optional)