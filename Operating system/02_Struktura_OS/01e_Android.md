---
aliases: [Android, Android architektura]
tags: [os]
---

# ANDROID

## ANDROID

The **Android** operating system was designed by the **Open Handset Alliance** (led primarily by Google) and was developed for Android smartphones and tablet computers.

Whereas iOS is designed to run on Apple mobile devices and is close-sourced, Android runs on a variety of mobile platforms and is ==open-sourced==, partly explaining its rapid rise in popularity.

### Struktura

The structure of Android appears in Figure 2.18.

Android is similar to iOS in that it is a ==layered stack of software== that provides a rich set of frameworks for developing mobile applications. At the bottom of this software stack is the **Linux kernel**, although it has been modified by Google and is currently outside the normal distribution of Linux releases.

Linux is used primarily for process, memory, and device-driver support for hardware and has been expanded to include power management.

### Runtime a vývoj aplikací

The Android runtime environment includes a core set of libraries as well as the **Dalvik virtual machine**.

Software designers for Android devices develop applications in the **Java** language. However, rather than using the standard Java API, Google has designed a separate **Android API** for Java development.

The Java class files are first compiled to Java bytecode and then translated into an executable file that runs on the Dalvik virtual machine. The Dalvik virtual machine was designed for Android and is optimized for mobile devices with limited memory and CPU processing capabilities.

### Knihovny

The set of libraries available for Android applications includes frameworks for developing web browsers (**webkit**), database support (**SQLite**), and multimedia.

The **libc** library is similar to the standard C library but is much smaller and has been designed for the slower CPUs that characterize mobile devices.

![[bd46721679550f458057b2f42f477625bea0e47b994c94599dd5125e6abbd76a.jpg]]

- https://www.theandroid-mania.com/android-architecture/

---

**Struktura OS:** [[01_STRUKTURA_OPERAČNÍCH_SYSTÉMŮ (1)|Architektury OS]] · [[01a_Windows|Windows]] · [[01b_Unix|UNIX]] · [[01c_Linux|Linux]] · [[01d_Apple|Apple]] · [[01e_Android|Android]]
