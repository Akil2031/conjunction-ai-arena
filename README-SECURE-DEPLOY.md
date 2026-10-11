# Conjunction AI Arena — secure deployment update

## Included
- `public/index.html`: updated standalone app with Firebase Email/Password presenter sign-in, Firestore result writes, admin-only results listing, and per-certificate QR links.
- `firestore.rules`: restricts result collection listing to `bhegan@gmail.com`; permits direct reads only for records marked `publicCertificate: true`; blocks public updates/deletes.
- `firebase.json`: Hosting + Firestore rules configuration.
- `.firebaserc.example`: project alias example. Do not overwrite an existing `.firebaserc` without checking it first.

## Before deploying
1. Back up the current Hosting `public` folder and `firebase.json`.
2. Copy the updated `public/index.html` into your existing project's `public` folder.
3. Keep your existing `certificate-template.png` in that same `public` folder. The HTML references this file; it was not included in the uploaded HTML attachment.
4. Copy `firestore.rules` into your project root. If your existing `firebase.json` contains other settings, merge the Firestore rules entry rather than replacing it blindly.
5. Check the project before deployment:
   ```powershell
   firebase use
   ```
   It must show `conjunction-ai-arena`.
6. Deploy rules first:
   ```powershell
   firebase deploy --only firestore:rules
   ```
7. Deploy the site:
   ```powershell
   firebase deploy --only hosting
   ```

## Authentication check
Firebase Console → Authentication → Sign-in method: enable Email/Password.
Authentication → Users: confirm `bhegan@gmail.com` exists and can sign in.

## Important limitations / production hardening
- The client restricts the presenter UI to `bhegan@gmail.com`, and Firestore rules independently restrict bulk reads to that email. If you later change the presenter email, update both the HTML and Firestore rules.
- Public certificate links are bearer links: anyone who has a particular QR/link can view that certificate's public fields. Do not put phone numbers, addresses, or other sensitive data in these documents.
- Public submissions are schema-validated but are not cryptographically verified. A determined visitor could submit a fabricated score using browser tools. For a high-stakes competition, use a trusted server/Cloud Function to calculate and write scores, and add App Check / abuse controls.
- The participant access code has not been implemented as a secure gate. A code checked only in browser JavaScript can be bypassed. Use a server-validated code or callable Cloud Function if you need to enforce one.
- This uploaded source contains a small sample question bank (8 questions per age level), not 28 per band. This update does not expand the bank.
- Existing old QR links containing `?certificate=...` remain supported, but those legacy links encode the certificate data in the URL and can be altered. Newly generated QR codes use Firestore document IDs.


## Direct certificate generation (added)
- After a quiz is saved, the result screen includes **Generate Certificate Now** and **Print / Save as PDF**.
- In Presenter Dashboard, each participant row has **Generate** and **View QR** actions.
- `public/certificate-template.png` is the blank English Exhibition certificate artwork used as the background; keep it in the `public` folder during deployment.
- The certificate opens in a new tab. Use **Print / Save as PDF** on that certificate page. Allow pop-ups for your hosting domain if the browser blocks it.
