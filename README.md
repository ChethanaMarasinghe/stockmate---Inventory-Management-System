# StockMate - Inventory Management App

**StockMate** is a comprehensive Flutter-based mobile application designed to help businesses efficiently manage their inventory, track stock levels, monitor suppliers, and streamline order processes—all in one place.

## 📱 Features

### 🔐 Authentication
- **User Registration**: Create accounts with email, password, full name, and mobile number
- **Secure Login**: Firebase Authentication for secure user access
- **User Data Storage**: Firestore integration for storing user profiles

### 🏠 Dashboard (Home Tab)
- **Inventory Overview**: Real-time display of total inventory quantity
- **Supplier Tracking**: Count of unique suppliers in the system
- **Low Stock Alerts**: Visual indicators (color-coded dots) for items with quantity < 10
- **Stock Status Indicators**:
  - 🟢 Green: Quantity > 10 (Healthy Stock)
  - 🟠 Orange: Quantity 1-10 (Low Stock)
  - 🔴 Red: Quantity = 0 (Out of Stock)

### 📦 Items Management
- **Add Items**: Create new inventory items with supplier details and quantities
- **Smart Duplicate Handling**: Automatically updates quantity if item-supplier combination exists
- **Search Functionality**: Real-time search by item name
- **Visual Stock Indicators**: Color-coded status for quick stock level assessment
- **Update Quantities**: Modify stock levels when adding existing items

### 🛒 Orders Management
- **Grouped Display**: Items organized by name with supplier breakdown
- **Order Placement**: Create orders directly from available stock
- **Quantity Management**: Specify order quantities with validation
- **Stock Deduction**: Automatic inventory updates when orders are placed
- **Search Integration**: Find items quickly using the search delegate
- **Insufficient Stock Protection**: Prevents over-ordering beyond available quantity

### 🏢 Suppliers Management
- **Unique Supplier List**: Displays all unique suppliers from inventory
- **Expandable Cards**: View all items from each supplier
- **Search Suppliers**: Filter suppliers by name in real-time
- **Item Details**: See item names and quantities per supplier
- **Supplier Inventory**: Complete overview of what each supplier provides

## 🛠️ Technology Stack

### Frontend
- **Flutter**: Cross-platform mobile development framework
- **Dart**: Programming language (SDK ^3.7.0)
- **Material Design**: Modern, responsive UI components

### Backend & Services
- **Firebase Core** (v3.12.1): Firebase SDK initialization
- **Firebase Authentication** (v5.5.1): User authentication and authorization
- **Cloud Firestore** (v5.5.0): NoSQL database for real-time data sync
- **FL Chart** (v0.63.0): Data visualization (ready for analytics features)

### Architecture
- **State Management**: StatefulWidget with setState
- **Real-time Updates**: StreamBuilder for live data synchronization
- **Navigation**: MaterialPageRoute with bottom navigation bar
- **Asset Management**: Local image assets for branding

## 📂 Project Structure

```
lib/
├── main.dart                    # App entry point with Firebase initialization
├── firebase_options.dart        # Firebase configuration
├── pages/
│   ├── slash_screen.dart       # Welcome screen with app introduction
│   ├── login.dart              # User login interface
│   ├── signup_screen.dart      # User registration interface
│   ├── home.dart               # Main navigation hub with bottom tabs
│   ├── home_tab.dart           # Dashboard with inventory overview
│   ├── items_tab.dart          # Item management and listing
│   ├── orders_tab.dart         # Order placement and management
│   ├── suppliers_tab.dart      # Supplier overview and details
│   └── add_item_page.dart      # Dialog for adding new items
└── utils/
    └── constants.dart          # App-wide constants (colors, styles)

android/                         # Android-specific configuration
├── build.gradle.kts            # Gradle build configuration (Kotlin DSL)
└── app/
    ├── build.gradle.kts        # App-level Gradle configuration
    └── google-services.json    # Firebase Android configuration

ios/                            # iOS-specific configuration
assets/                         # Image assets (splash, login screens)
```

## 🎨 Design System

### Color Palette
- **Background**: `#F2F2F2` (Light Gray)
- **Primary/Accent**: `#FFAD15` (Golden Yellow)
- **Status Colors**: Green (healthy), Orange (low), Red (critical)

### Typography
- **Headings**: Bold, 24px, Black
- **Buttons**: Bold, 18px, Black
- **Body**: Standard Material Design text styles

### UI Components
- **Cards**: Elevated with rounded corners for content grouping
- **Buttons**: Full-width rectangular buttons with consistent styling
- **Search Bars**: Integrated in app bars for quick filtering
- **Expansion Tiles**: Used for supplier details and grouped items

## 🚀 Getting Started

### Prerequisites
- Flutter SDK ^3.7.0
- Dart SDK ^3.7.0
- Android Studio / Xcode (for mobile emulators)
- Firebase project with Authentication and Firestore enabled

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd inventory_management_app
   ```

2. **Install dependencies**
   ```bash
   flutter pub get
   ```

3. **Configure Firebase**
   - Add `google-services.json` to `android/app/`
   - Add `GoogleService-Info.plist` to `ios/Runner/`
   - Ensure `firebase_options.dart` is properly configured

4. **Configure Android Build**
   - Ensure `android/build.gradle.kts` uses proper Kotlin DSL syntax
   - Verify `minSdk = 23` in `android/app/build.gradle.kts`
   - Set `ndkVersion = "27.0.12077973"` for Firebase compatibility

5. **Run the app**
   ```bash
   flutter run
   ```

## 📊 Database Schema

### Collections

#### `users`
```json
{
  "userId": "string (Firebase Auth UID)",
  "fullName": "string",
  "email": "string",
  "mobile": "string",
  "createdAt": "timestamp"
}
```

#### `items`
```json
{
  "itemName": "string",
  "supplierName": "string",
  "quantity": "number",
  "createdAt": "timestamp"
}
```

### Queries
- Items by name: `where('itemName', isEqualTo: name)`
- Items by supplier: `where('supplierName', isEqualTo: supplier)`
- Search items: `where('itemName', isGreaterThanOrEqualTo: query)`

## 🔧 Build Configuration

### Android
- **Min SDK**: 23 (Android 6.0 Marshmallow)
- **Compile SDK**: As defined by Flutter
- **NDK Version**: 27.0.12077973
- **Gradle**: Kotlin DSL (`.kts` files)
- **Java Version**: 11

### Build Fixes Applied
1. Converted Groovy syntax to Kotlin DSL in `build.gradle.kts`
2. Updated `minSdk` from 21 to 23 for Firebase Auth compatibility
3. Set explicit NDK version for Firebase plugins
4. Fixed classpath declarations to use parentheses: `classpath("...")`

## 🐛 Known Issues & Fixes

### Resolved
- ✅ Gradle build script compilation errors (Groovy to Kotlin DSL conversion)
- ✅ Firebase Auth minSdk version conflict
- ✅ NDK version incompatibility
- ✅ BuildContext usage across async gaps
- ✅ Unused field warnings

### Code Quality
- Proper `mounted` checks before using BuildContext after async operations
- Removed debug `print()` statements from production code
- Consistent error handling with user-friendly messages

## 📱 Screen Flow

```
SplashScreen → LoginScreen → HomeScreen (with BottomNavigationBar)
                    ↓                      ↓
              SignupScreen          [Home, Items, Orders, Suppliers Tabs]
```

## 🎯 Future Enhancements

- 📊 Analytics Dashboard using FL Chart
- 📤 Export inventory reports (PDF/Excel)
- 🔔 Push notifications for low stock alerts
- 📸 Item image uploads
- 📊 Order history tracking
- 👥 Multi-user role management (Admin, Manager, Staff)
- 🌐 Web version support
- 📱 iOS app distribution
- 🔍 Advanced search and filtering
- 📈 Sales tracking integration

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👨‍💻 Developer Notes

### Testing
```bash
flutter test                  # Run unit tests
flutter analyze              # Check for code issues
```

### Build APK
```bash
flutter build apk --release  # Build release APK
```

### Build for iOS
```bash
flutter build ios --release  # Build release iOS app
```

## 📞 Support

For issues, questions, or contributions, please open an issue on the GitHub repository.

---

**Smart Inventory, Smarter Business** 🚀
