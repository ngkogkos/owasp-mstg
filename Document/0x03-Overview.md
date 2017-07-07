# Introduction to the OWASP Mobile Security Testing Guide

The OWASP Mobile Security Testing Guide (MSTG) is an extension of the OWASP Testing Project specifically focusing on the security testing of Android and iOS devices.

The goal of this project is to help people understand the what, why, when, where, and how of testing applications on Android and iOS devices. The project delivers a complete suite of test cases designed to address the OWASP Mobile Top 10, the Mobile App Security Checklist and the Mobile Application Security Verification Standard (MASVS).

## Why Does the World Need a Mobile Application Security Testing Guide?

Every new technology introduces new security risks, and mobile computing is no different. Even though modern mobile operating systems like iOS and Android are arguably more secure by design compared to traditional Desktop operating systems, there's still a lot of things that can go wrong when security is not considered during the mobile app development process. Data storage, inter-app communication, proper usage of cryptographic APIs and secure network communication are only some of the aspects that require careful consideration.

Security concerns in the mobile app space differ from traditional desktop software in some important ways. Firstly, while not many people opt to carry a desktop tower around in their pocket, doing this with a mobile device is decidedly more common. As a consequence, mobile devices are more readily lost and stolen, so adversaries are more likely to get physical access to a device and access any of the data stored.

## Key Areas in Mobile AppSec

Many mobile app pen testers have a background in network and web app penetration testing, and a lot of their knowledge is useful in mobile app testing. Practically every mobile app talks to some kind of backend service, and those services are prone to the same kinds of attacks we all know and love. On the mobile app side however, there is only little attack surface for injection attacks and similar attacks. Here, the main focus shifts to data protection both on the device itself and on the network. The following are some of the key areas in mobile app security.

### Local Data Storage

The protection of sensitive data, such as user credentials and private information, is a key focus in mobile security. Firstly, sensitive data can be unintentionally exposed to other apps running on the same device if operating system mechanisms like IPC are used improperly. Data may also unintentionally leak to cloud storage, backups, or the keyboard cache. Additionally, mobile devices can be lost or stolen more easily compared to other types of devices, so an adversary gaining physical access is a more likely scenario.

From the view of a mobile app, this extra care has to be taken when storing user data, such as using appropriate key storage APIs and taking advantage of hardware-backed security features when available.

On Android in particular, one has to deal with the problem of fragmentation. Not every Android device offers hardware-backed secure storage. Additionally, a large percentage of devices run outdated versions of Android with older API versions. If those versions are to be supported, apps must restrict themselves to older API versions that may lack important security features. When the choice is between better security and locking out a good percentage of the potential user base, odds are in favor of better security.

### Communication with Trusted Endpoints

Mobile devices regularly connect to a variety of networks, including public WiFi networks shared with other (possibly malicious) clients. This creates great opportunities for network-based attacks, from simple packet sniffing to creating a rogue access point and going SSL man-in-the-middle (or even old-school stuff like routing protocol injection - the bad guys aren't picky).

It is crucial to maintain confidentiality and integrity of information exchanged between the mobile app and remote service endpoints. At the very least, a mobile app must set up a secure, encrypted channel for network communication using the TLS protocol with appropriate settings.

### Authentication and Authorization

In most cases, user login to a remote service is an integral part of the overall mobile app architecture. Even though most of the authentication and authorization logic happens at the endpoint, there are also some implementation challenges on the mobile app side. In contrast to web apps, mobile apps often store long-time session tokens that are then unlocked via user-to-device authentication features such as fingerprint scan. While this allows for a better user experience (nobody likes to enter a complex password every time they start an app), it also introduces additional complexity and the concrete implementation has a lot of room for errors.

Mobile app architectures also increasingly incorporate authorization frameworks such as OAuth2, delegating authentication to a separate service or outsourcing the authentication process to an authentication provider. Using OAuth2, even the client-side authentication logic can be "outsourced" to other apps on the same device (e.g. the system browser). Security testers must know the advantages and disadvantages of the different possible architectures.

### Interaction with the Mobile Platform

Mobile operating system architectures differ from that of classical Desktop architectures in important ways. For example, all mobile OSes implement app permission systems that regulate access to specific APIs. They also offer more (Android) or less (iOS) rich inter-process communication facilities that enable apps to exchange signals and data. These platform specific features come with their own set of pitfalls. For example, if IPC APIs are used incorrectly, sensitive data or functionality might be unintentionally exposed to other apps running on the device.

### Code Quality and Exploit Mitigation

"Classical" injection and memory management issues play less of a role on the mobile app side. This is mostly due to the lack of the necessary attack surface: For the most part, mobile apps only interface with the trusted backend service and the UI, so even if a ton of buffer overflow vulnerabilities exist in the app, those vulnerabilities usually don't open up any useful attack vectors. The same can be said for browser exploits such as XSS that are very prevalent in the web world. Of course, there's always exceptions, and XSS is theoretically possible in some cases, but it's very rare to see XSS issues that one can actually exploit for benefit.

All this doesn't mean however that we should let developers get away with writing sloppy code. Following security best practice results in hardened release builds that are resilient against tampering. "Free" security features offered by compilers and mobile SDKs help to increase security and mitigate attacks.

### Anti-Tampering and Anti-Reversing

There are three things you should never bring up in date conversations: Religion, politics and code obfuscation. Many security experts dismiss client-side protections outright. However, the fast is that software protection controls are widely used in the mobile app world, so security testers need ways to deal with them. We also think that there is *some* benefit to be had, as long as the protections are employed with a clear purpose and realistic expectations in mind, and aren't used to *replace* security controls.

## The OWASP Mobile AppSec Verification Standard, Checklist and Testing Guide

This guide belongs to a set of three closely related mobile application security documents. All three documents map to the same basic set of security requirements. Depending on the context, they can be used stand-alone or in combination to achieve different objectives:

- The **Mobile Application Security Verification Standard (MASVS):** A standard that defines a mobile app security model and lists generic security requirements for mobile apps. It can be used by architects, developers, testers, security professionals, and consumers to define what a secure mobile application is.
- The **Mobile Security Testing Guide (MSTG):** A manual for testing the security of mobile apps. It provides verification instructions for the requirements defined in the MASVS along with operating-system-specific best practices (currently for Android and iOS). The MSTG helps ensure completeness and consistency of mobile app security testing. It is also useful as a standalone learning resource and reference guide for mobile application security testers.
- The **Mobile App Security Checklist:** A checklist for tracking compliance against the MASVS during practical assessments. The list conveniently links to the MSTG test case for each requirement, making mobile penetration app testing a breeze.

![Document Overview](Images/Chapters/0x03/owasp-mobile-overview.jpg)

For example, the MASVS requirements could be used in the planning and architecture design stages, while the checklist and testing guide may serve as a baseline for manual security testing or as a template for automated security tests during or after development. In the next chapter, we'll describe how the checklist and guide can be practically applied during a mobile application penetration test.

## Organization of the Mobile Security Testing Guide

All requirements specified in the MASVS are described in technical detail in the testing guide. The main sections of the MSTG are explained briefly in this chapter.

The guide is organized as follows:

- In the general testing guide (the following few chapters), we present the mobile app security testing methodology, and talk about general vulnerability analysis techniques as they apply to mobile application security.

- The Android Testing Guide covers the everything specific to the Android platform, including security basics, security test cases, and reverse engineering and tampering techniques and preventions.

- The iOS Testing Guide Testing Guide covers everything specific to iOS, including an overview of the iOS OS, security testing, reverse engineering and anti-reversing.

- The appendix presents additional technical test cases that are OS-independent, such as authentication and session management, network communications and cryptography. We also include a methodology for assessing software protection schemes.
