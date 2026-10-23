# Linux Fundamentals

## Objective
To understand basic Linux commands, directory navigation, file management, file permissions, users, and groups using Kali Linux.

## Experiment 1: Basic Linux Commands

### Aim
To learn basic Linux commands for identifying the current directory, logged-in user, and directory contents.

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
Observation: Displays the present working directory.

**2. `whoami`**

Output:
```text
kali
```
Observation: Displays the username of the currently logged-in user.

**3. `ls -la`**

Output:
```text
total 8
drwxr-xr-x  2 kali kali 4096 Jul 21 15:38 .
drwx------ 18 kali kali 4096 Oct 23 10:12 ..
```
Observation: Lists files and directories, including hidden entries, along with their permissions and other details. The `.` represents the current directory, and `..` represents the parent directory.

### Result
Basic Linux commands were executed successfully to identify the current directory, user, and directory contents.

---

## Experiment 2: Linux File Permissions

### Aim
To create a file, examine its permissions, and modify its permissions using the `chmod` command.

### Commands Used
```bash
touch test.txt
ls -l test.txt
chmod 644 test.txt
ls -l test.txt
```

### Output and Observations

**1. Creating a file and checking its initial permissions**

Command:
```bash
touch test.txt
ls -l test.txt
```

Output:
```text
-rw-rw-r-- 1 kali kali 0 Oct 23 10:14 test.txt
```

Observation: An empty file named `test.txt` was created. Its initial permissions allowed the owner and group to read and write, while others could read it.

**2. Changing file permissions**

Command:
```bash
chmod 644 test.txt
ls -l test.txt
```

Output:
```text
-rw-r--r-- 1 kali kali 0 Oct 23 10:14 test.txt
```

Observation: The `chmod 644` command changed the file permissions.

- Owner (`rw-`): Read and write.
- Group (`r--`): Read only.
- Others (`r--`): Read only.

The numeric permission `644` represents `6` (read + write), `4` (read), and `4` (read).

### Result
A file was created, its initial permissions were examined, and its permissions were successfully changed to `644`.

---

## Experiment 3: Linux User and Group Identification

### Aim
To identify the current user's UID, primary GID, and supplementary group memberships.

### Command Used
```bash
id
```

### Output
```text
uid=1000(kali) gid=1000(kali) groups=1000(kali),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),100(users),101(netdev),102(scanner),118(wireshark),119(kaboxer),968(vboxsf),982(bluetooth),999(lpadmin)
```

### Observations

- **UID:** `1000` — identifies the user account `kali`.
- **GID:** `1000` — identifies the primary group `kali`.
- **Groups:** Lists the supplementary groups associated with the user.
- **sudo:** Membership may allow administrative commands, subject to system configuration.
- **wireshark:** A group associated with Wireshark-related permissions on this system.
- **vboxsf:** A group commonly associated with VirtualBox shared folders.

### Result
The `id` command was executed successfully to identify the current user's identity and group memberships.

---

## Overall Conclusion

The practical exercises introduced essential Linux fundamentals using Kali Linux. Basic terminal commands were used to inspect the working directory and logged-in user, file permissions were examined and modified, and user and group information was retrieved. These fundamentals provide a foundation for further cybersecurity exercises involving Linux security, reconnaissance, and security tools.

## Safety Note
All commands were performed in my own Kali Linux virtual machine. Further security testing will be restricted to systems and environments for which authorization has been obtained.
