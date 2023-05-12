<img src="assets/IWA.svg" width=200 align="right">

# OCA - Output Control MOSFET
2x MOSFET output and 2x GPIO
| Specifications | |
| --: | :--: |
| Communication | I²C |
| I²C Address | 0x20 (0x21) |
| ChipSet | NXP PCF8574T|
| Datasheet | [.pdf](https://www.nxp.com/docs/en/data-sheet/PCF8574_PCF8574A.pdf) |
| Suggested Arduino Library | [GitHub](https://github.com/xreef/PCF8574_library) |
| Suggested MicroPython Library | [GitHub](https://github.com/mcauser/micropython-pcf8574)|
| Channel 0 | MOSFET |
| Channel 1 | MOSFET |
| Channel 2 | GPIO HIGH/LOW Reversed |
| Channel 3 | GPIO HIGH/LOW Reversed|
| Channel 4-7 | N/A |

## Supported I²C Modes
- [X] 100 kbit/s Standard Mode (SM) 
- [ ] 400 kbit/s	Fast Mode	FM
- [ ] 1 Mbit/s	Fast Mode Plus	FM+
- [ ] 3.4Mbit/s	High Speed Mode	HS
- [ ] 5 Mbit/s	Ultra Fast Mode	UFM

## Arduino Code Example
```C
// LED's on MOSFET1 and MOSFET2, switch on GPIO4.

#include "Arduino.h"
#include "PCF8574.h"

PCF8574 OCA(0x20);
// Right to Left
#define MOSFET1 P0
#define MOSFET2 P1
#define GPIO3 P2
#define GPIO4 P3

void setup() {
  Serial.begin(115200);
  delay(1000);
  OCA.pinMode(MOSFET1, OUTPUT);
  OCA.pinMode(MOSFET2, OUTPUT);
  OCA.pinMode(GPIO3, OUTPUT);
  OCA.pinMode(GPIO4, INPUT);
  Serial.print("Init OCA...");
  if (OCA.begin()) {
    Serial.println("OK");
  } else {
    Serial.println("KO");
  }
  OCA.digitalWrite(MOSFET1, LOW);
  OCA.digitalWrite(MOSFET2, LOW);
  OCA.digitalWrite(GPIO3, LOW);
}

void loop() {
  if (OCA.digitalRead(GPIO4)) {
    OCA.digitalWrite(MOSFET1, LOW);
    OCA.digitalWrite(MOSFET2, HIGH);
  } else {
    OCA.digitalWrite(MOSFET1, HIGH);
    OCA.digitalWrite(MOSFET2, LOW);
  }
  delay(15); //Minimum delay for this to work!
}
```


# License: 
<img src="assets/CC-BY-NC-SA.svg" width=200 align="right">
Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International Public License

[View License Deed](https://creativecommons.org/licenses/by-nc-sa/4.0/) | [View Legal Code](https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode)
