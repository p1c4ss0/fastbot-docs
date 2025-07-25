# 🚀 FastBot - AI Trading Bot Documentation

[\![Documentation Status](https://img.shields.io/badge/docs-live-brightgreen)](https://p1c4ss0.github.io/fastbot-docs/)
[\![Version](https://img.shields.io/badge/version-v2.0-blue)](https://github.com/p1c4ss0/fastbot/releases)
[\![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

> **Complete documentation for the AI-enhanced Zerodha trading bot with automated intraday trading capabilities**

## 📖 **Documentation Site**

**🌐 Live Documentation**: [https://p1c4ss0.github.io/fastbot-docs/](https://p1c4ss0.github.io/fastbot-docs/)

## 📚 **Quick Navigation**

| Guide | Description | Link |
|-------|-------------|------|
| 🚀 **Quick Start** | Get started in 5 minutes | [Quick Start](quick-start.md) |
| 💾 **Installation** | Complete setup guide | [Installation Guide](INSTALLATION_GUIDE.md) |
| ⚠️ **Safety** | Risk management & safety | [Safety Guide](SAFETY_GUIDE.md) |
| 📱 **Zerodha Setup** | API integration steps | [Zerodha Setup](ZERODHA_SETUP_GUIDE.md) |
| 📖 **User Manual** | Complete feature guide | [User Manual](USER_MANUAL.md) |
| ⚙️ **Configuration** | Advanced settings | [Configuration](CONFIGURATION_GUIDE.md) |
| 🔧 **Troubleshooting** | Common issues & fixes | [Troubleshooting](TROUBLESHOOTING.md) |
| ❓ **FAQ** | Frequently asked questions | [FAQ](FAQ.md) |

## 🤖 **About FastBot**

FastBot is an advanced AI-enhanced trading bot designed for the Indian stock market through Zerodha integration. It combines:

- **🧠 AI Intelligence**: XGBOOST model with 75%+ accuracy
- **📊 Advanced Analytics**: 125-point scoring system with news integration
- **🛡️ Risk Management**: Dynamic stop-loss with trailing capabilities
- **📈 Real-time Analysis**: Technical indicators, volume analysis, and market sentiment

## 🔥 **Key Features**

### **Trading Modes**
- **📈 Live**: Real money trading with Zerodha API
- **🧪 Dryrun**: Risk-free simulation with real market data
- **📊 Backtest**: Historical performance analysis

### **AI & Analytics**
- **Hybrid AI Mode**: Statistical + Machine Learning signals
- **News Integration**: Real-time news analysis with price reaction scoring
- **Market Environment**: Dynamic strategy selection based on market conditions
- **Enhanced Logging**: Complete audit trail with event tracking

### **Safety & Control**
- **Paper Trading**: Test strategies without risking capital
- **Position Limits**: Configurable daily trade and capital limits  
- **Emergency Controls**: Instant stop-all and force-exit capabilities
- **Risk Metrics**: Real-time P&L tracking and exposure monitoring

## ⚡ **Quick Start**

```bash
# 1. Clone the main repository (private)
git clone https://github.com/p1c4ss0/fastbot.git
cd fastbot

# 2. Install dependencies
pip install -r requirements.txt

# 3. Configure Zerodha API credentials
cp secrets.json.template secrets.json
# Edit secrets.json with your API credentials

# 4. Start in dryrun mode (safe)
python main.py --mode dryrun
```

> ⚠️ **Important**: Always start with `--mode dryrun` to test without risking real money\!

## 📋 **Prerequisites**

- **Python 3.8+** 
- **Zerodha Account** with KiteConnect API access
- **Basic Trading Knowledge** (recommended)
- **Risk Management Plan** (essential)

## 🛡️ **Safety First**

> **🚨 CRITICAL**: This bot trades with real money in live mode. Always:
> 
> - Start with paper trading (`--mode dryrun`)
> - Set appropriate position limits
> - Never risk more than you can afford to lose
> - Read the [Safety Guide](SAFETY_GUIDE.md) completely
> - Test thoroughly before live trading

## 🤝 **Support & Community**

- **📖 Documentation**: [https://p1c4ss0.github.io/fastbot-docs/](https://p1c4ss0.github.io/fastbot-docs/)
- **🐛 Issues**: [Report Issues](https://github.com/p1c4ss0/fastbot/issues) (main repository)
- **💬 Discussions**: [GitHub Discussions](https://github.com/p1c4ss0/fastbot/discussions)

## 📄 **License**

This documentation is licensed under the [MIT License](LICENSE).

## ⚠️ **Disclaimer**

> **Trading involves substantial risk of loss and is not suitable for all investors. Past performance is not indicative of future results. This software is provided for educational purposes only. Use at your own risk.**

---

## 🔗 **Related Links**

- **Main Repository**: [p1c4ss0/fastbot](https://github.com/p1c4ss0/fastbot) (private)
- **Documentation Source**: [This Repository](https://github.com/p1c4ss0/fastbot-docs)
- **Live Documentation**: [GitHub Pages](https://p1c4ss0.github.io/fastbot-docs/)

---

*Last updated: 2025-07-24 | Version: v2.0 Stable*
EOF < /dev/null
