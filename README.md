✨[doyouwannagooutwithme.com](http://doyouwannagooutwithme.com)

A website to invite your lover for a date 🥰

## Save selected date/time to Google Sheets

The `yes.html` page now stores the selected date/time in the browser and can also send it to Google Sheets.

1. Create a Google Sheet (for example with columns: `date`, `time`, `timezone`, `submittedAt`).
2. Open **Extensions → Apps Script** and paste this script:

```javascript
const SHEET_NAME = 'Sheet1';

function doPost(e) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName(SHEET_NAME);
  const payload = JSON.parse(e.postData.contents || '{}');

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

3. Deploy it as a Web App:
   - Execute as: **Me**
   - Who has access: **Anyone**
4. Copy the Web App URL.
5. In `yes.html`, replace `PASTE_YOUR_GOOGLE_APPS_SCRIPT_WEB_APP_URL_HERE` with your Web App URL.
6. Redeploy your static site.
