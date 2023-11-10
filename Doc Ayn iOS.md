## Technical Documentation

### GETTING STARTED

Doc Ayn requires Xcode 15.0 and above for development. It uses Swift 5 as the main programming language, SwiftUI for the interface, and the Swift Package Manager (SPM) for third-party libraries. The minimum supported iOS version is 16.0.
### INSTALLATION AND DEVELOPMENT

An Apple account is required for development. This account must be in the Rogomi, Inc. development team. Xcode should be able to open `DocAyn.xcodeproj` found in the root directory of the source code. If possible, use SPM to update package dependencies to their latest versions.
### PROGRAMMING LANGUAGE

The app uses Swift 5 for development.
### MINIMUM VERSION

The minimum supported iOS version is 16.0.
### APPLICATION ID

`com.docayn.appdemo`
### DEBUGGING

Xcode provides a debugging suite that allows logging, breakpoint creation, variable testing, and more.

Several devices and iOS simulators are also used to test different screen sizes and iOS versions.
### THIRD-PARTY LIBRARIES

Libraries are installed using the [**Swift Package Manager (SPM)**](https://www.swift.org/package-manager/).
#### Firebase Services

- **FirebaseAnalytics** - Analytics such as app users, activity, demographics, etc.
- **FirebaseAuth** - Authorization to use other Firebase services.
- **FirebaseCrashlytics** - Detailed analysis of app crashes, crash logs, and device information on crash instances.
- **FirebaseFirestore** - Database system used to store various bits of info used in the app.
- **FirebaseMessaging** - Messaging system used for notifications and other messages.
#### Google Services

- **GoogleSignIn** - Authorization service that provides an interface for account signing-in using Google.

### NOTABLE UTILITIES AND VIEW DATA

#### Core Classes

`AppDelegate.swift` contains the AppDelegate that manages setup processes. It configures Firebase functionality on startup.  
#### Firestore Manager

Any methods related to Firestore is managed through the `FirestoreManager` environment object. It is used in any View that requires use of the database.

**Methods**
- `checkIfDocAyn` - checks if current user is Doc Ayn
- `getDoctorId` - retrieves the doctor's ID
- `checkIfPatientExists` - checks if any patient with the specified ID exists
- `getPatient` - retrieves a patient given their UID
- `getFaqs` - retrieves FAQs
- `createPatient` - creates a patient with a valid patient ID
- `updatePatientToken` - updates the FCM Token of a patient
- `updateDoctorToken` - updates the FCM Token of the doctor
- `generateValidPatientId` - creates a random patient ID and makes sure it doesn't already exist
- `getFirebaseMessagingToken` - retrieves the app's Firebase Messaging token
- `createNotification` - creates a notification to push
- `updateNotification` - modifies an existing notification
- `getNotifications` - retrieves all notifications stored in the remote database
- `deleteNotification` - deletes an existing notification
#### Navigation

Navigation is handled through the `navPath` array in `ContentView.swift`. This path can be manipulated by appending or removing a `NavRoute` to allow switching from one view to another. As such, it is passed on to every View as `path` for navigation functionality.
#### Login State

The app needs to determine if the current user is logged in, and if so, if they are a patient or doctor. As such, the `UserLoginStateObject` provides an observable object for Views to determine the state of the user.
#### Patient ID

In cases where the current user is a patient, a patient ID is saved in UserDefaults through the `@AppStorage` property wrapper. As long as the user remains logged in, this ID is accessible throughout any View.
### View Data

##### LoginView

**Methods**
- `googleSignIn` - handler for Google Sign-in
- `googleSignOut` - handler for Google Sign-out
- `randomNonceString` - generates a random nonce string for Apple Sign-in use
- `sha256` - hashes a string using SHA256
- `authenticate` - signs the user in using their preferred method

 **Variables**
- `isChecked` - determines if the checkbox is checked or not
- `isFetching` - state of fetching data asynchronously
- `isAnimatingAppleButton` - state of Apple Sign-in button animation
- `isAnimatingGoogleButton` - state of Google Sign-in button animation

##### LoadingView 

**Variables**
- `show` - state for if this View is shown

##### FaqView

**Methods**
- `fetchFaqs` - retrieves FAQs from the remote database

##### PatientDashboardView

**Methods**
- `googleSignOut` - handler for Google Sign-out

##### DoctorDashboardView

**Methods**
- `googleSignOut` - handler for Google Sign-out

##### NotificationsView

**Variables**
- `draftNotificationObject` - object used for holding unsaved (new/editing) notification data
- `notifications` - contains all retrieved notifications
- `showAlert` - state for if overlay is showing
- `selectedId` - ID of currently selected notification

##### NotificationFormView

**Variables**
- `draftNotificationObject` - object used for holding unsaved (new/editing) notification data
- `title` - title of the notification
- `message` - message of the notification
- `date` - timestamp for when the notification should be pushed
- `isLoading` - state for loading data
