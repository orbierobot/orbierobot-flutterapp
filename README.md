<div align="center">
  <br/>
  <img src="assets/images/pawme_logo.png" alt="Orbie Logo" width="120" height="120"/>
  <h1>Orbie</h1>
  <p><strong>Your Open-Source Robot Companion</strong></p>
  <p>
    <img src="https://img.shields.io/badge/Flutter-3.x-02569B?style=flat&logo=flutter" alt="Flutter 3.x"/>
    <img src="https://img.shields.io/badge/Firebase-FFCA28?style=flat&logo=firebase" alt="Firebase"/>
    <img src="https://img.shields.io/badge/Platform-Android-34A853?style=flat&logo=android" alt="Android"/>
    <img src="https://img.shields.io/badge/License-MIT-yellow?style=flat" alt="License"/>
  </p>
</div>

---

Orbie is a Flutter mobile app that turns your phone into the ultimate remote control for your Orbie robot companion. With a sleek dark cyber-themed UI, it gives you live camera streaming, real-time sensor data, full motor control, health monitoring, and more — all powered by ESP32 and Firebase.

## ✨ Features

###  Robot Control
- **Live Camera Feed** — MJPEG streaming from the robot's camera with real-time video preview
- **Motor Control** — Drive, turn, stop with smooth acceleration curves
- **Sensor Dashboard** — Distance (ultrasonic), ambient & object temperature (IR)
- **Laser Toggle** — On/off control for the robot's laser pointer
- **Video Recording** — Record robot POV footage, processed with FFmpeg, saved to your gallery

###  WiFi & Pairing
- **Smart WiFi Setup** — Scan nearby networks, connect the robot to your home WiFi
- **PAWME-SETUP Mode** — One-tap robot hotspot detection and configuration
- **Network Discovery** — Automatic robot discovery via NSD/mDNS
- **Reboot & Recovery** — Remote reboot with countdown and auto-reconnect

###  Health Monitoring
- **Pose Analysis** — Real-time dog/cat pose estimation metrics
- **Health Showcase** — Animated health dashboard with weight, activity, temperature trends
- **Health Cards** — Visual indicators for wellness tracking

###  Social & Feed
- **Video Feed** — Scrollable feed of recorded robot camera clips
- **Reels** — Short-form video reels from your robot's adventures
- **Remote Control** — Virtual joystick interface for manual navigation

###  Auki Portals
- **QR Scanning** — Scan QR codes to discover and interact with AR-like portals
- **Sensor Integration** — Gyroscope-based portal interaction
- **Portal Timeline** — History of discovered portal connections

###  Authentication
- **Email & Password** — Firebase email/password registration with email verification
- **Google Sign-In** — One-tap Google account login
- **Persistent Sessions** — Auto-login on app restart

###  UI / UX
- **Dark Futuristic Theme** — Deep blacks, neon purple/cyan gradients, glassmorphism cards
- **Animated Splash** — Elastic scale, glow pulse, particle background
- **CyberText** — Gradient glow text components
- **GlassCard & NeonButton** — Premium glassmorphism and neon-styled interactive elements
- **Particle Backgrounds** — Animated floating particle systems throughout
- **Staggered Animations** — Buttery smooth fade/slide transitions

##  Screens

| Screen | Description |
|---|---|
| **Splash** | Animated brand intro with pulsing loader |
| **Welcome** | Brand card with Email / Google sign-up options |
| **Google Sign-In** | One-tap Google authentication |
| **Email Registration** | Full registration with email verification |
| **Sign In** | Email/password login for returning users |
| **Home** | Robot dashboard — status, battery, quick actions |
| **Robot Control** | Live camera, motor controls, sensors, recording |
| **Robot Detail** | Per-robot stats: name, battery, signal, status |
| **Add Robot** | 3-step WiFi pairing wizard |
| **Remote Control** | Virtual D-pad + joystick for navigation |
| **Video Feed** | Scrollable camera clip library |
| **Reels** | TikTok-style short video feed |
| **Auki Portals** | QR scanner + AR portal discovery |
| **Health Analysis** | Dog/cat pose and wellness metrics |
| **Health Showcase** | Animated health trends dashboard |
| **Settings** | Account info, theme toggle, sign out |
| **Robot Reboot** | Remote reboot with animated countdown |

##  Architecture

```
lib/
├── constants/           # Colors, themes
│   ├── app_colors.dart
│   └── app_theme.dart
├── screens/             # All UI screens
│   ├── add_robot/       # WiFi pairing wizard
│   │   ├── enable_pairing_mode_screen.dart
│   │   ├── pairing_mode_enabled_screen.dart
│   │   └── press_pairing_button_screen.dart
│   ├── splash_screen.dart
│   ├── welcome_screen.dart
│   ├── home_page.dart
│   ├── robot_control_page.dart      # Main control hub (986 lines)
│   ├── robot_detail_page.dart
│   ├── robot_reboot_page.dart
│   ├── feed_screen.dart
│   ├── reels_screen.dart
│   ├── remote_screen.dart
│   ├── auki_portals_screen.dart
│   └── ... (settings, auth, health)
├── services/            # Business logic
│   ├── auth_service.dart
│   └── theme_provider.dart
├── widgets/             # Reusable UI components
│   └── futuristic_ui.dart           # 990 lines of cyber-themed widgets
├── main.dart            # App entry point
└── home_page.dart       # Legacy home (migrating)
```

##  Getting Started

### Prerequisites
- Flutter SDK ≥ 3.0
- Android Studio / VS Code
- Firebase project (with Auth, Realtime Database, Storage enabled)
- A built Orbie robot (ESP32-based) or the robot simulator

### Setup

```bash
# Clone the repo
git clone https://github.com/your-org/orbie.git
cd orbie

# Install dependencies
flutter pub get

# Configure Firebase
# 1. Place your google-services.json in android/app/
# 2. Enable Email/Password and Google Sign-In in Firebase Console

# Run on device
flutter run
```

### Firebase Configuration
1. Create a Firebase project at [console.firebase.google.com](https://console.firebase.google.com)
2. Enable **Authentication** → **Sign-in providers**: Email/Password + Google
3. Enable **Realtime Database** in test mode (lock down later)
4. Enable **Cloud Storage** for video clip uploads
5. Download `google-services.json` → place in `android/app/`
6. For Google Sign-In, register your SHA-1 fingerprint in Firebase

##  Dependencies

| Package | Purpose |
|---|---|
| `firebase_core` / `firebase_auth` | Authentication |
| `firebase_database` / `firebase_storage` | Data & media storage |
| `google_sign_in` | Google account login |
| `flutter_mjpeg` | MJPEG camera stream decoding |
| `ffmpeg_kit_flutter_new` | Video recording & processing |
| `wifi_iot` / `wifi_scan` | WiFi scanning & robot hotspot setup |
| `network_info_plus` | Current network SSID detection |
| `mobile_scanner` | QR code scanning (Auki Portals) |
| `sensors_plus` | Gyroscope / accelerometer data |
| `provider` | State management |
| `nsd` | Network service discovery (mDNS) |
| `media_scanner` | Save recordings to device gallery |
| `path_provider` | Local file paths |
| `shared_preferences` | Local settings persistence |

##  Robot API

The app communicates with the Orbie ESP32 robot over HTTP. Key endpoints:

| Endpoint | Method | Description |
|---|---|---|
| `/drive?x={0..255}&y={0..255}` | GET | Motor control |
| `/laser?state=on\|off` | GET | Laser toggle |
| `/status` | GET | JSON: distance, temps, battery |
| `/stream` | — | MJPEG video stream |
| `/record/start` | POST | Start video recording |
| `/record/stop` | POST | Stop and save recording |

##  Design System

The app uses a custom cyber-futuristic design language built entirely from scratch:

- **Color Palette**: `#8B5CF6` (vivid purple), `#22D3EE` (neon cyan), `#03050D` (deep black)
- **Typography**: Gradient-shaded text via `CyberText`, neon glow via `NeonText`
- **Components**: `ParticleBg` (animated particle system), `GlassCard` (glassmorphism), `NeonButton` (glowing elevated buttons), `StaggeredFadeIn` (list animations)
- **Animations**: Elastic scale bounces, glow pulses, fade/slide transitions, staggered reveal

##  Contributing

Contributions are welcome! Please open an issue or PR for:
- Bug fixes
- New robot sensor integrations
- UI polish and animations
- Platform support (iOS coming)

##  Known Issues

- iOS build not yet tested (PRs welcome!)
- MJPEG stream quality depends on robot's WiFi signal strength
- Google Sign-In requires SHA-1 fingerprint in Firebase console

##  License

MIT © AyvaLabs

---

<p align="center">
  Built with  by the Orbie team — <a href="https://ayvalabs.com">AyvaLabs</a>
</p>