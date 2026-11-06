---
aliases: [Apple, Apple a Android, macOS architektura, iOS architektura]
tags: [os]
---

# APPLE (MAC OS, iOS)

## APPLE

### MAC OS

The Apple **Mac OS X** operating system uses a ==hybrid structure==. As shown in Figure2.16, it is a layeredsystem. The top layersinclude the **Aqua** user interface (Figure 2.4) and a set of application environments and services. Notably, the **Cocoa** environment specifies an API for the Objective-C programming language, which is used for writing Mac OS X applications.

Below these layers is the **kernel environment**, which consists primarily of the **Mach microkernel** and the **BSD UNIX kernel**.

- **Mach** provides memory management; support for remote procedure calls (RPCs) and interprocess communication (IPC) facilities, including message passing; and thread scheduling.

The **BSD** component provides a BSD command-line interface, support for networking and file systems, and an implementation of POSIX APIs, including Pthreads. In addition to Mach and BSD, the kernel environment provides an **I/O kit** for development of device drivers and dynamically loadable modules (which Mac OS X refers to as kernel extensions). As shown in Figure 2.16, the BSD application environment can make use of BSD facilities directly.

![[95e067ca5d46cd55733468acacba09ed5fc7d5d54af9a8a142c3325496d7133b.png]]

### iOS

- **iOS** is a mobile operating system designed by Apple to run its smartphone, the iPhone, as well as its tablet computer, the iPad.

iOS is structured on the Mac OS X operating system, with added functionality pertinent to mobile devices, but does not directly run Mac OS X applications.

- The structure of iOS appears in Figure
- **CocoaTouch** is an API for Objective-C that provides several frameworks for developing applications that run on iOS devices.

The fundamental difference between Cocoa, mentioned earlier, and Cocoa Touch is that the latter provides support for hardware features unique to mobile devices, such as touch screens. The **media services layer** provides services for graphics, audio, and video. The **core services layer** provides a variety of features, including support for cloud computing and databases.

The bottom layer represents the **core operating system**, which is based on the Mac OS X kernel environment .

![[63f44043e37eaafa022113cb0f7b8e6ea3ae124adba4066fb9de7d7e8074fa06.png]]

---

**Struktura OS:** [[01_STRUKTURA_OPERAČNÍCH_SYSTÉMŮ (1)|Architektury OS]] · [[01a_Windows|Windows]] · [[01b_Unix|UNIX]] · [[01c_Linux|Linux]] · [[01d_Apple|Apple]] · [[01e_Android|Android]]
