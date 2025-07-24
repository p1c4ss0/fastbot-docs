# ⚙️ Configuration Guide

## 🎯 Overview

This guide explains how to customize the trading bot's behavior through various configuration files. Each file controls different aspects of the bot's operation.

**📂 Configuration Files Location:**
```
config/
├── trading_config.json          # Main trading settings
├── prefilter_config.json        # Stock filtering criteria
├── atr_config.json              # ATR management settings
├── news_config.json             # News detection settings
└── atr_master_config.json       # Advanced ATR profiles
```

---

## 🎛️ Main Trading Configuration (`trading_config.json`)

This is the primary configuration file that controls the bot's overall behavior.

### **Basic Structure:**
```json
{
  "strategy_selection": {
    "primary_strategy": "catalyst_gainers",
    "user_selected": true,
    "selection_time": "2024-07-24T12:30:00"
  },
  "position_management": {
    "max_positions": 8,
    "capital_per_trade": 12500,
    "min_position_value": 5000,
    "max_position_value": 25000
  },
  "risk_management": {
    "max_daily_loss": 5000,
    "max_daily_trades": 15,
    "stop_loss_percent": 1.0,
    "force_exit_time": "15:20"
  },
  "scoring": {
    "minimum_score": 12.0,
    "score_components": {
      "abnormality_weight": 0.35,
      "catalyst_weight": 0.25,
      "rrg_weight": 0.20,
      "timing_weight": 0.15,
      "news_weight": 0.05
    }
  },
  "exit_strategy": {
    "profit_targets": {
      "t1_percent": 1.0,
      "t2_percent": 2.0,
      "t3_percent": 3.0
    },
    "trailing_stop_loss": true,
    "time_based_exit": true
  },
  "ai_settings": {
    "enabled": true,
    "mode": "hybrid",
    "confidence_threshold": 70,
    "fallback_to_statistical": true
  }
}
```

### **Configuration Sections Explained:**

#### **🎯 Strategy Selection**
```json
"strategy_selection": {
  "primary_strategy": "catalyst_gainers",  // or "momentum_breakout"
  "user_selected": true,                   // Auto-set by CLI
  "selection_time": "2024-07-24T12:30:00" // Auto-set timestamp
}
```

**Options:**
- `"catalyst_gainers"`: AI-enhanced catalyst detection strategy
- `"momentum_breakout"`: Traditional momentum-based strategy

#### **💰 Position Management**
```json
"position_management": {
  "max_positions": 8,           // Maximum concurrent trades
  "capital_per_trade": 12500,   // Fixed amount per trade
  "min_position_value": 5000,   // Minimum trade size
  "max_position_value": 25000   // Maximum trade size
}
```

**Customization Tips:**
- **Conservative:** `max_positions: 3-5`, `capital_per_trade: 5000-10000`
- **Aggressive:** `max_positions: 10-15`, `capital_per_trade: 15000-25000`
- **Small Account (<₹50K):** `max_positions: 2-3`, `capital_per_trade: 5000-8000`

#### **🛡️ Risk Management**
```json
"risk_management": {
  "max_daily_loss": 5000,       // Stop trading after losing this much
  "max_daily_trades": 15,       // Limit total trades per day
  "stop_loss_percent": 1.0,     // Individual trade stop loss (1%)
  "force_exit_time": "15:20"    // Close all positions before market close
}
```

**Risk Levels:**
- **Conservative:** `max_daily_loss: 2000`, `stop_loss_percent: 0.5`
- **Moderate:** `max_daily_loss: 5000`, `stop_loss_percent: 1.0`
- **Aggressive:** `max_daily_loss: 10000`, `stop_loss_percent: 1.5`

#### **🎯 Scoring System**
```json
"scoring": {
  "minimum_score": 12.0,        // Minimum score to trigger trade
  "score_components": {
    "abnormality_weight": 0.35, // Weight for abnormality detection
    "catalyst_weight": 0.25,    // Weight for catalyst analysis
    "rrg_weight": 0.20,         // Weight for RRG momentum
    "timing_weight": 0.15,      // Weight for timing factors
    "news_weight": 0.05         // Weight for news reactions
  }
}
```

**Score Thresholds:**
- **Conservative (fewer trades):** `minimum_score: 15-20`
- **Moderate:** `minimum_score: 10-15`
- **Aggressive (more trades):** `minimum_score: 5-10`

#### **📈 Exit Strategy**
```json
"exit_strategy": {
  "profit_targets": {
    "t1_percent": 1.0,          // First target at 1% profit
    "t2_percent": 2.0,          // Second target at 2% profit  
    "t3_percent": 3.0           // Third target at 3% profit
  },
  "trailing_stop_loss": true,   // Enable trailing stop after T1
  "time_based_exit": true       // Force exit at 3:20 PM
}
```

**Target Strategies:**
- **Conservative:** `t1: 0.5`, `t2: 1.0`, `t3: 1.5`
- **Moderate:** `t1: 1.0`, `t2: 2.0`, `t3: 3.0`
- **Aggressive:** `t1: 1.5`, `t2: 3.0`, `t3: 5.0`

#### **🤖 AI Settings**
```json
"ai_settings": {
  "enabled": true,              // Enable AI-powered signals
  "mode": "hybrid",             // ai_only, statistical_only, or hybrid
  "confidence_threshold": 70,   // Minimum AI confidence (0-100)
  "fallback_to_statistical": true, // Use technical analysis if AI fails
  "max_memory_usage_gb": 12,    // AI model memory limit
  "circuit_breaker_enabled": true  // Emergency AI shutdown
}
```

**AI Modes:**
- `"ai_only"`: Use only AI predictions
- `"statistical_only"`: Use only technical analysis
- `"hybrid"`: Combine both (recommended)
- `"auto"`: Automatically choose best mode

---

## 🔍 Stock Filtering Configuration (`prefilter_config.json`)

Controls which stocks the bot considers for trading.

### **Complete Configuration:**
```json
{
  "filters": {
    "min_price": 50,
    "max_price": 5000,
    "min_volume": 50000,
    "min_atr_percent": 0.3,
    "max_atr_percent": 8.0,
    "min_rsi": 30,
    "max_rsi": 70,
    "min_adx": 20,
    "exclude_sectors": ["PHARMA", "IT"],
    "include_nse500_only": true
  },
  "scoring_criteria": {
    "volume_multiplier": 2.0,
    "price_change_threshold": 1.0,
    "rsi_oversold": 30,
    "rsi_overbought": 70,
    "bollinger_squeeze": 0.02
  },
  "risk_filters": {
    "max_beta": 2.0,
    "min_market_cap": 1000,
    "exclude_penny_stocks": true,
    "max_spread_percent": 0.5
  }
}
```

### **Key Parameters Explained:**

#### **📊 Basic Filters**
- `min_price`: Minimum stock price (₹50 default)
- `max_price`: Maximum stock price (₹5000 default)
- `min_volume`: Minimum daily trading volume (50,000 shares)
- `min_atr_percent`: Minimum Average True Range for volatility
- `max_atr_percent`: Maximum ATR to avoid overly volatile stocks

#### **📈 Technical Filters**
- `min_rsi/max_rsi`: RSI range for stock selection
- `min_adx`: Minimum ADX for trend strength
- `exclude_sectors`: Sectors to avoid (e.g., ["PHARMA", "BANK"])
- `include_nse500_only`: Only trade NSE 500 stocks

#### **🛡️ Risk Filters**
- `max_beta`: Maximum stock beta vs market
- `min_market_cap`: Minimum market capitalization (₹Cr)
- `exclude_penny_stocks`: Avoid stocks below ₹10
- `max_spread_percent`: Maximum bid-ask spread

### **Preset Configurations:**

#### **Conservative Profile:**
```json
{
  "filters": {
    "min_price": 100,
    "max_price": 2000,
    "min_volume": 100000,
    "min_atr_percent": 0.5,
    "max_atr_percent": 3.0,
    "include_nse500_only": true
  }
}
```

#### **Aggressive Profile:**
```json
{
  "filters": {
    "min_price": 20,
    "max_price": 10000,
    "min_volume": 25000,
    "min_atr_percent": 0.2,
    "max_atr_percent": 10.0,
    "include_nse500_only": false
  }
}
```

---

## 📊 ATR Configuration (`atr_config.json` & `atr_master_config.json`)

Controls Advanced True Range (volatility) management.

### **Basic ATR Config (`atr_config.json`):**
```json
{
  "default_threshold": 0.8,
  "time_based_thresholds": {
    "09:15-10:00": 0.2,
    "10:00-11:00": 0.5,
    "11:00-14:00": 0.8,
    "14:00-15:30": 1.0
  },
  "catalyst_override": {
    "enabled": true,
    "min_catalyst_score": 25,
    "override_threshold": 0.3
  },
  "sector_adjustments": {
    "BANK": 1.2,
    "IT": 0.8,
    "PHARMA": 1.5,
    "AUTO": 1.0
  }
}
```

### **Master ATR Config (`atr_master_config.json`):**
```json
{
  "profiles": {
    "conservative": {
      "base_threshold": 1.0,
      "max_threshold": 3.0,
      "catalyst_multiplier": 0.8
    },
    "moderate": {
      "base_threshold": 0.8,
      "max_threshold": 5.0,
      "catalyst_multiplier": 1.0
    },
    "aggressive": {
      "base_threshold": 0.5,
      "max_threshold": 8.0,
      "catalyst_multiplier": 1.2
    }
  },
  "current_profile": "moderate",
  "environment_overrides": {
    "backtest": {
      "base_threshold": 0.6
    },
    "live": {
      "base_threshold": 1.0
    }
  }
}
```

---

## 📰 News Configuration (`news_config.json`)

Controls news detection and scoring.

### **Complete News Config:**
```json
{
  "news_api": {
    "provider": "yahoo_finance_server",
    "base_url": "http://localhost:3001",
    "timeout": 10,
    "max_retries": 3
  },
  "detection_settings": {
    "news_window_minutes": 30,
    "volume_spike_threshold": 1.5,
    "price_reaction_threshold": 0.5,
    "enable_micro_gap_detection": true,
    "micro_gap_threshold": 0.3
  },
  "scoring_weights": {
    "full_news_reaction": 15,
    "price_breakout_only": 8,
    "volume_spike_only": 5,
    "micro_gap_bonus": 3
  },
  "filters": {
    "min_news_relevance": 0.7,
    "exclude_keywords": ["rumor", "unconfirmed"],
    "require_keywords": ["earnings", "results", "announcement"]
  }
}
```

### **News Scoring Logic:**
- **Full News Reaction (15 points):** News within 30 minutes + volume spike + price above news candle high
- **Price Breakout Only (8 points):** Price above news high without volume confirmation
- **Volume Spike Only (5 points):** Volume spike without price confirmation
- **Micro Gap Bonus (3 points):** Small gap (≥0.3%) detected at market open

---

## 🎨 Custom Configuration Examples

### **Day Trading Setup (High Frequency)**
```json
{
  "position_management": {
    "max_positions": 15,
    "capital_per_trade": 8000
  },
  "scoring": {
    "minimum_score": 8.0
  },
  "exit_strategy": {
    "profit_targets": {
      "t1_percent": 0.5,
      "t2_percent": 1.0,
      "t3_percent": 1.5
    }
  },
  "risk_management": {
    "stop_loss_percent": 0.5,
    "max_daily_trades": 25
  }
}
```

### **Swing Trading Setup (Lower Frequency)**
```json
{
  "position_management": {
    "max_positions": 5,
    "capital_per_trade": 20000
  },
  "scoring": {
    "minimum_score": 18.0
  },
  "exit_strategy": {
    "profit_targets": {
      "t1_percent": 2.0,
      "t2_percent": 4.0,
      "t3_percent": 6.0
    }
  },
  "risk_management": {
    "stop_loss_percent": 1.5,
    "max_daily_trades": 8
  }
}
```

### **Small Account Setup (<₹50,000)**
```json
{
  "position_management": {
    "max_positions": 3,
    "capital_per_trade": 8000,
    "min_position_value": 3000
  },
  "risk_management": {
    "max_daily_loss": 2000,
    "stop_loss_percent": 0.8
  },
  "filters": {
    "min_price": 100,
    "max_price": 1000,
    "include_nse500_only": true
  }
}
```

### **Large Account Setup (>₹5,00,000)**
```json
{
  "position_management": {
    "max_positions": 12,
    "capital_per_trade": 25000,
    "max_position_value": 50000
  },
  "risk_management": {
    "max_daily_loss": 15000,
    "max_daily_trades": 20
  },
  "scoring": {
    "minimum_score": 10.0
  }
}
```

---

## 🔧 Configuration Management

### **Backup Your Configurations**
```bash
# Create backup
cp -r config/ config_backup_$(date +%Y%m%d)/

# Restore from backup
cp -r config_backup_20240724/* config/
```

### **Validate Configuration**
```python
# Test configuration validity
python -c "
import json
import os

config_files = [
    'config/trading_config.json',
    'config/prefilter_config.json',
    'config/atr_config.json',
    'config/news_config.json'
]

for file in config_files:
    if os.path.exists(file):
        try:
            with open(file, 'r') as f:
                json.load(f)
            print(f'✅ {file} is valid')
        except json.JSONDecodeError as e:
            print(f'❌ {file} has JSON errors: {e}')
    else:
        print(f'⚠️ {file} not found')
"
```

### **Reset to Defaults**
```bash
# Reset all configurations to defaults
python -c "
from core.config_manager import ConfigManager
cm = ConfigManager()
cm.reset_to_defaults()
print('✅ All configurations reset to defaults')
"
```

---

## 🎯 Configuration Best Practices

### **🔰 For Beginners:**
1. **Start with defaults** - Don't change anything initially
2. **Paper trade first** - Test configurations with fake money
3. **Change one thing at a time** - Don't modify everything at once
4. **Keep backups** - Always backup working configurations
5. **Document changes** - Note what you changed and why

### **📊 For Testing:**
1. **Use backtesting** - Test configuration changes on historical data
2. **Compare performance** - Run A/B tests between configurations
3. **Monitor carefully** - Watch bot behavior after changes
4. **Start small** - Test with reduced position sizes first

### **🚀 For Advanced Users:**
1. **Market adaptation** - Adjust settings based on market conditions
2. **Seasonal changes** - Different settings for different market phases
3. **Strategy combination** - Use multiple configurations for different timeframes
4. **Automated adjustment** - Create scripts to modify configs based on performance

---

## ⚠️ Common Configuration Mistakes

### **❌ Avoid These Errors:**

1. **Over-aggressive settings:**
   ```json
   // DON'T DO THIS
   {
     "max_positions": 50,          // Too many positions
     "stop_loss_percent": 0.1,     // Stop loss too tight
     "minimum_score": 1.0          // Score threshold too low
   }
   ```

2. **Conflicting settings:**
   ```json
   // DON'T DO THIS
   {
     "capital_per_trade": 50000,   // Large position size
     "max_daily_loss": 5000        // But small daily loss limit
   }
   ```

3. **Unrealistic targets:**
   ```json
   // DON'T DO THIS
   {
     "profit_targets": {
       "t1_percent": 10.0,         // 10% profit target is unrealistic
       "t2_percent": 20.0,         // for intraday trading
       "t3_percent": 50.0
     }
   }
   ```

### **✅ Better Alternatives:**

1. **Balanced settings:**
   ```json
   {
     "max_positions": 8,
     "stop_loss_percent": 1.0,
     "minimum_score": 12.0
   }
   ```

2. **Consistent risk management:**
   ```json
   {
     "capital_per_trade": 12500,
     "max_daily_loss": 10000
   }
   ```

3. **Realistic targets:**
   ```json
   {
     "profit_targets": {
       "t1_percent": 1.0,
       "t2_percent": 2.0,
       "t3_percent": 3.0
     }
   }
   ```

---

## 📞 Configuration Support

### **Getting Help:**
- **Documentation:** Read this guide thoroughly
- **Examples:** Check example configurations above
- **Testing:** Use backtesting to validate changes
- **Community:** Ask in GitHub discussions
- **Issues:** Report bugs in GitHub issues

### **When Asking for Help:**
- Share your configuration files (remove API keys!)
- Describe what you're trying to achieve
- Explain what's not working as expected
- Include error messages if any

---

**💡 Remember: Good configuration is the key to successful algorithmic trading. Start conservative and gradually optimize based on real performance data!**

---

*Last updated: July 2025 | For configuration support, check GitHub discussions*