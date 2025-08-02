# SecureApp Lock

A comprehensive Android application that provides PIN and biometric authentication to lock selected installed apps, built with Kotlin and Jetpack Compose.

## Features

### 🔐 Security Features
- **PIN Authentication**: 4-6 digit numeric PIN with secure storage using Android Keystore
- **Biometric Authentication**: Support for fingerprint and face unlock via AndroidX BiometricPrompt
- **Secure Storage**: PIN is salted and hashed, never stored in plaintext
- **Encrypted Preferences**: All sensitive data stored using EncryptedSharedPreferences

### 📱 App Management
- **App Selection**: Choose which installed apps to protect
- **Real-time Monitoring**: Background service monitors app launches
- **System App Filtering**: Automatically filters out system apps and apps without launch intents
- **Easy Management**: Add/remove apps from protection with simple toggle interface

### 🎨 Modern UI
- **Material Design 3**: Modern, clean interface following Material Design guidelines
- **Jetpack Compose**: Fully built with Compose for smooth, reactive UI
- **Dark Theme Support**: Automatic dark/light theme switching
- **Responsive Design**: Optimized for different screen sizes

### ⚙️ Advanced Features
- **First-time Setup**: Guided setup process for PIN creation and biometric enrollment
- **Settings Management**: Change PIN, toggle biometric authentication
- **Usage Stats Integration**: Monitors app usage to detect when protected apps are launched
- **Boot Persistence**: Automatically starts monitoring service after device reboot

## Architecture

### Project Structure
\`\`\`
app/src/main/java/com/secureapplock/
├── MainActivity.kt                 # Main app interface
├── SetupActivity.kt               # First-time setup flow
├── AuthenticationActivity.kt      # PIN/biometric authentication
├── AppSelectionActivity.kt        # App selection interface
├── SettingsActivity.kt           # Settings and preferences
├── service/
│   └── AppMonitorService.kt      # Background monitoring service
├── utils/
│   └── SecurityManager.kt        # Security operations and storage
├── viewmodel/
│   ├── MainViewModel.kt          # Main screen logic
│   ├── SetupViewModel.kt         # Setup flow logic
│   └── AppSelectionViewModel.kt  # App selection logic
├── receiver/
│   └── BootReceiver.kt          # Boot completion receiver
└── ui/theme/                    # Compose theme configuration
\`\`\`

### Security Implementation

#### PIN Storage
- Uses Android Keystore for secure key generation
- PIN is salted with SecureRandom-generated salt
- SHA-256 hashing with salt for PIN verification
- EncryptedSharedPreferences for storing hashed PIN and salt

#### Biometric Authentication
- AndroidX BiometricPrompt for unified biometric authentication
- Support for fingerprint, face unlock, and device credentials
- Fallback to PIN authentication if biometric fails

#### App Monitoring
- UsageStatsManager for detecting app launches
- Background service with minimal resource usage
- Real-time monitoring with configurable intervals

## Setup Instructions

### Prerequisites
- Android Studio Arctic Fox or later
- Android SDK 26 (Android 8.0) or higher
- Device with biometric hardware (optional, for biometric features)

### Installation

1. **Clone the repository**
   \`\`\`bash
   git clone https://github.com/yourusername/secureapp-lock.git
   cd secureapp-lock
   \`\`\`

2. **Open in Android Studio**
   - Open Android Studio
   - Select "Open an existing project"
   - Navigate to the cloned directory and select it

3. **Build and Run**
   - Wait for Gradle sync to complete
   - Connect an Android device or start an emulator
   - Click "Run" or press Ctrl+R (Cmd+R on Mac)

### Required Permissions

The app requires the following permissions:

- `PACKAGE_USAGE_STATS`: Monitor app usage to detect when protected apps are launched
- `USE_BIOMETRIC`: Access biometric authentication hardware
- `USE_FINGERPRINT`: Legacy fingerprint support
- `SYSTEM_ALERT_WINDOW`: Display authentication screen over other apps
- `FOREGROUND_SERVICE`: Run background monitoring service
- `RECEIVE_BOOT_COMPLETED`: Start monitoring after device reboot

### First-time Setup

1. **Welcome Screen**: Introduction to the app's features
2. **PIN Creation**: Create a 4-6 digit numeric PIN
3. **Biometric Setup**: Optionally enable fingerprint/face unlock
4. **Permission Grant**: Grant usage access permission in device settings

## Usage Guide

### Protecting Apps

1. Open SecureApp Lock
2. Tap the "+" floating action button
3. Select apps you want to protect by toggling the switches
4. Selected apps will now require authentication to launch

### Unlocking Apps

When you try to open a protected app:
1. Authentication screen appears automatically
2. Enter your PIN or use biometric authentication
3. App launches after successful authentication

### Managing Settings

Access settings to:
- Change your PIN
- Toggle biometric authentication
- View app information

### Removing Protection

1. Go to app selection screen
2. Toggle off the switch for apps you want to unprotect
3. Apps will no longer require authentication

## Technical Details

### Dependencies

- **Jetpack Compose**: Modern UI toolkit
- **Material Design 3**: Latest Material Design components
- **AndroidX Biometric**: Unified biometric authentication
- **Security Crypto**: Encrypted storage for sensitive data
- **Lifecycle ViewModel**: MVVM architecture support
- **Kotlin Coroutines**: Asynchronous programming

### Security Considerations

- PIN is never stored in plaintext
- All sensitive data encrypted using Android Keystore
- Biometric authentication uses hardware-backed security
- App monitoring uses official Android APIs
- No network permissions - all data stays on device

### Performance Optimization

- Efficient background monitoring with minimal battery impact
- Lazy loading of app lists
- Optimized Compose UI with proper state management
- Minimal memory footprint

## Troubleshooting

### Common Issues

**App not detecting launches**
- Ensure usage access permission is granted
- Check if the monitoring service is running
- Restart the app if needed

**Biometric authentication not working**
- Verify device has biometric hardware
- Ensure biometric authentication is set up in device settings
- Check if biometric permission is granted

**PIN not working**
- Ensure PIN is 4-6 digits
- Try changing PIN in settings
- Clear app data if necessary (will require setup again)

### Debug Mode

For development and debugging:
1. Enable developer options on your device
2. Enable USB debugging
3. Use Android Studio's debugger and logcat for detailed logs

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Android team for excellent security APIs
- Jetpack Compose team for modern UI framework
- Material Design team for beautiful design guidelines
- Open source community for inspiration and best practices

## Support

For support, please open an issue on GitHub or contact [your-email@example.com](mailto:your-email@example.com).

---

**Note**: This app is designed for educational and personal use. Always follow your organization's security policies and local laws when using app locking software.
