# Asset Management Overview

In VRUnited, adding new content—primarily **Avatars** and **Scenarios** (environments)—is a core part of customizing your Metaverse experience. The platform is designed to be highly flexible, allowing developers to manage and distribute these assets in two distinct ways: **Local Assets** and **Remote Addressables**.

Understanding the difference between these two methods is crucial for optimizing your application's file size, loading times, and update frequency.

## 1. Local Assets (Embedded)

Local assets are integrated directly into your Unity project and compiled along with the application. When you build the `.apk` (or executable), these assets are packed inside it. 

The VRUnited template comes with a set of default local assets (such as the base avatars and the sample scene) to get you started immediately.

* **Pros:** 
    * Simpler to set up.
    * No internet connection is required to load the assets once the app is installed.
    * Content is guaranteed to be available instantly.
* **Cons:** 
    * Every new avatar or scenario increases the final file size of the application.
    * Updating, adding, or removing assets requires building a completely new version of the app and forcing users to download the full update.
* **Best used for:** Core assets that will never change (like basic menus, default avatars, or the main lobby), offline applications, or projects with a small, fixed amount of content.

[Learn how to add Local Assets ->](local_assets/index.md)

## 2. Remote Addressables (Cloud/Server Distribution)

VRUnited supports Unity's **Addressables** system, which allows you to store your heavy assets (like complex avatars or detailed environments) on a remote server or cloud storage. The application only downloads these assets on demand when the user needs them.

* **Pros:**
    * Keeps the initial application download size very small.
    * **Dynamic Updates:** You can add new avatars or scenarios, or modify existing ones, on the server. Users will see the new content the next time they open the app *without* needing to download a new version of the app itself.
* **Cons:**
    * Requires setting up a hosting server (e.g., AWS S3, Google Cloud, or a local server for testing).
    * Users must have an active internet connection to download new content.
    * Slightly more complex initial setup in Unity.
* **Best used for:** Expanding Metaverses, applications that receive frequent content updates, or projects with a massive library of avatars and scenarios that would make a local build too large.

[Learn how to configure Remote Addressables ->](remote_assets/index.md)

---

Choose the methodology that best fits your project's scope, or use a hybrid approach: keep your core experience local and distribute seasonal or heavy content via Addressables!