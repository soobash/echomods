# Idea: doing a 15Msps ADC for RPi0

Some inspiration [from earlier](/croaker/notes_RPi0.md)

## BOM

* CA3306E
* CMOS 74HC4050 -- 74HC4050 Hex Non-Inverting Buffer (http://fr.hobbytronics.co.uk/74hc4050)

* 2x 0.1µF
* 1x 0.2µF
* 1x 10µF

## Some links, working with BiVi ?

* http://dangerousprototypes.com/blog/2015/04/11/app-note-improving-adc-resolution-by-oversampling-and-averaging/
* https://edwardmallon.wordpress.com/2017/02/27/enhancing-arduinos-adc-resolution-by-dithering-oversampling/

* https://digibird1.wordpress.com/raspberry-pi-as-an-oscilloscope-10-msps/ -- [see PDF](/goblin/pi0/PiScopeDigibird.pdf).
* http://www.instructables.com/id/PiScope-Raspberry-Pi-based-Oscilloscope/  -- [see PDF](/goblin/pi0/PiScope.pdf).



* Other level shifter? http://www.nxp.com/documents/data_sheet/P82B96.pdf

## Step 2 : SMD? 

Given RPi0 capabilities in terms of [GPIOs](/croaker/notes_RPi0.md) - why not push it to 20Msps, 8 bits, for the cape?



## Other ideas

wiringPi is a PIN based GPIO library, however it does have a couple of functions that let you read up to 8 bits at a time from 2 different sets of pin (which overlap). If you're on a Pi v1 then digitalReadByte() reads in the 32-bits of the first register and does some bit fiddling to give you an 8-bit value based on the inputs of the first 8 usable GPIO pins. On a 40-pin Pi, you also have digitlaReadByte2() which reads an 8-bit value from 8 consecutive pins which only involves a single shift. See the source code to work out the actual pins. (and there is writeByte too)

* https://www.raspberrypi.org/forums/viewtopic.php?t=175645&p=1122820

Running it and its taking about 0.94 seconds on a v1 Pi @ 900Mhz so that's a little over 10 million digitalWrites per second. I think that's fast enough for you


