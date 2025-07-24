# ⚡ Quick Start Tutorial

## 🎯 Complete Setup in 15 Minutes

This tutorial will get you from zero to your first paper trade in just 15 minutes!

### **Before You Start - Check Requirements ✅**

Make sure you have:
- [ ] **Computer:** Windows 10+, macOS 10.14+, or Linux Ubuntu 18+
- [ ] **Internet:** Stable broadband connection
- [ ] **Zerodha Account:** Active with some balance
- [ ] **Time:** 15 minutes of focused attention

---

## 🚀 Step 1: Get Your Zerodha API Keys (5 minutes)

### **1.1 Visit Zerodha Console**
- Go to: https://console.zerodha.com/
- Log in with your Zerodha credentials

### **1.2 Create API App**
- Click **"Create new app"**
- Fill in details:
  - **App name:** "My Trading Bot"
  - **App type:** "Connect"
  - **Redirect URL:** http://localhost
- Click **"Create"**

### **1.3 Get Your Keys**
You'll receive:
- **API Key:** `abc123xyz` (example)
- **API Secret:** `def456uvw` (example)

### **1.4 Generate Access Token**
- Click **"Request access token"**
- Complete 2FA verification
- Copy the **Access Token:** `ghi789rst` (example)

**💡 Pro Tip:** Keep these keys safe - you'll need them in Step 3!

---

## 💻 Step 2: Install the Bot (5 minutes)

### **2.1 Download the Bot**
```bash
# Method 1: Download ZIP from GitHub
# Go to: https://github.com/himanshugupta/zerodha-ai-trading-bot
# Click "Code" → "Download ZIP"

# Method 2: Clone with Git (if you have it)
git clone https://github.com/himanshugupta/zerodha-ai-trading-bot.git
cd zerodha-ai-trading-bot
```

### **2.2 Install Python Dependencies**
```bash
# Make sure you have Python 3.8+
python --version

# Install all required packages
pip install -r requirements.txt
```

### **2.3 Quick Installation Test**
```bash
# Test if everything installed correctly
python -c "print('✅ Python is working!')"
python -c "import pandas, numpy, kiteconnect; print('✅ All packages installed!')"
```

If you see both ✅ messages, you're ready for Step 3!

---

## 🔐 Step 3: Configure Your Bot (3 minutes)

### **3.1 Create Your Secrets File**
Create a file called `secrets.json` with your API keys:

```json
{
  "api_key": "your_api_key_here",
  "api_secret": "your_api_secret_here", 
  "access_token": "your_access_token_here",
  "telegram_token": "",
  "telegram_chat_id": ""
}
```

**Replace the placeholder values** with your actual keys from Step 1.

### **3.2 Test API Connection**
```bash
# Quick test to make sure your keys work
python -c "
from kiteconnect import KiteConnect
import json

with open('secrets.json', 'r') as f:
    secrets = json.load(f)

kite = KiteConnect(api_key=secrets['api_key'])
kite.set_access_token(secrets['access_token'])

try:
    profile = kite.profile()
    print('✅ API connection successful!')
    print(f'Hello, {profile[\"user_name\"]}!')
except Exception as e:
    print(f'❌ API Error: {e}')
    print('Please check your API keys in secrets.json')
"
```

If you see "✅ API connection successful!", you're ready for your first trade!

---

## 🎪 Step 4: Your First Paper Trade (2 minutes)

### **4.1 Start Paper Trading**
```bash
# Start the bot in paper trading mode (no real money!)
python main.py --mode dryrun --strategy catalyst
```

You should see:
```
███████     █████     ███████    ████████        ██████   ██████  ████████ 
**************************************************                                                                           
F.A.S.T. Bot (fully automated super trading) v1.0                                     
--** Backtest | Dryrun | Live Trading **--

✓ System checks passed
✓ Current time: 2024-07-24 14:30:00 IST
✓ Market status: OPEN
✅ Using strategy from CLI: 🎯 Catalyst-Driven Strategy
🤖 AI Status: 🤖 ENABLED | Mode: HYBRID | Confidence: 70%

Starting dryrun with capital ₹1,00,000.00
Bot will run until market closes or process is terminated
```

### **4.2 Watch Your First Trades**
The bot will:
- 🔍 **Scan stocks** every 15 seconds
- 📊 **Analyze signals** using AI and technical indicators  
- 💰 **Make paper trades** when good opportunities arise
- 📈 **Show real-time updates** in the terminal

**Example trade output:**
```
[14:32:15] 🎯 SIGNAL DETECTED: RELIANCE (Score: 87.3)
[14:32:16] 💰 BUY ORDER: RELIANCE @ ₹2,456.70 (Qty: 5)
[14:32:17] ✅ ORDER EXECUTED: Trade ID: DR001
[14:47:23] 📈 TARGET HIT: T1 reached (+1.2%) - Partial exit
[14:52:10] 💵 TRADE CLOSED: +₹147.80 profit
```

### **4.3 Stop the Bot**
When you want to stop:
- Press **Ctrl+C** in the terminal
- The bot will show you a summary of all trades

---

## 🎉 Congratulations! You're Trading!

### **What Just Happened?**
In just 15 minutes, you've:
- ✅ **Connected to Zerodha's API**
- ✅ **Installed a professional trading bot**
- ✅ **Made your first automated trades** (with fake money)
- ✅ **Learned how algorithmic trading works**

### **Your Trade Summary Will Look Like:**
```
🏁 DRYRUN SESSION COMPLETED
═══════════════════════════════════════════════════════
📊 Session Duration: 2.3 hours
💰 Total P&L: ₹847.30
📈 Total Trades: 6
🎯 Win Rate: 66.7% (4W/2L)
📊 Average P&L per Trade: ₹141.22

✅ WINNING TRADES:
   RELIANCE: +₹147.80 (T1 Target)
   INFY: +₹234.50 (T2 Target)
   TCS: +₹189.30 (T1 Target)
   HDFC: +₹98.70 (T1 Target)

❌ LOSING TRADES:
   WIPRO: -₹67.50 (Stop Loss)
   AXIS: -₹155.50 (Stop Loss)

🏆 SESSION RESULT: PROFITABLE! 🎉
```

---

## 🎓 What's Next?

### **Immediate Next Steps:**
1. **📖 Read the [User Manual](USER_MANUAL.md)** - Understand all features
2. **🔧 Check [Configuration Guide](CONFIGURATION_GUIDE.md)** - Customize settings
3. **📊 Run more paper trading** - Practice different market conditions
4. **🛡️ Read [Safety Guide](SAFETY_GUIDE.md)** - Before using real money

### **This Week:**
- **Practice daily** with paper trading
- **Keep notes** of what works and what doesn't
- **Try different strategies** (catalyst vs momentum)
- **Join the community** for tips and support

### **Before Going Live:**
- **At least 1 week** of successful paper trading
- **Understand all features** and configuration options
- **Set strict risk limits** you can afford to lose
- **Start with small amounts** (₹5,000-10,000)

---

## 🆘 Quick Troubleshooting

### **Problem: "Invalid API credentials"**
```bash
# Check your secrets.json file
cat secrets.json

# Make sure no extra spaces or quotes
# Keys should look like: "abc123xyz" not " abc123xyz " 
```

### **Problem: "No module named 'xyz'"**
```bash
# Reinstall dependencies
pip install -r requirements.txt --force-reinstall
```

### **Problem: Bot not making any trades**
```bash
# Check if market is open
python -c "
from utils.time_utils import TimeUtils
print(f'Market open: {TimeUtils.is_market_open()}')
"

# If market is closed, try backtesting instead:
python main.py --mode backtest --start-date 2024-07-20 --end-date 2024-07-22
```

### **Problem: Bot stopped working**
- **Check internet connection**
- **Look at terminal for error messages**
- **Check `logs/monitoring.log` file**
- **Restart with:** `python main.py --mode dryrun`

---

## 🎯 Quick Command Reference

```bash
# Paper trading (recommended for beginners)
python main.py --mode dryrun

# Backtesting on historical data
python main.py --mode backtest --start-date 2024-07-01 --end-date 2024-07-31

# Live trading (only after mastering paper trading!)
python main.py --mode live

# Choose different strategies
python main.py --strategy catalyst    # AI-enhanced catalyst detection
python main.py --strategy momentum    # Traditional momentum breakout

# AI control
python main.py --ai-enabled           # Enable AI signals
python main.py --ai-mode hybrid       # Use both AI and technical analysis
python main.py --ai-confidence 80     # Set AI confidence threshold
```

---

## 🎪 Interactive Mode

If you don't want to remember commands, just run:
```bash
python main.py
```

The bot will ask you questions and guide you through setup!

---

## 📞 Need Help?

### **Quick Help:**
- **❓ Common questions:** [FAQ.md](FAQ.md)
- **🔧 Technical issues:** [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
- **📖 Complete guide:** [USER_MANUAL.md](USER_MANUAL.md)

### **Community Support:**
- **💬 GitHub Discussions:** Ask questions and share experiences
- **🐛 Bug Reports:** Create issues for technical problems
- **💡 Feature Requests:** Suggest improvements

---

**🎉 Welcome to algorithmic trading! You've just taken your first step into a more automated trading future. Happy trading! 📈**

---

*Last updated: July 2025 | Questions? Check the [FAQ](FAQ.md) or ask in [GitHub Discussions](https://github.com/himanshugupta/zerodha-ai-trading-bot/discussions)*