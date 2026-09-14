## About This Repository

This repository hosts the QR scanner used by the Security Patrol System.

Production scanner:

https://securitypatrolop.github.io/security-patrol-scanner/

The scanner is opened by the Guard interface whenever the next checkpoint needs to be scanned.

Its job is deliberately limited:

1. Open the phone camera.
2. Read the checkpoint QR code.
3. Return the scanned checkpoint information to the Guard interface.

The scanner itself does **not** decide whether a checkpoint is valid.

Final acceptance is handled by the Security Patrol backend, which checks things such as:

- expected checkpoint
- patrol sequence
- GPS location
- patrol state
- timing
- duplicate or incorrect scans

In other words:

> The scanner reads the QR. The backend decides whether it counts.

---

## Production File

The live GitHub Pages scanner must use:

`/index.html`

Development versions may have versioned filenames, but once a version is approved, its contents are copied into the production `index.html`.

---

## Current Scanner Features

The scanner is designed primarily for mobile patrol use.

Current functionality includes:

- rear camera preference
- QR detection
- manual camera switching where supported
- torch control where supported
- zoom control where supported
- vibration feedback
- voice feedback
- Wake Lock support where available
- expected-checkpoint awareness
- return to the active Guard session after scanning
- protection against accidental stale navigation

Unsupported phone features should not prevent basic QR scanning.

---

## Deployment

When updating the scanner:

1. Test the new version on a phone.
2. Confirm QR detection works.
3. Confirm the correct checkpoint is returned to Guard.
4. Confirm camera, torch and navigation behaviour.
5. Replace the repository root `index.html`.
6. Commit the change.
7. Wait for GitHub Pages to publish.
8. Test the production URL again.

Suggested commit messages should briefly describe the actual change.

---

## Important

This repository must remain **PUBLIC**.

GitHub Pages serves the production scanner directly from this repository.

Making the repository private can make the scanner unavailable during a patrol.

Yes, I learned this one the practical way.

---

## Security

This repository contains only public frontend code.

Do not store:

- passwords
- Google Sheet IDs that should remain private
- signing secrets
- API credentials
- Supervisor credentials
- private patrol records

The authoritative patrol data and verification logic remain on the backend.

---

## Related Components

The complete system also includes:

- Guard interface
- Google Apps Script patrol backend
- Supervisor Portal
- permanent checkpoint QR redirect
- signed patrol summaries
- public authenticity verification

This repository is only the scanner component.
