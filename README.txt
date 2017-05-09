# ECE387-Final-Camera
# Author: Grant P
# Based on code from https://github.com/ComputerNerd/ov7670-no-ram-arduino-uno
		 and https://github.com/ComputerNerd/simpleFrameGrabber
# 10 May 2017

Uses an OV7670 non-FIFO VGA camera module to take a picture on the press of a button, and 
save the image as a JPEG on a MicroSD card.

In this configuration, the Arduino requires a USB connection to power itself and the circuit.

The Camera Code requires the following gcc libraries:
	stdint.h
	avr/io.h
	avr/interrupt.h
	util.twi.h
	util.delay.h
	avr/pgmspace.h

The Frame Grabber requires the following gcc libraries:
	stdio.h
	string.h
	unistd.h
	fcntl.h
	errno.h
	termios.h
	stdint.h
	linux/serial.h (if on a Linux OS)
	sys/ioctl.h
	SDL/SDL.h  (Must have SDL 1 installed)
	jpeglib.h
	setjmp.h
	
Pin Connections:
	MicroSD Adaptor <->  Uno (Incomplete, do not attach.  For future reference only)
		  CS - D10
		 SCK - D13
		MOSI - D11***
		MISO - D12
		 VCC - 5V
		 GND - GND

	OV7670 <-> Uno
			  3v3 - 3v3
			  GND - GND
			 SIOC - A5
		   SIOC - 10 kOhm - 3v3
			 SIOD - A4
		   SIOD - 10 kOhm - 3v3
			VSYNC - D3
		  HREF - Floating, or GND
			 PCLK - D2
		   XCLK - 4.7 kOhm - D11
		   XCLK - 4.7 kOhm - GND
			   D7 - D7
			   D6 - D6
			   D5 - D5
			   D4 - A4
			   D3 - A3
			   D2 - A2
			   D1 - A1
			   D0 - A0
			RESET - 3v3
			 PWDN - GND

	Button <-> Uno
		1 - 10 kOhm - GND
		1 - D9
		2 - 5V
	
Instructions to run from ~bash terminal, tested on Kubuntu 17.04
	cd to Camera_Code/
		make clean
		make hex
		make writeflash
		
	cd to Frame_Grabber/
		./build
		Now, there are several options for the executable:
			./qqvga
				Lowest quality, fastest transfer
			./qvga
				Medium quality and transfer speed
			./vga
				Highest quality, slowest transfer
		If the command fails and prints "no such file or directory", type ls /dev.  If your Arduino is
		connected correctly, one of the items displayed should say "ttyACM*" where "*" is some number.
		Go back to whichever script you are using, and open it in a text editor.  Where it says
		"/dev/ttyACM0", replace "0" with whichever port was displayed.  Run the command again to execute.
		
	Once upload is complete, the camera is ready.  Press the button to take a picture.
