# Arduino_ESP32_IRRemote_Mods
Quick and dirty patch to get standard Arduino (1.8.5) IRRemote running on your ESP32. 

This is by no means the only place that can be used to patch it but is the first I found and edited to make it work.

The section of boarddefs.h that I modified is here below:

<pre>#elif defined(ESP32)
        // No system LED on ESP32, disable blinking by NOT defining BLINKLED

        // avr/interrupt.h is not present
#       undef HAS_AVR_INTERRUPT_H

	// BEGIN - Grrarth@GitHub - 20181213
	// Arduino 1.8.5 (ESP32 Selected) will not compile because it needs 
	// a send pin even though not used due to no IRSend() support
	// Edit (Grrarth@github - 20190530)
        // 68gt500@github reported errors while trying to compile where I did with the 
        // #define format so I have put both lines here and you can comment out
        // the line that doesn't work for you. If it still diesn't work then try
        // something else.
        //
	// Following line won't compile for 68gt500@github:
	//const int SEND_PIN = 0; 
	//
	// Following line won't compile for me:
#       define SEND_PIN 0        
	// END - Grrarth@GitHub - 20181213, 20190530

        // Sending not implemented
#       undef SENDING_SUPPORTED#

        // Supply own enbleIRIn
#       undef USE_DEFAULT_ENABLE_IR_IN
</pre>
