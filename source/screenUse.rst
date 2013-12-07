Branchement d'un écran LCD sur breadboard
=========================================

Présentation du LCD
-------------------

Connection du LCD
-----------------

La connection du LCD sur la breadboard est très simple il suffit de le pluger.

La mise sous tension est tout aussi simple:

* relier la broche 3V3 du `Raspberry` à la broche VCC de l’écran,
* relier la broche GND du `Raspberry` à la broche GND de l’écran,
* relier une des broche GPIO (dans mon premier test la 18) du `Raspberry`
à la broche LED de l’écran (elle permettra d’allumer une led bleu sur l’écran).

.. image:: _static/lcdConnected.jpg
   :align: center
   :scale: 20%
