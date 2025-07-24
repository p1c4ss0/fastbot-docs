# 📖 User Manual - Complete Guide to Using the Trading Bot

**This comprehensive guide will teach you everything you need to know to use the trading bot safely and effectively.**

## ⚠️ **SAFETY FIRST - READ THIS**

🛡️ **Start with Paper Trading** - Never use real money until you're confident  
📊 **Practice for at least 1 week** with dryrun mode  
💰 **Start small** - Use only money you can afford to lose  
📞 **This is not financial advice** - You are responsible for all trading decisions

---

## 🎯 **Prerequisites**

Before using this manual, make sure you have:
- ✅ **Completed** [🔐 Zerodha Setup Guide](ZERODHA_SETUP_GUIDE.md)
- ✅ **Installed the bot** using [💻 Installation Guide](INSTALLATION_GUIDE.md)
- ✅ **Working secrets.json** with your API credentials
- ✅ **Basic understanding** of stock trading concepts

---

## 📚 **Manual Overview**

This manual is organized by experience level:

### **👶 Complete Beginners:**
1. [🎪 First Time Setup](#first-time-setup) - Get everything working
2. [📊 Understanding the Dashboard](#understanding-the-dashboard) - Learn the interface
3. [🧪 Your First Backtest](#your-first-backtest) - Safe historical testing

### **🎓 Learning Phase:**
4. [🎪 Paper Trading Guide](#paper-trading-guide) - Practice with fake money
5. [📈 Reading Results](#reading-results) - Understand what the bot is doing
6. [⚙️ Basic Configuration](#basic-configuration) - Customize for your needs

### **💰 Ready for Live Trading:**
7. [🚀 Going Live](#going-live) - Trade with real money
8. [📅 Daily Operations](#daily-operations) - Your daily routine
9. [🔧 Monitoring & Maintenance](#monitoring--maintenance) - Keep it running smoothly

---

## 🎪 **First Time Setup**

*Estimated time: 15 minutes*

### **Step 1: Verify Installation**

Open your terminal/command prompt and navigate to the bot directory:

```bash
# Navigate to your bot folder
cd /path/to/your/TradingBot

# Test that everything is working
python main.py --help
```

**Expected output:** You should see a help message with available commands.

**If you get errors:** Go back to [💻 Installation Guide](INSTALLATION_GUIDE.md)

### **Step 2: Check Your API Credentials**

```bash
# Test your Zerodha connection
python -c "
import json
from kiteconnect import KiteConnect

# Load and test credentials
with open('secrets.json', 'r') as f:
    secrets = json.load(f)

kite = KiteConnect(api_key=secrets['api_key'])
kite.set_access_token(secrets['access_token'])

try:
    profile = kite.profile()
    print(f'✅ Connected! Hello {profile[\"user_name\"]}')
    print(f'📊 Available funds: ₹{profile[\"equity\"][\"available\"][\"cash\"]}')
except Exception as e:
    print(f'❌ Connection failed: {e}')
    print('Please check your secrets.json file')
"
```

**Expected output:** Connection success with your name and available funds.

**If connection fails:** 
- Check if your access token is fresh (less than 24 hours old)
- Verify all credentials in `secrets.json` are correct
- See [🔐 Zerodha Setup Guide](ZERODHA_SETUP_GUIDE.md) for token refresh

### **Step 3: Initialize Configuration**

The bot comes with sensible defaults, but let's make sure everything is set up:

```bash
# Create default configuration (if not exists)
python setup.py
```

This creates:
- `trading_config.json` - Main trading settings
- `prefilter_config.json` - Stock filtering rules
- Necessary directories (`logs/`, `reports/`, etc.)

### **Step 4: Test Basic Functionality**

```bash
# Quick system test
python main.py --test-system
```

**Should show:**
- ✅ Python packages working
- ✅ TA-Lib functioning
- ✅ AI components loaded
- ✅ Configuration files present
- ✅ Zerodha API connected

**🎉 If all tests pass, you're ready to proceed!**

---

## 📊 **Understanding the Dashboard**

*Learn what everything means before trading*

### **Starting the Dashboard**

```bash
# Start the web dashboard
streamlit run dashboard/dashboard.py
```

**Opens in browser:** Usually `http://localhost:8501`

### **Dashboard Sections Explained**

#### **🏠 Home Page**
- **Account Summary:** Your current balance and positions
- **Bot Status:** Whether the bot is running and what mode
- **Recent Activity:** Last few trades and signals
- **Quick Actions:** Start/stop bot, change modes

#### **📊 Trading Performance**
- **Total P&L:** Your overall profit/loss
- **Win Rate:** Percentage of profitable trades
- **Average Trade:** Typical profit/loss per trade
- **Maximum Drawdown:** Worst losing streak
- **Sharpe Ratio:** Risk-adjusted returns

#### **📈 Active Trades**
- **Current Positions:** What you're currently holding
- **Entry Price:** Price you bought at
- **Current Price:** Live market price
- **P&L:** Current profit/loss per position
- **Targets:** T1, T2, T3 exit levels
- **Stop Loss:** Automatic exit price if trade goes wrong

#### **🎯 Signals & Analysis**
- **Latest Signals:** Stocks the bot wants to buy
- **Signal Strength:** Score out of 100 points
- **Technical Indicators:** RSI, MACD, Volume analysis
- **AI Confidence:** How confident the AI model is

#### **⚙️ Configuration**
- **Trading Mode:** Backtest, Dryrun, or Live
- **Strategy:** Which trading strategy is active
- **Risk Settings:** Position size, stop loss, daily limits
- **AI Settings:** AI mode (hybrid, statistical, AI-only, off)

---

## 🧪 **Your First Backtest**

*Test the bot on historical data - completely risk-free*

Backtesting shows how the bot would have performed on past market data. This is the safest way to learn.

### **Step 1: Choose Your Test Period**

Pick a recent period with good market activity:

```bash
# Test last week (safe, recent data)
python main.py --mode backtest --start-date 2025-07-15 --end-date 2025-07-22

# Test a volatile period (more interesting)
python main.py --mode backtest --start-date 2025-06-01 --end-date 2025-06-30

# Test with specific capital
python main.py --mode backtest --start-date 2025-07-15 --end-date 2025-07-22 --capital 100000
```

### **Step 2: Understanding Backtest Output**

While running, you'll see:

```
🔍 Scanning stocks... 
📊 Processing RELIANCE: Score 78/100 - STRONG BUY signal
💰 BT ORDER#001: Bought 10 shares of RELIANCE at ₹2,450.00
⏰ Monitoring positions...
💰 BT ORDER#001: Sold RELIANCE at ₹2,489.50 - Profit: ₹395.00 (+1.61%)
```

**What this means:**
- **Scanning:** Bot is looking at stocks
- **Score 78/100:** Strong signal (above 60 threshold)
- **BT ORDER#001:** Backtest order ID
- **Bought/Sold:** Simulated trades with prices
- **Profit:** How much each trade made/lost

### **Step 3: Reading Backtest Results**

After completion, check the report:

```bash
# Find your report
ls reports/backtest/

# Example: reports/backtest/backtest_results_20250724_143022.json
```

**Key metrics to understand:**

```json
{
  "backtest_summary": {
    "initial_capital": 100000,
    "final_capital": 108450,
    "total_pnl": 8450,
    "total_return_percent": 8.45,
    "total_trades": 25,
    "winning_trades": 18,
    "losing_trades": 7,
    "win_rate_percent": 72.0,
    "max_drawdown_percent": -3.2
  }
}
```

**What these numbers mean:**
- **Total Return:** 8.45% profit over the test period
- **Win Rate:** 72% of trades were profitable
- **Max Drawdown:** Worst losing streak was -3.2%
- **Total Trades:** Bot made 25 trades during the period

### **Step 4: Analyze Individual Trades**

```bash
# View detailed trade analysis
python -c "
import json
with open('reports/backtest/backtest_results_20250724_143022.json', 'r') as f:
    data = json.load(f)

print('🏆 Best Trades:')
for trade in sorted(data['trades'], key=lambda x: x['pnl'], reverse=True)[:5]:
    print(f'  {trade[\"symbol\"]}: +₹{trade[\"pnl\"]:.2f} ({trade[\"return_percent\"]:.1f}%)')

print('💸 Worst Trades:')
for trade in sorted(data['trades'], key=lambda x: x['pnl'])[:5]:
    print(f'  {trade[\"symbol\"]}: ₹{trade[\"pnl\"]:.2f} ({trade[\"return_percent\"]:.1f}%)')
"
```

### **Step 5: Experiment with Different Settings**

Try different configurations to see what works:

```bash
# Test with higher minimum score (more selective)
# Edit trading_config.json: "min_score_threshold": 70.0
python main.py --mode backtest --start-date 2025-07-15 --end-date 2025-07-22

# Test with lower capital (smaller positions)
python main.py --mode backtest --start-date 2025-07-15 --end-date 2025-07-22 --capital 50000

# Test different strategy
# Edit trading_config.json: "primary_strategy": "momentum_breakout"
python main.py --mode backtest --start-date 2025-07-15 --end-date 2025-07-22
```

---

## 🎪 **Paper Trading Guide**

*Practice with live market data but fake money*

Paper trading (dryrun mode) uses real current market prices but doesn't place actual orders. This is perfect for learning how the bot behaves in live market conditions.

### **Step 1: Start Your First Paper Trading Session**

```bash
# Start paper trading for 1 hour
python main.py --mode dryrun --duration 60

# Or run continuously (stop with Ctrl+C)
python main.py --mode dryrun
```

### **Step 2: What Happens During Paper Trading**

You'll see real-time activity:

```
🌅 Market opened! Starting scan...
🔍 Scanning 502 stocks...
📊 Found 12 potential signals
🎯 TATAMOTORS: Score 84/100 - Strong signal detected
💰 DR ORDER#001: PAPER BUY 15 shares of TATAMOTORS at ₹789.50
⏱️  Monitoring 1 active position...
📈 TATAMOTORS: Current ₹795.20 (+0.72%), Target T1: ₹801.37
💰 DR ORDER#001: PAPER SELL TATAMOTORS at ₹801.37 - T1 Hit! Profit: ₹177.75
```

**Understanding the output:**
- **DR ORDER#001:** Dryrun (paper) order - no real money
- **PAPER BUY/SELL:** Simulated transactions
- **Real prices:** Using live market data
- **T1 Hit:** First target reached, partial exit

### **Step 3: Monitor in Real-Time**

Open another terminal and watch the dashboard:

```bash
# In a new terminal
streamlit run dashboard/dashboard.py
```

**Navigate to:** "Active Trades" section to see:
- Current positions
- Live P&L updates
- Target levels
- Stop loss levels

### **Step 4: Understanding Paper Trading Behavior**

#### **Entry Process:**
1. **Scanning:** Bot scans stocks every 5 minutes
2. **Scoring:** Applies 100-point scoring system
3. **Filtering:** Only trades stocks above threshold (default 60)
4. **Position Sizing:** Calculates quantity based on available capital
5. **Entry:** Places simulated buy order

#### **Exit Process:**
1. **Monitoring:** Checks positions every 15 seconds
2. **Target Levels:** T1 (1.5%), T2 (2.5%), T3 (4.0%)
3. **Partial Exits:** Sells 50% at T1, 30% at T2, 20% at T3
4. **Stop Loss:** Automatic exit if price drops too much
5. **Time Exit:** Force close all positions at 3:20 PM

### **Step 5: Analyze Paper Trading Results**

After running for a while, check your results:

```bash
# Check latest dryrun report
ls reports/dryrun/

# View summary
python -c "
import json
import glob

# Find latest report
reports = glob.glob('reports/dryrun/*.json')
latest = max(reports)

with open(latest, 'r') as f:
    data = json.load(f)

print(f'📊 Paper Trading Summary:')
print(f'   Duration: {data.get(\"duration_minutes\", \"N/A\")} minutes')
print(f'   Total Trades: {len(data.get(\"trades\", []))}')
print(f'   Paper P&L: ₹{data.get(\"total_pnl\", 0):.2f}')
print(f'   Win Rate: {data.get(\"win_rate_percent\", 0):.1f}%')
"
```

### **Step 6: Common Paper Trading Observations**

#### **What to Expect:**
- **Trade Frequency:** 3-8 trades per day typically
- **Win Rate:** 60-80% in good market conditions
- **Average Trade:** 1-3% profit/loss per trade
- **Drawdowns:** Occasional 2-5% losing streaks

#### **Red Flags to Watch For:**
- **No trades all day:** Check if market is open, API working
- **Too many losses:** Market might be very volatile
- **Very high frequency:** Settings might be too aggressive
- **No target hits:** Targets might be set too high

---

## 📈 **Reading Results**

*Understand what the bot is telling you*

### **Key Performance Metrics**

#### **📊 Profit & Loss (P&L)**
- **Total P&L:** Overall profit/loss in rupees
- **Return %:** Percentage return on invested capital
- **Daily P&L:** Profit/loss per day
- **Average per Trade:** Typical profit/loss per trade

#### **🎯 Trade Statistics**
- **Total Trades:** Number of buy/sell cycles completed
- **Win Rate:** Percentage of profitable trades
- **Loss Rate:** Percentage of losing trades
- **Average Win:** Typical profit from winning trades  
- **Average Loss:** Typical loss from losing trades

#### **📉 Risk Metrics**
- **Maximum Drawdown:** Worst losing streak
- **Sharpe Ratio:** Risk-adjusted returns (higher is better)
- **Volatility:** How much daily returns vary
- **Recovery Time:** How long to recover from losses

### **Understanding Trade Details**

Each trade report shows:

```json
{
  "trade_id": "DR ORDER#001",
  "symbol": "TATAMOTORS", 
  "entry_time": "2025-07-24T10:15:30",
  "exit_time": "2025-07-24T11:42:15",
  "entry_price": 789.50,
  "exit_price": 801.37,
  "quantity": 15,
  "pnl": 177.75,
  "return_percent": 1.50,
  "exit_reason": "T1_HIT",
  "duration_minutes": 87,
  "signal_score": 84
}
```

**What each field means:**
- **Signal Score:** How strong the buy signal was (84/100 = very strong)
- **Duration:** How long the trade lasted (87 minutes)
- **Exit Reason:** Why the bot sold (T1_HIT = first target reached)
- **Return %:** Percentage profit (1.50% = good intraday return)

### **Signal Analysis**

The bot shows detailed signal information:

```json
{
  "symbol": "TATAMOTORS",
  "total_score": 84,
  "components": {
    "rsi_score": 15,
    "macd_score": 8,
    "volume_score": 12,
    "bollinger_score": 7,
    "momentum_score": 18,
    "ai_score": 24
  },
  "technical_indicators": {
    "rsi": 45.2,
    "macd_histogram": 2.3,
    "volume_ratio": 2.1,
    "price_vs_vwap": 1.02
  }
}
```

**Interpreting signals:**
- **Total Score 84:** Very strong signal (>80 = excellent)
- **AI Score 24:** AI model is very confident
- **Volume Ratio 2.1:** 2.1x normal volume (good)
- **RSI 45.2:** Not overbought, room to grow

---

## ⚙️ **Basic Configuration**

*Customize the bot for your needs*

### **Main Configuration File**

Edit `trading_config.json` for basic settings:

```json
{
  "min_score_threshold": 60.0,      // Minimum signal strength to trade
  "max_position_size": 0.1,         // Max 10% of capital per trade
  "max_daily_loss": 0.05,           // Stop trading if lose 5% in a day
  "max_drawdown": 0.1,              // Stop if total losses reach 10%
  "risk_per_trade": 0.02,           // Risk 2% of capital per trade
  "max_trades_per_day": 7,          // Maximum 7 trades per day
  "max_active_trades": 3            // Hold maximum 3 positions at once
}
```

### **Common Adjustments for Beginners**

#### **More Conservative (Safer):**
```json
{
  "min_score_threshold": 70.0,      // Only very strong signals
  "max_position_size": 0.05,        // Max 5% per trade (smaller positions)
  "max_daily_loss": 0.03,           // Stop at 3% daily loss
  "risk_per_trade": 0.01,           // Risk only 1% per trade
  "max_trades_per_day": 5           // Fewer trades
}
```

#### **More Aggressive (Higher Risk/Reward):**
```json
{
  "min_score_threshold": 50.0,      // Accept weaker signals
  "max_position_size": 0.15,        // Larger positions
  "max_daily_loss": 0.08,           // Allow higher daily losses
  "risk_per_trade": 0.03,           // Risk 3% per trade
  "max_trades_per_day": 10          // More trades
}
```

### **AI Configuration**

Edit AI settings in `trading_config.json`:

```json
"ai_settings": {
  "enabled": true,
  "mode": "hybrid",                 // hybrid, statistical_only, ai_only, off
  "confidence_threshold": 75.0,     // Minimum AI confidence
  "fallback_to_statistical": true   // Use technical analysis if AI fails
}
```

**AI Modes Explained:**
- **hybrid:** Combines AI + technical analysis (recommended)
- **statistical_only:** Only technical indicators, no AI
- **ai_only:** Only AI predictions, no technical analysis
- **off:** Disables all AI features

---

## 🚀 **Going Live**

*Trade with real money - be very careful*

### **⚠️ CRITICAL SAFETY CHECKLIST**

**Before going live, you MUST:**

- [ ] **Practiced for at least 1 week** with paper trading
- [ ] **Understand how the bot works** and what all the numbers mean
- [ ] **Have emergency fund** separate from trading capital
- [ ] **Set strict daily loss limits** that you can afford
- [ ] **Know how to stop the bot** immediately if needed
- [ ] **Start with small amounts** (₹10,000-25,000 maximum)
- [ ] **Have recent access token** (generated today)

### **Step 1: Final Preparation**

#### **1.1 Update Your Access Token**
```bash
# Generate fresh token (daily requirement)
python generate_token.py
```

#### **1.2 Set Conservative Settings**
```json
// In trading_config.json - use VERY conservative settings first
{
  "min_score_threshold": 75.0,      // Only strongest signals
  "max_position_size": 0.05,        // Small positions (5% max)
  "max_daily_loss": 0.02,           // Stop at 2% daily loss
  "risk_per_trade": 0.01,           // Risk only 1% per trade
  "max_trades_per_day": 3,          // Very few trades
  "max_active_trades": 1            // Only 1 position at a time
}
```

#### **1.3 Check Available Funds**
```bash
# Verify your account balance
python -c "
import json
from kiteconnect import KiteConnect

with open('secrets.json', 'r') as f:
    secrets = json.load(f)

kite = KiteConnect(api_key=secrets['api_key'])
kite.set_access_token(secrets['access_token'])

funds = kite.margins()
available = funds['equity']['available']['cash']
print(f'💰 Available for trading: ₹{available:,.2f}')

# Recommend starting amount
safe_amount = min(available * 0.1, 25000)  # 10% of available or ₹25,000, whichever is less
print(f'🛡️  Recommended starting capital: ₹{safe_amount:,.2f}')
"
```

### **Step 2: Start Live Trading**

#### **2.1 Start with Ultra-Short Session**
```bash
# Start with just 30 minutes of live trading
python main.py --mode live --duration 30
```

#### **2.2 Monitor Extremely Closely**
- **Watch every trade** - Don't leave it unattended
- **Keep dashboard open** in browser
- **Have mobile notifications** enabled if possible
- **Know your profit/loss** at all times

#### **2.3 First Live Session Checklist**
During your first 30 minutes:

- [ ] **Bot connects successfully** - No API errors
- [ ] **Scanning works** - Shows stock analysis
- [ ] **Orders execute** - Actual buy/sell orders go through
- [ ] **Positions show correctly** - Dashboard matches Zerodha account
- [ ] **Exits work** - Stop losses and targets function
- [ ] **You can manually exit** if needed

### **Step 3: Gradual Scale-Up**

#### **Week 1: Learning**
- **Duration:** 30-60 minutes per day
- **Capital:** ₹10,000-15,000 maximum
- **Trades:** 1-2 per day maximum
- **Focus:** Understanding real market behavior

#### **Week 2: Building Confidence**
- **Duration:** 1-2 hours per day
- **Capital:** ₹15,000-25,000 maximum
- **Trades:** 2-3 per day maximum
- **Focus:** Consistent execution

#### **Week 3+: Normal Operations**
- **Duration:** Full market hours (if desired)
- **Capital:** Based on your results and comfort
- **Trades:** Based on market opportunities
- **Focus:** Optimization and improvement

### **Step 4: Emergency Procedures**

#### **How to Stop Immediately**
1. **Press Ctrl+C** in the terminal running the bot
2. **Close all positions manually** in Zerodha Kite/mobile app
3. **Check your account** to ensure all positions are closed
4. **Investigate logs** to understand what happened

#### **Daily Safety Routine**
- **Morning:** Generate fresh access token
- **Pre-market:** Check bot settings and balance
- **During trading:** Monitor active trades
- **Post-market:** Review performance and close bot
- **Evening:** Analyze results and plan improvements

---

## 📅 **Daily Operations**

*Your daily routine as a bot trader*

### **🌅 Morning Routine (8:30-9:15 AM)**

#### **1. Generate New Access Token**
```bash
# Daily token refresh (takes 2 minutes)
python generate_token.py
```

#### **2. Check Market Conditions**
```bash
# Quick market environment check
python -c "
import yfinance as yf
nifty = yf.Ticker('^NSEI')
data = nifty.history(period='2d')
change = ((data['Close'][-1] / data['Close'][-2]) - 1) * 100
print(f'📊 Nifty 50: {change:+.2f}% from yesterday')
if abs(change) > 2:
    print('⚠️  High volatility expected - consider more conservative settings')
else:
    print('✅ Normal market conditions')
"
```

#### **3. Review Overnight News**
- Check financial news for major events
- Look for corporate announcements affecting your target stocks
- Consider if any major global events might impact the market

#### **4. Prepare Bot Settings**
```bash
# Quick settings review
python -c "
import json
with open('trading_config.json', 'r') as f:
    config = json.load(f)
print(f'📊 Today\\'s settings:')
print(f'   Min Score: {config[\"min_score_threshold\"]}')
print(f'   Max Trades: {config[\"max_trades_per_day\"]}')
print(f'   Daily Loss Limit: {config[\"max_daily_loss\"]*100:.1f}%')
"
```

### **🚀 Market Open Routine (9:15 AM)**

#### **Start Trading**
```bash
# For paper trading
python main.py --mode dryrun

# For live trading (after you're experienced)
python main.py --mode live
```

#### **Open Dashboard**
```bash
# In a separate terminal
streamlit run dashboard/dashboard.py
```

### **📊 During Market Hours**

#### **Active Monitoring Checklist (Every 30 minutes)**
- [ ] **Check active positions** - Are they moving as expected?
- [ ] **Review new signals** - Any new opportunities?
- [ ] **Monitor overall P&L** - Are you within daily limits?
- [ ] **Check for errors** - Any technical issues in logs?

#### **Key Things to Watch For**
- **Unusual market movements** - Major news or events
- **Bot behavior changes** - Suddenly more/fewer trades
- **Position sizes** - Are they reasonable for your capital?
- **Exit timing** - Are targets and stop losses working?

### **🌅 Post-Market Routine (3:30 PM onwards)**

#### **1. Stop the Bot**
```bash
# Stop gracefully with Ctrl+C
# Bot should automatically close all positions by 3:20 PM
```

#### **2. Review Daily Performance**
```bash
# Check today's results
python -c "
import json, glob, datetime

# Find today's reports
today = datetime.date.today().strftime('%Y%m%d')
mode = 'dryrun'  # Change to 'live' if trading live

# Find latest report
reports = glob.glob(f'reports/{mode}/*{today}*.json')
if reports:
    latest = max(reports)
    with open(latest, 'r') as f:
        data = json.load(f)
    
    print(f'📊 Today\\'s Performance:')
    print(f'   Trades: {len(data.get(\"trades\", []))}')
    print(f'   P&L: ₹{data.get(\"total_pnl\", 0):.2f}')
    print(f'   Win Rate: {data.get(\"win_rate_percent\", 0):.1f}%')
    
    if data.get('trades'):
        best_trade = max(data['trades'], key=lambda x: x.get('pnl', 0))
        worst_trade = min(data['trades'], key=lambda x: x.get('pnl', 0))
        print(f'   Best Trade: {best_trade[\"symbol\"]} +₹{best_trade[\"pnl\"]:.2f}')
        print(f'   Worst Trade: {worst_trade[\"symbol\"]} ₹{worst_trade[\"pnl\"]:.2f}')
else:
    print('No reports found for today')
"
```

#### **3. Daily Review Questions**
- **What worked well today?** Which signals were most profitable?
- **What didn't work?** Which trades lost money and why?
- **Any technical issues?** Bot errors, API problems, etc.
- **Market conditions?** How did overall market affect performance?
- **Settings adjustment needed?** Should I change any parameters?

#### **4. Plan for Tomorrow**
- **Update access token** if needed for tomorrow
- **Adjust settings** based on today's learnings
- **Check economic calendar** for tomorrow's events
- **Set reminders** for any special market conditions

### **📊 Weekly Review**

Every weekend, do a comprehensive review:

```bash
# Generate weekly performance report
python -c "
import json, glob, datetime, pandas as pd

# Get all this week's reports
mode = 'dryrun'  # or 'live'
reports = glob.glob(f'reports/{mode}/*.json')

# Filter to this week
this_week = []
for report in reports:
    # Extract date from filename and filter
    # (Add date filtering logic here)
    pass

# Analyze weekly performance
# (Add comprehensive analysis here)
"
```

**Weekly review questions:**
- **Overall performance trend?** Getting better or worse?
- **Consistency?** Steady performance or wild swings?
- **Settings optimization?** What changes improved results?
- **Market adaptation?** How did bot handle different market conditions?

---

## 🔧 **Monitoring & Maintenance**

*Keep your bot running smoothly*

### **📊 Health Monitoring**

#### **Daily Health Checks**
```bash
# Quick health check script
python -c "
import os, json, datetime
from pathlib import Path

print('🏥 Bot Health Check')
print('=' * 30)

# Check critical files
critical_files = ['secrets.json', 'trading_config.json', 'requirements.txt']
for file in critical_files:
    if os.path.exists(file):
        print(f'✅ {file} present')
    else:
        print(f'❌ {file} MISSING!')

# Check log files
log_files = ['logs/main.log', 'logs/errors.log']
for log_file in log_files:
    if os.path.exists(log_file):
        size = os.path.getsize(log_file) / 1024 / 1024  # MB
        print(f'📊 {log_file}: {size:.1f}MB')
        if size > 100:
            print(f'⚠️  {log_file} is large - consider rotating')
    else:
        print(f'⚠️  {log_file} not found')

# Check disk space
free_space = os.statvfs('.').f_frsize * os.statvfs('.').f_bavail / 1024 / 1024 / 1024
print(f'💾 Free disk space: {free_space:.1f}GB')
if free_space < 1:
    print('⚠️  Low disk space!')

print('\\n🔍 Run python main.py --test-system for detailed diagnostics')
"
```

#### **Error Log Monitoring**
```bash
# Check for recent errors
tail -20 logs/errors.log

# Count error types
grep -c "ERROR" logs/main.log
grep -c "WARNING" logs/main.log
```

### **🔧 Regular Maintenance Tasks**

#### **Weekly Maintenance**
- **Clean old logs** - Remove logs older than 30 days
- **Update dependencies** - Check for package updates
- **Review performance** - Analyze weekly results
- **Check disk space** - Ensure adequate storage

#### **Monthly Maintenance**
- **Full system backup** - Save all configurations and data
- **Update AI models** - Retrain if necessary
- **Review strategy** - Analyze monthly performance
- **Security audit** - Check API credentials, change passwords

### **📈 Performance Optimization**

#### **Speed Optimization**
```bash
# Profile bot performance
python -m cProfile -o profile_stats.prof main.py --mode dryrun --duration 10

# Analyze bottlenecks
python -c "
import pstats
stats = pstats.Stats('profile_stats.prof')
stats.sort_stats('cumulative')
stats.print_stats(10)
"
```

#### **Memory Usage**
```bash
# Monitor memory usage during operation
python -c "
import psutil
import time

process = psutil.Process()
print(f'Memory usage: {process.memory_info().rss / 1024 / 1024:.1f}MB')
print(f'CPU usage: {process.cpu_percent():.1f}%')
"
```

### **🚨 Troubleshooting Common Issues**

#### **Bot Won't Start**
1. **Check Python version:** `python --version`
2. **Check dependencies:** `pip list | grep -E "(pandas|numpy|kiteconnect)"`
3. **Check API credentials:** Run connection test
4. **Check logs:** `tail -50 logs/errors.log`

#### **No Trades All Day**
1. **Market open?** Check if it's a trading day
2. **Settings too strict?** Lower `min_score_threshold`
3. **API working?** Test connection to Zerodha
4. **Stocks available?** Check prefilter results

#### **Frequent Errors**
1. **API rate limits:** Reduce API call frequency
2. **Network issues:** Check internet connection
3. **Invalid tokens:** Generate fresh access token
4. **Insufficient funds:** Check available balance

### **🔄 Updates and Upgrades**

#### **Updating the Bot**
```bash
# Backup current setup
cp -r . ../bot-backup-$(date +%Y%m%d)

# Pull latest changes (if using git)
git pull origin main

# Update dependencies
pip install -r requirements.txt --upgrade

# Test after update
python main.py --test-system
```

#### **Configuration Migrations**
When updating, check for configuration changes:
```bash
# Compare configurations
diff trading_config.json ../bot-backup-*/trading_config.json
```

---

## 🎓 **Advanced Tips & Best Practices**

### **🎯 Trading Psychology**
- **Stick to your rules** - Don't override the bot emotionally
- **Accept losses** - No system wins 100% of the time
- **Scale gradually** - Increase position sizes slowly as you gain confidence
- **Keep learning** - Markets evolve, so should your understanding

### **📊 Performance Analysis**
- **Track metrics daily** - Don't just look at profit/loss
- **Understand drawdowns** - How long do losing streaks last?
- **Market correlation** - How does bot perform in different market conditions?
- **Risk-adjusted returns** - Focus on Sharpe ratio, not just profits

### **⚙️ Optimization Strategies**
- **A/B testing** - Test different settings with paper trading
- **Seasonal adjustments** - Different strategies for different market phases
- **News integration** - Use news scores to enhance signals
- **Multiple timeframes** - Consider longer-term trends

---

## 🆘 **Emergency Procedures**

### **🚨 Immediate Actions if Things Go Wrong**

#### **Financial Emergency**
1. **Stop the bot immediately:** `Ctrl+C`
2. **Open Zerodha Kite** and manually close all positions
3. **Calculate your losses** and ensure they're within acceptable limits
4. **Don't panic** - Review what happened calmly
5. **Don't restart** until you understand the issue

#### **Technical Emergency**
1. **Save error messages** - Screenshot or copy error text
2. **Check logs** - Look in `logs/` folder for clues
3. **Test connection** - Verify API still works
4. **Restore from backup** if necessary
5. **Document the issue** for future reference

### **📞 Getting Help**

#### **Self-Help Resources**
1. **Check [🛠️ Troubleshooting Guide](TROUBLESHOOTING.md)**
2. **Review [❓ FAQ](FAQ.md)**
3. **Search error messages** in documentation
4. **Check GitHub issues** for similar problems

#### **Community Support**
1. **Create detailed GitHub issue** with logs and screenshots
2. **Join trading communities** for general trading advice
3. **Consult financial advisor** for investment guidance

---

## 🎉 **Congratulations!**

You've completed the comprehensive user manual! You now know:

- ✅ **How to set up** the bot safely
- ✅ **How to practice** with paper trading
- ✅ **How to go live** responsibly
- ✅ **How to monitor** and maintain the system
- ✅ **How to troubleshoot** common issues

### **Your Next Steps:**

1. **🎪 Start with backtesting** - Get comfortable with historical data
2. **📊 Practice paper trading** - Spend at least a week learning
3. **💰 Go live cautiously** - Start with small amounts
4. **📈 Keep learning** - Markets and technology constantly evolve

---

**Remember: Trading involves risk. Never trade with money you can't afford to lose, and always maintain strict risk management practices! 🛡️**

---

*Last updated: July 2025 | Questions? Check [FAQ.md](FAQ.md) or [TROUBLESHOOTING.md](TROUBLESHOOTING.md)*