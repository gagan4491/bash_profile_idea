# bash_profile_idea
# Bash Profile Configuration

This Bash profile setup enhances your shell environment by providing:
- **Automatic Homebrew configuration (for macOS users)**
- **Predefined SSH shortcut functions for different subnets**
- **Customized command prompt (`PS1`) showing username, hostname, and IP**
- **Environment variable for storing system IP**
- **Alias for `nano` with line numbers**

## 📌 Installation
1. Copy the script content into your **`~/.bashrc`** (Linux) or **`~/.bash_profile`** (macOS).
2. Apply changes by running:
   ```sh
   source ~/.bashrc   # For Linux
   source ~/.bash_profile  # For macOS
   ```

---

## ⚙️ Features & Explanation

### **1️⃣ Configure Homebrew (Mac Only)**
```sh
eval "$(/opt/homebrew/bin/brew shellenv)"
```
- Ensures that **Homebrew's environment** is properly set up.
- Required only for **Apple Silicon Macs** (M1, M2, M3 chips).

---

### **2️⃣ Set Default Editor to Nano**
```sh
export EDITOR=nano
alias nano='nano -l'
```
- **Sets `nano` as the default text editor**.
- `nano -l` enables **line numbers**.

---

### **3️⃣ Create SSH Shortcut Functions**
#### 🔹 **For IP Range: `10.15.X.Y`**
```sh
for subnet in 2 5 7 8 9; do
    for num in {1..254}; do
        eval "function q${subnet}${num}() { ssh root@10.15.${subnet}.$num; }"
    done
done
```
✅ **Creates SSH functions like:**  
- `q215` → Connects to `root@10.15.2.15`
- `q909` → Connects to `root@10.15.9.9`

#### 🔹 **For IP Range: `192.168.4.X`**
```sh
for num in {1..254}; do
    eval "function i$num() { ssh root@192.168.4.$num; }"
done
```
✅ **Creates SSH functions like:**  
- `i25` → Connects to `root@192.168.40.25`
- `i100` → Connects to `root@192.168.40.100`

#### 🔹 **For IP Range: `10.10.10.X`**
```sh
for num in {1..254}; do
    eval "function p$num() { ssh root@10.10.10.$num; }"
done
```
✅ **Creates SSH functions like:**  
- `p50` → Connects to `root@10.10.10.50`
- `p200` → Connects to `root@10.10.10.200`

---

### **4️⃣ Get System IP Address**
```sh
THEIP=$(ifconfig en0 | grep 'inet ' | awk '{print $2}')
if [ -z "$THEIP" ]; then
    THEIP="No-IP"
fi
```
✅ **Retrieves the primary IPv4 address on macOS**  
✅ **Stores "No-IP" if no IP is found**

---

### **5️⃣ Get System Hostname**
```sh
HOSTNAME=$(hostname)
```
✅ **Retrieves the system's hostname**  
✅ Used in the **command prompt display**

---

### **6️⃣ Customize the Bash Prompt (`PS1`)**
```sh
PS1="\[\e[33;1;31m\][\u@$HOSTNAME ($THEIP) \w] \[\e[0m\] "
export PS1
```
✅ **Displays username, hostname, and IP in the prompt**  
✅ **Example:**
```
[user@MacBookPro (192.168.1.100) ~/Documents] $
```

---

### **7️⃣ Export the IP as an Environment Variable**
```sh
MY_IP_ADDRESS=$THEIP
export MY_IP_ADDRESS
```
✅ **Makes the system’s IP available in other scripts**  
✅ Can be accessed using `$MY_IP_ADDRESS`

---

## 🎯 **Usage Guide**
### **🔹 Use SSH Shortcuts:**
```sh
q2015  # SSH into 10.15.20.15
i50   # SSH into 192.168.40.50
p100  # SSH into 10.10.10.100
```

### **🔹 Check Your IP & Hostname in Prompt**
```
[user@MyMac (192.168.1.10) ~/Desktop] $
```

---

## 🚀 **Summary**
| **Feature** | **Purpose** |
|------------|------------|
| **Homebrew config** | Ensures correct environment on macOS |
| **Nano as default editor** | Sets `nano` with line numbers |
| **SSH shortcuts** | Quick SSH access to different subnets |
| **Dynamic IP detection** | Fetches system’s primary IP |
| **Custom Bash Prompt** | Shows username, hostname, and IP |
| **Environment variable (`MY_IP_ADDRESS`)** | Stores system IP for use in scripts |

---

### 🎯 **Now your Bash profile is optimized for quick SSH access and system visibility!** 🚀

