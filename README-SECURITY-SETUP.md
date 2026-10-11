# Conjunction AI Arena — Presenter Authentication Setup

This package adds Firebase Email/Password sign-in to the Presenter Dashboard and Challenge Settings. The quiz and certificate pages remain publicly reachable so participants can play and scan certificate QR codes. There is no public sign-up form; create presenter accounts yourself in Firebase Console.

## 1. Enable Email/Password authentication

1. Open https://console.firebase.google.com/ and select the Firebase project already hosting Conjunction AI Arena.
2. Go to **Authentication → Get started → Sign-in method**.
3. Enable **Email/Password** and save.
4. Open **Authentication → Users → Add user**.
5. Create the presenter/admin account with an email and strong password. Do not share this account with participants.

## 2. Register a Web App and copy its config

1. In Firebase Console, open **Project settings → General → Your apps**.
2. If there is no Web App, click **Add app → Web** and register it (e.g. `Conjunction AI Arena Web`).
3. Copy the Firebase web configuration values: `apiKey`, `authDomain`, `projectId`, and `appId`.
4. Open `public/index.html` and find `const firebaseConfig = { ... }` near the top of the scripts.
5. Replace the four `REPLACE_...` placeholder values with the matching values from your Web App config. Keep the quotation marks. Never put a service-account key or private credential in this file.

Example format (use your real values, not these placeholders):

```js
const firebaseConfig = {
  apiKey: "your-web-api-key",
  authDomain: "your-project-id.firebaseapp.com",
  projectId: "your-project-id",
  appId: "your-web-app-id"
};
```

## 3. Add authorized domains

In **Authentication → Settings → Authorized domains**, make sure the deployed Firebase Hosting domain (for example `your-project-id.web.app`) is listed. Add your custom domain too if you use one.

## 4. Deploy

From this folder, verify the right Firebase project is selected:

```powershell
firebase use
```

Then deploy:

```powershell
firebase deploy --only hosting
```

Refresh the website with **Ctrl+F5**. Clicking **Presenter Dashboard** or **Challenge Settings** should show a sign-in form. Sign in using the presenter account you created in Firebase Console. There is intentionally no public registration option.

## Important data and security notes

- Participant quiz play and certificate URLs remain public by design. Anyone with a certificate QR/link can view that certificate. Do not encode private data in certificates.
- Participant results are currently saved in `localStorage` on the presenter browser/device. They are not synced to Firestore and won't automatically appear on another device. Clearing browser data can remove them.
- This update protects the Presenter Dashboard/Settings through Firebase Authentication in the interface, but it does **not** move results to a server-side database. For stronger server-enforced access control and multi-device reporting, the next step is to save results in Firestore with restrictive Security Rules and allow reads only to authorized presenter accounts.
- Firebase web config is designed to be present in client apps; the security boundary must be Firebase Authentication and Security Rules, not secrecy of the web config.
- Use only the data needed for the school activity. Since participants may be children, obtain school/parent approval for the data collection and avoid collecting phone numbers or other unnecessary personal details.
