# Security Patrol QR Scanner

Public QR scanner frontend used by the Security Patrol System.

Production scanner:

https://securitypatrolop.github.io/security-patrol-scanner/

---

## A Little Background

I’m not a professional software developer.

Back in university, I learned some C and C++. This was also the era when, during exams, we sometimes had to write code using an actual pen on actual paper — no compiler, no syntax highlighting, no Stack Overflow, just confidence and whatever you could remember.

So technically, I had some programming background.

Then many years passed.

With the help of AI, I somehow ended up building this.

What started as a simple idea to make security patrol records harder to fake gradually became a full patrol verification system with:

- QR checkpoint scanning
- strict checkpoint sequence
- GPS location verification
- patrol timing
- audit logs
- Supervisor monitoring
- signed completion records
- verification QR codes
- permanent checkpoint links

The goal was never to build a giant commercial security platform.

The goal was much simpler:

> Prove that a patrol actually reached the required checkpoint, in the correct order, at the correct location, and leave behind a record that can be independently verified.

AI has helped heavily with the coding, debugging, architecture, and occasionally explaining JavaScript to someone whose last serious programming memories involved C, C++, and handwritten exam code.

I still make the final decisions, test the system in the real environment, break things occasionally, fix them, and then try very hard not to break the parts that are already working.

This repository is one part of that system.

---

## About This Repository

This repository hosts the mobile QR scanner used by the Security Patrol System.

The scanner is opened by the Guard interface whenever the next checkpoint needs to be scanned.

Its job is deliberately limited:

1. Open the phone camera.
2. Read the checkpoint QR code.
3. Return the scanned checkpoint information to the Guard interface.

The scanner itself does **not** decide whether a checkpoint is valid.

Final acceptance is handled by the Security Patrol backend.

That backend checks things such as:

- expected checkpoint
- checkpoint sequence
- active patrol state
- GPS location
- patrol timing
- duplicate scans
- incorrect checkpoint scans
- final patrol completion

In short:

> The scanner reads the QR. The backend decides whether it counts.

---

## Production URL

The live scanner is available at:

https://securitypatrolop.github.io/security-patrol-scanner/

This URL is used by the Guard interface during patrol operations.

---

## Production File

The production GitHub Pages file must be:

`/index.html`

Development or test versions may use versioned filenames.

Example:

`index_v2_0_0_alpha8.html`

However, once a version is approved for production, its contents should be copied into:

`index.html`

The production website always serves the root `index.html`.

---

## Current Scanner Responsibilities

The scanner is responsible for the frontend QR capture process only.

Current functionality includes:

- rear camera preference
- QR detection
- expected checkpoint awareness
- manual camera switching where supported
- torch control where supported
- zoom control where supported
- vibration feedback
- voice feedback
- Wake Lock support where available
- mobile-first layout
- returning the scan result to the active Guard session
- protection against stale or accidental navigation where possible

Unsupported device capabilities should not prevent basic QR scanning.

For example, if a phone does not support torch or zoom controls, QR scanning should still continue normally.

---

## What the Scanner Does Not Do

The scanner is **not** the authority for patrol verification.

It does not independently decide:

- whether the QR is the expected checkpoint
- whether the checkpoint is in the correct sequence
- whether the guard is physically near the checkpoint
- whether GPS accuracy is acceptable
- whether the checkpoint is on time or late
- whether a patrol has started or finished

Those decisions belong to the backend.

This separation is intentional.

The scanner captures evidence.

The backend evaluates it.

---

## Typical Scan Flow

A normal patrol scan works roughly like this:

1. The Guard interface knows which checkpoint is expected next.
2. The scanner opens with that expected checkpoint information.
3. The guard scans the physical QR code.
4. The scanner reads the checkpoint number.
5. The result is returned to the Guard interface.
6. The Guard requests location verification.
7. The backend checks sequence, GPS, timing and patrol state.
8. The backend accepts or rejects the checkpoint.
9. The Guard interface shows the result.

A successful QR read does not automatically mean a successful patrol checkpoint.

---

## Deployment

When updating the production scanner:

1. Test the new scanner version on a real mobile phone.
2. Confirm the rear camera opens correctly.
3. Confirm QR detection works.
4. Confirm the expected checkpoint is passed correctly.
5. Confirm the scan returns to the correct Guard session.
6. Test camera switching if supported.
7. Test torch if supported.
8. Test zoom if supported.
9. Confirm unsupported features do not block scanning.
10. Replace the repository root `index.html`.
11. Commit the change.
12. Wait for GitHub Pages to publish.
13. Test the production URL again from a real phone.

Do not consider a scanner update complete just because the HTML loads successfully on desktop.

The scanner is a field component.

Phone testing matters.

---

## Important

This repository must remain **PUBLIC**.

GitHub Pages serves the production scanner directly from this repository.

If the repository is changed to Private, the scanner may stop being publicly reachable during patrol operations.

Yes, this was learned through practical testing.

---

## Security

This repository contains public frontend code only.

Do not store sensitive information here.

Do not commit:

- passwords
- authentication secrets
- signing keys
- Supervisor credentials
- private patrol records
- private Google Sheet IDs
- API secrets
- session tokens

The authoritative patrol data and security logic remain on the backend.

---

## Reliability Principles

The scanner should remain simple and predictable.

A few rules matter more than adding extra features:

- scanning must work on common mobile browsers
- unsupported camera features must fail gracefully
- the guard should always know what checkpoint is expected
- successful scans should return cleanly to the Guard interface
- stale pages should not accidentally restart old patrol actions
- camera controls should not interfere with QR detection
- scanner changes should not alter backend patrol rules

The scanner should do one job well:

> Capture the checkpoint QR reliably and hand the result back to the patrol system.

---

## Related Components

The complete Security Patrol System also includes:

- Guard interface
- Google Apps Script patrol backend
- GPS verification
- checkpoint sequence enforcement
- patrol timing
- Patrol Log
- Supervisor Portal
- signed patrol summaries
- public authenticity verification
- permanent checkpoint QR redirect

This repository contains only the QR scanner component.

---

## Project Philosophy

This system is intentionally not trying to become a giant workforce-management platform.

The focus is patrol verification.

That means answering a few important questions clearly:

- Was the required checkpoint reached?
- Was it reached in the correct order?
- Was the guard actually at the required location?
- Was the result recorded by the backend?
- Can the completed patrol record be verified afterward?

If a feature does not improve patrol proof, reliability, usability, or auditability, it probably does not belong here.

---

## Final Note

This project started with a fairly simple problem and slowly became much more capable than originally planned.

It has also confirmed one important lesson:

Writing C on paper during university exams was somehow easier than debugging mobile browser camera behavior.
