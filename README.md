# Tesla-Front-Drive-Unit
Open Source Logic board to control the Tesla Model S Front Drive Unit
This board replaces the Tesla OEM control board in the high efficency front drive unit
and enables full control of the inverter and motor using simple analog / digital and CAN communication. Design files in DesignSpark 8 format.

Software may be downladed here:
https://github.com/jsphuebner/stm32-sine/releases

Fully built and tested boards and bare PCBs available here : http://www.evbmw.com/index.php/evbmw-webshop

Support forum : https://openinverter.org/forum/

23/09/17 : Released V1 schematic for the logic board. Untested. Also released pinout for the logic to igbt board interface header and Autocad dxf of the board outline with critical component locations.

02/10/17 : Released V1 design files. Untested. Unproven. Educational use only.

06/11/17 : V1 board bench tested and working well. No in car testing as yet.

29/12/17 : Uploaded V2 design files for small drive unit logic board. Compatible with both front and rear small Tesla drive units.

Just one change :

ULN2003 replaced by NCV8401ADT for driving precharge relay and main contactor following in car testing of the large drive unit.

Happy new year :)

14/08/18 : Following some excellent testing and investigation by a european customer, V3 design files are released. Small changes to component values in the current sensor opamp circuit as well as addition of two filter capacitors in the same. Now running well in vehicle. Also uploaded working parameter file.

18/10/18 : Two customers reported failures of their inverter when using the V2 board. One customer reported they had fixed the issue but then refused to share the details. I have worked with the second customer in Romania on the problems. Here are some details :

Root cause of the drive unit inverter failures discovered and fixed.
NOT caused by overcurrent through the igbts but rather the combination of using 8.8kHz switching frequency through a very low inductance stator and the sudden release of the main contactor on an overcurrent detection. The small drive unit inverter works perfectly at 17.6khz switching frequency and setting tripmode to prechon ensures the pre charge resistor can provide a path back to the battery during release of the main contactor. This was tested to the Nth degree on my recent trip to Romania

Working on a fix for a hardware bug that is limiting power. The tesla current sensors span +/- 1250A over a range of 0-5v with 2.5v representing 0A. Seems Tesla use the EXACT SAME hardware overcurrent detection circuit on their logic board as designed by Johannes. They set trip points at .1V and 4.9V giving a total span of 1200A. (1A=2mV). The component choice in the opamp circuit on the open source board causes a hardware overcurrent event at +850A regardless of settings above this value thus limiting power. It was this trip coupled with the above issues relating to main contactor control and switching frequency that lead to inverter deaths.

Identified the hall effect current sensor used in the small drive units as the MLX91209. So at least now if I wreck one they only cost 3 Euros to replace. A V4 design will be released shortly along with details on how to modify the V2 and V3 boards to avoid this problem. 

28/10/18 : V4 Design files released. Major changes : 

Updated current sensor opamp component values to allow the full +/-1200A swing.

Deleted the encoder polarity jumper as no longer needed.

Added option to fit ESP WiFi module on board (untested)

Added jumper to disable RS232 Transciever (required if using on board wifi)

Latest sourcecode and binaries will available from https://github.com/jsphuebner/stm32-sine

V2 and V3 boards can still be used by changing the following component values : R44,R49 = 62k, R48 = 3k16.

On the web interface set the following two parameters :

PWMFRQ=17.6kHz

Tripmode = Prechon

Working and tested full parameter files will be released shortly.

29/10/18 : V2 Design files and BOM updated for modifications and also incorrect values for temp sensor load resistors in BOM.

Test run with modification : https://www.youtube.com/watch?v=mhGwcPWCbsA

21/01/20 : V6 design files now released. Both fully built and partial built boards available from the EVBMW webshop : https://www.evbmw.com/index.php/evbmw-webshop
Don't want to buy from me and support ongoing development? That's ok as this release also includes the BOM, CPL and Gerber files needed to build your own at JLCPCB : https://jlcpcb.com
