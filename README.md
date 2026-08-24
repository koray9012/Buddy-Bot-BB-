                                  Engineer's friend Buddy bot (BB)
                                          By Koray                                                                                                  
![image](https://raw.githubusercontent.com/koray9012/Buddy-Bot-BB-/refs/heads/main/20260815_213051.jpg)
An interactive ESP32 workbench assistant featuring an onboard solder fume extractor fan, ESP32-CAM visual monitoring, sound-activated sequences, and expression animations. 
It brings personality to your workspace while driving up to clear soldering fumes on command so you don't look like you're working with just a plain piece of silicon.

## Key Upgrades & Features
  
 Dual-Microphone Clap Detection:

  • Uses a high-sensitivity sound sensor to listen for specific clap patterns to trigger movement and fume extraction routines automatically.

 Onboard ESP32-CAM & Solder Fume Fan:

  • Combines a wireless ESP32-CAM module for bench inspection with a K2272 relay-controlled fan to suck away toxic soldering fumes right at the work area.

 Expressive Animated OLED Display:

  • Features dynamic pixel expressions (Normal, Surprised, and Fan Eyes) on an SSD1306 OLED screen to make the helper look alive on your workbench.
 
 3 Dynamic Operating Modes (Clap-Cycled):

  • Standby Mode: Idle face expression waiting for acoustic sound commands.

  • Fume Extractor Mode: Runs the solder fan sequence for a set duration before re-enabling sound detection.

  • Fume Fan Listening Mode: Active fan state listening specifically for a 3-clap pattern to execute the victory dance and return to idle.

 Safe Drive Motor Timing:

  • Custom 200ms pulsed motor routines prevent current spikes and voltage sags, keeping the 4-motor L298N drive smooth and stable.

## How to use: 

To use it first you need to connect the custom 2S battery pack to the battery connectors and then switch on the master power switch. After you switch it on you will instantly be in standby mode with the normal eye expression on the OLED display. To trigger the robot, clap twice clearly. The robot will show a surprised face, wait 3 seconds, drive forward for 200ms, run the fan eye animation, and turn on the solder fume extractor fan via the K2272 relay. After 7 seconds of fan operation, the robot enters listening mode. Clap 3 times while the fan is blowing, and the robot will immediately turn off the fan relay, show a surprised face, perform a 200ms victory dance sequence, and return to standby mode with the normal face expression.

Here is so clean instructions on how to do it step by step:

## Operating Instructions
1. Power On
  1.Connect your custom 2S battery pack to the battery connectors.

  2.Flip the master power switch to turn on the robot.

  3.The robot defaults to Standby Mode on startup with the normal face on the OLED screen.

2. Sequence Triggering (Starting Fume Extraction)
  1.Clap twice (2 claps) near the sound sensor.

  2.The display switches to a Surprised Face.

  3.The robot drives forward for 200ms and pauses to stabilize power.

  4.The fan eye animation plays on the screen, the display dims to save power, and the K2272 relay turns ON the solder fume extractor fan.

3. Stopping the Fan & Victory Dance
  1.Wait 7 seconds for the robot to switch to Fume Fan Listening Mode.

  2.Clap three times (3 claps) near the sound sensor.

  3.The robot turns off the relay to stop the fan.

  4.The display shows a Surprised Face for 3 seconds.

  5.The robot performs its 200ms victory dance sequence, then resets back to Standby Mode with the normal face.

  ## Why I made it:

When working at my workbench soldering electronics, breathing in solder flux fumes gets annoying fast, and stationary fume extractors take up too much desk space. I wanted to build an active bench assistant that moves into position, extracts fumes on command, and has enough personality that it feels like a real desktop companion rather than just a lifeless piece of silicon.

I integrated an ESP32-CAM for inspection alongside a sound sensor module with custom clap filtering so I could trigger driving and fume extraction completely hands-free while my hands are holding a soldering iron and wire. I designed custom facial animations on an SSD1306 OLED screen so the robot communicates its status visually, and wired a K2272 relay module to control the heavy current draw of the fume fan independently. Handling 4 DC motors alongside an OLED, camera, and a high-draw relay on a single rail caused severe power sags and I2C freezes, which taught me how to strictly optimize power states, isolate logic grounds, and tune precision 200ms motor timing pulses. I powered the entire system with my custom 2-cell 18650 battery pack (7.4V, 3400mAh each) with a 2S BMS, providing clean, rechargeable, and long-lasting power compared to standard 9V batteries.

It started as a simple relay-trigger test, but turned into a full-on crash course in power rail stabilization, back-EMF spike isolation, C++ non-blocking state machines, and hardware integration and i plan to upgrade it constantly and one day to make it absolutely perfect.

### Wiring & Connections:

Below is the visual schematic diagram for Buddy bot the engineer's friend (BB).

![image](https://github.com/koray9012/Engineering-Helper-Robot/blob/main/%D0%95%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D0%B0%20%D1%81%D0%BD%D0%B8%D0%BC%D0%BA%D0%B0%202026-07-29%20005514.png?raw=true)

### Pinout Breakdown:

| ESP32 Pin | Component | Connected Pin / Note |
| :--- | :--- | :--- |
| **GPIO 25** | L298N Motor Driver | IN1 (Motor Drive) |
| **GPIO 26** | L298N Motor Driver | IN2 (Motor Drive) |
| **GPIO 27** | L298N Motor Driver | IN3 (Motor Drive) |
| **GPIO 33** | L298N Motor Driver | IN4 (Motor Drive) |
| **GPIO 18** | K2272 Relay Module | Signal / IN (Fume Fan Control) |
| **GPIO 34** | Sound Sensor Module | OUT / Signal (Clap Detection) |
| **GPIO 21** | OLED Display | Shared I2C SDA |
| **GPIO 22** | OLED Display | Shared I2C SCL |
| **5V / 3.3V** | ESP32-CAM | Camera Module Power & Data Lines |
| **5V** | L298N Motor Driver | 5V screw for esp32 power |
| **Battery +** | power switch -> L298N Motor Driver | 12V screw for motor power |
| **Battery -** | Shared GND of all devices | Shared GND cable |
| **Motor R1** | L298N Motor Driver | + to OUT1 - to OUT2 |
| **Motor R2** | L298N Motor Driver | + to OUT1 - to OUT2 |
| **Motor L1** | L298N Motor Driver | + to OUT4 - to OUT3 |
| **Motor L2** | L298N Motor Driver | + to OUT4 - to OUT3 |

## Code:

The code can be found in repo: Engineering Helper Robot Code

## Bill of materials:

| Item | Quantity | Price (USD) | Link |
| :--- | :--- | :--- | :--- |
| Esp32 38 pins | 1 | 8.68 USD | https://www.ardboard.com/index.php?route=product/product&product_id=413 |
| ESP32-CAM Module | 1 | 9.50 USD | https://www.ardboard.com/index.php?route=product/product&product_id=273&search=Cam |
| L298N Motor Driver | 1 | 4.60 USD | https://elimex.bg/product/71197-kit-k2010-drayver-za-postoyannotokovi-motori |
| 0.96 Oled Display | 1 | 5.60 USD | https://www.ardboard.com/index.php?route=product/product&product_id=264&search=oled |
| K2272 Relay Module | 1 | 2.50 USD | https://elimex.bg/product/86303-kit-k2272-modul-s-edno-rele-aktivno-nivo-visoko |
| Sound Sensor Module | 1 | 1.80 USD | https://www.ardboard.com/index.php?route=product/product&product_id=312 |
| Car Chasis | 1 | 20.93 USD | https://elimex.bg/product/84826-shasi-za-robot-4wd-s-4-motora-i-2-osnovi-kit-za-sglobqvane |
| 18650 Battery | 2 | 5.77 USD x2 = 11.54 USD | https://elimex.bg/product/85664-akumulator-3.7v-3400mah-lc18650-lava |
| Battery holder | 4 | 0.28 USD x4 = 1.12 USD | https://elimex.bg/product/77722-battery-holder-lc18650 |
| 2S BMS | 1 | 1.52 USD | https://elimex.bg/product/77415-bsmpcm-kontroler-za-zaryada-i-razryada-na-li-ion-paket-2x18650-7-4v-8-4v3a |
| Power Switch | 1 | 0.35 USD | https://elimex.bg/product/44024-switch-smrs101-1-black | 
| DC Motors | 4 | 2.27 USD x4 = 9.08 USD | https://elimex.bg/product/79622-kit-k2178-postoyannotokov-motor-za-robo-platforma |
| Solder Fume Fan | 1 | 4.50 USD | https://elimex.bg/product/89100-mini-fan-5v |
| Jumper Cables | ~30 | 2.86 USD + 2.27 USD = 5.13 USD | https://elimex.bg/product/75823-komplekt-provodnitsi-40-broya-s-konektori-mazhki-zhenski-30sm AND  https://elimex.bg/product/74894-komplekt-provodnitsi-40-broya-s-konektori-mazhki-mazhki-20sm |

## Very important: The motors came with the chasis because they are a kit and also the cables arent exacly 30 bc i cut them up and soldered them 

## Video for BB demo ()

## Credits: 

This project uses:

Kicad

Hack Club Macondo 

Btw thank you for the pinecil Hack Club :)
