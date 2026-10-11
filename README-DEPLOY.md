# Conjunction AI Arena — Firebase Hosting

This package includes the quiz application and a redesigned academic-style English Exhibition certificate page. The certificate is personalized from the quiz QR link and does not show a class field. Signature areas are blank for authorized school signatories.

## Deploy/update an existing Firebase Hosting site

1. Extract this ZIP.
2. Open PowerShell in the `conjunction-ai-arena-hosting` folder.
3. Confirm the correct Firebase project is selected:

   ```powershell
   firebase use
   ```

4. Deploy the site:

   ```powershell
   firebase deploy --only hosting
   ```

5. Open the deployed site and hard-refresh with `Ctrl + F5`.
6. Run a test quiz, finish the three questions, and scan the QR with a phone that has internet access.
7. On the phone, use **Print / Save as PDF** to save the certificate.

## Notes
- QR creation currently loads QRCode.js from a CDN, so the laptop needs internet while displaying the QR code.
- The phone needs internet to open the hosted certificate URL.
- Quiz results are stored in that browser's local storage, not uploaded to Firebase.
- The CEO and Correspondent areas are signature lines; obtain authorized signatures/approval before issuing certificates as official school documents.

### View a participant's QR code later
Open Presenter Dashboard / View Results. Each saved participant row now has a **View QR** button. Click it to display that participant's certificate QR again. Results are stored in the current browser's localStorage, so use the same browser/device that recorded the participant. Clearing browser data or using another device will not retain those local results.
