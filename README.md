✨[doyouwannagooutwithme.com](http://doyouwannagooutwithme.com)

A website to invite your lover for a date 🥰

## Google Sheet connection (your sheet is pre-filled)

Your sheet URL is already wired into `yes.html`:

- https://docs.google.com/spreadsheets/d/1LoEVfNh6R56ITLgwW1IpciXLI-Yky5bR0n4W5HpVzco/edit?gid=0#gid=0

Your expected columns are supported:

- `date`
- `time`
- `timezone`
- `submittedAt`

## Final step required (important)

A static website cannot append rows directly to a private Google Sheet URL.
You still need a **Google Apps Script Web App URL** (`.../exec`) and paste it in `yes.html`.

1. Open your target sheet.
2. Go to **Extensions → Apps Script**.
3. Paste:

```javascript
const SHEET_ID = '1LoEVfNh6R56ITLgwW1IpciXLI-Yky5bR0n4W5HpVzco';
const SHEET_NAME = 'Sheet1';

function doPost(e) {
  const payload = JSON.parse(e.postData.contents || '{}');
  const sheet = SpreadsheetApp.openById(SHEET_ID).getSheetByName(SHEET_NAME);

  sheet.appendRow([
    payload.date || '',
    payload.time || '',
    payload.timezone || 'Asia/Karachi',
    payload.submittedAt || new Date().toISOString()
  ]);

  return ContentService
    .createTextOutput(JSON.stringify({ ok: true }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

4. Click **Deploy → New deployment → Web app**.
5. Set:
   - Execute as: **Me**
   - Who has access: **Anyone**
6. Copy the Web App URL (ends with `/exec`).
7. In `yes.html`, replace:
   - `PASTE_YOUR_GOOGLE_APPS_SCRIPT_WEB_APP_URL_HERE`
8. Redeploy your site.
