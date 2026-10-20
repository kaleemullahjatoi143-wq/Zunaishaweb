# Zunaisha Home Kitchen Larkana — Complete Food Delivery Platform

**Location:** Larkana City, Sindh, Pakistan  
**Contact / WhatsApp:** 03133744437  
**Free Delivery:** Free delivery across Larkana City  
**Timezone:** Asia/Karachi (PKT)  
**Currency:** Pakistani Rupee (PKR / Rs.)

---

## 1. Overview & Architecture

**Zunaisha Home Kitchen Larkana** is a full-featured, mobile-responsive food delivery web application built with HTML5, CSS3, Vanilla JavaScript, Firebase Authentication (Email/Password), and Firebase Realtime Database.

The system features 5 specialized portals:
1. **Storefront & Homepage (`index.html`)** — Customer browsing, category filters, cart drawer, Larkana free delivery messaging, and WhatsApp direct ordering.
2. **Customer Portal (`customer.html`)** — Checkout form, live order tracking with visual progress timeline, order history, and address profile.
3. **Kitchen Order Display (`Restaurant.html`)** — Real-time kitchen ticket display, Web Audio chime alerts on new orders, prep-time tracking, printable KOT slips, and menu item stock toggling.
4. **Delivery Rider Portal (`Delivery.html`)** — Assigned deliveries, turn-by-turn Google Maps links, direct phone call / WhatsApp buttons, Cash on Delivery collection, and shift status.
5. **Admin Dashboard (`admin.html`)** — Analytics, live order management, rider dispatch, menu CRUD (create, read, update, delete dishes), user role manager, and restaurant settings.

---

## 2. Quick Demo Credentials (Out-of-the-Box)

The application comes pre-configured with reactive real-time database synchronisation that works both locally and seamlessly with Google Firebase.

| Role | Email | Password | Access / Panel |
|------|-------|----------|----------------|
| **Admin** | `admin@zunaisha.com` | `123456` | `admin.html` (Full management & analytics) |
| **Kitchen Chef** | `kitchen@zunaisha.com` | `123456` | `Restaurant.html` (Live KOD & KOT printing) |
| **Delivery Rider 1** | `rider1@zunaisha.com` | `123456` | `Delivery.html` (Asadullah Brohi, Honda 70) |
| **Delivery Rider 2** | `rider2@zunaisha.com` | `123456` | `Delivery.html` (Tariq Ali Abbasi, Yamaha 100) |
| **Customer** | Any email (e.g. `customer@example.com`) | Any password | `customer.html` / `index.html` |

*Note: You can switch between panels at any time using the top navigation bar.*

---

## 3. Connecting to Google Firebase Realtime Database

### Step 1: Create a Firebase Project
1. Go to the [Firebase Console](https://console.firebase.google.com/).
2. Click **Add project** and name it `zunaisha-kitchen-larkana` (or your chosen project name).
3. Disable or enable Google Analytics (optional) and click **Create Project**.

### Step 2: Enable Firebase Authentication
1. In the Firebase console left menu, click **Build > Authentication**.
2. Click **Get Started**.
3. Under the **Sign-in method** tab, choose **Email/Password**.
4. Enable the first toggle (**Email/Password**) and click **Save**.

### Step 3: Create Firebase Realtime Database
1. In the left menu, click **Build > Realtime Database**.
2. Click **Create Database**.
3. Select database location (e.g. `Singapore (asia-southeast1)` or `United States (us-central1)`).
4. Choose **Start in locked mode** or **test mode** (you will paste the security rules in Step 5).
5. Copy your Realtime Database URL (e.g. `https://zunaisha-kitchen-larkana-default-rtdb.firebaseio.com/`).

### Step 4: Register Web App & Get Config
1. In Firebase Project Overview, click the **Web icon (`</>`)** to register a web app.
2. Enter App nickname: `Zunaisha Web`.
3. Copy the `firebaseConfig` object values:
   - `apiKey`
   - `authDomain`
   - `databaseURL`
   - `projectId`
   - `storageBucket`
   - `messagingSenderId`
   - `appId`

### Step 5: Apply Database Security Rules
1. In Firebase Console, navigate to **Realtime Database > Rules**.
2. Replace all contents with the contents of `database.rules.json` included in this repository.
3. Click **Publish**.

### Step 6: Insert Your Config
Open `js/firebase-config.js` — your project credentials are now pre-configured:
```javascript
const DEFAULT_FIREBASE_CONFIG = {
  apiKey: "AIzaSyBaJmvzGK7_4XYhpXqXjuQaOGLu9j31yV8",
  authDomain: "zunaishafood.firebaseapp.com",
  databaseURL: "https://zunaishafood-default-rtdb.firebaseio.com",
  projectId: "zunaishafood",
  storageBucket: "zunaishafood.appspot.com",
  messagingSenderId: "109583985442",
  appId: "1:109583985442:web:zunaishafood"
};
```
*Note: In Firebase Console > Realtime Database, ensure your database is created and that you publish the rules from `database.rules.json`.*

---

## 4. How to Deploy Online

### Option A: Deploying on Netlify (Recommended for Quickest Setup)
1. Go to [Netlify](https://www.netlify.com/).
2. Drag and drop the folder containing `index.html`, `customer.html`, `Restaurant.html`, `Delivery.html`, `admin.html`, `css/`, and `js/` into Netlify Drop.
3. Your food delivery site is instantly live with a free custom SSL URL!

### Option B: Deploying to Firebase Hosting
1. Install Firebase CLI: `npm install -g firebase-tools`
2. Run `firebase login`
3. Run `firebase init hosting`
   - Choose your Firebase project.
   - Specify public directory: `.` (current directory).
   - Configure as single-page app: `No`.
4. Run `firebase deploy --only hosting`

---

## 5. Testing Guide (Testing All 5 Panels)

1. **Placing an Order (Customer)**:
   - Open `index.html`. Browse dishes (e.g. Special Larkana Sindhi Biryani, Zinger Burger).
   - Click **+ Add to Cart**. Open the cart drawer, see Larkana free delivery calculation.
   - Click **Proceed to Checkout**. Enter name, phone, and Larkana address.
   - Click **Confirm & Place Order**.
2. **Accepting & Cooking (Kitchen)**:
   - Open `Restaurant.html`. Notice the audio chime alert and new incoming order card.
   - Click **Accept & Cook**. Notice the status updates to `preparing`.
   - Click **Print KOT Slip** to preview the kitchen slip.
   - Click **Mark Ready for Pickup**.
3. **Dispatching & Delivering (Rider)**:
   - Open `Delivery.html`. Notice the order is now ready for pickup.
   - Click **Acknowledge & Pick Up**. Status becomes `out_for_delivery`.
   - Test the **Google Maps** and **WhatsApp** customer action buttons.
   - Click **Mark Delivered & Cash Collected**.
4. **Monitoring & Analytics (Admin)**:
   - Open `admin.html`. Notice Total Revenue counter and Completed Deliveries increment.
   - Test adding a new dish in **Menu & Dishes CRUD**.
   - Test generating a printable customer receipt.

---

## 6. Troubleshooting & Diagnostics

- **Orders not appearing in another tab**:
  Ensure both tabs are open in the same browser session or connected to the same Firebase Realtime Database URL.
- **Audio alert not playing in Kitchen**:
  Modern browsers require at least one user interaction (such as clicking anywhere or toggling "Sound: ON") before playing web audio.
- **Permission Denied in Firebase**:
  Verify you have published the rules from `database.rules.json` and that your user UID is registered with `role: "admin"` in the `users` collection.
- **WhatsApp link opening web instead of app on desktop**:
  On mobile devices (Android / iOS), `wa.me/` links open the WhatsApp application directly. On laptops, it opens WhatsApp Web.
