---
title: Grove - Light Sensor
category: Sensor
bzurl: https://www.seeedstudio.com/Grove-Light-Sensor-(P)-v1.1-p-2693.html
oldwikiname: Grove_-_Light_Sensor
prodimagename: cover.jpg
sku: 101020173
tags: io_3v3, io_5v, plat_duino, plat_wio, plat_pi, plat_bbg, plat_linkit
---


![enter image description here](https://raw.githubusercontent.com/SeeedDocument/Grove_Light_Sensor/master/images/cover.jpg)


The Grove - Light sensor integrates a photo-resistor(light dependent resistor) to detect the intensity of light. The resistance of photo-resistor decreases when the intensity of light increases. A dual OpAmp chip LM358 on board produces voltage corresponding to intensity of light(i.e. based on resistance value). The output signal is analog value, the brighter the light is, the larger the value.

This module can be used to build a light controlled switch i.e. switch off lights during day time and switch on lights during night time.


!!!Warning
    The light sensor value only reflects the approximated trend of the intensity of light, it DOES NOT represent the exact Lumen.

<p style="text-align:center"><a href="https://www.seeedstudio.com/Grove-Light-Sensor-v1.2-p-2727.html" target="_blank"><img src="https://raw.githubusercontent.com/SeeedDocument/Seeed-WiKi/master/docs/images/get_one_now_small.png" width="210" height="41"  border=0 /></a></p>

## Version

| Product Version              | Changes                                                            | Released Date |
|------------------------------|--------------------------------------------------------------------|---------------|
| Grove - Light Sensor 1.0     | Initial                                                            | Apr 28 2013   |
| Grove - Light Sensor(P)      | Move Grove connector to back side                                  | May 15 2014   |
| Grove - Light Sensor(P) V1.1 | Replace photoresistor-5528 with LS06-S Vs.Grove - Light Sensor(P)  | Dec 31 2015   |
| Grove - Light Sensor 1.2     | Replace photoresistor-5528 with LS06-S Vs.Grove - Light Sensor 1.0 | Jan 20 2016   |


## Features

* Analog value output
* High reliability and sensibility
* Small footprint
* Recognize wider spectrum

!!!Tip
    More details about Grove modules please refer to [Grove System](http://wiki.seeedstudio.com/Grove_System/)

### Platform Support

| Arduino                                                                                             | Raspberry Pi                                                                                             | BeagleBone                                                                                      | Wio                                                                                               | LinkIt ONE                                                                                         |
|-----------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/arduino_logo.jpg) | ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/raspberry_pi_logo.jpg) | ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/bbg_logo.jpg) | ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/wio_logo.jpg) | ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/linkit_logo.jpg) |

!!!Caution
    The platforms mentioned above as supported is/are an indication of the module's hardware or theoritical compatibility. We only provide software library or code examples for Arduino platform in most cases. It is not possible to provide software library / demo code for all possible MCU platforms. Hence, users have to write their own software library.


## Specification

|Item|Value|
|-----|--------|
|Operating voltage|3~5V|
|Operating current|	0.5~3 mA|
|Response time|20-30 milliseconds|
|Peak Wavelength|540 nm|
|Weight|4 g|


## Getting Started

### Play With Arduino

#### Hardware

- Step 1. Prepare the below stuffs:

| Seeeduino V4 | Base Shield |Grove - Light Sensor | Grove - LED Bar |
|--------------|----------------------|-----------------|---------------------|
|![enter image description here](https://raw.githubusercontent.com/SeeedDocument/Grove_Light_Sensor/master/images/gs_1.jpg)|![enter image description here](https://raw.githubusercontent.com/SeeedDocument/Grove_Light_Sensor/master/images/gs_4.jpg)|![enter image description here](https://github.com/SeeedDocument/Grove_Light_Sensor/raw/master/img/light_sensor_s.jpg)|![enter image description here](https://raw.githubusercontent.com/SeeedDocument/Grove_Light_Sensor/master/images/gs_3.jpg)|
|[Get One Now](http://www.seeedstudio.com/Seeeduino-V4.2-p-2517.html)|[Get One Now](http://www.seeedstudio.com/Base-Shield-V2-p-1378.html)|[Get One Now](https://www.seeedstudio.com/Grove-Light-Sensor-v1.2-p-2727.html)|[Get One Now](http://www.seeedstudio.com/Grove-LED-Bar-v2.0-p-2474.html)|

- Step 2. Connect Grove-Light Sensor to port A0 of Grove-Base Shield.
- Step 3. Connect Grove-Led Bar to port D2 of Grove-Base Shield.
- Step 4. Plug Grove - Base Shield into Seeeduino.
- Step 5. Connect Seeeduino to PC through a USB cable.

![](https://github.com/SeeedDocument/Grove_Light_Sensor/raw/master/img/seeeduino_light.jpg)

!!!Note
	If we don't have Grove Base Shield, We also can directly connect Grove-Light Sensor to Seeeduino as below.

| Seeeduino       | Grove-Light Sensor |
|---------------|-------------------------|
| 5V           | Red                     |
| GND           | Black                   |
| Not Conencted | White                   |
| A0            | Yellow                  |


| Seeeduino       | Grove-Led Bar |
|---------------|-------------------------|
| 5V            | Red                     |
| GND           | Black                   |
| D3            | White                   |
| D2            | Yellow                  |

#### Software

- Step 1. Download the  [ Grove-LED Bar Library](https://github.com/Seeed-Studio/Grove_LED_Bar/archive/master.zip) from Github.
- Step 2. Refer [How to install library](http://wiki.seeedstudio.com/How_to_install_Arduino_Library) to install library for Seeeduino.
- Step 3. Copy the code into Seeeduino IDE and upload.

```c

#include <Grove_LED_Bar.h>

Grove_LED_Bar bar(3, 2, 0);  // Clock pin, Data pin, Orientation

void setup()
{
  // nothing to initialize
  bar.begin();
  bar.setGreenToRed(true);
}

void loop()
{

  int value = analogRead(A0);
  value = map(value, 0, 800, 0, 10);

  bar.setLevel(value);
  delay(100);
}
```

- Step 2. The Led bar will change base on light.

### Play With Raspberry Pi

#### Hardware

- Step 1. Prepare the below stuffs:

| Raspberry pi | GrovePi_Plus | Grove - Light Sensor | Grove - Red LED |
|--------------|-------------|-----------------|-----------------|
|![enter image description here](https://github.com/SeeedDocument/wiki_english/raw/master/docs/images/rasp.jpg)|![enter image description here](https://github.com/SeeedDocument/wiki_english/raw/master/docs/images/Grovepi%2B.jpg)|![enter image description here](https://github.com/SeeedDocument/Grove_Light_Sensor/raw/master/img/light_sensor_s.jpg)|![enter image description here](https://github.com/SeeedDocument/Grove-Red_LED/raw/master/img/Red%20LED_s.jpg)|
|[Get One Now](https://www.seeedstudio.com/Raspberry-Pi-3-Model-B-p-2625.html)|[Get One Now](https://www.seeedstudio.com/GrovePi%2B-p-2241.html)|[Get One Now](https://www.seeedstudio.com/Grove-Light-Sensor-v1.2-p-2727.html)|[Get One Now](https://www.seeedstudio.com/s/Grove-Red-LED-p-1142.html)|

- Step 2. Plug the GrovePi_Plus into Raspberry.
- Step 3. Connect Grove-light sensor to A0 port of GrovePi_Plus.
- Step 4. Connect Grove-Red Led to D4 port of GrovePi_Plus.
- Step 5. Connect the Raspberry to PC through USB cable.

![](https://github.com/SeeedDocument/Grove_Light_Sensor/raw/master/img/rasp_light.jpg)

#### Software

- Step 1. Follow [Setting Software](https://www.dexterindustries.com/GrovePi/get-started-with-the-grovepi/setting-software/) to configure the development environment.
- Step 2. Git clone the Github repository.

```
cd ~
git clone https://github.com/DexterInd/GrovePi.git

```

- Step 3. Excute below commands.


```
cd ~/GrovePi/Software/Python
python grove_light_sensor.py
```

Here is the grove_light_sensor.py code.

```python
import time
import grovepi

# Connect the Grove Light Sensor to analog port A0
# SIG,NC,VCC,GND
light_sensor = 0

# Connect the LED to digital port D4
# SIG,NC,VCC,GND
led = 4

# Turn on LED once sensor exceeds threshold resistance
threshold = 10

grovepi.pinMode(light_sensor,"INPUT")
grovepi.pinMode(led,"OUTPUT")

while True:
    try:
        # Get sensor value
        sensor_value = grovepi.analogRead(light_sensor)

        # Calculate resistance of sensor in K
        resistance = (float)(1023 - sensor_value) * 10 / sensor_value

        if resistance > threshold:
            # Send HIGH to switch on LED
            grovepi.digitalWrite(led,1)
        else:
            # Send LOW to switch off LED
            grovepi.digitalWrite(led,0)

        print("sensor_value = %d resistance = %.2f" %(sensor_value,  resistance))
        time.sleep(.5)

    except IOError:
        print ("Error")
```

- Step 4. The led will turn on when the light sensor gets covered.

```
pi@raspberrypi:~/GrovePi/Software/Python $ python grove_light_sensor.py
sensor_value = 754 resistance = 3.57
sensor_value = 754 resistance = 3.57
sensor_value = 752 resistance = 3.60
sensor_value = 752 resistance = 3.60
sensor_value = 752 resistance = 3.60
sensor_value = 313 resistance = 22.68
sensor_value = 155 resistance = 56.00
sensor_value = 753 resistance = 3.59
```


## Resources


- **[Eagle&PDF]** [Eagle File for Grove - Light Sensor V1.0](https://github.com/SeeedDocument/Grove_Light_Sensor/raw/master/resources/Grove%20-%20Light%20Sensor.zip)
- **[Eagle&PDF]**  [Eagle File for Grove - Light Sensor(P) V1.0](https://github.com/SeeedDocument/Grove_Light_Sensor/raw/master/resources/Grove%20-%20Light%20Sensor%28P%29.zip)
- **[Eagle&PDF]**  [Eagle File for Grove - Light Sensor(P) V1.1](https://github.com/SeeedDocument/Grove_Light_Sensor/raw/master/resources/Grove%20-%20Light%20Sensor%28P%29%20v1.1.zip)
- **[Datasheet]** [LS06-MΦ5 Reference Information](https://github.com/SeeedDocument/Grove_Light_Sensor/raw/master/res/LS06-M%CE%A65_datasheet.pdf)
- **[Datasheet]**  [LM358.PDF](https://github.com/SeeedDocument/Grove_Light_Sensor/raw/master/res/LM358.pdf)
- **[More Reading]** Secret Box

![enter image description here](https://raw.githubusercontent.com/SeeedDocument/Grove_Light_Sensor/master/images/secret_box.png)

Here we will show you a project made with Grove - Light Sensor - Secret Box. First you need a box, a paper box, wooden box, any box is ok. Put something in the box, because we named it secret box, that means we don't want anybody to open it, otherwise there will be an alarm to inform you.

Here we use LinkIt ONE as the controller, which is an Arduino compatible board and consist of rich function. And you need things below:

* [LinkIt ONE](http://www.seeedstudio.com/LinkIt-ONE-p-2017.html)
* Grove - Light Sensor
* Grove - Base Shield
* A Sim Card

Let's connect Grove - Light Sensor to A0 or Base Shield, and open Arduino IDE, copy below code and upload the example to LinkIt ONE. Then someone open the box, the light will detect it, and send you a SMS.

```c
// demo of Grove Starter kit for LinkIt ONE
// Secret box

#include <LGSM.h>

char num[20] = "13425171053";           // your number write here
char text[100] = "Warning: Your box had been opened!!";    // what do you want to send


const int pinLight = A0;                // light sensor connect to A0

bool isLightInBox()
{
    return (analogRead(pinLight)<50);   // when get data less than 50, means light sensor was in box
}

void setup()
{
    Serial.begin(115200);

    while(!isLightInBox());             // until put in box
    delay(2000);
}


void loop()
{
    if(!isLightInBox())                 // box is open
    {
        Serial.println("box had been opened");

        while(!LSMS.ready())
        {
            delay(1000);
        }

        Serial.println("SIM ready for work!");
        LSMS.beginSMS(num);
        LSMS.print(text);

        if(LSMS.endSMS())
        {
            Serial.println("SMS is sent");
        }
        else
        {
            Serial.println("SMS send fail");
        }

        while(!isLightInBox());             // until put in box
        delay(2000);
    }

    delay(10);
}
```

Have fun.

## Projects

**Grove - Introduction in a Light Sensor**:

<iframe frameborder='0' height='327.5' scrolling='no' src='https://www.hackster.io/ingo-lohs/grove-introduction-in-a-light-sensor-a55efd/embed' width='350'></iframe>

**The Environment Cube! Know the Land Beneath You using Sigfox**: A cube with all the necessary sensors, suitable for a wide range of applications like agriculture, monitoring, ,etc.

<iframe frameborder='0' height='327.5' scrolling='no' src='https://www.hackster.io/dhairya-parikh/the-environment-cube-know-the-land-beneath-you-using-sigfox-952f29/embed' width='350'></iframe>


**Light sensor Grove module**:
 
<iframe width="560" height="315" src="https://www.youtube.com/embed/ZvFswNYY2mU" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/GOROc2f5Xkg" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## Tech Support
Please submit any technical issue into our [forum](http://forum.seeedstudio.com/).
