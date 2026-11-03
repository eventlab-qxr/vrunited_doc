# Adding Remote Assets (Addressables)

In VRUnited, Remote Assets are distributed using Unity's Cloud Content Delivery (CCD) system. Unlike Local Assets, which are embedded directly into the application build, Remote Assets are stored on a cloud server and downloaded on-demand when a user requests them. This approach keeps the initial download size of your application small and allows for dynamic content updates without requiring users to install a new version of the app.

## Architecture Overview

The VRUnited remote asset architecture is designed to be highly scalable and relies on two distinct roles:

1. **The Consumer (Main Project):** The core VRUnited application. It acts purely as a consumer. It does not contain the original prefabs or heavy files of the remote assets. Instead, it queries the cloud to discover available content and downloads it dynamically.
2. **The Producers (Secondary Projects):** Separate Unity projects where developers create, configure, and build new custom avatars or environments. Once built, these projects upload their resulting Addressable packages (AssetBundles and catalogs) directly to Unity Cloud.

## Unity Cloud Content Delivery (CCD) Structure

To link the producers and the consumer, we use Unity CCD. The structure mimics a traditional web server:

* **Project & Environment:** A single Unity Cloud Project and Environment (e.g., `production`) acts as the root directory.
* **Buckets (Sub-projects):** Inside the environment, every producer project creates its own independent "Bucket" (e.g., `avatars`, `restaurant_scene`). This ensures updates from one project do not overwrite assets from another.
* **Platform Paths:** Within each bucket, assets are separated by platform using dynamic paths (e.g., `StandaloneWindows64/` or `Android/`).
