# Beautinix

Beauty clinic appointment app. This repository holds the first HTML prototype and the brand logos.

## App sections

- **Admin**: sign-in and three tabs. **Salon Owners** lists every salon whose owner has created an account (contact details, services, bookings, T&C date). **Guests** lists every guest account with their bookings. **Add Salon Details**: salon name, name of the person, WhatsApp number, email (required; the owner signs in and resets their password with it), state, city and PIN code. Saving stores the salon in the database, creates a unique code (for example `BX-7KQ2MP`) and opens WhatsApp with an invite to the owner containing the code, salon name and person's name. The admin can also delete a salon, which removes it, its code and its bookings.
- **Salon de Beauté**: on first visit the owner must agree to the [terms for salons](TERMS.md) and the platform fee of ₹200 per month; the acceptance is saved on their salon. Then the owner taps **Create account**, enters the code, checks the details the admin added and sets a password. After that they sign in with their email and password. Signed in, they add their services with a starting price (for example Facial, shown as ₹450 & onwards) or a price range when it depends on the guest (for example Facial ₹450–₹900, typed as 450-900), upload one large salon photo (guests see it as a thumbnail on the salon card and can tap it to enlarge; the owner can change or remove it anytime), set **Available**, **Busy** or **Not available**, see guest bookings as they come in (with **booking alerts** turned on, a new booking sounds a buzzer, vibrates the phone, shows a banner and a browser notification, and a second buzzer sounds 15 minutes before the guest is due; the Salon de Beauté page must be open), and use **Edit details** to change the salon name, person, WhatsApp, state, city and PIN (email stays fixed because it's the sign-in).
- **die Gäste**: anyone can see each salon's name and availability; location, WhatsApp, services and prices are masked (`*****`) until the guest creates an account (name, WhatsApp, email, password). Signed-in guests can book a service and time at salons marked **Available** (Busy and Not available salons can't be booked) and see their bookings.

WhatsApp numbers always start with a fixed +91 followed by exactly 10 digits. **Forgot password?** emails a reset link (Firebase sends it). Tabs are locked by role: the admin can open all three, a signed-in salon owner only Salon de Beauté, and a signed-in guest only die Gäste.

Live app: https://vishalsaxen.github.io/beautinix/ (GitHub Pages, branch `main`, `/ (root)`). Prices are in rupees (₹).

## Firebase

Sign-in uses Firebase Authentication (email and password) and data is stored in Cloud Firestore, project `beautinix`.

| Collection | What's in it | Who can read it |
| --- | --- | --- |
| `salons` | Full salon details, services, availability, owner | Signed-in users |
| `listings` | Salon name, availability and photo thumbnail | Everyone |
| `photos` | Each salon's large photo (resized in the browser, under 1 MB) | Everyone |
| `invites` | Sign-up codes | Anyone with the code; only the admin can list them |
| `guests` | Guest name, WhatsApp, email | The guest and the admin |
| `bookings` | Guest bookings | The guest, the salon owner and the admin |

`firestore.rules` holds the security rules. One-time setup in the [Firebase console](https://console.firebase.google.com/project/beautinix):

1. **Authentication → Get started → Sign-in method → Email/Password → Enable.**
2. **Authentication → Users → Add user** with the admin email below and a password of your choice.
3. **Firestore Database → Rules**: paste `firestore.rules` and **Publish**.

To test locally against the Firebase emulator: `firebase emulators:start --only auth,firestore`, serve the folder on `localhost` and open `http://localhost:<port>/?emulator`.

## Admin login

The admin login ID is **vishalsaxen@gmail.com**, with the password set in Firebase (not stored in this repository). The first time the admin signs in, the app emails a verification link to that Gmail inbox; after opening it, the admin taps **I've verified, continue**. Only a verified account with this email gets admin access, so nobody else can take the admin role by registering the email. **Forgot password?** sends a reset link to the same inbox.

To change the admin email, change `ADMIN_ID` in `index.html` and `isAdmin()` in `firestore.rules`, then publish the rules again.

## Logos

`assets/logo/` holds the Beautinix and Beautizo logos as SVG and transparent PNG.

## Not done yet

- **WhatsApp:** the app opens WhatsApp with the invite filled in, and the admin presses Send. Sending automatically needs the WhatsApp Business API.
- **Deleted owners:** deleting a salon removes its data, but the owner's sign-in stays in Firebase Authentication. Remove it there (Authentication → Users) if needed.
- **Alerts when the app is closed:** booking alerts only reach a salon whose Salon de Beauté page is open. Alerts to a closed app need Firebase Cloud Messaging plus a Cloud Function (Blaze plan), or WhatsApp messages via the Business API.
- **Double bookings:** two guests can book the same time slot; the salon sees both.
