# CodeMind Summer — Registration

This repository contains the static registration page for CodeMind Summer and an Apps Script backend that saves submissions to a Google Sheet.

Contents

- `summer.html` — registration form (posts to Apps Script web app URL)
- `apps_script/Code.gs` — Google Apps Script `doPost` / `doGet` handlers that write/read the sheet

Deploy & test

1. Deploy Apps Script as a Web App (execute as: Me, who has access: Anyone)
   - Open the project in the Apps Script editor
   - `Deploy` → `New deployment` → select `Web app`
   - Set the deployment to run as your account and allow access as appropriate
   - Copy the deployed web app URL and paste it into the `action` attribute of the form in `summer.html` (it already contains a URL — confirm it matches your deployment)

2. Set `ADMIN_KEY` in Script Properties (for `doGet` viewer)
   - In Apps Script editor: `Project Settings` → `Script properties` → add `ADMIN_KEY`

3. Submit a registration
   - Open `summer.html` in a browser (serve it via static host or open file directly)
   - Fill and submit the form; the form posts to the Apps Script `doPost` and writes a row to the linked Google Sheet

Git / Push (on your machine)

Run these commands from the project root if you want me to prepare and push — you can also run them locally if you prefer.

```bash
git init
git remote add origin https://github.com/Mrseun247/summer-school.git
git branch -M main
git add summer.html README.md
git commit -m "Add registration page and README"
# Requires git auth (SSH key or credential helper / PAT). If configured, this will push:
git push -u origin main
```

If you want me to attempt the push from this environment, confirm you have git auth configured here (SSH key or credential helper). If not, run the commands above locally.

Email confirmations (optional)

- This project can send an automatic confirmation email to each registrant using EmailJS.
- Create an EmailJS account, add an email `service` (your service id is `service_tbzjg6k`) and create a `template` (for example `template_congrats`) with variables: `to_name`, `to_email`, `student_name`, `track`, `message`.
- In the browser (before loading `summer.html`) set two global variables to enable sending:

```html
<script>
   window.EMAILJS_PUBLIC_KEY = 'your_public_key_here';
   window.EMAILJS_TEMPLATE_ID = 'template_congrats';
</script>
```

- The page will load the EmailJS SDK and send the template after a successful form post (the form posts to Apps Script via a hidden iframe). If EmailJS isn't configured, the page will simply skip sending email.
