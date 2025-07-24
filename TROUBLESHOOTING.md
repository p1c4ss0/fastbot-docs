# 🔧 Troubleshooting Guide

## 🚨 Quick Emergency Solutions

### **🛑 Bot is Trading Erratically - STOP IMMEDIATELY**
```bash
# Press Ctrl+C in terminal to stop the bot
# Or close the terminal window completely

# Then manually check and close positions in Zerodha
```

### **💰 Unexpected Losses - Immediate Actions**
1. **Stop the bot** (Ctrl+C)
2. **Log into Zerodha** and check open positions
3. **Manually close** any unwanted positions
4. **Check logs** in `logs/monitoring.log`
5. **Don't restart** until you understand the issue

### **🔌 Bot Won't Start - Quick Fixes**
```bash
# Check if all dependencies are installed
pip install -r requirements.txt

# Verify Python version (needs 3.8+)
python --version

# Check if config files exist
ls secrets.json prefilter_config.json
```

---

## 🔐 API & Authentication Issues

### **Problem: "Invalid API credentials" Error**

**Symptoms:**
- Bot fails to start with authentication errors
- "Invalid API key" or "Invalid access token" messages

**Solutions:**
```bash
# 1. Verify API credentials in secrets.json
{
  "api_key": "your_api_key_here",
  "api_secret": "your_api_secret_here", 
  "access_token": "your_access_token_here"
}

# 2. Check if credentials are correct in Zerodha Console
# Go to: https://console.zerodha.com/
# Verify: API key, secret, and generate new access token

# 3. Ensure no extra spaces or characters
# Copy-paste directly from Zerodha console
```

**Advanced Fix:**
```python
# Test API connection manually
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
    print(f'User: {profile[\"user_name\"]}')
except Exception as e:
    print(f'❌ API Error: {e}')
"
```

### **Problem: "IP not whitelisted" Error**

**Symptoms:**
- API calls fail with IP restriction errors

**Solutions:**
1. **Get your current IP:**
   ```bash
   curl ifconfig.me
   ```

2. **Add IP to Zerodha Console:**
   - Go to https://console.zerodha.com/
   - Navigate to API section
   - Add your IP to whitelist
   - Wait 5 minutes for changes to take effect

3. **For dynamic IPs:**
   ```bash
   # Create a script to update IP automatically
   # (Contact Zerodha support for guidance)
   ```

### **Problem: "Rate limit exceeded" Error**

**Symptoms:**
- Bot slows down or fails after running for a while
- "Too many requests" errors in logs

**Solutions:**
```python
# The bot already has rate limiting built-in
# If you see this error:

# 1. Check if you're running multiple instances
ps aux | grep python | grep main.py

# 2. Verify API call frequency in logs
tail -f logs/monitoring.log | grep "API"

# 3. Increase delays in config (if needed)
# Edit trading_config.json:
{
  "api_settings": {
    "request_delay": 1.0,  # Increase from 0.5 to 1.0
    "max_retries": 3
  }
}
```

---

## 📊 Market Data Issues

### **Problem: "No market data available"**

**Symptoms:**
- Bot can't fetch current prices
- Empty or old price data
- Trading signals not generating

**Solutions:**
```bash
# 1. Check market hours (9:15 AM - 3:30 PM IST)
python -c "
from utils.time_utils import TimeUtils
print(f'Market open: {TimeUtils.is_market_open()}')
print(f'Current time: {TimeUtils.format_timestamp()}')
"

# 2. Verify instrument data is updated
# Check file date of instruments.csv
ls -la instruments.csv

# 3. Update instruments manually
python -c "
from core.data_manager import DataManager
dm = DataManager()
dm.update_instruments()
print('✅ Instruments updated')
"
```

### **Problem: Historical Data Missing**

**Symptoms:**
- Backtesting fails
- "Insufficient historical data" errors

**Solutions:**
```bash
# 1. Download historical data
python scripts/download_historical_data.py --start-date 2024-01-01

# 2. Check data directory
ls -la data_cache/historical/

# 3. Clear cache and re-download
rm -rf data_cache/historical/
python scripts/download_historical_data.py --force-refresh
```

---

## 💻 Installation & Environment Issues

### **Problem: Dependencies Installation Failed**

**Symptoms:**
- `pip install -r requirements.txt` fails
- Missing module errors when running bot

**Solutions:**
```bash
# 1. Update pip and setuptools
python -m pip install --upgrade pip setuptools

# 2. Install dependencies one by one
pip install pandas numpy talib kiteconnect pytz requests

# 3. For TA-Lib installation issues (common problem):

# On Windows:
# Download TA-Lib wheel from: https://www.lfd.uci.edu/~gohlke/pythonlibs/#ta-lib
pip install TA_Lib-0.4.24-cp39-cp39-win_amd64.whl

# On macOS:
brew install ta-lib
pip install TA-Lib

# On Linux:
sudo apt-get install libta-lib-dev
pip install TA-Lib
```

### **Problem: Python Version Compatibility**

**Symptoms:**
- Syntax errors or import failures
- "Feature not supported in this Python version"

**Solutions:**
```bash
# 1. Check Python version (needs 3.8+)
python --version

# 2. Install correct Python version
# Visit: https://www.python.org/downloads/

# 3. Use virtual environment
python -m venv trading_bot_env
source trading_bot_env/bin/activate  # Linux/Mac
# OR
trading_bot_env\Scripts\activate     # Windows

pip install -r requirements.txt
```

### **Problem: File Permission Errors**

**Symptoms:**
- "Permission denied" when creating logs or reports
- Can't write to configuration files

**Solutions:**
```bash
# 1. Check and fix permissions
chmod 755 .
chmod 644 *.json *.csv
chmod 755 logs/ reports/ data_cache/

# 2. Run with appropriate permissions
# On Linux/Mac (if needed):
sudo python main.py

# 3. Change ownership (if needed)
sudo chown -R $USER:$USER .
```

---

## 🎯 Trading Logic Issues

### **Problem: Bot Not Making Any Trades**

**Symptoms:**
- Bot runs but no buy signals generated
- "No suitable stocks found" messages

**Diagnostic Steps:**
```bash
# 1. Check prefilter results
python -c "
from core.prefilter import Prefilter
pf = Prefilter()
stocks = pf.apply_prefilters()
print(f'Stocks passing prefilter: {len(stocks)}')
for stock in stocks[:5]:
    print(f'  - {stock}')
"

# 2. Check scoring thresholds
# Look at config/trading_config.json
cat config/trading_config.json | grep -A5 "scoring"

# 3. Lower score threshold temporarily for testing
# Edit trading_config.json:
{
  "scoring": {
    "minimum_score": 10.0  # Lower from default 15.0
  }
}
```

**Solutions:**
```python
# 1. Relax prefilter criteria
# Edit prefilter_config.json:
{
  "filters": {
    "min_price": 10,        # Lower from 50
    "max_price": 10000,     # Increase from 2000
    "min_volume": 25000,    # Lower from 100000
    "min_atr_percent": 0.5  # Lower from 1.0
  }
}

# 2. Check market conditions
# Bot may wait for better opportunities

# 3. Verify strategy is active
# Check strategy_selection in trading_config.json
```

### **Problem: Too Many Trades (Over-trading)**

**Symptoms:**
- Bot makes excessive trades
- Many small positions
- High brokerage costs

**Solutions:**
```json
// Edit trading_config.json:
{
  "position_management": {
    "max_positions": 3,           // Reduce from 8
    "min_position_value": 10000   // Increase minimum
  },
  "scoring": {
    "minimum_score": 20.0         // Increase from 15.0
  }
}
```

### **Problem: Bot Exiting Too Early/Late**

**Symptoms:**
- Missing profit opportunities
- Excessive losses from late exits

**Solutions:**
```json
// Adjust exit strategy in trading_config.json:
{
  "exit_strategy": {
    "profit_targets": {
      "t1_percent": 0.8,    // Reduce from 1.0 for quicker exits
      "t2_percent": 1.5,    // Reduce from 2.0
      "t3_percent": 2.5     // Reduce from 3.0
    },
    "stop_loss_percent": 0.8,  // Tighten from 1.0
    "trailing_stop_loss": true
  }
}
```

---

## 📈 Performance Issues

### **Problem: Bot Running Slowly**

**Symptoms:**
- Long delays between operations
- High CPU/memory usage
- Sluggish response to market changes

**Solutions:**
```bash
# 1. Check system resources
top -p $(pgrep -f "python.*main.py")

# 2. Optimize settings
# Edit trading_config.json:
{
  "system_settings": {
    "update_interval": 30,     # Increase from 15 seconds
    "max_concurrent_requests": 5,  # Reduce from 10
    "enable_caching": true
  }
}

# 3. Clear data cache
rm -rf data_cache/temp/
mkdir data_cache/temp/

# 4. Restart with clean state
pkill -f "python.*main.py"
python main.py
```

### **Problem: Memory Usage Growing**

**Symptoms:**
- Bot consumes more RAM over time
- System becomes unresponsive
- Out of memory errors

**Solutions:**
```python
# 1. Enable garbage collection optimization
# Edit main.py (add at top):
import gc
gc.set_threshold(700, 10, 10)

# 2. Monitor memory usage
python -c "
import psutil
import os
process = psutil.Process(os.getpid())
print(f'Memory usage: {process.memory_info().rss / 1024 / 1024:.1f} MB')
"

# 3. Restart bot daily (automated)
# Add to cron job:
# 0 8 * * * pkill -f "python.*main.py" && cd /path/to/bot && python main.py --mode dryrun
```

---

## 📊 Dashboard & Reporting Issues

### **Problem: Dashboard Not Loading**

**Symptoms:**
- Blank dashboard page
- "No data available" messages
- Charts not displaying

**Solutions:**
```bash
# 1. Check if report files exist
ls -la reports/*/

# 2. Verify dashboard dependencies
pip install streamlit plotly pandas

# 3. Run dashboard separately
cd dashboard/
streamlit run dashboard.py

# 4. Check port conflicts
netstat -an | grep 8501
# Kill conflicting processes if needed
```

### **Problem: Missing Trade Reports**

**Symptoms:**
- Empty reports directory
- No trade history in dashboard
- Missing performance metrics

**Solutions:**
```python
# 1. Verify report generation is enabled
# Check trading_config.json:
{
  "reporting": {
    "enable_reports": true,
    "save_individual_trades": true,
    "generate_daily_summary": true
  }
}

# 2. Check file permissions
ls -la reports/
chmod 755 reports/ reports/*/

# 3. Manually generate report
python -c "
from engines.backtest_engine import BacktestEngine
be = BacktestEngine()
be.generate_performance_report()
"
```

---

## 🔍 Debugging & Log Analysis

### **Understanding Log Files**

**Key Log Locations:**
```bash
logs/monitoring.log      # Main application logs
logs/trades.log         # Trade execution logs  
logs/errors.log         # Error messages only
logs/api.log           # API communication logs
```

**Reading Logs Effectively:**
```bash
# Monitor real-time logs
tail -f logs/monitoring.log

# Filter for errors only
grep -i "error\|exception\|failed" logs/monitoring.log

# Check API issues
grep -i "api\|rate limit\|timeout" logs/monitoring.log

# Find specific trade information
grep "TRADE_ID" logs/trades.log
```

### **Common Log Patterns and Solutions**

**Pattern:** `ConnectionError: Max retries exceeded`
```bash
# Solution: Network connectivity issue
# 1. Check internet connection
ping google.com

# 2. Verify Zerodha API status
curl -I https://api.kite.trade/

# 3. Increase retry settings in config
```

**Pattern:** `KeyError: 'instrument_token'`
```bash
# Solution: Outdated instruments file
python scripts/update_instruments.py
```

**Pattern:** `ValueError: insufficient funds`
```bash
# Solution: Account balance issue
# 1. Check account balance in Zerodha
# 2. Reduce position sizes in config
# 3. Add funds to trading account
```

---

## 🚨 Emergency Procedures

### **Complete System Reset**

If everything is broken and you need to start fresh:

```bash
# 1. Stop all running processes
pkill -f "python.*main.py"

# 2. Backup important data
cp secrets.json secrets.json.backup
cp -r reports/ reports_backup/

# 3. Clean installation
rm -rf __pycache__/ */__pycache__/
rm -rf data_cache/temp/
git checkout -- .  # Reset to original state

# 4. Reinstall dependencies
pip install -r requirements.txt

# 5. Restore secrets
cp secrets.json.backup secrets.json

# 6. Test installation
python -c "print('✅ Basic Python import works')"
python -c "from bot_controller import BotController; print('✅ Bot imports work')"
```

### **Emergency Position Closure**

If bot positions need immediate attention:

```python
# Emergency position closure script
# Save as emergency_close.py and run when needed

from kiteconnect import KiteConnect
import json

# Load credentials
with open('secrets.json', 'r') as f:
    secrets = json.load(f)

kite = KiteConnect(api_key=secrets['api_key'])
kite.set_access_token(secrets['access_token'])

# Get all positions
positions = kite.positions()

print("Current positions:")
for position in positions['day']:
    if position['quantity'] != 0:
        print(f"Symbol: {position['tradingsymbol']}")
        print(f"Quantity: {position['quantity']}")
        print(f"P&L: {position['pnl']}")
        
        # Uncomment next lines to actually close positions
        # if position['quantity'] > 0:
        #     kite.place_order(variety="regular", exchange="NSE", 
        #                     tradingsymbol=position['tradingsymbol'],
        #                     transaction_type="SELL", quantity=position['quantity'],
        #                     product="MIS", order_type="MARKET")
        print("---")
```

---

## 📞 Getting Additional Help

### **Before Seeking Help:**

1. **Check this troubleshooting guide** thoroughly
2. **Read the FAQ** for common questions
3. **Review log files** for specific error messages
4. **Try basic solutions** (restart, check config)
5. **Test with minimal settings** (paper trading, small amounts)

### **When Creating Support Requests:**

**Include This Information:**
- **Operating System:** Windows 10, macOS 12, Ubuntu 20.04, etc.
- **Python Version:** `python --version`
- **Bot Version:** Check VERSION file or git commit
- **Error Message:** Exact text from logs
- **Steps to Reproduce:** What were you doing when it failed?
- **Configuration:** Share relevant config files (redact API keys!)

**Example Good Support Request:**
```
Title: Bot fails to start with "KeyError: instrument_token"

Environment:
- OS: Ubuntu 20.04
- Python: 3.9.5
- Bot Version: v2.1

Error:
File "core/strategy_manager.py", line 45, in get_instrument_token
KeyError: 'instrument_token'

Steps to reproduce:
1. Started bot with: python main.py --mode dryrun
2. Bot initializes but crashes during strategy loading
3. Happens consistently on startup

Config: (attached trading_config.json with API keys removed)

Logs: (attached last 50 lines of monitoring.log)
```

### **Support Channels:**

1. **GitHub Issues:** Technical bugs and feature requests
2. **GitHub Discussions:** General questions and community help
3. **Documentation:** This guide and other .md files
4. **Zerodha Support:** API-related issues (mention you're using their API)

---

**💡 Pro Tip: Most issues are configuration-related. Double-check your config files before assuming there's a bug!**

---

*Last updated: July 2025 | For technical support, create a detailed issue on GitHub*