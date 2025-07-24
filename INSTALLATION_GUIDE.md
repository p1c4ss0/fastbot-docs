# 💻 Installation Guide - Set Up the Trading Bot on Your Computer

**This guide will help you install the trading bot software on Windows, Mac, or Linux computers.**

## ⚠️ **Before You Start**

🔑 **You need Zerodha API credentials** - Get them first from [🔐 Zerodha Setup Guide](ZERODHA_SETUP_GUIDE.md)  
⏰ **Allow 30-60 minutes** for complete installation  
💻 **You need admin/sudo access** on your computer  
🌐 **Stable internet connection** required for downloading dependencies

---

## 🎯 **What You'll Accomplish**

After following this guide, you'll have:
- ✅ **Python 3.8+** installed and working
- ✅ **Trading bot software** installed on your computer
- ✅ **All dependencies** properly configured
- ✅ **Working installation** tested and verified
- ✅ **Ready to configure** with your API credentials

---

## 🖥️ **Choose Your Operating System**

Click on your operating system for specific instructions:

- [🪟 **Windows Installation**](#windows-installation) - Windows 10/11
- [🍎 **Mac Installation (Apple Silicon)**](#mac-installation-apple-silicon) - M1/M2/M3/M4 Macs
- [🍎 **Mac Installation (Intel)**](#mac-installation-intel) - Older Intel Macs
- [🐧 **Linux Installation**](#linux-installation) - Ubuntu/Debian/CentOS

---

## 🪟 **Windows Installation**

### **Step 1: Check Your Windows Version**

1. **Press `Windows + R`** keys together
2. **Type `winver`** and press Enter
3. **Make sure you have:** Windows 10 (version 1909+) or Windows 11
4. **If older:** Update Windows before continuing

### **Step 2: Install Python**

#### **2.1 Download Python**
1. **Go to:** https://www.python.org/downloads/windows/
2. **Download:** Latest Python 3.11 or 3.12 (stable release)
3. **Choose:** Windows installer (64-bit) - file ends with `-amd64.exe`

#### **2.2 Install Python**
1. **Run the downloaded file** (python-3.11.x-amd64.exe)
2. **IMPORTANT:** Check "Add Python to PATH" at the bottom
3. **Choose:** "Install Now" (recommended)
4. **Wait:** Installation takes 2-5 minutes
5. **Click:** "Close" when done

#### **2.3 Verify Python Installation**
1. **Press `Windows + R`**
2. **Type `cmd`** and press Enter
3. **Type:** `python --version`
4. **Should show:** `Python 3.11.x` or similar
5. **If error:** Restart your computer and try again

### **Step 3: Download Trading Bot**

#### **3.1 Get the Bot Files**
**Option A: Download ZIP (Easier)**
1. **Go to:** Your bot's GitHub page or source
2. **Click:** Green "Code" button
3. **Choose:** "Download ZIP"
4. **Extract:** To `C:\TradingBot\` folder

**Option B: Use Git (Advanced)**
1. **Install Git:** Download from https://git-scm.com/
2. **Open Command Prompt**
3. **Run:** `git clone <repository-url> C:\TradingBot`

#### **3.2 Navigate to Bot Folder**
1. **Open Command Prompt** as Administrator
2. **Type:** `cd C:\TradingBot`
3. **Press Enter**

### **Step 4: Run Automated Setup**

1. **In Command Prompt, type:**
   ```cmd
   python setup.py
   ```
2. **Press Enter** and wait
3. **Follow prompts** on screen
4. **When asked about TA-Lib:** Choose "Install manually" 

### **Step 5: Install TA-Lib (Technical Analysis Library)**

TA-Lib is tricky on Windows, but here's the easiest way:

#### **5.1 Download TA-Lib Wheel File**
1. **Go to:** https://www.lfd.uci.edu/~gohlke/pythonlibs/#ta-lib
2. **Find:** `TA_Lib‑0.4.28‑cp311‑cp311‑win_amd64.whl` (adjust for your Python version)
3. **Download:** The .whl file to your Downloads folder

#### **5.2 Install TA-Lib**
1. **In Command Prompt:**
   ```cmd
   cd C:\Users\%USERNAME%\Downloads
   pip install TA_Lib-0.4.28-cp311-cp311-win_amd64.whl
   ```
2. **Adjust filename** to match what you downloaded
3. **Wait:** Should install successfully

### **Step 6: Test Installation**

1. **Go back to bot folder:**
   ```cmd
   cd C:\TradingBot
   ```
2. **Run test:**
   ```cmd
   python -c "import pandas, numpy, talib; print('✅ All packages working!')"
   ```
3. **Should see:** `✅ All packages working!`

### **Step 7: Configure API Credentials**

1. **In the TradingBot folder, find:** `secrets.json`
2. **Open with:** Notepad or any text editor
3. **Add your credentials** from the Zerodha setup guide
4. **Save the file**

### **Step 8: Test Complete Installation**

```cmd
python main.py --help
```

**Should show:** Help text with available commands

**🎉 Congratulations! Windows installation complete!**

---

## 🍎 **Mac Installation (Apple Silicon)**

*For M1, M2, M3, M4 MacBooks and iMacs*

### **Step 1: Check Your Mac**

1. **Click Apple menu** → About This Mac
2. **Look for:** "Apple M1", "Apple M2", "Apple M3", or "Apple M4"
3. **If you see Intel:** Use Intel Mac instructions instead

### **Step 2: Install Homebrew (Package Manager)**

1. **Open Terminal** (Applications → Utilities → Terminal)
2. **Copy and paste this command:**
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
3. **Press Enter** and follow prompts
4. **Enter your password** when asked
5. **Wait:** Installation takes 5-10 minutes

### **Step 3: Install Python**

```bash
# Install Python via Homebrew
brew install python@3.11

# Verify installation
python3 --version
```

**Should show:** `Python 3.11.x`

### **Step 4: Download Trading Bot**

#### **4.1 Create folder and download**
```bash
# Create directory
mkdir ~/TradingBot
cd ~/TradingBot

# Download bot (replace with actual URL)
curl -L -o tradingbot.zip "YOUR_BOT_DOWNLOAD_URL"
unzip tradingbot.zip
```

#### **4.2 Or use Git**
```bash
git clone <repository-url> ~/TradingBot
cd ~/TradingBot
```

### **Step 5: Run Automated Setup**

```bash
# Navigate to bot folder
cd ~/TradingBot

# Run setup script
python3 setup.py
```

**The setup script will:**
- Install all Python dependencies
- Install TA-Lib automatically
- Create necessary directories
- Test everything for you

### **Step 6: Install Additional Dependencies**

```bash
# Install TA-Lib (for technical analysis)
brew install ta-lib

# Install Python packages
pip3 install -r requirements.txt
```

### **Step 7: Test Installation**

```bash
# Test Python packages
python3 -c "import pandas, numpy, talib, torch; print('✅ All packages working!')"

# Test bot
python3 main.py --help
```

**Should see:** Help text with available commands

### **Step 8: Configure API Credentials**

```bash
# Edit secrets file
nano secrets.json
```

1. **Add your API credentials** from Zerodha setup guide
2. **Save:** Press `Ctrl+X`, then `Y`, then `Enter`

**🎉 Congratulations! Mac (Apple Silicon) installation complete!**

---

## 🍎 **Mac Installation (Intel)**

*For older Intel-based Macs*

### **Step 1: Check Your Mac**

1. **Click Apple menu** → About This Mac
2. **Look for:** "Intel Core i5", "Intel Core i7", etc.
3. **If you see Apple M1/M2/M3/M4:** Use Apple Silicon instructions instead

### **Step 2: Install Homebrew**

```bash
# Open Terminal and install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### **Step 3: Install Python and Dependencies**

```bash
# Install Python
brew install python@3.11

# Install TA-Lib (might take longer on Intel Macs)
brew install ta-lib

# Verify installations
python3 --version
```

### **Step 4: Download and Setup Bot**

```bash
# Create directory and download bot
mkdir ~/TradingBot
cd ~/TradingBot

# Run automated setup
python3 setup.py
```

### **Step 5: Handle Common Intel Mac Issues**

**If TA-Lib installation fails:**
```bash
# Try installing Xcode command line tools first
xcode-select --install

# Then try TA-Lib again
brew reinstall ta-lib
pip3 install TA-Lib
```

**If you get permission errors:**
```bash
# Fix Python permissions
sudo chown -R $(whoami) /usr/local/lib/python3.11/site-packages
```

### **Step 6: Test and Configure**

```bash
# Test installation
python3 -c "import pandas, numpy, talib; print('✅ All packages working!')"

# Configure credentials
nano secrets.json
```

**🎉 Congratulations! Mac (Intel) installation complete!**

---

## 🐧 **Linux Installation**

*For Ubuntu, Debian, CentOS, and other Linux distributions*

### **Step 1: Update System**

#### **Ubuntu/Debian:**
```bash
sudo apt update && sudo apt upgrade -y
```

#### **CentOS/RHEL:**
```bash
sudo yum update -y
# or for newer versions:
sudo dnf update -y
```

### **Step 2: Install Python and Dependencies**

#### **Ubuntu/Debian:**
```bash
# Install Python and development tools
sudo apt install python3 python3-pip python3-dev build-essential -y

# Install additional dependencies for TA-Lib
sudo apt install wget curl git -y
```

#### **CentOS/RHEL:**
```bash
# Install Python and development tools
sudo yum install python3 python3-pip python3-devel gcc gcc-c++ make -y

# Install additional tools
sudo yum install wget curl git -y
```

### **Step 3: Install TA-Lib from Source**

```bash
# Download TA-Lib source
cd /tmp
wget http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-src.tar.gz
tar -xzf ta-lib-0.4.0-src.tar.gz
cd ta-lib/

# Compile and install
./configure --prefix=/usr
make
sudo make install

# Update library cache
sudo ldconfig
```

### **Step 4: Download Trading Bot**

```bash
# Create directory
mkdir ~/TradingBot
cd ~/TradingBot

# Clone or download bot
git clone <repository-url> .
# or download and extract ZIP file
```

### **Step 5: Run Automated Setup**

```bash
# Navigate to bot directory
cd ~/TradingBot

# Run setup script
python3 setup.py
```

### **Step 6: Install Python Dependencies**

```bash
# Install Python packages
pip3 install -r requirements.txt

# Install TA-Lib Python wrapper
pip3 install TA-Lib
```

### **Step 7: Test Installation**

```bash
# Test all packages
python3 -c "import pandas, numpy, talib, sklearn, torch; print('✅ All packages working!')"

# Test bot
python3 main.py --help
```

### **Step 8: Configure Credentials**

```bash
# Edit secrets file
nano secrets.json
```

Add your Zerodha API credentials and save.

**🎉 Congratulations! Linux installation complete!**

---

## 🔧 **Post-Installation Setup (All Platforms)**

### **Step 1: Verify All Components**

Run this comprehensive test:

```bash
# Test all major components
python main.py --test-installation
```

**Should show:**
- ✅ Python version OK
- ✅ All packages installed
- ✅ TA-Lib working
- ✅ AI components ready
- ✅ Configuration files created

### **Step 2: Configure Your Settings**

1. **Edit `secrets.json`** with your Zerodha API credentials
2. **Review `trading_config.json`** for trading parameters
3. **Check `prefilter_config.json`** for stock filtering settings

### **Step 3: Run Your First Test**

```bash
# Test with paper trading (safe)
python main.py --mode dryrun --duration 60
```

**This will:**
- Run in simulation mode (no real money)
- Test for 60 minutes
- Show you how the bot works
- Generate a test report

---

## 🚨 **Troubleshooting Common Issues**

### **"Python command not found"**
**Windows:** Reinstall Python and check "Add to PATH"  
**Mac/Linux:** Use `python3` instead of `python`

### **"Permission denied" errors**
**Windows:** Run Command Prompt as Administrator  
**Mac/Linux:** Use `sudo` for system-wide installations

### **TA-Lib installation fails**
**Windows:** Download .whl file manually (see Step 5 above)  
**Mac:** Install Xcode command line tools first  
**Linux:** Install build tools and compile from source

### **"Module not found" errors**
```bash
# Reinstall requirements
pip install -r requirements.txt --force-reinstall
```

### **PyTorch/AI components fail**
**Check your platform:**
- Apple Silicon Macs: Should auto-detect MPS
- Intel Macs: Will use CPU only
- Windows: Will use CPU only (unless CUDA available)

---

## 📞 **Getting Help**

### **Installation Issues:**
1. **Check error messages** carefully
2. **Try running setup.py again** - it's safe to re-run
3. **Look in logs folder** for detailed error information
4. **Check our [Troubleshooting Guide](TROUBLESHOOTING.md)**

### **Platform-Specific Help:**
- **Windows:** Check Windows version compatibility
- **Mac:** Ensure Xcode command line tools installed
- **Linux:** Verify you have build tools installed

### **Still Stuck?**
- Create an issue in the GitHub repository
- Include your operating system and error messages
- Attach relevant log files

---

## ✅ **Installation Complete Checklist**

Before proceeding, make sure you have:

- [ ] **Python 3.8+** installed and working
- [ ] **All dependencies** installed successfully
- [ ] **TA-Lib** working (test with technical analysis)
- [ ] **Trading bot** responds to `python main.py --help`
- [ ] **secrets.json** created with your API credentials
- [ ] **Test run** completed successfully in dryrun mode
- [ ] **Logs folder** created and accessible

---

## 🎯 **What's Next?**

Now that installation is complete:

1. 👉 **Go to [📖 User Manual](USER_MANUAL.md)** - Learn how to use the bot
2. 👉 **Or go to [⚙️ Configuration Guide](CONFIGURATION_GUIDE.md)** - Customize settings
3. 👉 **Or go to [📊 Examples](EXAMPLES.md)** - See real trading examples

---

**🎉 Congratulations! Your trading bot is now installed and ready to use! 🎉**

---

*Last updated: July 2025 | Having issues? Check [TROUBLESHOOTING.md](TROUBLESHOOTING.md)*