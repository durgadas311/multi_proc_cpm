# MultProcessor CP/M System Simulator

This project is inspired by vintage systems like
the [Molecular Computer]
(http://www.bitsavers.org/pdf/molecularComputer/Molecular_Hardware_Maintenance_Dec82.pdf).
and others.

[General block diagram](doc/BlockDiag.pdf)

Initial bus design:

Bus Ports:

* control/status
* bus owner
* message destination
* data (FIFO)

Send Protocol:

* wait for !BUSY
* output node ID to bus owner register
* if (bus owner != node ID) repeat
* output message to FIFO
* output destination node ID
* set FULL
* wait for !FULL
* release bus

Poll Protocol:

* if (!FULL) return false
* if (destination != node ID) return false
* input message from FIFO
* clear FULL
