# Configuring Secondary Projects (Producers)

Secondary projects (also known as Producers) are standalone Unity projects where developers create, configure, and compile custom avatars or environments. Once compiled, these assets are uploaded to Unity Cloud Content Delivery (CCD) so the main VRUnited application can download them dynamically.

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto; margin-bottom: 2rem;">
    <iframe src="https://www.youtube.com/embed/TU_YOUTUBE_ID" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
</div>

## 1. Creating the CCD Bucket

To prevent assets from different secondary projects from overwriting each other, you must create an independent Bucket for each producer project.

* Log into the [Unity Cloud Dashboard](https://cloud.unity.com/) and select your main VRUnited project.
* Navigate to **LiveOps > Cloud Content Delivery**.
* In the top-right corner, click **Create Bucket**.
* Name the bucket after the specific content you are producing (e.g., `MyRemoteEnvironments`) and complete the creation process.

![Create Bucket](images/producers_00.png)

## 2. Bucket Initialization

Before configuring Unity, you must initialize the newly created bucket. This step is mandatory. Since the bucket was just created, it does not have any active Releases. Without at least one Release, the Cloud Dashboard will not generate the internal metadata (Project ID, Environment ID, Bucket ID) that you will need later to configure your Addressables.

To force the creation of the first Release and reveal these IDs, you must upload a dummy file:

* In the Dashboard, open the bucket that you created in the previous step. 
* Click the **Upload content using the dashboard** option (or click "Upload Files").
* Drag and drop any small, temporary file from your computer (e.g., a simple text file named `MyDummyFile.txt`) into the drop area.
* Once the upload finishes, a "Create Release" dialog will appear. Click **Submit** to confirm.
* Wait a few seconds for the Dashboard to refresh. You should now see the `Release 1` badge and, more importantly, a new section detailing your **Project ID**, **Environment ID**, and **Bucket ID**.

*(Screenshot suggestion: Timestamp 01:54)*
![Bucket Initialization](images/producers_01.png)

Now that you have access to the necessary IDs, you must clean up the bucket to ensure it remains strictly for your project assets:

* In the dashboard, click **Remove All Entries**.
* Click **Create Release** again and confirm to generate a new empty Release (e.g., `Release 2`). Your bucket is now empty and properly initialized with all its IDs exposed.

## 3. Installing the VRUnited SDK

With the cloud bucket initialized, the next step is to configure your local Unity editor to handle remote asset creation. To do this, you must install the VRUnited SDK, which contains the automatic CCD configuration tools.

* Open your secondary Unity project, i.e., the Addressables producer.
* Navigate to **Window > Package Manager**.
* Click the `+` icon in the top-left corner and select **Add package from git URL...**
* Input the VRUnited SDK repository URL:

```text
https://github.com/vrunited/vrunited.sdk.git
```

* Click **Install** to proceed with the package installation. Wait for the process to finish. 

*(Screenshot suggestion: Timestamp 02:18)*
![Install SDK via Git URL](images/producers_02.png)

## 3. Configuring the Addressables Profile

To ensure files are organized by platform (Windows vs Android) without overwriting each other, VRUnited uses a custom CCD configuration tool.

* From the top menu, go to **VRUnited > CCD Configuration**.
* A custom window will appear. Input the **Project ID**, **Environment ID** (or name, e.g., `production`), and the **Bucket ID** matching the bucket you just created.
* Leave the **Release ID** field empty to automatically target the `latest` version.
* Click **Apply to Addressables Profile**. 

*(Screenshot suggestion: Timestamp 03:11)*
![VRUnited CCD Configuration Window](images/producers_02.png)

This tool automatically overrides your active Addressables Profile to use the `[BuildTarget]` macro, ensuring builds are strictly separated into `StandaloneWindows64/` and `Android/` paths during compilation.

*(Screenshot suggestion: Timestamp 04:06)*
![Addressables Profile Configuration](images/producers_03.png)

## 4. Converting Assets to Addressables

Your custom content (scenes or prefabs) must be marked as Addressables and assigned to a Remote Group.

* Go to **Window > Asset Management > Addressables > Groups**.
* Create a new Group (e.g., `RemoteEnvironments`) or select an existing one.
* In the Inspector for that group, ensure both **Build Path** and **Load Path** are set to **Remote.BuildPath** and **Remote.LoadPath**.

*(Screenshot suggestion: Timestamp 05:21)*
![Group Remote Paths](images/producers_04.png)

* Locate your scene or avatar prefab in the Project window and check the **Addressable** box in its Inspector. 
* Drag and drop the asset into your newly created Remote Group in the Addressables Groups window.
* Simplify its **Address** string (e.g., `RomanPantheon`) as this will be the ID used to load the asset in VRUnited.

*(Screenshot suggestion: Timestamp 07:18)*
![Make Asset Addressable](images/producers_05.png)

## 5. Building the Addressables

You must generate the AssetBundles locally before uploading them.

* In the Addressables Groups window, navigate to **Build > New Build > Default Build Script**.
* Wait for the compilation process to finish. The generated files (catalogs, hashes, and `.bundle` files) are now stored in your local `ServerData/[BuildTarget]` folder.

*(Screenshot suggestion: Timestamp 09:32)*
![Build Addressables](images/producers_06.png)

## 6. Uploading Content to CCD

The final step is to push the generated local files into the cloud bucket using the Unity Gaming Services Command Line Interface (UGS CLI) to properly maintain the platform folder structure.

* Open a terminal or command prompt at the root directory of your Unity project.
* Execute the sync command targeting the root `ServerData` folder, and automatically create a release:

```bash
ugs ccd entries sync ./ServerData --create-release -n "First Upload"