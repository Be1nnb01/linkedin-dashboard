# LinkedIn Outreach Dashboard

Real-time dashboard for tracking InMail campaigns via Google Sheets.

## Setup

1. Clone this repo to your server
2. Point your web server to serve `index.html`

## Nginx Config

```nginx
server {
    listen 80;
    server_name dashboard.yourdomain.com;

    root /var/www/linkedin-dashboard;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Then enable HTTPS:
```bash
sudo certbot --nginx -d dashboard.yourdomain.com
```

## Configuration

Edit `index.html` line 27 to point to your Google Sheet CSV:

```javascript
const SHEET_CSV = 'https://docs.google.com/spreadsheets/d/e/YOUR_SHEET_ID/pub?gid=0&single=true&output=csv';
```

## Google Sheet Requirements

Your sheet must be published to web (File → Share → Publish to web → CSV).

Required columns:
- `LinkedIn URL` - Profile URL
- `Sent?` - TRUE/FALSE
- `SentDate` - ISO date (e.g., 2025-12-12T10:30:00Z)
- `Replied?` - TRUE/FALSE

## Features

- Auto-refreshes every 30 seconds
- Tracks: Sent, Replied, Response Rate, Today's Activity, Sent This Week, Queue Depth
- Zero backend required - reads directly from published Google Sheet
