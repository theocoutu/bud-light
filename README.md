# bud-light
Reversible modification for the Budweiser Red Light, to trigger the light over local Wi-Fi using ESPHome.
The modification is an SD card original Wi-Fi microcontroller is not modified, and th

## The Light
The first three models of the Budweiser Red Light (v1, v2, v3) have an accessible SD card slot on the side. The one I received had the plastic cover missing, so the SD card could be clicked in and out like any normal SD card. This SD card is a Wi-Fi microcontroller, the Electric Imp imp001. Probing SD card pins with an adapter while pressing and releasing the TEST button, I discovered a pin that is directly connected to the TEST button, so this could be used to trigger the light. I decided to cannibalize a micro-SD to SD adapter, but found that two contacts on the connector are bridged. Using the pinout of the imp001 from the datasheet, I found that my micro-SD adapter bridges GND and the ID pin, which the microcontroller uses to communicate with an on-board EEPROM. To avoid potentially damaging the ID pin, I added a small piece of tape to the ID pin contact on my adapter. I broke out the 3.3V, GND, and trigger pins for use with my custom hardware.

## Custom Hardware
I chose the ESP32-C2 for this project as I only needed Wi-Fi for this project, not Bluetooth. The C2 is low-power, so it can run on the light's D batteries but I added capacitors (10pF, 22pF, 10uF) for Wi-Fi spikes.
