# Linux Fundamentals — Practical Report

## Objective
To understand Linux commands, directory navigation, file management, file permissions, users, groups, running processes, and operating system information using Kali Linux.

---

## Experiment 1: Basic Linux Commands

### Aim
To identify the current working directory, logged-in user, and directory contents.

### Commands Used
```bash
pwd
whoami
ls -la
```

### Output and Observations

**1. `pwd`**

Output:
```text
/home/kali/Desktop
```

Displays the current working directory.

**2. `whoami`**

Output:
```text
kali
```

Displays the username of the currently logged-in user.

**3. `ls -la`**

Output:
```text
total 8
drwxr-xr-x  2 kali kali 4096 Jul 21 15:38 .
drwx------ 18 kali kali 4096 Oct 23 10:12 ..
```

Lists files and directories, including hidden entries, with detailed information. The `.` represents the current directory, and `..` represents the parent directory.

### Result
Basic Linux commands were executed to identify the current directory, username, and directory contents.

---

## Experiment 2: Linux File Permissions

### Aim
To create a file, examine its permissions, and modify them using `chmod`.

### Commands Used
```bash
touch test.txt
ls -l test.txt
chmod 644 test.txt
ls -l test.txt
```

### Output and Observations

**Initial permissions:**
```text
-rw-rw-r-- 1 kali kali 0 Oct 23 10:14 test.txt
```

**After running `chmod 644 test.txt`:**
```text
-rw-r--r-- 1 kali kali 0 Oct 23 10:14 test.txt
```

- `touch test.txt`: Creates an empty file.
- `ls -l test.txt`: Displays file permissions and details.
- `chmod 644 test.txt`: Changes file permissions.
- Owner (`rw-`): Read and write access.
- Group (`r--`): Read-only access.
- Others (`r--`): Read-only access.

The numeric permission `644` represents owner permissions `6` (read + write), group permissions `4` (read), and others' permissions `4` (read).

### Result
File permissions were examined and successfully changed to `644`.

---

## Experiment 3: Linux User and Group Identification

### Aim
To identify the current user's UID, primary GID, and supplementary groups.

### Command Used
```bash
id
```

### Output
```text
uid=1000(kali) gid=1000(kali) groups=1000(kali),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),100(users),101(netdev),102(scanner),118(wireshark),119(kaboxer),968(vboxsf),982(bluetooth),999(lpadmin)
```

### Observations
- **UID:** `1000` identifies the user account `kali`.
- **GID:** `1000` identifies the primary group `kali`.
- **Groups:** Displays the supplementary groups associated with the user.
- **sudo:** Membership may allow administrative commands, subject to system configuration.
- **wireshark:** A group associated with Wireshark-related permissions.
- **vboxsf:** A group commonly associated with VirtualBox shared folders.

### Result
The `id` command was used to inspect the current user's identity and group memberships.

---

## Experiment 4: Viewing Running Processes

### Aim
To identify processes running in the current terminal session.

### Command Used
```bash
ps
```

### Output
```text
PID TTY          TIME CMD
2198 pts/0    00:00:00 zsh
7686 pts/0    00:00:00 ps
```

### Observations
- **PID:** The unique process identification number.
- **TTY:** The terminal associated with the process.
- **TIME:** CPU time consumed by the process.
- **CMD:** The command or program name.
- `zsh` is the command-line shell used in the current terminal.
- `ps` displays process information for the current terminal session.

### Result
The `ps` command was executed to view processes associated with the current terminal.

---

## Experiment 5: Identifying Linux Distribution Information

### Aim
To identify the Linux distribution, version, and related system information.

### Command Used
```bash
cat /etc/os-release
```

### Output
```text
PRETTY_NAME="Kali GNU/Linux Rolling"
NAME="Kali GNU/Linux"
VERSION_ID="2026.3"
VERSION="2026.3"
VERSION_CODENAME=kali-rolling
ID=kali
ID_LIKE=debian
HOME_URL="https://www.kali.org/"
SUPPORT_URL="https://forums.kali.org/"
BUG_REPORT_URL="https://bugs.kali.org/"
ANSI_COLOR="1;31"
```

### Observations
- `PRETTY_NAME`: Displays the distribution's full name.
- `NAME`: Identifies the operating system.
- `VERSION_ID`: Shows the installed version, `2026.3`.
- `VERSION_CODENAME`: Identifies the rolling-release codename.
- `ID`: Identifies the distribution as Kali Linux.
- `ID_LIKE`: Indicates its relationship to Debian.

### Result
The operating system and version information were retrieved successfully.

---

## Experiment 6: Linux File and Directory Management

### Aim
To create directories and files, navigate between directories, write text into a file, and display its contents.

### Commands Used
```bash
mkdir recon-practice
cd recon-practice
touch notes.txt
echo "Learning Linux file management for cybersecurity." > notes.txt
cat notes.txt
ls -l
```

### Output

Output of `cat notes.txt`:
```text
Learning Linux file management for cybersecurity.
```

The `ls -l` command displays the file's permissions, owner, group, size, and filename.

### Observations
- `mkdir recon-practice`: Creates a directory.
- `cd recon-practice`: Changes the current working directory.
- `touch notes.txt`: Creates an empty file.
- `echo "..." > notes.txt`: Writes text into the file, replacing any existing contents.
- `cat notes.txt`: Displays the file contents.
- `ls -l`: Lists files with detailed information.

### Result
Directory creation, navigation, file creation, writing, and reading were practiced using Linux commands.

---

## Overall Conclusion

These practical exercises introduced essential Linux fundamentals using Kali Linux. They covered basic terminal commands, file permissions, user and group identification, process monitoring, operating system identification, and file management. These skills provide a foundation for further cybersecurity work involving reconnaissance, network enumeration, and security analysis.

## Safety and Authorization

All practical activities are intended for my own Kali Linux virtual machine or other authorized lab environments. Any security testing beyond my own systems will be conducted only with appropriate permission.
