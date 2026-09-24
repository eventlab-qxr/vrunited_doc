# VRUnited Template Setup Guide

Follow these steps to download, configure, and build your custom VRUnited project.

## 1. Download VRUnited Template
* Open your preferred Git client (the video demonstrates using TortoiseGit via Windows File Explorer).
* Clone the main repository using the following URL: `git@gitlab.com:vrunited/VRUnited-Main.git`.
* Set your local destination folder (e.g., `C:\Users\[YourUser]\UnityProjects\MyVRUnitedProject`) and complete the clone process.

*(Insert Image 1 here - Timestamp: 00:15 - Git Clone dialog box)*

*(Insert Image 2 here - Timestamp: 00:32 - Download progress window)*

## 2. Open Project in Unity
* Open **Unity Hub** and click **Add** to locate your newly cloned project folder.
* Open the project. The template currently runs on **Unity 6000.0.4f1**.
* Once the editor loads, a prompt may appear asking to "Enable Meta XR Features". Click **Yes**.
* The **Project Setup Tool** window will open with recommended fixes. Click **Fix All** in the bottom right corner to automatically resolve missing configuration settings.

*(Insert Image 3 here - Timestamp: 01:21 - Unity Hub Add Project)*

*(Insert Image 4 here - Timestamp: 02:00 - Enable Meta XR Features prompt)*

*(Insert Image 5 here - Timestamp: 02:24 - Project Setup Tool 'Fix All')*

## 3. Configure Photon (PUN & Voice)
* In Unity, navigate to the top menu and select **Window > Photon Unity Networking > PUN Wizard**, then click **Locate PhotonServerSettings**.
* Open your web browser and sign in to your [Photon Dashboard](https://dashboard.photonengine.com).
* **Create the PUN App:** Click **Create a New App**, set the Photon SDK to **Pun**, enter an Application Name (e.g., `MyVRUnitedProject`), and click **Create**.
* **Create the Voice App:** Click **Create a New App** again, set the Photon SDK to **Voice**, enter an Application Name (e.g., `MyVRUnitedProject_Voice`), and click **Create**.
* From your dashboard, copy the **App ID** of your new PUN application and paste it into the **App Id PUN** field within Unity's `PhotonServerSettings` inspector.
* Copy the **App ID** of your new Voice application and paste it into the **App Id Voice** field in the same inspector.

*(Insert Image 6 here - Timestamp: 02:51 - Unity Menu PUN Wizard)*

*(Insert Image 7 here - Timestamp: 03:21 - Photon Dashboard Create App)*

*(Insert Image 8 here - Timestamp: 04:10 - Unity Inspector PhotonServerSettings)*

## 4. Check VR Configuration
* Go to **Edit > Project Settings** and select **XR Plug-in Management** from the left sidebar.
* Under the **Android** tab, ensure that the **OpenXR** plug-in provider is checked.
* Click on **OpenXR** under the XR Plug-in Management dropdown.
* In the **Interaction Profiles** section, click the `+` icon to add both the **Oculus Touch Controller Profile** and the **Meta Quest Touch Pro Controller Profile**.
* Under the **OpenXR Feature Groups** section, ensure that **Meta XR** is checked and enabled.

*(Insert Image 9 here - Timestamp: 04:54 - XR Plug-in Management OpenXR checked)*

*(Insert Image 10 here - Timestamp: 05:25 - Interaction Profiles list)*

## 5. Switch Profile and Update Player Settings
* Navigate to **File > Build Profiles**.
* Select the **Meta Quest** profile from the list and click **Switch Platform**. Wait for Unity to recompile the scripts and compress assets.
* Go to **Edit > Project Settings** and select **Player**.
* Update the **Company Name** and **Product Name** to match your specific project details.
* Scroll down to **Publishing Settings** and check the **Keystore Manager**. Select your custom keystore file and enter the required **Keystore password** and **Key password**.

*(Insert Image 11 here - Timestamp: 05:58 - Build Profiles Switch Platform)*

*(Insert Image 12 here - Timestamp: 06:22 - Player Settings Company/Product Name)*

*(Insert Image 13 here - Timestamp: 06:50 - Publishing Settings Keystore)*

## 6. Build the Project
* Return to **File > Build Profiles**.
* Click **Build**.
* Create a new folder named `Builds` inside your project directory to keep things organized.
* Name your file (e.g., `MyVRUnitedProject.apk`) and click **Save**.
* If a warning prompt appears stating "Missing Project ID", click **Yes** to continue. 
* Wait for the build process to complete. Your APK is now ready to be deployed to your headset.

*(Insert Image 14 here - Timestamp: 08:14 - Build Profiles Build button)*

*(Insert Image 15 here - Timestamp: 08:26 - Windows Explorer Save APK)*

*(Insert Image 16 here - Timestamp: 08:37 - Missing Project ID warning)*