A General Reader for LIGGGHTS dump files into
============================================

Contributing Authors
---------------
Stefan Radl 
https://github.com/richti83 (provided basic implementation)

How To Build & Integrate
------------------
Run cmake

>> cmake .

Then, compile

>> make

To clean, to a 

>> make clean

WARNING: after doing "make clean", you MUST creat the "liggghts_reader.xml" file manually. Use the template "TEMPLATE_liggghts_reader.xml" therefore!! Otherwise, the reader will NOT be found in Paraview!

In paraview, go to "Tools / Manage Plugins", and then simply "Load New" (select the *.so file). Press the "+" button in the newly loaded plugin, and activate "Auto Load". The latter will auto-load the plugin every time you load paraview. Hint: if you do not see the new plugin, you have not compiled the plugin for the used ParaView version.
Hint:
In order to compile the reader, it may be necessary to create several symbolic links to libraries of the Qt package. 


Features
----------------------
The Plugin detects the sequence of columns and assigns all known scalars and vectors to the corresponding column in PV. "unknow" values like f_,v_ and c_ are passed as scalar or vectors with their name. Note, a vector must have as last value in the name "[1]" or "[2]" or "[3]" in its name. Also, all three components must be dumped.

use dump command like this:

>> dump		dmp all custom ${dumpstep} post/dump*.liggghts id type x y z vx vy vz fx fy fz radius f_color f_myVec[1] f_myVec[2] f_myVec[3]

the order and count of dump-attributes is detected automatically ! you can add custom fixes by f_<NAME>[item]


Hints / Options
---------------------

You can add a lable to the dumpfile with

>> dump_modify	dmp label ASDFG'

which is passed to Praview as field-data.
For Example if you wish to have the simtime in the dumpfile do like this:

>> variable 	simtime equal step*dt #calculate simtime

>> dump_modify	dmp label ${simtime}  #modify custom dump

>> run		8000 upto every ${dumpstep} "dump_modify	dmp label ${simtime}" #recalculate simtime every dumpstep

--------------------------------------------------------------------------------------
