# LinkHive Auth Package (Firebase)

This folder adds **login + signup + profile** to a static site using **Firebase Authentication** and **Firestore** (works on Vercel/GitHub Pages).

## Files
- `auth.html` — Sign up / Sign in page
- `profile.html` — Profile editor (requires login)
- `auth.js` — Auth logic (email/password + Google) and user doc creation
- `profile.js` — Loads/saves the user's profile in Firestore
- `auth-style.css` — Minimal shared styling

## Setup (10 minutes)
1. Go to https://console.firebase.google.com → **Add project** (e.g., `linkhive`).
2. **Authentication → Sign-in method**: Enable **Email/Password** and (optional) **Google**.
3. **Project settings → Your apps → Web app**: copy your **firebaseConfig**.
4. **Firestore Database**: Create a database (production is fine). Set rules:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```

5. Open `/auth.js` and `/profile.js` and **replace** the `firebaseConfig` object with your real values.
6. Commit these files to your repo. On Vercel, deploy as normal.
7. Visit `/auth.html` to sign up/sign in. You’ll be redirected to `/profile.html`.

## Notes
- This is client-only and secure thanks to Firebase rules.
- To add an **Upload Avatar** feature, enable **Firebase Storage** and I can extend `profile.js`.
