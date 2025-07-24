# 🔐 Zerodha API Setup Guide - Complete Step-by-Step Instructions

**This guide will help you get the API credentials needed to connect the trading bot to your Zerodha account.**

## ⚠️ **Important Before You Start**

🛡️ **Your API credentials are like your account password - keep them secret!**  
💰 **API access costs ₹2,000/month from Zerodha (charged automatically)**  
🎓 **You need an active Zerodha trading account with some balance**  
📞 **API access is different from normal Zerodha login - you need to apply separately**

---

## 🎯 **What You'll Get From This Guide**

After following this guide, you'll have:
- ✅ **API Key** - Identifies your application to Zerodha
- ✅ **API Secret** - Like a password for your API Key  
- ✅ **Access Token** - Temporary token to make trades (changes daily)
- ✅ **Working credentials** - Tested and ready to use with the bot

---

## 🏁 **Prerequisites Checklist**

Before starting, make sure you have:

- [ ] **Active Zerodha account** with trading enabled
- [ ] **PAN card** linked to your Zerodha account
- [ ] **Mobile number** registered with Zerodha
- [ ] **Email address** registered with Zerodha
- [ ] **Some balance** in your trading account (for testing)
- [ ] **Computer/phone** to access Zerodha website

---

## 📋 **Step 1: Understanding Zerodha API Charges**

### **What It Costs:**
- **₹2,000 per month** - Charged automatically from your account
- **Pro-rated billing** - If you subscribe mid-month, you pay proportionally
- **No setup fees** - Just the monthly subscription

### **What You Get:**
- **Unlimited API calls** during market hours
- **Real-time market data** access
- **Order placement** capabilities
- **Portfolio and position** information
- **Historical data** access

### **When Charges Start:**
- Billing starts immediately after approval
- First charge appears in your account within 24 hours
- Monthly charges on the same date each month

---

## 🚀 **Step 2: Apply for API Access**

### **2.1 Go to Zerodha Kite Connect Website**

1. **Open your web browser**
2. **Go to:** `https://kite.trade/`
3. **Look for:** "Kite Connect" section or "API" link
4. **Click on:** "Create App" or "Get Started" button

### **2.2 Login to Your Zerodha Account**

You'll be redirected to Zerodha login page:

1. **Enter your User ID** (6-character code like AB1234)
2. **Enter your Password**
3. **Complete 2FA** (TOTP or SMS verification)
4. **Click Login**

### **2.3 Fill Out the API Application Form**

You'll see a form with several fields. Here's what to enter:

#### **App Name:** 
- **What to enter:** `My Trading Bot` or `Personal Trading App`
- **Why:** This is just for your reference - can be anything meaningful

#### **App Type:**
- **What to select:** `Personal` 
- **Why:** You're using this for your own trading, not commercial

#### **App Description:**
- **What to enter:** `Personal algorithmic trading bot for automated stock trading`
- **Why:** Explains what you'll use the API for

#### **Redirect URL:**
- **What to enter:** `http://localhost:8080`
- **Why:** This is where Zerodha sends authentication responses
- **Important:** Use exactly this URL - the bot expects it

#### **Publisher:**
- **What to enter:** Your full name (same as Zerodha account)
- **Why:** Must match your account holder name

#### **Publisher Website:**
- **What to enter:** `http://localhost` or leave blank if optional
- **Why:** Not important for personal use

### **2.4 Submit Application**

1. **Review all information** carefully
2. **Check the checkbox** agreeing to terms
3. **Click "Submit Application"**
4. **Note down your Application ID** - you'll get an email with this

---

## ⏰ **Step 3: Wait for Approval (Usually 1-2 Business Days)**

### **What Happens Next:**
1. **Zerodha reviews** your application (usually quick for personal use)
2. **You'll get an email** when approved or if they need more information
3. **Check your email** regularly - sometimes goes to spam
4. **Login to Kite Connect** portal once approved

### **If Your Application is Rejected:**
- **Common reasons:** Incomplete information, commercial use detected
- **What to do:** Reapply with correct information
- **Contact support:** Email connect@zerodha.com for help

---

## 🔑 **Step 4: Get Your API Credentials (After Approval)**

### **4.1 Access Your App Dashboard**

1. **Go back to:** `https://kite.trade/`
2. **Click:** "Login" or "Dashboard"
3. **Login** with your Zerodha credentials
4. **Find your app** in the dashboard

### **4.2 Find Your API Key and Secret**

In your app dashboard, you'll see:

#### **API Key:**
- **Looks like:** `abcdef123456` (alphanumeric string)
- **Purpose:** Identifies your app to Zerodha
- **Important:** This doesn't change - save it safely

#### **API Secret:**
- **Looks like:** `xyz789abc123def456` (longer alphanumeric string)  
- **Purpose:** Like a password for your API Key
- **CRITICAL:** Keep this absolutely secret - anyone with this can trade!

### **4.3 Copy and Save Credentials Safely**

1. **Copy API Key** - highlight and copy the entire string
2. **Copy API Secret** - highlight and copy the entire string
3. **Save both** in a secure text file on your computer
4. **Double-check** - make sure you copied complete strings

---

## 🎟️ **Step 5: Generate Access Token (Required Daily)**

### **Understanding Access Tokens:**
- **What it is:** A temporary permission to make trades
- **How long it lasts:** Usually 24 hours (expires daily)
- **Why needed:** Extra security layer for trading operations
- **When to generate:** Every day before using the bot

### **5.1 Generate Your First Access Token**

1. **In your app dashboard** on Kite Connect
2. **Look for:** "Generate Token" or "Access Token" button
3. **Click it** - you'll be redirected to Zerodha login
4. **Login again** with your credentials
5. **Authorize the app** - click "Allow" or "Authorize"
6. **You'll be redirected** to `http://localhost:8080?request_token=...`

### **5.2 Extract the Request Token**

The URL will look like: `http://localhost:8080?request_token=ABC123DEF456&action=login&status=success`

1. **Copy everything after `request_token=`** and before the next `&`
2. **Example:** If URL is `http://localhost:8080?request_token=ABC123DEF456&action=login`
3. **Your request token is:** `ABC123DEF456`

### **5.3 Convert Request Token to Access Token**

**Option A: Use Zerodha's Token Generator Tool**
1. **Go to:** Your app dashboard on Kite Connect
2. **Look for:** "Generate Session" or similar tool
3. **Paste your request token**
4. **Get your access token** - save this!

**Option B: Use the Trading Bot's Token Generator**
1. **Run:** `python generate_token.py` in the bot folder
2. **Follow the prompts** to enter API key, secret, and request token
3. **Bot will generate** the access token for you

---

## 💾 **Step 6: Configure the Trading Bot**

### **6.1 Create secrets.json File**

1. **Navigate to** your trading bot folder
2. **Create a new file** called `secrets.json`
3. **Copy this template:**

```json
{
  "api_key": "YOUR_API_KEY_HERE",
  "api_secret": "YOUR_API_SECRET_HERE", 
  "access_token": "YOUR_ACCESS_TOKEN_HERE",
  "token_generated_at": "2025-07-24T10:30:00.000000",
  "refresh_token": "",
  "user_id": "YOUR_USER_ID_HERE"
}
```

### **6.2 Fill in Your Actual Values**

Replace the placeholder values:

- **YOUR_API_KEY_HERE** → Your actual API key from Step 4
- **YOUR_API_SECRET_HERE** → Your actual API secret from Step 4  
- **YOUR_ACCESS_TOKEN_HERE** → Your access token from Step 5
- **YOUR_USER_ID_HERE** → Your Zerodha User ID (like AB1234)

### **6.3 Example of Completed secrets.json**

```json
{
  "api_key": "abcdef123456",
  "api_secret": "xyz789abc123def456",
  "access_token": "generated_token_here_very_long_string",
  "token_generated_at": "2025-07-24T10:30:00.000000",
  "refresh_token": "",
  "user_id": "AB1234"
}
```

### **6.4 Save and Secure the File**

1. **Save the file** in your trading bot folder
2. **Check permissions** - only you should be able to read it
3. **Make a backup** copy in a secure location
4. **Never share** this file with anyone

---

## ✅ **Step 7: Test Your API Credentials**

### **7.1 Test Basic Connection**

Run this simple test to make sure your credentials work:

```bash
python -c "
from kiteconnect import KiteConnect
import json

# Load credentials
with open('secrets.json', 'r') as f:
    secrets = json.load(f)

# Test connection
kite = KiteConnect(api_key=secrets['api_key'])
kite.set_access_token(secrets['access_token'])

# Try to get profile
try:
    profile = kite.profile()
    print('✅ SUCCESS: Connected to Zerodha!')
    print(f'Account: {profile[\"user_name\"]} ({profile[\"user_id\"]})')
    print(f'Email: {profile[\"email\"]}')
except Exception as e:
    print(f'❌ ERROR: {e}')
    print('Check your credentials and try again')
"
```

### **7.2 Expected Success Output**

If everything works, you should see:
```
✅ SUCCESS: Connected to Zerodha!
Account: Your Name (AB1234)
Email: your.email@example.com
```

### **7.3 If You See Errors**

**Common errors and solutions:**

**"Invalid API credentials"**
- Check that you copied API key and secret correctly
- Make sure there are no extra spaces or characters

**"Access token expired"**
- Generate a new access token (Step 5)
- Update your secrets.json file

**"Invalid access token"**
- Double-check you copied the complete access token
- Make sure you used the correct request token

---

## 🔄 **Step 8: Daily Token Refresh Process**

### **Why You Need to Do This:**
Access tokens expire after 24 hours for security. You need to generate a new one each day.

### **8.1 Quick Daily Process (2 minutes):**

1. **Go to** your Kite Connect app dashboard
2. **Click** "Generate Token" 
3. **Login** to Zerodha when prompted
4. **Copy** the request token from the redirect URL
5. **Run** `python generate_token.py` in your bot folder
6. **Enter** the request token when prompted
7. **New access token** is automatically saved to secrets.json

### **8.2 Automated Token Refresh (Advanced)**

The bot can help remind you:
- Set up daily reminders on your phone
- Bot will detect expired tokens and guide you
- Consider this part of your daily trading routine

---

## 🛡️ **Step 9: Security Best Practices**

### **Protecting Your Credentials:**

1. **Never share** your API secret or access tokens
2. **Don't commit** secrets.json to git or version control
3. **Use strong passwords** for your computer and Zerodha account
4. **Enable 2FA** on your Zerodha account
5. **Regularly monitor** your account for unauthorized activity

### **Safe Storage:**
- Keep backups in encrypted storage
- Use password managers for sensitive data
- Don't store credentials in cloud drives unencrypted

### **Regular Security Checks:**
- Review API usage in Zerodha dashboard monthly
- Monitor unusual trading activity
- Keep your trading bot software updated

---

## 🚨 **Troubleshooting Common Issues**

### **Issue: "Application Rejected"**
**Possible causes:**
- Incomplete application form
- Using it for commercial purposes without proper approval
- Mismatch between account name and publisher name

**Solutions:**
- Reapply with complete, accurate information
- Contact connect@zerodha.com for clarification
- Ensure you're applying for personal use

### **Issue: "API Charges Not Clear"**
**What happens:**
- ₹2,000 charged monthly from your trading account
- Charges appear as "API Subscription" in account statement
- Pro-rated if you start mid-month

**To check charges:**
- Login to Kite/Console
- Check "Funds" or "Account Statement" 
- Look for "API" related charges

### **Issue: "Cannot Generate Access Token"**
**Common causes:**
- Request token copied incorrectly
- Trying to use old request tokens (they expire quickly)
- API key or secret is wrong

**Solutions:**
- Generate a fresh request token
- Copy the complete token string carefully
- Verify API key and secret are correct

### **Issue: "Bot Cannot Connect"**
**Debugging steps:**
1. **Test credentials** manually (Step 7.1)
2. **Check secrets.json** format and values
3. **Verify access token** is recent (less than 24 hours old)
4. **Check internet connection**
5. **Look at bot logs** for specific error messages

---

## 📞 **Getting Help**

### **Zerodha API Support:**
- **Email:** connect@zerodha.com
- **Documentation:** https://kite.trade/docs/
- **Response time:** Usually 1-2 business days

### **Bot-Specific Issues:**
- Check the bot's [TROUBLESHOOTING.md](TROUBLESHOOTING.md) guide
- Look at log files in the `logs/` folder
- Create an issue in the bot's GitHub repository

### **Emergency Contact:**
If you suspect unauthorized API access:
1. **Immediately disable** API access in Kite Connect dashboard
2. **Contact Zerodha** support urgently
3. **Change your passwords**
4. **Review account activity**

---

## ✅ **Final Checklist**

Before moving to the next step, make sure you have:

- [ ] **API Key** - copied and saved securely
- [ ] **API Secret** - copied and saved securely  
- [ ] **Access Token** - generated and tested
- [ ] **secrets.json** - created and populated correctly
- [ ] **Connection test** - passed successfully
- [ ] **Understanding** - know how to generate new tokens daily
- [ ] **Security** - credentials stored safely

---

## 🎉 **Congratulations!**

You now have working Zerodha API credentials! 

**Your next steps:**
1. 👉 **Go to [💻 Installation Guide](INSTALLATION_GUIDE.md)** - Set up the bot software
2. 👉 **Or go to [📖 User Manual](USER_MANUAL.md)** - Learn how to use the bot

---

**Remember: Keep your credentials secret and generate new access tokens daily! 🔐**

---

*Last updated: July 2025 | For questions: Check FAQ.md or TROUBLESHOOTING.md*