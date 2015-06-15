# IOIO Corvova Plugin

This is cordova android plugin for controlling [IOIO OTG](https://github.com/ytai/ioio/wiki)
It provides javascript inteface to interrcat with the board

Also you will need to read this article to find out how pins work
https://github.com/ytai/ioio/wiki/Getting-To-Know-The-Board#detailed-pin-function-table

## How to install

You can use plugman to install the plugin

    plugman install --platform android --project <path to your project> --plugin https://github.com/AppShed/ioio-cordova-plugin

[Read about plugman](http://cordova.apache.org/docs/en/4.0.0/plugin_ref_plugman.md.html)

## Requirements

The only requirement is that your IOIO firmware must be up to date. (App-IOIO0500.ioioapp was the latest firmware at the moment of writing this article)

Here is a link that explains how to check your current firmware and update it
https://github.com/ytai/ioio/wiki/IOIO-OTG-Bootloader-and-IOIODude

## How to use

First of all you need to define port you want to work with. Once IOIO succesfully initialized,
led on IOIO started blinking

	window.ioio.open({ // start ioio and open ports we need
		inputs: {
			analogue: [37,39,40,41],
			digital:[38]
	    },
		outputs: {
			digital:[33],
			pwm: [
				{pin: 10, freq: 1}, // set default frequency for the pin 10
				{pin: 12, freq: 1}
			]
		},
		delay: 200 // Optionally set minimum delay between receiving data from IOIO
	}, function() {
		// success
	}, function() {
		//fail
	}, function(vals) {
		// global all open pin listener

		for(var i=0;i<vals.length;i++){
			var pin = vals[i];
			//for(var key in pin){console.log(key + ":" + pin[key]);}
			switch(pin.class){
				case window.ioio.PIN_INPUT_DIGITAL:
				case window.ioio.PIN_OUTPUT_DIGITAL:
				case window.ioio.PIN_INPUT_ANALOG:
				//pin.pin pin.value
				break;
				case window.ioio.PIN_OUTPUT_PWM:
				//pin.pin pin.freq
				break;
			}
		}
	});

You can add some listeners to read values from pins

		window.ioio.addPinListener(37, function(value) { // parameter value is boolean for digital ports and float for other ports in range from 0.00000 to 1.00000
			// todo
		});

		window.ioio.addValuePinListener(37, 0.5, function(value) { // if value goes high that 0.5 it will fire, if it then goes lower, it will fire again
			// todo
		});

And you can control some pins

		window.ioio.setPwnOutput(10, 0);  // set frequency for the pin 10
		window.ioio.setPwnOutput(12, 0); // set frequency for the pin 12
		window.ioio.setDigitalOutput(33, true);  // enable pin 33
		window.ioio.setDigitalOutput(33, false); // disable pin 33
		window.ioio.toggleDigitalOutput(33); // toggle pin 33
		
		
Once you finish, you have to close IOIO
		
		window.ioio.close(); // finish work with ioio