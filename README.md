# Parking Roster

A static weekly parking allocation site for two shared parking permits, with a fixed employee rotation, annual leave and office closure handling.

## Files
- `index.html` — website
- `data.json` — employee list, rotation settings, leave and closure records
- `logo.png` — supplied company logo
- `DATA_GUIDE.md` — data field reference

## Publish with GitHub Pages
1. Upload all files in this folder to the root of your GitHub repository.
2. Open **Settings → Pages** in the repository.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Choose branch `main` and folder `/ (root)`, then save.
5. Wait for the site URL to appear on the Pages settings screen.

## Updating the roster
The website is static. Changes made in the browser do not automatically write to GitHub. Open **Data Management**, download the updated `data.json`, then upload it to the repository and replace the existing file.

## Privacy
If the repository is public, the website and `data.json` are public. Do not include private leave reasons, contact details, or other sensitive personal information.
