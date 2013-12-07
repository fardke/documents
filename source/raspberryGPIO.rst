Le GPIO du Raspberry Pi
=======================

Présentation du GPIO
--------------------

Le **GPIO**, General Purpose Input/Output, est un ensemble de broches pouvant
être controllées par une couche logicielle. 

Chaque broche à son utilité, et toutes les broches ne sont pas programmables. Sur le GPIO du Raspberry, 17 sont utilisables sur les 26 broches.

Le schéma de ce bus est:

.. image:: _static/gpio.png
   :align: center
   :scale: 50%

Utilisation du T-Cobbler
------------------------

Le principal avantage du **T-Cobbler** est que le schema précédent se retrouve
sur la face visible de la partie connectée à la breadboard du coup plus besoin
du schéma on sait directement à quoi correspond chaque broche :

.. image:: _static/breadboardConnect.jpg
        :align: center
        :scale: 20%

Activer une broche du GPIO
--------------------------
 
Le plus simple pour activer une broche du `Raspberry` rapidement c'est de se connecter en ssh et de lancer ces commandes :

.. code-block:: guess

   $ cd /sys/class/gpio
   $ ls
   export     gpiochip0  unexport
   $ echo 18 > export
   $ ls
   export     gpio18     gpiochip0  unexport
   $ cd gpio18
   $ ls
   active_low  direction   edge        subsystem   uevent      value
   $ echo out > direction
   $ cat value
   0
   $ echo 1 > value

La valeur que je met dans export dépend du numéro de la broche GPIO à
laquelle j'ai connecté le broche LED de l'écran; dans cette exemple 18.

Écrire `out` dans direction pour dire que je veux écrire et non lire.

Je met 1 dans value pour allumer la LED 0 pour l'éteindre. 
