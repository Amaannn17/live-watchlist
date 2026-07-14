# Live Market Watchlist

A live, web-based market dashboard for tracking stock prices, calculating Profit & Loss (P&L), and logging manual snapshots, backed by Google Apps Script.

## Features

- **Live Polling**: Automatically fetches live stock data every 30 seconds.
- **Add/Delete Tickers**: Easily add new stock tickers to your watchlist or remove them.
- **P&L Calculation**: Displays live Profit and Loss based on historical baseline prices and investments.
- **Manual Snapshots**: Take and store point-in-time price snapshots (checkpoints) to track historical performance directly from the dashboard.

## Technologies Used

- **Frontend**: HTML5, CSS3, Vanilla JavaScript
- **Backend/Database**: Google Apps Script (communicating with Google Sheets)

## Setup & Usage

Since this is a simple static HTML file that communicates with a Google Apps Script endpoint:

1. Clone or download this repository.
2. Open `index.html` in your preferred web browser. No local server is required.
3. Start adding stock tickers to see live data and P&L!

**Note**: To use your own Google Sheet as the backend, you'll need to deploy a new Google Apps Script web app and update the `APP_SCRIPT_URL` constant in the `<script>` section of `index.html`.
