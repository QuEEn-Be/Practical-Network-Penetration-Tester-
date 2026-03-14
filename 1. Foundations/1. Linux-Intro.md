==================================================

🐧 INTRO TO LINUX

==================================================



📌 Overview

\--------------------------------------------------



Linux is the primary operating system used in penetration testing, cybersecurity research, and server infrastructure.



Most offensive security tools run on Linux-based distributions such as Kali Linux, Parrot OS, or Ubuntu.



Understanding core Linux commands is essential for navigating systems, managing files, analyzing processes, and interacting with networks during penetration testing engagements.



This section provides a reference for commonly used Linux commands.



\--------------------------------------------------

🧠 Helpful Linux Commands

\--------------------------------------------------



==============================

📂 File \& Directory Navigation

==============================



ls

List directory contents.



cd

Change directory.



pwd

Print the current working directory.



cp

Copy files and directories.



mv

Move or rename files and directories.



rm

Remove files and directories.



mkdir

Create a new directory.



touch

Create a new file or update timestamps.



find

Search for files based on criteria.



locate

Quickly search for files using a database.



\--------------------------------------------------



==============================

📄 File Viewing \& Editing

==============================



cat

Display file contents.



less

View file contents with navigation.



more

Display file contents page by page.



tail

Display the end of a file.



tac

Display file contents in reverse order.



vi

Terminal text editor.



\--------------------------------------------------



==============================

💾 Disk \& Storage Management

==============================



df

Display filesystem disk space usage.



du

Estimate disk usage for files and directories.



fdisk

Manipulate disk partition tables.



parted

Create and modify disk partitions.



blkid

Display block device attributes.



mkfs

Create a filesystem.



fsck

Check and repair filesystem consistency.



\--------------------------------------------------



==============================

📦 Compression \& Archiving

==============================



tar

Archive files into a single file.



gzip

Compress files using gzip.



bzip2

Compress files using the bzip2 algorithm.



zip

Create compressed ZIP archives.



\--------------------------------------------------



==============================

🖥️ System Monitoring

==============================



top

Display active processes and system usage.



htop

Interactive process viewer.



pstree

Display running processes in a tree format.



vmstat

Show memory, CPU, and system statistics.



dstat

Display real-time system statistics.



uptime

Show system uptime and load average.



ps

Display currently running processes.



kill

Terminate a process by PID.



killall

Terminate processes by name.



\--------------------------------------------------



==============================

🌐 Networking Commands

==============================



ip

Manage network interfaces and routing.



ping

Test network connectivity using ICMP.



traceroute

Display packet routing paths.



mtr

Real-time network diagnostic tool.



netstat

Display network statistics and connections.



ss

Investigate socket connections.



nslookup

Query DNS servers.



dig

Advanced DNS lookup utility.



host

Perform DNS lookups.



nc

Netcat networking utility.



\--------------------------------------------------



==============================

🔐 Remote Access \& File Transfer

==============================



ssh

Secure remote access to systems.



scp

Secure file transfer over SSH.



rsync

Synchronize files between systems.



wget

Download files over HTTP/FTP.



curl

Transfer data using multiple protocols.



\--------------------------------------------------



==============================

👤 User \& Permission Management

==============================



sudo

Execute commands with elevated privileges.



chmod

Change file permissions.



chown

Change file ownership.



useradd

Create a new user.



userdel

Delete a user account.



usermod

Modify user account attributes.



passwd

Change a user password.



\--------------------------------------------------



==============================

⚙️ System Services \& Logs

==============================



systemctl

Manage system services.



journalctl

Query system logs.



dmesg

Display kernel ring buffer messages.



\--------------------------------------------------



==============================

🧵 Process \& Session Control

==============================



nohup

Run commands immune to hangups.



screen

Maintain sessions on remote servers.



tmux

Terminal multiplexer for managing sessions.



sleep

Pause command execution for a period of time.



wait

Wait for background processes to finish.



\--------------------------------------------------



==============================

🛠️ Additional Utilities

==============================



clear

Clear the terminal screen.



env

Run commands in a modified environment.



cheat

Display command-line cheatsheets.



tldr

Simplified help pages for commands.



bashtop

Modern system resource monitor.



bpytop

Python-based system resource monitor.



\--------------------------------------------------



==============================

⚡ Bash Scripts

==============================



Bash scripts allow automation of repetitive tasks and workflows.



Example execution:



./bashscript.sh



Automation through scripting is extremely valuable during penetration testing engagements.



\--------------------------------------------------



📚 Key Takeaways

\--------------------------------------------------



✔ Linux is the primary operating system used in penetration testing environments.



✔ Mastering basic command-line tools improves efficiency during security assessments.



✔ Many offensive security tools rely on Linux utilities and scripting for automation.



✔ Understanding system monitoring, networking, and file management commands is essential for both attackers and defenders.



\--------------------------------------------------



⚠️ Disclaimer

\--------------------------------------------------



All commands and demonstrations are intended for educational purposes and controlled lab environments only.



Always ensure you have authorization before interacting with any system or network.



==================================================

