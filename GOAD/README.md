\# 🧠 GOAD Lab Deployment – Lessons Learned \& Troubleshooting Guide



\## 📌 Overview



This document captures the full deployment process of the \*\*GOAD (Game of Active Directory)\*\* lab, including challenges encountered, root causes, and resolutions.



The goal was to build a realistic Active Directory lab environment for penetration testing practice aligned with PNPT objectives.



\---



\## 🏗️ Final Working Architecture



| Component        | Role                                  |

| ---------------- | ------------------------------------- |

| Windows Host     | Runs VirtualBox + Vagrant             |

| WSL (Ubuntu)     | Ansible control node + GOAD execution |

| Kali VM (VMware) | Attack machine (post-deployment)      |



\---



\## ⚠️ Key Lessons Learned



\### 1. ❌ Native Windows is NOT a Valid Ansible Control Node



\* Attempted to run `goad.py` using Windows Python

\* Encountered repeated dependency and build failures (`ansible-core`)



\*\*Root Cause:\*\*



\* Ansible is not designed to run as a control node on native Windows



\*\*Solution:\*\*



\* Installed WSL (Ubuntu)

\* Ran GOAD from Linux environment



\---



\### 2. ❌ Python Version Compatibility Issues



\* Initial system used Python 3.14

\* `ansible-core` failed to build wheels



\*\*Root Cause:\*\*



\* Python 3.14 is too new for some dependencies



\*\*Solution:\*\*



\* Switched to Python 3.12

\* Used `requirements\_311.yml` instead of `requirements.yml`



\---



\### 3. ❌ Installing Dependencies Outside a Virtual Environment



\* Encountered:



&#x20; ```

&#x20; externally-managed-environment

&#x20; ```



\*\*Root Cause:\*\*



\* Ubuntu prevents global pip installs



\*\*Solution:\*\*



\* Created virtual environment:



&#x20; ```

&#x20; python3 -m venv goad-venv

&#x20; source goad-venv/bin/activate

&#x20; ```



\---



\### 4. ❌ Running from Windows-Mounted Path (`/mnt/c`)



\* Errors:



&#x20; \* `Operation not permitted`

&#x20; \* Failed pip installs



\*\*Root Cause:\*\*



\* WSL filesystem permissions conflict with Windows-mounted drives



\*\*Solution:\*\*



\* Moved repo to Linux filesystem:



&#x20; ```

&#x20; \~/labs/GOAD-main

&#x20; ```



\---



\### 5. ❌ Vagrant Not Found in WSL



\* Error:



&#x20; ```

&#x20; vagrant: command not found

&#x20; ```



\*\*Root Cause:\*\*



\* Vagrant installed on Windows, not visible to WSL



\*\*Solution:\*\*



\* Located binary:



&#x20; ```

&#x20; /mnt/c/Program Files/Vagrant/bin/vagrant.exe

&#x20; ```

\* Added to PATH:



&#x20; ```

&#x20; export PATH="$PATH:/mnt/c/Program Files/Vagrant/bin"

&#x20; ```

\* Created alias:



&#x20; ```

&#x20; alias vagrant=vagrant.exe

&#x20; ```



\---



\### 6. ❌ GOAD Installed in OneDrive Path



\* Potential file locking and sync conflicts



\*\*Solution:\*\*



\* Moved repo to:



&#x20; ```

&#x20; C:\\GOAD

&#x20; ```



\---



\### 7. ❌ Nested Repository Structure



\* Duplicate `GOAD-main` folder detected



\*\*Solution:\*\*



```

rm -rf GOAD-main

```



\---



\## ✅ Final Working Commands



\### WSL Setup



```

sudo apt update

sudo apt install -y python3 python3-pip python3-venv ansible-core

```



\### Environment Setup



```

cd \~/labs/GOAD-main

python3 -m venv goad-venv

source goad-venv/bin/activate

pip install -r requirements\_311.yml

```



\### Vagrant Integration



```

export PATH="$PATH:/mnt/c/Program Files/Vagrant/bin"

alias vagrant=vagrant.exe

```



\### Launch GOAD



```

python3 goad.py -t install -l GOAD-Light -p virtualbox

```



\---



\## 💥 Key Takeaways



\* Always match tools to their \*\*supported operating environment\*\*

\* Avoid mixing Linux tooling with Windows paths

\* Use \*\*virtual environments\*\* for Python projects

\* Understand \*\*host vs guest architecture\*\*

\* Read error messages — they often point directly to the root cause



\---



\## 🎯 Outcome



Successfully deployed:



\* Active Directory Domain

\* Domain Controller(s)

\* Workstations

\* Vulnerable configurations for pentesting practice



\---



\## 🚀 Next Steps



\* Validate network connectivity from Kali VM

\* Begin enumeration (LDAP, SMB, Kerberos)

\* Practice:



&#x20; \* NTLM Relay

&#x20; \* Kerberoasting

&#x20; \* Privilege escalation



\---



\## 🧠 Author Notes



This setup process reinforced real-world troubleshooting skills including:



\* Cross-platform integration (Windows + Linux)

\* Dependency resolution

\* Virtualization layering

\* Infrastructure-as-Code deployment



\---



\## 🔥 Summary



This was not just a lab setup — it was a practical exercise in:



\* Systems thinking

\* Debugging complex environments

\* Building a professional pentesting lab from scratch



\---



