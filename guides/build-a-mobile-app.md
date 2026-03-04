# Make a Mobile App

> **Time:** ~1 hour | **Experience needed:** Some patience (this is the longest guide) | **Setup required:** [Mac Setup](00-mac-setup.md), [Cursor Setup](01-cursor-and-ai.md), and [Accounts Setup](02-accounts-and-services.md)

Get an app running on your phone — iOS, Android, or both. Two paths: **React Native** lets you build for both platforms at once, or **SwiftUI** gives you the most native-feeling iPhone experience.

> **First time building anything?** Start with [Prototype an Idea](build-a-prototype.md) or [Create a Personal Website](build-a-personal-website.md) to get comfortable with the workflow, then come back here.

---

## Choose Your Path


| Path | Approach                | Best For                                        | Languages  | Platforms                   |
| ---- | ----------------------- | ----------------------------------------------- | ---------- | --------------------------- |
| **A** | **React Native + Expo** | Teams with web experience, cross-platform needs | TypeScript | iOS + Android               |
| **B** | **SwiftUI**             | iOS-first apps, best native experience          | Swift      | iOS only (+ macOS, watchOS) |


---

## Path A: React Native + Expo

### What You'll End Up With

- A cross-platform mobile app (iOS + Android)
- Convex backend with real-time sync
- Clerk authentication (Google sign-in)
- Runs in the iOS Simulator and on your physical device

### Quick Start: One Prompt (Path A)

**This is all you need for Path A.** Create your Expo project (step A2), then paste this prompt into Cursor Agent mode. The AI sets up navigation, auth, backend, and all your screens. You just review, accept, add your API keys, and run it.

The numbered steps below break down the same process if you want to learn how each part works.

> "Set up this Expo project with React Native, Convex for the backend, and Clerk for authentication.
>
> Set up:
> - Expo Router with a tab-based layout in the app/ directory
> - Root layout (app/_layout.tsx) with ClerkProvider using expo-secure-store for token cache, wrapping ConvexProviderWithClerk
> - convex/schema.ts with tables for [describe your data — e.g., items with title, description, status, userId]
> - convex/auth.config.ts for Clerk JWT validation using `process.env.CLERK_ISSUER_URL`
> - Convex query and mutation functions with auth checks via `ctx.auth.getUserIdentity()`
> - A sign-in screen using Clerk's Google OAuth with expo-auth-session and expo-web-browser
>
> Build these screens:
> 1. Home tab — list of [items] with pull-to-refresh
> 2. Create screen — form to add new items
> 3. Detail screen — tapping an item shows full details with edit/delete
> 4. Profile tab — user info from Clerk with sign-out button
>
> Environment variables: `EXPO_PUBLIC_CONVEX_URL`, `EXPO_PUBLIC_CLERK_PUBLISHABLE_KEY`
>
> Use React Native StyleSheet for styling, clean modern design, safe area handling."

Replace `[describe your data]` and `[items]` with your actual data model.

> **Power user tip:** Install the [AI Dev Stack skill](https://github.com/janeyou/ai-dev-stack-cursor-skill) for ongoing AI context beyond the initial scaffold. It teaches Cursor your preferred patterns across all projects.

### A1: Install Expo Tools (~10 min)

You need a few extra tools beyond the base Mac setup:

```bash
# Install Watchman (file watcher, needed by React Native)
brew install watchman
```

#### iOS: Install Xcode

1. Open the **App Store** on your Mac
2. Search for **Xcode** and install it (it's large — ~12 GB, takes 15-30 min)
3. Open Xcode once, accept the license agreement
4. Install iOS Simulator:

```bash
xcode-select --install  # if not already done
```

5. Open Xcode → **Settings > Platforms** → Make sure **iOS** is downloaded

> **No Xcode?** You can still develop using **Expo Go** on your physical iPhone — skip the Xcode install and see the "Run on your phone" section below.

#### Android: Install Android Studio

1. Download [Android Studio](https://developer.android.com/studio) and install it
2. Open Android Studio → **More Actions > SDK Manager**
3. Under **SDK Platforms**, check **Android 15 (VanillaIceCream)** (or the latest) and click **Apply**
4. Under **SDK Tools**, make sure **Android SDK Build-Tools**, **Android Emulator**, and **Android SDK Platform-Tools** are checked
5. Set up an emulator: **More Actions > Virtual Device Manager > Create Device**
   - Pick a device (e.g., **Pixel 8**), select the latest system image, and finish

Add the Android SDK to your shell so Expo can find it:

```bash
echo 'export ANDROID_HOME=$HOME/Library/Android/sdk' >> ~/.zshrc
echo 'export PATH=$PATH:$ANDROID_HOME/emulator:$ANDROID_HOME/platform-tools' >> ~/.zshrc
source ~/.zshrc
```

> **No Android Studio?** You can still develop using **Expo Go** on your physical Android phone — skip the Android Studio install and see the "Run on your phone" section below.

### A2: Create the Project (~5 min)

```bash
cd ~/Dev
npx create-expo-app@latest my-mobile-app
cd my-mobile-app
```

Install backend and auth dependencies:

```bash
npx expo install convex @clerk/clerk-expo expo-web-browser expo-auth-session expo-secure-store
```

Open in Cursor:

```bash
cursor .
```

### A3: Set Up with AI (~10 min)

Open Agent mode (Cmd + L, toggle Agent) and say:

> "Set up this Expo project with Convex for the backend and Clerk for authentication. Create a convex/ folder with schema.ts and auth.config.ts for Clerk JWT validation. Wire up ClerkProvider with Expo SecureStore for token cache and ConvexProviderWithClerk in the app root layout. Use Expo Router for navigation with a tab-based layout. Create a sign-in screen that uses Clerk's Google OAuth with expo-auth-session and expo-web-browser."

### A4: Configure Environment (~3 min)

Create `.env.local`:

```bash
echo 'EXPO_PUBLIC_CONVEX_URL=https://your-slug-123.convex.cloud' > .env.local
echo 'EXPO_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_...' >> .env.local
```

> **Note:** Expo uses `EXPO_PUBLIC_` prefix (not `VITE_`).

Initialize Convex:

```bash
npx convex dev
```

### A5: Run the App (~5 min)

#### iOS

**In the iOS Simulator (iPhone 16 Pro):**

```bash
npx expo run:ios --device "iPhone 16 Pro"
```

**On your physical iPhone (no Xcode needed):**

1. Install **Expo Go** from the App Store on your phone
2. Run `npx expo start` in your terminal
3. Scan the QR code with your iPhone camera

#### Android

**In the Android Emulator:**

```bash
npx expo run:android
```

This will boot your emulator automatically and install the app. If you have multiple emulators, you'll be prompted to choose one.

**On your physical Android phone (no Android Studio needed):**

1. Install **Expo Go** from the Google Play Store on your phone
2. Run `npx expo start` in your terminal
3. Scan the QR code with the Expo Go app (or your phone's camera)

### A6: Build the UI (~15 min)

Tell the AI what screens you need:

> "Build the main app screens:
>
> 1. Home tab — shows a list of [your primary data] with pull-to-refresh
> 2. Create screen — a form to add new [items] with [fields]
> 3. Detail screen — tapping an item shows full details with edit/delete
> 4. Profile tab — shows user info from Clerk with sign-out button
>
> Use React Native StyleSheet, clean modern design, safe area handling."

### A7: Deploy (~5 min)

First, install the EAS CLI and configure your project:

```bash
# Install EAS CLI
npm install -g eas-cli

# Log in to Expo
eas login

# Configure the build
eas build:configure
```

#### iOS — TestFlight

```bash
eas build --platform ios
```

Follow the prompts to set up an Apple Developer account ($99/year, required for App Store). Once the build completes, it's automatically uploaded to App Store Connect where you can distribute via TestFlight.

#### Android — Google Play

```bash
eas build --platform android
```

This produces an `.aab` file (Android App Bundle). To distribute:

1. Create a [Google Play Developer account](https://play.google.com/console) ($25 one-time fee)
2. Create a new app in the Play Console
3. Upload the `.aab` file under **Production > Create new release** (or use internal testing for beta)

> **Both at once?** Run `eas build --platform all` to build iOS and Android in parallel.

---

## Path B: SwiftUI (iOS Native)

### What You'll End Up With

- A fully native iOS app with Apple's latest UI framework
- Convex backend for data persistence and real-time sync
- Clean, native-feeling animations and interactions
- Runs on iPhone, iPad, and potentially Mac

### Quick Start: One Prompt (Path B)

**This is all you need for Path B.** Create your project in Xcode (step B2), open it in Cursor, then paste this prompt into Agent mode. The AI sets up the Convex SDK, data model, and all your SwiftUI views. You just review, accept, and run it.

The numbered steps below break down the same process if you want to learn how each part works.

> "Set up this SwiftUI project with the Convex Swift SDK. Add the Convex Swift package dependency (https://github.com/get-convex/convex-swift).
>
> Create:
> - A ConvexClient singleton in Services/ConvexService.swift that connects to my Convex deployment
> - A Config.swift with the Convex URL placeholder
> - convex/schema.ts with tables for [describe your data — e.g., items with title, description, status, userId]
> - Convex query and mutation functions for CRUD operations
>
> Build the main app with SwiftUI:
> 1. A NavigationStack with a list of [items] fetched from Convex
> 2. A detail view when tapping an item
> 3. A sheet to create new items with a form
> 4. Swipe-to-delete on list items
> 5. Use SF Symbols for icons, modern iOS 18 design
>
> Use MVVM architecture with ObservableObject view models."

Replace `[describe your data]` and `[items]` with your actual data model.

> **Power user tip:** Install the [AI Dev Stack skill](https://github.com/janeyou/ai-dev-stack-cursor-skill) for ongoing AI context beyond the initial scaffold. It teaches Cursor your preferred patterns across all projects.

### B1: Install Xcode (~20 min)

1. Open the **App Store** on your Mac
2. Search for **Xcode** and install it
3. Open Xcode once and accept the license agreement
4. Go to **Settings > Platforms** and ensure **iOS 18** SDK is downloaded

### B2: Create the Project (~3 min)

1. Open Xcode → **File > New > Project**
2. Choose **App** under iOS
3. Settings:
  - Product Name: `MyApp`
  - Organization Identifier: `com.yourname` (e.g., `com.janedoe`)
  - Interface: **SwiftUI**
  - Language: **Swift**
  - Storage: **None** (Convex handles this)
4. Save to `~/Dev/`
5. Close Xcode, open in Cursor: `cursor ~/Dev/MyApp`

### B3: Add Convex Swift SDK (~5 min)

Open Agent mode in Cursor and say:

> "Set up this SwiftUI project with the Convex Swift SDK. Add the Convex Swift package dependency. Create a ConvexClient singleton that connects to my Convex deployment. Create a simple data model for [your data] and views that query and mutate data through Convex."

Add your Convex URL. Create a `Config.swift` file or use an `.xcconfig` file:

```swift
enum Config {
    static let convexURL = "https://your-slug-123.convex.cloud"
}
```

### B4: Build with AI (~20 min)

SwiftUI works great with AI. Describe your screens:

> "Build the main app with SwiftUI:
>
> 1. A NavigationStack with a list of [items] fetched from Convex
> 2. A detail view when tapping an item
> 3. A sheet to create new items with a form
> 4. Swipe-to-delete on list items
> 5. Use SF Symbols for icons, modern iOS 18 design"

### B5: Run on Simulator (~2 min)

In Cursor's terminal:

```bash
# Open in Xcode for running on simulator
open ~/Dev/MyApp/MyApp.xcodeproj
```

In Xcode: select **iPhone 16 Pro** simulator from the toolbar, then press **Cmd + R** to run.

### B6: Deploy to TestFlight

1. In Xcode: **Product > Archive**
2. **Distribute App > App Store Connect**
3. Go to [appstoreconnect.apple.com](https://appstoreconnect.apple.com)
4. Add the build to TestFlight for beta testing

---

## Mobile-Specific Tips

### Debugging

- **React Native:** Use `npx expo start` and press `j` for Chrome DevTools debugger
- **SwiftUI:** Xcode's built-in debugger and Preview canvas (Cmd + Option + P)

### Push Notifications

Ask the AI:

> "Add push notifications using [Expo Notifications / APNs]. Send a notification when [event happens] using a Convex scheduled function."

### Offline Support

Convex syncs automatically when the app reconnects. For offline-first:

> "Add optimistic updates and a local cache that persists data when offline using [AsyncStorage / SwiftData]."

### App Store Submission

- **iOS:** Requires Apple Developer account ($99/year), app icons, screenshots, privacy policy
- **Android:** Requires Google Play Developer account ($25 one-time), similar assets plus a content rating questionnaire

---

## Troubleshooting

### "No simulator available" (iOS)

Open Xcode → Settings → Platforms → Download iOS runtime. Then: `xcrun simctl list devices` to verify.

### Android emulator won't start

- Make sure virtualization is enabled: **Android Studio > Virtual Device Manager** — if the emulator shows errors, try creating a new device with a different system image
- If you see "ANDROID_HOME is not set," re-run the shell export commands from step A1 and restart your terminal

### Android build fails with SDK errors

Make sure the Android SDK path is set correctly:

```bash
echo $ANDROID_HOME
# Should print: /Users/yourname/Library/Android/sdk
```

If it's empty, re-run the export commands from step A1.

### Expo app crashes on start

Check terminal for errors. Common fix: `npx expo start --clear` to clear cache.

### "Unable to resolve module" in React Native

```bash
npx expo install --fix
```

### SwiftUI preview not loading

Press **Cmd + Option + P** in Xcode. If it still fails, clean the build: **Product > Clean Build Folder** (Cmd + Shift + K).

---

## What's Next?

- **Want a web version too?** [Build a Web App](build-a-web-app.md) — Convex keeps data in sync across both automatically
- **Need a landing page for your app?** [Create a Personal Website](build-a-personal-website.md)
- **Going to production?** Set up production Convex deployment and Clerk credentials

