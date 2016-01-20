# Design Journal


## Want List

- I want auto connection when discovery phase determines only one ESP is available.
  - If connecting to multiple ESP8266, it's fair to expect user programs to provide discovery/identity information
- I want it to behave the same as other IO plugins w/r to connection: this must be addressed as part of the instance initialization phase (ie. as a condition of ready event completion). I appreciate the efforts that came before this, but they are not acceptable w/r to ease of use. There is no way that anyone should be expected write programs that require initializing the transport, io plugin _AND_ board instances.
- I don't want users to be required to edit C code to make network configurations. If that seems necessary, then we can live with it, but ideally: no thanks.
- I want this list to grow. 

## Questions

- With [esp8266/Arduino](https://github.com/esp8266/Arduino), we can support a "flavor" of Firmata that looks like StandardFirmata, **but with a different com layer**
  - What transport **protocol**?
    - Need to discuss pros and cons
    - Needs to be something that is discoverable, requires no user configuration 
      - For example, I power on an ESP8266 and using [mdns-js](https://github.com/mdns-js/node-mdns-js) I can discover that device and initiate a connection. 





## IO

Boards: 

- [Adafruit Huzzah](https://learn.adafruit.com/adafruit-huzzah-esp8266-breakout/), `AFH`
- [SparkFun Thing](https://learn.sparkfun.com/tutorials/esp8266-thing-hookup-guide/), `SFT`
  - https://learn.sparkfun.com/tutorials/esp8266-thing-hookup-guide/programming-the-thing
  - https://cdn.sparkfun.com/datasheets/Wireless/WiFi/ESP8266ThingV1.pdf



- GPIO
  - `AFH`: D0, D2, D4, D5, D12, D13, D14, D15, D16
  - `SFT`: D0, D2, D4, D5, D7, D8, D12, D13, D14, D16
- ADC
  - `AFH`: A0
  - `SFT`: A0
- I2C
  - `AFH`: ✓
  - `SFT`: ✓

![](http://www.esp8266.com/wiki/lib/exe/fetch.php?media=pin_functions.png)


## Reviewed

- https://gist.github.com/ajfisher/5fe60fe7d8c49b3223f0
- https://github.com/esp8266/Arduino
  - Interested peeps should look at: https://github.com/esp8266/Arduino/tree/master/libraries to find answers

## Review Needed

- https://github.com/sparkfun/Rogue_Router (might be useful?)

## Issues Encountered

- OSX Yosemite failed to upload code to ESP8266 via FTDI breakout
  - Possibly just a power issue?
    - Confirmed! Attaching a 3.7V Lipo to the Thing and switching it ON made flashing successful.


