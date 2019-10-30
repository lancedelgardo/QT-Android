Installation on a Xubuntu 18.04
Installation works on Physicle Device and VirtualBox

First update your Xubuntu on latest Version:
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade

VirtualBox

Wenn VirtualBox verwendet wird. Gemeinsamen Ordner anlegen:

Virtualbox Reiter "Geräte" -> Gasterweiterung einlegen

In VBox Maschinen Settings Ordner anlegen.
In virtueller Umgebung:

 sudo adduser <User> vboxsf

[Bearbeiten] Synaptics

sudo apt-get install synaptic #synaptics install
sudo apt-get install apt-xapian-index  #schnellsuche synaptics
sudo update-apt-xapian-index -vf 	# filter

[Bearbeiten] Download / Installation Qt

https://download.qt.io/archive/qt/ #QT mit Android Treiber
Version wählen und runterladen. Bei Installation benötigte Punkte auswählen.
[Bearbeiten] OpenJDK Installation

sudo apt-get install openjdk-8-jre
sudo apt-get install openjdk-8-jdk openjdk-8-demo openjdk-8-doc openjdk-8-jre-headless openjdk-8-source

[Bearbeiten] Android Studio

https://developer.android.com/studio #Android Studio
1. Entpacken
2. In Ordner "bin" "./studio.sh" um Installation bzw. später das Programm zu starten
3. Installations Ordner für SDK merken!
4. Nach installation öffnet sich Android Studio
5. Recht unten auf Settings und SDK Manager
5.1 Reiter "SDK Platforms" alle nötigen Versionen anklicken
5.2 Reiter "SDK Tools" anklicken:

Android SDK Build-Tools
LLDB
CMake
NDK

Das sind die wichtigsten. Andere Optional
6. Checken ob oben auch die SDK Location passt
7. Apply. Ok. Alles Bestätigen und Installieren
[Bearbeiten] Android Dependencies für QT

sudo apt-get install libstdc++6:i386 libgcc1:i386 zlib1g:i386 libncurses5:i386
sudo apt-get install libsdl1.2debian:i386

[Bearbeiten] Qt Pakete

sudo apt-get install -y qt5-default qtmultimedia5-examples libqt5designer5 clang-8 clang libclang-8-dev qt5-doc qt5-doc-html lldb liblldb-6.0-dev build-essential

[Bearbeiten] Qt Konfigurieren

Tools -> Options -> Devices -> Android:
Suchpfade für JDK, SDK und NDK eingeben

JDK (Beispiel) "/usr/lib/jvm/java-8-openjdk-amd64"
SDK (Beispiel) "/home/dev/Android/Sdk"
NDK (Beispiel) "/home/dev/Android/Sdk/ndk-bundle"

Apply -> Ok -> Nochmal Settings Öffnen und schauen ob bei Kits Android Kits vorhanden sind.

Test: Example -> "Bluetooth Low Energy Heart Rate Game" aufrufen
[Bearbeiten] Fehlermeldungen

- cannot find -lc++
Hier wird wahrscheinlich falsch gelinkt
"Show Output" aufrufen
Beispielmeldung: /home/dev/Android/Sdk/ndk-bundle/toolchains/aarch64-linux-android-4.9/prebuilt/linux-x86_64/lib/gcc/aarch64-linux-android/4.9.x/../../../../aarch64-linux-android/bin/ld: cannot find -lc++
Über diesem Pfad im Output ist der Pfad/Datei wo er nix findet.
"/home/dev/Android/Sdk/ndk-bundle/sources/cxx-stl/llvm-libc++/libs/arm64-v8a/libc++.so.21"

Im Terminal auf oberen Ordner gehen

ls -n

Hier sollten ganz viele libc++.a.XX Dateien vorhanden sein

Mit dem befehl

ln -s libc++.so.XX libc++.so

verlinkt man die von QT gesuchte Datei mit einer vorhandenen.

Bis jetzt war es egal welche versionsnummer man hergenommen hat.

Rebuild sollte jetzt funktionieren 
