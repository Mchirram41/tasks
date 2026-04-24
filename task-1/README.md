
# B17 - Linux Tasks

This repository contains basic to intermediate Linux practice tasks covering file management, permissions, process monitoring, package management, and networking.

---

## Level 1: Basic Linux Commands

```bash
# 1. Create directory
mkdir ~/linux_practice

# 2. Create 5 empty files
cd ~/linux_practice
touch file1.txt file2.txt file3.txt file4.txt file5.txt

# 3. Write name and date into file1.txt
echo "Mahesh - $(date)" > file1.txt

# 4. Display content
cat file1.txt
less file1.txt

# 5. Copy file
cp file1.txt backup_file1.txt

# 6. Rename file
mv file2.txt data.txt

# 7. Delete file
rm file5.txt
```

---

## Level 2: File Permissions & Ownership

```bash
# 8. Check permissions
ls -l

# 9. Change permission of data.txt to rw-r-----
chmod 640 data.txt

# 10. Make file executable
chmod +x file3.txt

# 11. Change ownership
sudo chown username file4.txt
```

### Permission Explanation

* **r (read)** → View file content
* **w (write)** → Modify file content
* **x (execute)** → Run file as a program/script

---

## Level 3: Searching & Viewing Files

```bash
# 13. Search for "Linux"
grep "Linux" *.txt

# 14. Count lines, words, characters
wc file1.txt

# 15. View last 10 lines of logs
tail -10 /var/log/syslog     # Ubuntu
tail -10 /var/log/messages   # RHEL/CentOS

# 16. Find all .txt files
find ~/linux_practice -name "*.txt"
```

---

## Level 4: Process & System Monitoring

```bash
# 17. List running processes
ps -ef

# 18. Find PID
pidof sshd
pidof systemd

# 19. Kill process
kill <PID>

# 20. CPU & memory usage
top

# 21. Disk usage
df -h
du -sh *
```

---

## Level 5: Package Management

```bash
# 22. Install tree
sudo apt install tree        # Ubuntu
sudo yum install tree        # RHEL/CentOS

# 23. Remove tree
sudo apt remove tree
sudo yum remove tree

# 24. Check git version
git --version

# 25. List installed packages
dpkg -l        # Ubuntu
rpm -qa        # RHEL/CentOS
```

---

## Level 6: Networking Basics

```bash
# 26. Check IP address
ip a

# 27. Test connectivity
ping google.com

# 28. Display open ports
ss -tuln

# 29. Check DNS configuration
cat /etc/resolv.conf

# 30. Download a file
wget <URL>
curl -O <URL>
```

---

## Notes

* Replace `username` with your system username.
* Use `sudo` where required.
* Commands may vary slightly depending on Linux distribution.
* Ensure required packages are installed before running commands.

---

## Author

Mahesh
