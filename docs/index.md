# Welcome to VRUnited

**VRUnited** is a virtual reality (VR) application developed by the Event Lab (University of Barcelona) that supports multiple people simultaneously interacting in the same shared environment. It serves as a platform for delivering shared virtual experiences, functioning as a customized Metaverse.

The platform has been successfully used for a variety of remote applications, including virtual meetings, conferences, concerts, interactive games (like remote chess), and even professional journalistic interviews. A notable use case involved a two-hour interview for the *Financial Times*, conducted in a virtual restaurant with the interviewer in London and the interviewee in New York (read more about this in our [academic publication](#references)).

## Key Features

VRUnited is designed to meet several crucial requirements for successful collaborative virtual environments:

* **Simultaneous Presence:** Multiple participants can be present in the same virtual space, perceiving the same events from their own unique embodied perspectives.
* **Realistic Embodiment:** Participants are represented by 3D virtual human avatars that closely resemble their real-world appearance. Using state-of-the-art deep learning methods, the system can automatically generate a realistic avatar from just a single frontal RGB image in about 30 minutes.
* **Cross-Platform Body Tracking:** The platform utilizes the [QuickVR library](#references), adapting automatically to the tracking data provided by different VR devices. It tracks head and hand movements using inverse kinematics and can also track feet, fingers, eyes, or facial expressions if the hardware supports it.
* **Object Interaction:** Participants can intuitively interact with virtual objects (such as grabbing and "eating" virtual sushi). The state of these objects is seamlessly synchronized across all clients in the environment.
* **Robust Networking:** VRUnited uses the Photon Network engine to manage client synchronization, ensuring low latency and a persistent, consistent world state across all connected users.

## Cross-Device Compatibility

While VRUnited has been extensively tested on the most common head-mounted displays on the market—such as **Meta Quest**, **Pico**, and **Oculus Rift**—its underlying architecture is highly adaptable. Because QuickVR (and therefore VRUnited) is built on top of the Unity XR Plugin framework, it should natively run on **any device supported by the Unity XR Plugin**, including all OpenXR compatible devices (such as HTC VIVE or Valve Index).

Additionally, while a VR headset is highly recommended for a fully immersive experience, **it is not strictly required**. VRUnited can also be used on a standard PC in **Desktop mode**. This allows users without VR hardware to join and interact in the same shared environment, ensuring accessibility for everyone (though with a reduced level of immersion).

Using the VRUnited SDK, developers can easily expand upon the official distribution to add custom scenarios, avatars, and interactions.

## References

If you want to learn more about the technical details, the development of the platform, and the specific use case, you can read our published papers:

* Oliva, R., Beacco, A., Gallego, J., Gallego Abellan, R., & Slater, M. (2023). **[The Making of a Newspaper Interview in Virtual Reality: Realistic Avatars, Philosophy, and Sushi](https://www.computer.org/csdl/magazine/cg/2023/06/10309197/1RRj4f3COvm)**. *IEEE Computer Graphics and Applications*, 43(6), 117-125.
* Oliva, R., Beacco, A., Navarro, X., & Slater, M. (2022). **[QuickVR: A standard library for virtual embodiment in unity](https://www.frontiersin.org/journals/virtual-reality/articles/10.3389/frvir.2022.937191/full)**. *Frontiers in Virtual Reality*, 3:937191.

---

**Next Steps:** Ready to create your own Metaverse? Check out our [Setup Guide](sections/setupguide/index.md) to download the template and configure your project.