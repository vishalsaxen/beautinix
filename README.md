# Beautinix

Beauty clinic appointment app. This repository holds the first HTML prototype and the brand logos.

## App sections

- **Admin**: sign-in, overview, add salon (salon name, person, WhatsApp number, optional email and description), appointments, salons, staff, services and guests. Saving a new salon sends it to Salon de Beauté.
- **Salon de Beauté**: each salon's contact details and today's timeline for each stylist, with guest check-in
- **die Gäste**: online booking (treatment → salon → date and time → confirm)

The Admin tab is locked for salon staff and guests until the admin signs in.

Open `app/index.html` in a browser to try it. Everything in it is sample data. Prices are in rupees (₹).

## Admin login (prototype)

| Login ID | Password |
| --- | --- |
| `admin@beautinix.de` | `Beautinix@2026` |

This starting login is hard-coded in `app/index.html`. "Forgot password?" lets the admin set a new password with a 6-digit code. In the prototype the code is shown on screen and the new password is saved only in that browser.

> This repository is public, so anyone can read this password. Change it before the app holds real data, and move the password check to a server when the backend is built.

## Logos

`assets/logo/` holds the Beautinix and Beautizo logos as SVG and transparent PNG.
