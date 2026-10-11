# Conjunction AI Arena — English Exhibition Certificate

This version uses the supplied certificate artwork as the exact visual template and overlays the participant name from the quiz result. The Class field is not shown. The existing result-screen QR and Presenter Dashboard → View Results → View QR features remain available.

## Deploy to the existing Firebase Hosting project
1. Extract this ZIP.
2. Open PowerShell in `conjunction-ai-arena-hosting`.
3. Run `firebase use` and confirm the correct project.
4. Run `firebase deploy --only hosting`.
5. Open the hosted site and hard refresh with Ctrl+F5.

## QR behaviour
The app generates a QR code on the results screen and can reopen it from saved results. It encodes the public hosted certificate URL plus the participant's quiz data. The current QRCode.js library is loaded from a CDN, so internet is required when generating the QR code. The phone needs internet to open the hosted certificate.

## Certificate artwork
`public/certificate-template.png` is the certificate background. The app overlays the participant's name dynamically. The existing artwork includes the English Exhibition wording, year, and CEO/Correspondent signature areas.

Note: participant results remain in browser localStorage on the laptop unless you separately configure server-side storage.
