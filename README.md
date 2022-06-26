# Patched LWJGL Natives For Optifine  1.7.10 #

So I decided to start Gregtech: New Horizons the other day. The problem was that Optifine is essential to getting good performance out of early (1.7.10) Minecraft.
On any reasonable operating system, this would have worked out just fine, but I have a Mac, which usually means running macOS.
An obscure LWJGL bug that never got fixed in LWJGL2 before it was deprecated means that a forge instance of Minecraft 1.7.10 with optifine will always crash when launching from macOS.

Fortunately, there was hope. A recent effort to build LWJGL2 to run older Minecraft versions on Apple's ARM M1 architecture by [@r58Playz](https://github.com/r58Playz) included a [very promising commit](https://github.com/r58Playz/lwjgl2-m1/commit/2320dbd082fcb0e99d8eaf9fb0ce0f969b8c8ef5) which fixed the error.
Unfortunately, his project was specifically setup to build for the M1 chip's arm64 architecture, meaning that this bug, while fixed on M1, was still left unpatched on Intel macs. This is where I come in to the picture.
Using a few of the general modernization techniques from r58Playz's repo, a lot of slamming my head into the wall and some questionable deletion of legacy code, I got the ancient [lwjgl2](https://github.com/LWJGL/lwjgl) code to compile.
With some more fiddling I figured out how to convert the natives I built into a `natives-osx.jar`, which is a JAR file that contains the native `.dylib`s that interface directly with macOS. After replicating the old crash with my new, freshly compiled libraries, I rebuilt them with the r58Playz patches and Optifine worked!

This repository contains prebuilt lwjgl binaries packaged in a jarfile. You need to use a multi/polyMC json patch to override the default native path for your instance.
