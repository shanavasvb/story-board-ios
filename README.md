# story-board-ios

---

###  **Most Repeated & Important Questions (Chapter 1)**

1. **What is Info.plist? Why is it used in iOS applications?**
2. **Briefly explain Interface Builder and Storyboard in iOS.**
3. **Differentiate between touches and gestures in iOS.**
4. **Differentiate between Global thread and Main thread.**
5. **Explain the architecture of iOS (layers).**
6. **What is the Cocoa Touch framework? Give examples.**

---

💯 **Tip:**
If you study only these 6, you can answer **any short + most long questions** from Unit 1.

### 📌 **What is Info.plist? Why is it used in iOS applications?**

**Info.plist (Information Property List)** is a configuration file used in every iOS application.
It stores key-value information that tells the **iOS system how the app should run**.

### ✔️ **Purpose/Uses of Info.plist**

* Defines **basic app information** (App name, version, bundle identifier).
* Stores **permissions** (Camera, Location, Microphone, Bluetooth, etc.).
* Used to configure **launch screen, app icons, supported device orientations**, etc.
* Read by the system **before the app launches** to set up required rules.

### 📝 **Examples of data stored in Info.plist**

| Key                        | Purpose                       |
| -------------------------- | ----------------------------- |
| `CFBundleDisplayName`      | App name shown on device      |
| `NSCameraUsageDescription` | Ask permission for camera     |
| `UILaunchStoryboardName`   | Sets launch screen storyboard |

👉 **In short:**
**Info.plist is like the identity + permissions rule book of an iOS app.**
Without correct settings in it, an app may not run or access device features.

---

If you want, I can provide a **2-line version for exam**. 😃
