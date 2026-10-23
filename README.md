# Bridgewater Site Visibility Calendar

A shared calendar for Events, Contractors, and PTO / OOO. It works on a Smart TV, laptops, tablets, and phones.

- **Hosting:** Netlify (free plan)
- **Shared database:** Netlify Blobs (built in, free, nothing else to sign up for)
- **Passkey:** checked on the server. It is never in the browser code.
- **Stays signed in:** a secure cookie keeps the device signed in for 180 days and renews on every visit, so the TV won't keep asking for the passkey.

## Files
```
public/            the website (index.html, styles.css, app.js)
netlify/functions/ login, session, and entries API
netlify/lib/       passkey and session helper
netlify.toml       Netlify settings
package.json
```

## Deploy (one-time, about 10 minutes)

> Note: Netlify's drag-and-drop "Drop" does NOT run the server functions, so the passkey and shared data wouldn't work. Use GitHub as shown below.

1. **Create a GitHub repo** (it can be private). Upload all of these files, keeping the folders exactly as they are.
2. Go to **app.netlify.com**, then **Add new project**, then **Import an existing project**, then **GitHub**, and pick the repo.
   - The build settings are read from `netlify.toml`. Leave the build command blank and click **Deploy**.
3. In Netlify, go to **Project configuration**, then **Environment variables**, and add:
   | Key | Value |
   |---|---|
   | `SITE_PASSKEY` | the passkey your team will type |
   | `SESSION_SECRET` | a long random string of 32+ characters (just mash the keyboard) |
4. Go to **Deploys**, then **Trigger deploy**, then **Deploy site**, so the variables take effect.
5. Open the site URL on the TV, enter the passkey once, and you're done.

Optional: change the site name under **Domain management** (for example `bridgewater-ptc-calendar.netlify.app`).

## Changing things later
- **Change the passkey:** update `SITE_PASSKEY` and redeploy.
- **Sign every device out** (for example after someone leaves): change `SESSION_SECRET` and redeploy.
- **Update the app:** edit the files in GitHub. Netlify redeploys automatically and the data is kept.

## Notes
- Data refreshes every 60 seconds and whenever the tab comes back into view. Refreshes pause while a form is open so nobody loses what they're typing.
- Events and Contractors support multi-day ranges (start and end date) the same way PTO does.
- PTO does not store a reason.
- Everyone with the passkey has equal edit rights. There are no individual accounts in this version.
