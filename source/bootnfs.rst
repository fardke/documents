.. _nfs:

Utiliser un système de fichier en nfs
=====================================

Installer raspbian
------------------

Pour booter en nfs je suppose que :ref:`raspbian <raspbianInstall>` est installé
sur le raspberry.

Installer un serveur nfs sur le host
------------------------------------

Pour partager le système de fichier du `Raspberry` il faut installer
un serveur nfs sur le pc hôte : 

.. code-block:: guess

   sudo apt-get install nfs-kernel-server nfs-common

Ensuite il faut modifier le fichier /etc/exports sur le host pour
exporter le répertoire qui contiendra par la suite le système de fichier.

Récupérer le système de fichier existant
----------------------------------------

Après avoir démarré le `Raspberry` il faut monter le répertoire de l'hôte
en nfs. Puis il faut copier l'ensemble du système dans ce répertoire
(ici on suppose que le fichier partagé est monté sous */mnt/*

.. code-block:: guess

   cp -axv /. /mnt/.
   cp -axv /dev/. /mnt/dev/.

.. note:: la première étape est très longue !

Il faut modifier le nouveau fichier *fstab* (dans /mnt/etc/fstab) pour
ne plus monter /dev/mmcblk0p2 dans / (commenter la ligne).

Changer directive de boot
-------------------------

Une fois le système de fichiers copié sur l'hôte il faut modifier la
séquence de boot pour demander au `Raspberry` de démarrer en nfs et
non sur une partition interne. 

Il faut donc éditer le fichier /boot/cmdline.txt:

.. code-block:: guess

   # a modifier
   root=/dev/nfs
   rootfstype=nfs

   # a ajouter
   nfsroot=<ipserver>:/chemin/vers/partage,udp,vers=3
   smsc95xx.turbo_mode=N #pas sur que ce soit necessaire...
   ip=dhcp


.. note:: On peut modifier directement /boot/cmdline.txt car /boot est un 
   partition à part (mmcblk0p1) qui sera conservée même quand on bootera
   en nfs.

Il ne reste plus qu'à redémarrer le `Raspberry` et normalement le système
de fichier sera monté en nfs.

