Environnement de cross compilation
==================================

Configurer le *host* et le `Raspberry` pour qu'il boot en :ref:`nfs <nfs>`.

Maintenant le but est de développer et compiler directement depuis le *host* et
de pouvoir tester le résultat sur le `Raspberry` via une connection ssh par exemple.

Pour commencer il faut installer l'environnement de cross compilation.

Installation de croostool-ng
----------------------------

Télécharger crosstool-ng_ et l'installer:

.. code-block:: guess

   tar -xvf crosstool-ng-xxxx.tar.bz2
   ./configure
   make
   make install

Ajouter le répertoire bin d'installation dans le *PATH*.

Construction du gcc de cross compilation
----------------------------------------

Pour configurer le futur compilateur pour notre `Raspberry` il suffit de lancer:

.. code-block:: guess

   ct-ng menuconfig

Les options que choisies pour l'environnement ciblé sont les suivantes :

* Path and misc options:

  + *Try features*
  + *Debug crosstool-NG*
  + *Save intermediate steps*
  + *gzip saved steps*
  + *Prefix directory* = path/destination
  + *Number of parallel jobs* = nombre de core + 2
* Target options:

  + *Target Architecture* = arm
  + *Endianness* = Little endian
  + *Bitness* = 32-bit
  + *Architecture level* = armv6zk
  + *Emit assembly for cpu* = arm1176jzf-s
  + *Tune for cpu* = arm1176jzf-s
  + *Use specific FPU* = vfp
  + *Floating point* = hardware (FPU)
  + *Default instruction set mode* = arm
  + *Use EABI*
* Toolchain options:

  + *Tuple's vendor string* = rpi
* Operating system:

  + *Target OS* = linux
  + *Linux kernel version* = 3.6.11
* Binary utilities:

  + *Binary format* = ELF
  + *binutils version* = 2.22
* C compiler:

  + *Show Linaro versions*
  + *C++*
  + *Link libstdc++ statically into gcc binary*
  + *Enable GRAPHITE loop optimisations*
  + *Enable LTO*
  + *Optimize gcc libs for size*
  + *Use __cxa_atexit*
* C-library:

  + *C library* = eglibc
  + *eglibc version* = 2_17

Ensuite il suffit de lancer le build:

.. code-block:: guess

   ct-ng build

.. _crosstool-ng: http://crosstool-ng.org/

Tester le résultat
------------------

Commencer par exporter le répertoire résultat *crosscompile/bin* dans
votre PATH pour pouvoir exécuter sans soucis *arm-rpi-linux-gnueabi-ct-ng-g++*.

Créer un fichier source d'exemple dans le système de fichier du raspberry sur
l'hote.

Un simple helloworld suffira pour tester.

.. code-block:: guess

   arm-rpi-linux-gnueabi-ct-ng-g++ helloworld.cpp
   file a.out
     a.out: ELF 32-bit LSB executable, ARM, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 3.6.11, not stripped    

Et normalement cet exécutable devrait fonctionner sur le `Raspberry`.

