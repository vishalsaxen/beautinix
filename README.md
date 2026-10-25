# Beautinix

Beauty clinic appointment app. This repository holds the first HTML prototype and the brand logos.

## App sections

- **Admin**: sign-in and one tab, **Add Salon Details**: salon name, name of the person, WhatsApp number, email (required, used for password OTPs), state, city and PIN code. Saving creates a unique code (for example `BX-7KQ2MP`) and opens WhatsApp with an invite to the owner containing the code, salon name and person's name.
- **Salon de Beauté**: the owner taps **Create account**, enters the code, checks the details the admin added and sets a password. After that they sign in with their email and password, and can reset it with **Forgot password?** (6-digit code to their email). Once signed in they see their salon's details and today's timeline.
- **die Gäste**: online booking (treatment → salon → date and time → confirm)

The Admin tab is locked for salon staff and guests until the admin signs in.

Open `index.html` in a browser to try it, or visit https://vishalsaxen.github.io/beautinix/ once GitHub Pages is on (Settings → Pages → Deploy from a branch → `main`, `/ (root)`). Everything in it is sample data. Prices are in rupees (₹).

## Admin login (prototype)

| Login ID | Password |
| --- | --- |
| `admin@beautinix.de` | `Beautinix@2026` |

This starting login is hard-coded in `index.html`. "Forgot password?" lets the admin set a new password with a 6-digit code. In the prototype the code is shown on screen and the new password is saved only in that browser.

> This repository is public, so anyone can read this password. Change it before the app holds real data, and move the password check to a server when the backend is built.

## Logos

`assets/logo/` holds the Beautinix and Beautizo logos as SVG and transparent PNG.

## What the prototype can't do yet

These need a backend before real salons use the app:

- **WhatsApp:** the app opens WhatsApp with the invite filled in, and the admin presses Send. Sending automatically needs the WhatsApp Business API.
- **Email OTPs:** reset codes are shown on screen instead of being emailed.
- **Shared data:** salons, codes and passwords are saved in the browser where they were entered. For an owner to create an account on their own phone, the salons have to live in a database.

