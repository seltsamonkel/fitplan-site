# fitplan-site

Static site for FitPlan, published by ASSSK LLC.

Hosts the public pages required for App Store and Google Play submission:

- `https://fitplan.asssk.me/` — minimal landing
- `https://fitplan.asssk.me/privacy/` — privacy policy
- `https://fitplan.asssk.me/terms/` — terms of use
- `https://fitplan.asssk.me/support/` — support / contact

The site is plain HTML with one shared stylesheet. No build step, no dependencies. GitHub Pages serves the files directly from the default branch.

## Repository layout

```
.
├── index.html             # Landing page
├── privacy/index.html     # Privacy policy → /privacy/
├── terms/index.html       # Terms of use  → /terms/
├── support/index.html     # Support page  → /support/
├── style.css              # Shared stylesheet
├── CNAME                  # Custom domain for GitHub Pages
├── .nojekyll              # Tell Pages to skip Jekyll processing
└── README.md              # This file
```

## One-time setup

Do these once. After that, editing the legal pages is just `git commit` + `git push`.

### 1. Enable GitHub Pages

1. Go to <https://github.com/seltsamonkel/fitplan-site/settings/pages>.
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
3. Set **Branch** to `main` and folder to `/ (root)`. Save.
4. The page will immediately show that your site is being built. Wait ~1 minute.

### 2. Add the DNS record at your domain registrar

The site lives at the subdomain `fitplan.asssk.me`. Add this record to the `asssk.me` zone:

| Type  | Name (host) | Value                    | TTL     |
| ----- | ----------- | ------------------------ | ------- |
| CNAME | `fitplan`   | `seltsamonkel.github.io.` | Auto / 3600 |

Notes:

- The **Name** field expects only the subdomain label (`fitplan`), not the full `fitplan.asssk.me`. Your registrar's UI will append the domain automatically.
- The **Value** is the GitHub Pages hostname for your user. The trailing dot is optional; most registrars normalize it.
- Do **not** create an A record for this subdomain; CNAME is correct for subdomains on GitHub Pages.
- DNS propagation is usually under 10 minutes. It can take up to an hour in the worst case.

### 3. Verify on GitHub

Once DNS has propagated:

1. Go back to <https://github.com/seltsamonkel/fitplan-site/settings/pages>.
2. The **Custom domain** field should already show `fitplan.asssk.me` (picked up from the `CNAME` file in this repo).
3. GitHub will run a DNS check. When it succeeds (green check), tick **Enforce HTTPS**. A Let's Encrypt certificate will be provisioned automatically within a few minutes.

### 4. Confirm the URLs resolve

Open each of the following in a browser and confirm they load over HTTPS:

- <https://fitplan.asssk.me/>
- <https://fitplan.asssk.me/privacy/>
- <https://fitplan.asssk.me/terms/>
- <https://fitplan.asssk.me/support/>

If any of them 404 or show a certificate warning, wait a few more minutes for the cert to issue, then hard-refresh.

### 5. Set up the support mailbox

The site uses `info@asssk.me` as the contact address. Make sure mail to that address actually reaches you. At most registrars, the simplest zero-cost option is **email forwarding**: create an alias `info@asssk.me` that forwards to your real inbox. No mail server required.

## Updating content

Edit the relevant `.html` file, commit, push. GitHub Pages redeploys automatically on push to the default branch, usually within 30 seconds.

Legal-page changes should always:

1. Update the **Effective date** at the top of the page.
2. Be committed with a descriptive message so the git history serves as a change log.

## Store submission

When filling out store submission forms, paste these URLs:

- **App Store Connect → App Information → Privacy Policy URL**: `https://fitplan.asssk.me/privacy/`
- **App Store Connect → App Information → Marketing URL (optional)**: `https://fitplan.asssk.me/`
- **Google Play Console → Store listing → Privacy Policy**: `https://fitplan.asssk.me/privacy/`
- **Google Play Console → Store listing → Website (optional)**: `https://fitplan.asssk.me/`
- **Google Play Console → Store listing → Email**: `info@asssk.me`

## License

Content in this repository (HTML, CSS, and legal text) is &copy; ASSSK LLC. The legal pages describe the terms under which FitPlan itself is offered.
