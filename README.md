---

# 🚀 Affiliate Management - Coin Listing Alert System

A fully automated system that:
- ✅ Fetches **coin listing alerts** from **Slack**.
- ✅ Matches alerts with **affiliate links** stored in **Google Sheets**.
- ✅ Stores results in a dynamic **JSON file** (`coin_listing_alerts.json`).
- ✅ Displays the latest listings on a public **index.html** page.
- ✅ Automatically removes alerts older than **3 days**.
- ✅ Keeps the list sorted by **newest to oldest**.
- ✅ Runs on **GitHub Actions** for full automation.

---

## 🛠️ What You Need to Prepare

### 1️⃣ Google Sheet for Affiliate Links
Prepare a **Google Sheet** with the following structure:

| Name    | Link                              |
|---------|-----------------------------------|
| Binance | Binance referral link   |
| MEXC    | MEXC referral link     |
| Bybit   | Bybit referral link |

- **Make it public** or accessible via **Google Sheets API**.
- Get your **Sheet ID** from the URL:
  ```
  https://docs.google.com/spreadsheets/d/**YOUR_SHEET_ID**/edit
  ```
- Generate your **Google Sheets API Key** from [Google Cloud Console](https://console.cloud.google.com/).

---

### 2️⃣ Slack Bot for Reading Alerts
Prepare a **Slack Bot**:
- Create via [Slack API Apps](https://api.slack.com/apps).
- Add **OAuth Scope**: `channels:history`.
- Install to your workspace.
- Copy your **Bot Token** (`xoxb-...`).
- Copy the **Channel ID** of the Slack channel where alerts are posted.

---

### 3️⃣ Environment Variables
You must set these as **GitHub Secrets** for your Actions to work:

| Secret Name          | Description                   |
|----------------------|-------------------------------|
| `GOOGLE_SHEET_API`  | Your Google Sheets API Key   |
| `SLACK_BOT_TOKEN`   | Your Slack Bot Token         |
| `SLACK_CHANNEL_ID`  | The Slack Channel ID         |

---

## 📁 Project Structure
```
├── .github/workflows/           # GitHub Actions workflow
│   └── update_alerts.yml        # Auto-updates alerts on schedule
├── coin_listing_alerts.json     # Auto-updated JSON with latest listings
├── fetch_alerts.py              # Python script to fetch and process alerts
├── index.html                   # Frontend display of the latest listings
├── README.md                    # Project documentation
```

---

## 🔄 How It Works
1. **Fetch exchanges** and affiliate links from Google Sheets.
2. **Fetch latest messages** from your Slack channel.
3. **Parse messages** for coin listing patterns like:
   ```
   Dogecoin (DOGE) just listed on Binance -
   ```
4. **Match exchanges** and attach affiliate links.
5. **Remove old alerts** (older than 3 days).
6. **Save to `coin_listing_alerts.json`**, sorted from newest to oldest.
7. **GitHub Actions** runs this automatically on schedule.
8. **index.html** displays the live feed from `coin_listing_alerts.json`.

---

## 📝 Example Output (`coin_listing_alerts.json`)
```json
[
    {
        "exchange": "Binance",
        "coin": "Ethereum",
        "ticker": "ETH",
        "affiliate_url": "Binance referral link",
        "date_added": "2025-03-06"
    },
    {
        "exchange": "MEXC",
        "coin": "Dogecoin",
        "ticker": "DOGE",
        "affiliate_url": "MEXC referral link",
        "date_added": "2025-03-05"
    }
]
```

---

## ⚙️ How to Run Locally
```bash
# Clone the repo
git clone https://github.com/yourusername/affiliate-management-list.git
cd affiliate-management-list

# Install dependencies
pip install -r requirements.txt

# Run the script
python fetch_alerts.py
```

---

## 🔁 Automation with GitHub Actions
This project uses **`.github/workflows/update_alerts.yml`** to:
- Auto-run the `fetch_alerts.py` script on schedule (every X hours/days).
- Push updates to `coin_listing_alerts.json`.
- Keep your frontend (`index.html`) always displaying fresh data.

---

## 🖥️ Frontend Integration Example (`index.html`)
```javascript
fetch("coin_listing_alerts.json")
    .then(response => response.json())
    .then(data => {
        data.forEach(alert => {
            console.log(`${alert.coin} (${alert.ticker}) listed on ${alert.exchange}`);
        });
    });
```

---

## 🗓️ Future Improvements
- Telegram integration for alerts.
- Email notifications on new listings.
- Webhooks for external services.
- Admin dashboard for manual adjustments.

---

## 👤 Author
Made with ❤️ by Aaqil Ahamad  
🔗 [[GitHub Profile Link] ](https://github.com/Aaqil456) 

---

## 📜 License
MIT License

---
