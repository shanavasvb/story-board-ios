# iOS Storyboard & Interface Builder - Study Guide

A comprehensive guide covering the most important iOS development concepts for beginners.

![Course Syllabus](./syllabusjpeg)

---

## 📚 Table of Contents

- [Most Important Questions](#most-important-questions)
- [Info.plist](#infoplist)
- [Interface Builder](#interface-builder)
- [Storyboard](#storyboard)
- [iOS Architecture Layers](#ios-architecture-layers)
- [Touches vs Gestures](#touches-vs-gestures)
- [Global Thread vs Main Thread](#global-thread-vs-main-thread)
- [Cocoa Touch Framework](#cocoa-touch-framework)
- [Value Change Controls](#value-change-controls)
- [UI Components Deep Dive](#ui-components-deep-dive)
  - [UITextField vs UITextView](#uitextfield-vs-uitextview)
  - [Alert vs Action Sheet](#alert-vs-action-sheet)
  - [IBAction vs IBOutlet](#ibaction-vs-iboutlet)
- [Navigation](#navigation)
  - [UINavigationController](#uinavigationcontroller)

---

## 🎯 Most Important Questions (Chapter 1)

These are the most frequently asked questions in exams:

1. **What is Info.plist? Why is it used in iOS applications?**
2. **Briefly explain Interface Builder and Storyboard in iOS.**
3. **Differentiate between touches and gestures in iOS.**
4. **Differentiate between Global thread and Main thread.**
5. **Explain the architecture of iOS (layers).**
6. **What is the Cocoa Touch framework? Give examples.**

> 💡 **Pro Tip:** Mastering these 6 questions will help you answer most short and long questions from Unit 1.

---

## 📄 Info.plist

### What is Info.plist?

**Info.plist (Information Property List)** is a configuration file present in every iOS application. It stores key-value information that instructs the iOS system on how the app should run.

### Purpose and Uses

- Defines **basic app information** (app name, version, bundle identifier)
- Stores **permissions** (camera, location, microphone, Bluetooth, etc.)
- Configures **launch screen, app icons, and supported device orientations**
- Read by the system **before app launch** to establish required rules

### Common Info.plist Keys

| Key | Purpose |
|-----|---------|
| `CFBundleDisplayName` | App name displayed on device |
| `NSCameraUsageDescription` | Request permission for camera access |
| `UILaunchStoryboardName` | Specifies the launch screen storyboard |

### Example Values

```xml
<key>CFBundleDisplayName</key>
<string>My Awesome App</string>

<key>NSCameraUsageDescription</key>
<string>This app needs camera access to take photos</string>
```

> **Summary:** Info.plist is the identity and permissions rulebook of an iOS app. Without correct settings, an app may not run or access device features.

---

## 🛠️ Interface Builder

### What is Interface Builder?

**Interface Builder (IB)** is a visual UI design tool integrated into Xcode that enables developers to create and arrange user interfaces for iOS apps without writing layout code. It provides a drag-and-drop environment, making UI design faster and more intuitive.

### Where is it Used?

- **Storyboard (.storyboard)** files
- **XIB (.xib)** files

Both file types use Interface Builder for visual screen design.

### Key Features

| Feature | Description |
|---------|-------------|
| **Drag-and-drop UI elements** | Add labels, buttons, text fields, images, etc., directly onto screens |
| **Live Preview** | Visualize app layout across different screen sizes |
| **Auto Layout Support** | Create responsive UIs for all devices (iPhone, iPad) using constraints |
| **Connect UI to Swift Code** | Link UI elements via **IBOutlet** (properties) and **IBAction** (events) |
| **Inspectors** | Modify text, colors, fonts, and more through Attribute Inspector |

### Why Interface Builder Matters

1. **Faster UI Development** — Eliminates manual layout coding
2. **Easy Maintenance** — Visual layouts are simpler to modify
3. **Beginner-Friendly** — Build UIs with minimal coding knowledge
4. **Real-time Preview** — Instant layout visualization across devices
5. **Complex UI Support** — Easily manage auto layout, constraints, stack views, and animations

### Connecting UI to Code

To use UI elements in Swift code, create:

- **IBOutlet** → Read/modify UI element properties (e.g., `label.text`)
- **IBAction** → Handle user interactions (e.g., button taps)

#### Example

```swift
@IBOutlet weak var nameLabel: UILabel!

@IBAction func submitBtnClicked(_ sender: UIButton) {
    nameLabel.text = "Welcome!"
}
```

> **Connection Method:** Use **Ctrl + Drag** from the UI element in Interface Builder to the ViewController Swift file.

### Exam Definition

> *Interface Builder is a graphical design tool in Xcode used to create, edit, and connect user interface elements of an iOS application without writing layout code. It allows drag-and-drop UI creation, supports auto layout, and lets developers link UI elements to Swift code using IBOutlet and IBAction.*

---

## 📱 Storyboard

### What is Storyboard?

**Storyboard** is a visual representation of the user interface of an iOS application. It shows all the screens (View Controllers) and the transitions (segues) between them in a single file. Storyboard makes it easy to design and understand the app's flow without writing code.

### Key Features of Storyboard

- **Visual App Flow**: See all screens and their connections in one place
- **Segues**: Visual transitions between screens (show, present, unwind)
- **Prototype Cells**: Design reusable table view cells visually
- **Auto Layout**: Set up constraints for responsive design
- **Multiple View Controllers**: Manage entire app navigation in one file

### Benefits of Using Storyboard

1. **Easy to visualize** the complete app flow
2. **Faster UI development** with drag-and-drop
3. **Better collaboration** - designers can understand the flow
4. **Simplified navigation** setup between screens
5. **Reusable components** like prototype cells

### Storyboard vs XIB

| Feature | Storyboard | XIB |
|---------|-----------|-----|
| **Scope** | Multiple screens in one file | Single screen per file |
| **Navigation** | Shows segues between screens | No navigation shown |
| **Use Case** | Complete app flow | Individual reusable views |
| **File Size** | Larger (contains multiple VCs) | Smaller (single view) |

### Creating Segues in Storyboard

**Types of Segues:**
- **Show (Push)**: Pushes to next screen in navigation stack
- **Present Modally**: Shows screen as a modal popup
- **Unwind**: Returns to previous screen

**Code to Trigger Segue:**

```swift
performSegue(withIdentifier: "showDetail", sender: self)
```

### Exam Definition

> *Storyboard is a visual interface file in iOS that displays all the app's screens and transitions in one place. It allows developers to design the complete user interface flow, set up navigation between screens using segues, and create prototype cells for table views, all without writing layout code.*

![Storyboard Diagram](./Storyboard_pdf)

---

<a name="ios-architecture-layers"></a>

---

## 🏗️ iOS Architecture Layers

iOS architecture is organized into **four layers**, where each layer provides specific services to the layer above it. This architecture helps developers build secure, fast, and well-structured apps.

![iOS Architecture Layers](ioslayers.png)

### 1️⃣ Cocoa Touch Layer (Topmost Layer)

#### Purpose
Provides all **User Interface (UI)** and **user interaction** features. Contains frameworks for creating app screens, buttons, animations, navigation, and gestures.

#### Key Features
- Implements **MVC (Model–View–Controller)** design pattern
- Provides interaction features like touch, gestures, alerts, navigation
- Manages app behavior using controllers (`UIViewController`, `UITableViewController`, etc.)

#### Important Frameworks

| Framework | Purpose |
|-----------|---------|
| **UIKit** | All UI elements (Button, Label, TableView, TextField) |
| **MapKit** | Maps & location display |
| **PushKit** | Push notifications |
| **MessageUI** | Emails/SMS interface |
| **EventKit** | Calendar and events |

> **Summary:** This layer is responsible for UI design and interaction.

---

### 2️⃣ Media Layer

#### Purpose
Handles everything related to **multimedia, graphics, audio, and animation**, making apps visually rich and interactive.

#### Key Features
- Provides 2D/3D graphics rendering
- Controls audio and video playback/recording
- Enables complex animations in UI

#### Important Frameworks

| Framework | Purpose |
|-----------|---------|
| **Core Graphics** | 2D drawing (shapes, images, rendering) |
| **Core Animation** | Smooth animations, transitions |
| **AVFoundation** | Audio/video playback and recording |
| **Metal / OpenGL ES** | High-performance 3D graphics for games |

> **Summary:** This layer makes apps visually impressive and interactive.

---

### 3️⃣ Core Services Layer

#### Purpose
Provides **fundamental system services** such as networking, data storage, contact access, and file handling. Acts as the brain of the system, managing logic and data.

#### Key Features
- Handles data storage: databases, files
- Handles networking and communication
- Manages sensors like GPS, accelerometer

#### Important Frameworks

| Framework | Purpose |
|-----------|---------|
| **Foundation** | Data types, strings, collections, dates |
| **Core Data** | Local database & object persistence |
| **Core Location** | GPS/location tracking |
| **Core Motion** | Accelerometer, gyroscope motion |
| **CFNetwork** | Internet communication |
| **Security** | Encryption, passwords, certificates |

> **Summary:** This layer manages app logic, data, and system communication.

---

### 4️⃣ Core OS Layer (Lowest Layer)

#### Purpose
The bottom layer that directly interacts with **hardware**. Ensures security, device control, low-level communication, and system performance.

#### Key Features
- Runs on **Darwin (Unix-based kernel)**
- Provides memory management and hardware access
- Handles system security, drivers, file system

#### Important Components

| Component | Purpose |
|-----------|---------|
| **Darwin Kernel** | OS core responsible for process management |
| **Security Framework** | Encryption, keychain passwords |
| **Power Management** | Battery control and optimization |
| **Drivers (Wi-Fi, Bluetooth)** | Hardware communication |
| **File System** | Manages storage/security sandbox |

> **Summary:** This layer ensures hardware access, security, and system stability.

---

### iOS Architecture Summary

| Layer | Role | Examples |
|-------|------|----------|
| **Cocoa Touch** | UI + User Interaction | UIKit, PushKit |
| **Media** | Graphics + Audio/Video | Core Animation, AVFoundation |
| **Core Services** | Logic + Data + Networking | Core Data, Core Location |
| **Core OS** | Hardware + Security | Kernel, Power, Drivers |

---

## 🤏 Touches vs Gestures

### What are Touches?

**Touches** are raw, low-level finger interactions detected on the screen, such as when a user places, moves, or lifts their finger. They provide detailed information like location, movement, number of fingers, and duration.

#### Examples of Touches
- One finger touching the screen
- Moving a finger slowly or fast
- Multiple fingers placed on the screen

#### Handled Using UIResponder Methods

```swift
touchesBegan(_:with:)
touchesMoved(_:with:)
touchesEnded(_:with:)
touchesCancelled(_:with:)
```

---

### What are Gestures?

**Gestures** are interpreted touch patterns recognized automatically by iOS using the `UIGestureRecognizer` class. They simplify detecting common interactions like tap, swipe, pinch, rotate, and long press, without manually handling touch data.

#### Examples of Gestures
- Double tap to zoom
- Swipe to delete
- Pinch to zoom
- Rotate image

#### Handled Using Gesture Recognizers

```swift
let tap = UITapGestureRecognizer(target: self, action: #selector(tapAction))
view.addGestureRecognizer(tap)
```

---

### Key Differences

| Feature | Touches | Gestures |
|---------|---------|----------|
| **Definition** | Low-level raw finger interaction | High-level meaningful pattern |
| **Usage** | Detailed finger tracking needed | Action pattern recognition |
| **Implementation** | Uses `touchesBegan`, `touchesEnded` methods | Uses `UIGestureRecognizer` |
| **Complexity** | More complex to code | Easy, automatic recognition |
| **Example** | Track finger drawing | Tap, swipe, pinch, rotate actions |

### When to Use

**Touches:**
- Drawing apps (Sketch, Notes)
- Games requiring finger movement tracking

**Gestures:**
- Swipe to delete (Lists)
- Tap to select items
- Pinch/Zoom gallery apps

### Exam Definition

> *Touches represent raw finger interactions on the screen and are handled using low-level methods like `touchesBegan()` and `touchesEnded()`. Gestures are interpreted touch patterns like tap, swipe, or pinch, recognized automatically using `UIGestureRecognizer`. Touches provide detailed data, while gestures provide simplified high-level actions.*

---

## 🧵 Global Thread vs Main Thread

### Main Thread

The **Main Thread** (also called UI Thread) is responsible for:
- Updating the User Interface (UI)
- Handling user interactions
- Running tasks that affect what the user sees immediately

#### Characteristics
- Runs UI code such as updating labels, buttons, table views, animations
- Must be fast; if slow → app becomes laggy or freezes
- Cannot perform heavy tasks (e.g., downloading files)

#### Example (UI Update Must Be on Main Thread)

```swift
DispatchQueue.main.async {
    self.label.text = "Downloaded!"
}
```

---

### Global Thread

The **Global Thread** (Background thread) is used to perform heavy operations such as:
- Downloading data from the internet
- Saving large files
- Processing images
- Complex calculations

#### Characteristics
- Improves performance by doing heavy work in the background
- Cannot directly update UI
- Prevents app from freezing

#### Example (Doing a Heavy Task)

```swift
DispatchQueue.global().async {
    // Heavy task like downloading
}
```

---

### Key Differences

| Feature | Main Thread | Global (Background) Thread |
|---------|-------------|---------------------------|
| **Usage** | UI updates, animations, user interaction | Heavy tasks like downloads, processing |
| **UI Update** | Allowed | Not Allowed |
| **Performance** | Must be fast | Can take time |
| **Risk** | UI freeze if heavy work is done | Safe for heavy tasks |
| **Queue Name** | `DispatchQueue.main` | `DispatchQueue.global()` |

### Why UI Must Run on Main Thread?

Because UI updates are time-sensitive and need immediate response to user actions. If heavy work is done on it → App freezes or crashes.

### Exam Definition

> *The Main Thread handles UI updates and user interactions, while the Global Thread performs heavy tasks like downloading or calculations in the background. UI operations can only be done on the main thread, whereas heavy tasks should run on global threads to prevent app freezing.*

---

## 🍏 Cocoa Touch Framework

### What is Cocoa Touch?

**Cocoa Touch** is the top layer of the iOS architecture that contains all the frameworks required to build interactive applications for iPhone and iPad. It provides User Interface (UI) components and user interaction features such as buttons, alerts, table views, navigation, gestures, etc.

### Purpose of Cocoa Touch

- Helps developers design UI screens using UIKit
- Manages touch interaction, gestures, multitasking, notifications
- Implements MVC (Model-View-Controller) architecture
- Provides built-in controllers like `UIViewController`, `UITableViewController`, etc.

### Key Frameworks in Cocoa Touch

| Framework | Key Function |
|-----------|--------------|
| **UIKit** | Provides buttons, labels, sliders, table views, navigation, alerts, gestures |
| **MapKit** | Supports map views and navigation systems |
| **PushKit / UserNotifications** | Push notification services |
| **EventKit** | Calendar and event handling |
| **MessageUI** | SMS and Email composer |

### UIKit – The Core Part of Cocoa Touch

UIKit contains most of the visual components used in iOS apps:
- `UILabel`, `UIButton`, `UITextField`, `TableView`, `CollectionView`
- `UINavigationController`, `UITabBarController`
- Gestures (Tap, Swipe, Pinch)

#### Example of Cocoa Touch Usage

```swift
@IBOutlet weak var titleLabel: UILabel!

override func viewDidLoad() {
    super.viewDidLoad()
    titleLabel.text = "Welcome to iOS!"
}
```

> Here, `UILabel` belongs to UIKit, which is part of Cocoa Touch.

### Exam Definition

> *Cocoa Touch is the top layer of iOS architecture that provides frameworks for building user interfaces and handling user interactions. It includes UIKit, MapKit, PushKit, and other frameworks. It follows MVC and provides UI components like buttons, table views, alerts, and gestures.*

---

<a name="value-change-controls"></a>

## 🎚️ Value Change Controls

iOS provides several interactive controls that allow users to change values through intuitive gestures. The three main value change controls are **Slider**, **Switch**, and **Stepper**.

![Value Change Controls](./valuechange.png)

### UISlider

**UISlider** allows users to select a value from a continuous range by dragging a thumb along a horizontal track.

#### Key Properties
- `minimumValue`: Lowest value (default: 0.0)
- `maximumValue`: Highest value (default: 1.0)
- `value`: Current value
- `minimumTrackTintColor`: Color of track before thumb
- `maximumTrackTintColor`: Color of track after thumb

#### Example Use Cases
- Volume control
- Brightness adjustment
- Age/price range selection
- Video playback progress

#### Code Example

```swift
@IBOutlet weak var volumeSlider: UISlider!
@IBOutlet weak var volumeLabel: UILabel!

override func viewDidLoad() {
    super.viewDidLoad()
    volumeSlider.minimumValue = 0
    volumeSlider.maximumValue = 100
    volumeSlider.value = 50
}

@IBAction func sliderValueChanged(_ sender: UISlider) {
    let currentValue = Int(sender.value)
    volumeLabel.text = "Volume: \(currentValue)"
}
```

---

### UISwitch

**UISwitch** is a binary control that toggles between ON and OFF states.

#### Key Properties
- `isOn`: Boolean value (true/false)
- `onTintColor`: Color when switch is ON
- `thumbTintColor`: Color of the movable thumb

#### Example Use Cases
- Enable/Disable notifications
- Dark mode toggle
- WiFi/Bluetooth ON/OFF
- Show/Hide password

#### Code Example

```swift
@IBOutlet weak var notificationSwitch: UISwitch!
@IBOutlet weak var statusLabel: UILabel!

@IBAction func switchValueChanged(_ sender: UISwitch) {
    if sender.isOn {
        statusLabel.text = "Notifications Enabled"
    } else {
        statusLabel.text = "Notifications Disabled"
    }
}
```

---

### UIStepper

**UIStepper** provides increment and decrement buttons to adjust a numeric value by a fixed step amount.

#### Key Properties
- `minimumValue`: Lowest allowed value
- `maximumValue`: Highest allowed value
- `stepValue`: Amount to change per tap (default: 1)
- `value`: Current numeric value
- `wraps`: Whether value wraps around at limits

#### Example Use Cases
- Quantity selector (shopping cart)
- Font size adjustment
- Rating counter
- Timer minutes/seconds

#### Code Example

```swift
@IBOutlet weak var stepper: UIStepper!
@IBOutlet weak var quantityLabel: UILabel!

override func viewDidLoad() {
    super.viewDidLoad()
    stepper.minimumValue = 1
    stepper.maximumValue = 10
    stepper.stepValue = 1
    stepper.value = 1
}

@IBAction func stepperValueChanged(_ sender: UIStepper) {
    let quantity = Int(sender.value)
    quantityLabel.text = "Quantity: \(quantity)"
}
```

---

### Comparison of Value Change Controls

| Control | Input Method | Value Type | Use Case |
|---------|--------------|------------|----------|
| **UISlider** | Drag thumb | Continuous range | Volume, brightness, progress |
| **UISwitch** | Tap to toggle | Boolean (ON/OFF) | Enable/disable features |
| **UIStepper** | Tap +/- buttons | Discrete numeric | Quantity, counter, rating |

### Exam Definition

> *UISlider allows continuous value selection by dragging a thumb along a track. UISwitch is a binary toggle control for ON/OFF states. UIStepper uses increment/decrement buttons to adjust numeric values by fixed steps. These controls provide intuitive ways for users to modify values without keyboard input.*

---

## 📱 UI Components Deep Dive

### UITextField vs UITextView

In iOS, `UITextField` and `UITextView` are two commonly used input components for taking text from users, but they are used for different purposes based on the amount and type of text input.

#### UITextField

`UITextField` is mainly used to input short, single-line text, such as names, email IDs, phone numbers, passwords, or search fields. It does not support multi-line typing and shows only one line at a time.

It has built-in features like placeholder text, clear button, autocorrection, and return key actions. It is often used with delegates (`textFieldShouldReturn`) to control behavior such as jumping to next field, validation, or closing the keyboard.

**Example Use Cases:**
- Login screen (Username, Email, Password)
- Search bar
- Phone number input

**Code Example:**

```swift
import UIKit

class ViewController: UIViewController, UITextFieldDelegate {
    @IBOutlet weak var nameField: UITextField!
    @IBOutlet weak var resultLabel: UILabel!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        nameField.delegate = self   // assigning delegate
    }
    
    // Button Action
    @IBAction func submitButton(_ sender: UIButton) {
        resultLabel.text = "Hello, \(nameField.text!)"
    }
    
    // Dismiss keyboard when return key pressed
    func textFieldShouldReturn(_ textField: UITextField) -> Bool {
        textField.resignFirstResponder()
        return true
    }
}
```

#### UITextView

`UITextView` is designed for multi-line text input, where users need to type large descriptions or paragraph-length content. Unlike UITextField, it supports scrolling, text formatting, and editing multiple lines easily.

It is useful when capturing longer input from the user. Using its delegate (`textViewDidChange`), we can track typing or customize text entry. It can also display formatted text, links, or rich text content.

**Example Use Cases:**
- Feedback form message
- User profile bio
- Comments box
- Notes or descriptions

#### Key Differences

| Feature | UITextField | UITextView |
|---------|-------------|------------|
| **Input Length** | Short, single-line | Long, multi-line |
| **Scrolling** | Not supported | Scrolls automatically |
| **Return Key** | Used to submit/close keyboard | Adds a new line |
| **Auto-Resize** | Stays single line | Expands vertically |
| **Best Use Case** | Login fields, Search | Reviews, Description boxes |

#### Exam Definition

> *In summary, UITextField is best suited for short and single-line input such as login forms, whereas UITextView is used for long, multi-line content like comments or descriptions since it supports scrolling and rich text editing.*

---

### Alert vs Action Sheet

#### What is an Alert?

An **Alert** (`UIAlertController` with `.alert` style) is a small popup message that appears in the center of the screen. It is used to display important messages, warnings, errors, or decisions that need immediate attention. The user must respond before continuing.

**Examples of When to Use:**
- Invalid login credentials
- Delete confirmation
- Warning message (e.g., "Low Battery!")

#### What is an Action Sheet?

An **Action Sheet** (`UIAlertController` with `.actionSheet` style) appears from the bottom of the screen. It is used when the user must choose between multiple actions usually related to a UI element.

**Examples of When to Use:**
- Choose image source: Camera or Gallery
- Select sharing option: Email, WhatsApp, Bluetooth
- File handling options: Rename, Delete, Move

#### Key Differences

| Feature | Alert | Action Sheet |
|---------|-------|--------------|
| **Position** | Appears in center | Slides up from bottom |
| **Purpose** | Display important information or warnings | Provide choices/actions related to a task |
| **Use Case Example** | Wrong password | Choose image: Camera/Gallery |
| **User Attention** | High priority | Medium priority |

#### Scenario Example

Suppose a user wants to upload a profile photo. Action Sheet is used to choose Camera or Gallery. If login fails, Alert is used to display a warning.

#### Swift Code Example

```swift
import UIKit

class ViewController: UIViewController {

    @IBAction func showAlertButton(_ sender: UIButton) {
        // MARK: - ALERT
        let alert = UIAlertController(title: "Login Failed",
                                      message: "Invalid username or password.",
                                      preferredStyle: .alert)

        alert.addAction(UIAlertAction(title: "OK", style: .default, handler: nil))
        alert.addAction(UIAlertAction(title: "Forgot Password?", style: .destructive, handler: nil))

        self.present(alert, animated: true, completion: nil)
    }

    @IBAction func showActionSheetButton(_ sender: UIButton) {
        // MARK: - ACTION SHEET
        let actionSheet = UIAlertController(title: "Upload Photo",
                                            message: "Choose source",
                                            preferredStyle: .actionSheet)

        actionSheet.addAction(UIAlertAction(title: "Camera", style: .default, handler: nil))
        actionSheet.addAction(UIAlertAction(title: "Gallery", style: .default, handler: nil))
        actionSheet.addAction(UIAlertAction(title: "Cancel", style: .cancel, handler: nil))

        self.present(actionSheet, animated: true, completion: nil)
    }
}
```

#### Exam Definition

> *Alert appears in the center and is used for warnings or important messages (e.g., login error). Action Sheet appears from the bottom and is used for choosing actions like Camera/Gallery. Both are created using `UIAlertController`, but with different styles.*

![Action Sheet Example](./actionsheet.png)

---

<a name="ibaction-vs-iboutlet"></a>

### IBAction vs IBOutlet

#### What is IBOutlet?

**IBOutlet** (Interface Builder Outlet) is a connection that links a UI component from Storyboard to Swift code. It is used to access and modify UI elements programmatically (like labels, buttons, text fields, etc.).

**Example Uses of IBOutlet:**
- Change text of a label
- Read value from a text field
- Hide/show UI elements

**Syntax Example:**

```swift
@IBOutlet weak var nameLabel: UILabel!
```

#### What is IBAction?

**IBAction** (Interface Builder Action) is used to connect UI events (like button clicks) from the Storyboard to a function in Swift. It is triggered when the user interacts with the UI.

**Example Uses of IBAction:**
- Button click
- Slider value change
- Switch toggle

**Syntax Example:**

```swift
@IBAction func submitButton(_ sender: UIButton) {
    // code to handle button click
}
```

#### Difference Table

| Feature | IBOutlet | IBAction |
|---------|----------|----------|
| **Purpose** | To reference a UI element in code | To handle an event triggered by UI |
| **Type** | Variable/property | Function/method |
| **Used For** | Reading & modifying UI data | Responding to user interaction |
| **Connected From** | UI component → Code | UI event (Button/Slider) → Code |

#### Combined Example

```swift
import UIKit

class ViewController: UIViewController {

    @IBOutlet weak var nameField: UITextField!     // IBOutlet
    @IBOutlet weak var resultLabel: UILabel!       // IBOutlet
    
    @IBAction func submitButton(_ sender: UIButton) {  // IBAction
        resultLabel.text = "Hello, \(nameField.text!)"
    }
}
```

**Explanation:**
- `nameField` and `resultLabel` are connected from UI to code using IBOutlet
- `submitButton()` is connected to a button using IBAction and updates the label when clicked

#### Exam Definition

> *IBOutlet is used to connect UI elements (like labels or text fields) to Swift code so they can be accessed or edited. IBAction connects UI events (like button clicks) to a function in Swift. IBOutlet is a variable, whereas IBAction is a function triggered by user interaction.*

---

## 🧭 Navigation

### UINavigationController

#### What is UINavigationController?

A **UINavigationController** is a special controller in iOS that manages the navigation between multiple screens (View Controllers) using a stack-based system. It lets users move forward (push) to a new screen and go back (pop) automatically with a back button.

#### Why Use UINavigationController?

- To move between multiple screens easily
- Automatically shows a navigation bar and back button
- Maintains the history of screens using a stack (push & pop)
- Used in most apps with hierarchical navigation (Settings, Contacts, Mail, etc.)

#### How It Works (Push & Pop)

| Action | Meaning | Example |
|--------|---------|---------|
| **Push** | Go to next screen | Open Profile from Home |
| **Pop** | Go back to previous screen | Back to Home from Profile |

#### Navigation Stack Diagram

```
Top of Stack → Profile Screen (Current)
               Home Screen
Bottom →       Main App Root
```

#### Code Examples

**Push to Next Screen:**

```swift
// Inside a button action
let nextVC = storyboard?.instantiateViewController(withIdentifier: "ProfileVC") as! ProfileVC
self.navigationController?.pushViewController(nextVC, animated: true)
```

**Pop Back to Previous Screen:**

```swift
self.navigationController?.popViewController(animated: true)
```

#### In Storyboard

1. Select the first View Controller
2. Go to **Editor → Embed In → Navigation Controller**
3. Drag another View Controller and make a **Show (Push)** segue

#### Where It Is Commonly Used

| App | Navigation Example |
|-----|-------------------|
| **Settings App** | Settings → Display → Brightness |
| **Contacts** | List → Person Details |
| **Shopping** | Home → Product → Cart |

#### Exam Definition

> *UINavigationController manages navigation between multiple screens using a stack mechanism (push and pop). It displays a navigation bar with a back button automatically and is used to build hierarchical screen flows such as in Contacts, Settings, or Shopping apps.*

---

## 📋 Chapter 3: Protocols, Delegates & TableView

### Protocols and Delegates

#### What is a Protocol?

A **Protocol** in iOS is like a blueprint that defines a set of methods or properties that a class must implement. It does not provide implementation, only the method structure.

**Example:**

```swift
protocol MessageDelegate {
    func sendMessage(_ text: String)
}
```

#### What is a Delegate?

A **Delegate** is an object that implements a protocol and performs tasks on behalf of another object. Delegation helps one class communicate with another without a strong connection, improving modularity and reusability.

> **In short:** Protocol = Rules, Delegate = Follower who implements the rules

#### Why Use Delegates?

- To send data between screens or classes
- To handle UI actions (like TableView, TextField, TextView)
- To reduce tight coupling between classes

#### Real Example: Sending Data Back Using Delegate

**Step 1: Create Protocol**

```swift
protocol DataPassingDelegate {
    func passData(message: String)
}
```

**Step 2: Declare a Delegate Variable in Second Screen**

```swift
class SecondVC: UIViewController {
    var delegate: DataPassingDelegate?
    
    @IBAction func sendBack(_ sender: UIButton) {
        delegate?.passData(message: "Hello from Second VC!")
        self.dismiss(animated: true)
    }
}
```

**Step 3: Adopt and Implement Protocol in First Screen**

```swift
class FirstVC: UIViewController, DataPassingDelegate {

    @IBOutlet weak var messageLabel: UILabel!
    
    func passData(message: String) {
        messageLabel.text = message
    }

    @IBAction func goToSecondVC(_ sender: Any) {
        let vc = storyboard?.instantiateViewController(withIdentifier: "SecondVC") as! SecondVC
        vc.delegate = self     // Assign delegate
        present(vc, animated: true)
    }
}
```

#### Simple Practical Explanation

- **SecondVC** sends data
- **FirstVC** receives data because it implements the protocol and becomes the delegate
- `.delegate = self` makes FirstVC responsible to follow the protocol

#### Examples Where iOS Uses Delegates

| UI Component | Delegate Used For |
|--------------|-------------------|
| **UITableView** | Selecting rows, loading data |
| **UITextField** | Handling return key, editing |
| **UITextView** | Tracking text changes |
| **UIImagePicker** | Selecting camera/gallery images |

#### Exam Definition

> *A Protocol defines a set of rules (methods) without implementation, while a Delegate is an object that implements these rules to perform tasks on behalf of another object. Delegation is used to communicate between classes, reducing coupling. It is commonly used in UITableView, UITextField, and passing data between screens.*

---

## 🏛️ MVC Design Pattern

### What is MVC?

**MVC** stands for **Model–View–Controller**, a widely used architecture in iOS that separates data (Model), user interface (View), and business logic (Controller). It helps keep code organized, reusable, and easy to maintain.

### Components of MVC

#### 1️⃣ Model

Represents **data and business logic** of the application.

**Contains:**
- Data structures (e.g., User, Product)
- Database logic (Core Data, JSON models)
- API services or calculations

**Example (Swift Model):**

```swift
struct Student {
    var name: String
    var mark: Int
}
```

#### 2️⃣ View

Contains everything **visible to the user**.

- Created with Storyboard, XIB files, AutoLayout, UIKit elements (labels, buttons)
- Does not contain logic

**Example:** A label, button, or table cell designed in Storyboard.

#### 3️⃣ Controller

**Connects View and Model**.

- Handles user interactions
- Receives data
- Updates UI
- Subclasses like: `UIViewController`, `UITableViewController`

**Example Controller Code:**

```swift
class ViewController: UIViewController {

    @IBOutlet weak var nameLabel: UILabel!
    var student = Student(name: "John", mark: 90)

    override func viewDidLoad() {
        super.viewDidLoad()
        nameLabel.text = student.name   // Controller updating View using Model
    }
}
```

### How MVC Works (Flow)

```
User interacts with View (Button press)
        ↓
Controller receives input
        ↓
Controller updates Model or fetches data
        ↓
Model changes data
        ↓
Controller updates View with new data
```

### Advantages of MVC

- ✅ Clean separation of concerns (UI vs Logic vs Data)
- ✅ Easy to test and debug
- ✅ UI can be redesigned without changing logic
- ✅ Better collaboration in large teams (UI devs vs backend devs)

### MVC Diagram

```
┌─────────────┐
│    Model    │  (Data & Logic)
└──────┬──────┘
       │
       │ updates
       ↓
┌─────────────┐      user action      ┌─────────────┐
│ Controller  │ ←─────────────────────│    View     │
│  (Logic)    │───────────────────────→│    (UI)     │
└─────────────┘      updates UI       └─────────────┘
```

### Exam Definition

> *MVC separates an app into Model (data), View (UI), and Controller (logic). The Controller connects the View and Model and updates the UI when data changes. MVC improves code reusability, maintainability, and organization in iOS apps.*

---

### Implementing Contact List Using UITableView

#### Introduction

`UITableView` is a scrolling list used to display data in rows. To build a contact list, we use a TableView to show names, and when a user selects a row, we can show more details.

#### Steps to Implement Contact List

**Step 1: Design UI in Storyboard**

- Drag a `UITableView` to the ViewController
- Add Prototype Cell and set its Identifier (e.g., `"cell"`)
- Connect the UITableView to the IBOutlet

```swift
@IBOutlet weak var tableView: UITableView!
```

**Step 2: Prepare Data (Array of Contacts)**

```swift
let contacts = ["Rahul", "Akhil", "John", "Meera", "Sandra"]
```

**Step 3: Set DataSource & Delegate**

Make the ViewController conform to:

```swift
class ViewController: UIViewController, UITableViewDataSource, UITableViewDelegate {
```

**Step 4: Implement Required TableView Methods**

```swift
// Number of rows
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return contacts.count
}

// Display cell data
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath)
    cell.textLabel?.text = contacts[indexPath.row]
    return cell
}
```

**Step 5: Handle Row Selection**

```swift
func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
    print("Selected Contact: \(contacts[indexPath.row])")
}
```

**Optional: Show Selected Contact in Label**

```swift
@IBOutlet weak var selectedLabel: UILabel!

func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
    selectedLabel.text = "You Selected: \(contacts[indexPath.row])"
}
```

#### Flow Diagram

```
User taps a row
        ↓
didSelectRowAt() triggered
        ↓
App shows selected contact name or moves to details screen
```

#### Exam Definition

> *UITableView displays a list of contacts using `UITableViewDataSource` and `UITableViewDelegate`. Contacts are stored in an array, displayed in table cells using `cellForRowAt()`, and selection is handled using `didSelectRowAt()`.*

---

### DataSource vs Delegate in UITableView

#### Introduction

`UITableView` uses two separate protocols to work properly:
- **UITableViewDataSource**
- **UITableViewDelegate**

These protocols help divide responsibilities:
- ✔️ DataSource handles **data**
- ✔️ Delegate handles **UI behavior and actions**

#### UITableViewDataSource

**Purpose:** Provides data for the table view, including number of rows and how each cell is displayed.

**Important Methods:**

```swift
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int
```

```swift
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell
```

**Responsibilities:**
- Number of rows
- Creating and populating cells with data

#### UITableViewDelegate

**Purpose:** Handles user interactions and appearance of the table view.

**Important Methods:**

```swift
func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath)
```

```swift
func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat
```

**Responsibilities:**
- Handling row selection
- Customizing cell height
- Editing actions (delete, insert)
- Section headers/footers

#### Key Differences

| Feature | UITableViewDataSource | UITableViewDelegate |
|---------|----------------------|---------------------|
| **Role** | Provides data | Controls behavior & appearance |
| **Type of Methods** | Must be implemented | Optional |
| **Controls** | Rows & cell content | Selection, height, actions |
| **Example** | Display text in cells | Change color on selection |
| **Without this** | Table is empty | Table cannot react to user |

#### Exam Definition

> *`UITableViewDataSource` supplies the data for the table by defining how many rows and what each cell displays. `UITableViewDelegate` handles the appearance and user interaction such as row selection, row height, and editing. DataSource is mandatory, while Delegate is optional and used to customize behavior.*

---

### TableView Cell Lifecycle & Reuse Mechanism

#### Introduction

UITableView displays many repeating rows. To improve performance and memory usage, iOS does not create a new cell for every row. Instead, it reuses existing cells using a mechanism called **Cell Reuse**.

#### Why Reuse?

If a table has 500 rows, creating 500 cells will slow the app. Instead, only a few visible cells (around 10–15) are created. When a cell scrolls off the screen, it is recycled and reused for new data.

#### How Cell Reuse Works

1. Create a Prototype Cell in Storyboard or register one manually
2. Give the cell a **Reuse Identifier** (e.g., `"cell"`)
3. In `cellForRowAt()`, request a reusable cell using:

```swift
tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath)
```

4. UITableView recycles old cells instead of creating new ones

#### Example Code

```swift
func tableView(_ tableView: UITableView,
               cellForRowAt indexPath: IndexPath) -> UITableViewCell {

    let cell = tableView.dequeueReusableCell(withIdentifier: "cell",
                                             for: indexPath)
    cell.textLabel?.text = contacts[indexPath.row]
    return cell
}
```

> `dequeueReusableCell` ensures reuse automatically.

#### Cell Lifecycle Flow

```
User scrolls → Cell goes off-screen → OS puts cell in reuse queue →
dequeueReusableCell() → Cell is reused for new content
```

#### Advantages of Cell Reuse

| Benefit | Explanation |
|---------|-------------|
| **Fast scrolling** | Updates content without creating new objects |
| **Saves memory** | Only small number of cells exist in memory |
| **Improves performance** | Reduces CPU load and increases efficiency |

#### Exam Definition

> *UITableView uses a cell reuse mechanism to recycle off-screen cells instead of creating new ones for every row. By using `dequeueReusableCell(withIdentifier:)`, only a limited number of cells are kept in memory, resulting in faster scrolling, reduced memory usage, and improved performance.*

---

### Prototype Cells in UITableView

#### What is a Prototype Cell?

A **Prototype Cell** is a pre-designed table cell created inside Storyboard, used as a template to display repeated data in a UITableView. It allows developers to customize how each row looks without writing code for UI design.

Prototype cells are used only when using Storyboard/TableView in Storyboard (not created by code).

#### Why Use Prototype Cells?

- To design custom row layouts visually
- To add UI elements like:
  - Images (e.g., contact photo)
  - Labels (name, phone number)
  - Buttons (call, delete)
- To avoid creating custom cells completely by code

#### How to Use a Prototype Cell (Steps)

**In Storyboard:**

1. Drag a UITableView into your ViewController
2. Select the table view and set:
   - **Prototype Cells = 1** (or more if needed)
3. Select the cell → set a **Reuse Identifier** (e.g., `"contactCell"`)
4. Add UI components inside the cell (e.g., UIImageView + UILabel)
5. Optional: Create a UITableViewCell subclass and connect outlets

**Code to Use Prototype Cell:**

```swift
func tableView(_ tableView: UITableView,
               cellForRowAt indexPath: IndexPath) -> UITableViewCell {

    let cell = tableView.dequeueReusableCell(withIdentifier: "contactCell",
                                             for: indexPath)

    cell.textLabel?.text = contacts[indexPath.row]
    return cell
}
```

> **Note:** Identifier must match the one set in the Storyboard.

#### Prototype Cell with Custom Class (Optional)

**Create a cell class:**

```swift
class ContactCell: UITableViewCell {
    @IBOutlet weak var nameLabel: UILabel!
    @IBOutlet weak var photoView: UIImageView!
}
```

**Then in code:**

```swift
let cell = tableView.dequeueReusableCell(withIdentifier: "contactCell",
                                         for: indexPath) as! ContactCell
cell.nameLabel.text = contacts[indexPath.row]
```

#### Advantages of Prototype Cells

| Benefit | Explanation |
|---------|-------------|
| **Custom UI design** | Easily add image, labels, buttons |
| **Saves time** | No need to build layout using code |
| **Works with Reuse mechanism** | Improves performance |
| **Supports multiple templates** | e.g., message cell + call cell |

#### Exam Definition

> *Prototype Cells are pre-designed table cells in Storyboard used as templates for repeated rows in UITableView. They allow adding custom UI components like images and labels visually. Each prototype cell must have a Reuse Identifier and can be connected to a custom class. These cells support reuse and improve performance.*

---

## 📝 Quick Revision Summary

### Chapter 1 Key Points

| Topic | One-Line Summary |
|-------|------------------|
| **Info.plist** | Configuration file storing app metadata and permissions |
| **Interface Builder** | Visual UI design tool with drag-and-drop features |
| **Storyboard** | Visual representation of all app screens and transitions |
| **iOS Layers** | 4 layers: Cocoa Touch, Media, Core Services, Core OS |
| **Touches** | Raw finger interactions tracked with touch methods |
| **Gestures** | High-level patterns (tap, swipe) using UIGestureRecognizer |
| **Main Thread** | Handles UI updates and user interactions |
| **Global Thread** | Performs heavy background tasks |
| **Cocoa Touch** | Top iOS layer providing UIKit and interaction frameworks |

### Chapter 2 Key Points

| Topic | One-Line Summary |
|-------|------------------|
| **UITextField** | Single-line text input for short data like usernames |
| **UITextView** | Multi-line text input with scrolling for long content |
| **Alert** | Center popup for important messages/warnings |
| **Action Sheet** | Bottom sheet for choosing between multiple actions |
| **IBOutlet** | Connects UI elements to code as properties |
| **IBAction** | Connects UI events to functions in code |
| **UISlider** | Continuous value selection with draggable thumb |
| **UISwitch** | Binary ON/OFF toggle control |
| **UIStepper** | Increment/decrement buttons for numeric values |
| **UINavigationController** | Stack-based navigation between screens with back button |

### Chapter 3 Key Points

| Topic | One-Line Summary |
|-------|------------------|
| **Protocol** | Blueprint defining method signatures without implementation |
| **Delegate** | Object implementing protocol to perform tasks for another object |
| **MVC** | Separates app into Model (data), View (UI), Controller (logic) |

---

