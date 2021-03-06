---
title: Grove - Air Quality Sensor v1.3
category: Sensor
bzurl: https://www.seeedstudio.com/Grove-Air-quality-sensor-v1.3-p-2439.html
oldwikiname: Grove - Air Quality Sensor v1.3
prodimagename: Grove%20Air%20Quality%20Sensor.jpg
surveyurl: https://www.surveymonkey.com/r/grove-air-quality-sensor-v3
sku: 101020078
---

---
![](https://github.com/SeeedDocument/Grove_Air_Quality_Sensor_v1.3/raw/master/img/Grove%20Air%20Quality%20Sensor_big.jpg)

This sensor is designed for comprehensive monitor over indoor air condition. It's responsive to a wide scope of harmful gases, as carbon monoxide, alcohol, acetone, thinner, formaldehyde and so on. Due to the measuring mechanism, this sensor can't output specific data to describe target gases' concentrations quantitatively. But it's still competent enough to be used in applications that require only qualitative results, like auto refresher sprayers and auto air cycling systems.

<p style="text-align:center"><a href="https://www.seeedstudio.com/Grove-Air-quality-sensor-v1.3-p-2439.html" target="_blank"><img src="https://raw.githubusercontent.com/SeeedDocument/Seeed-WiKi/master/docs/images/get_one_now_small.png" width="210" height="41"  border=0 /></a></p>

## Version

| Product Version | Changes | Released Date |
|-----------------|---------|---------------|
| Grove - Air Quality Sensor v1.3 | Initial | May 2016      |

## Features
- Responsive to a wide scope of target gases
- Cost efficient
- Durable
- Compatible with 5V and 3.3V

!!!Cautions
    1. Requires relatively clean air as an initial condition.
    2. Long time exposure to highly polluted air can significantly weaken its sensitivity.
    3. Coffre-fort et armoire forte:

## Platforms Supported

| Arduino                                                                                             | Raspberry Pi                                                                                             | BeagleBone                                                                                      | Wio                                                                                               | LinkIt ONE                                                                                         |
|-----------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/arduino_logo.jpg) | ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/raspberry_pi_logo.jpg) | ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/bbg_logo_n.jpg) | ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/wio_logo_n.jpg) | ![](https://raw.githubusercontent.com/SeeedDocument/wiki_english/master/docs/images/linkit_logo_n.jpg) |

!!!Caution
    The platforms mentioned above as supported is/are an indication of the module's hardware or theoritical compatibility. We only provide software library or code examples for Arduino platform in most cases. It is not possible to provide software library / demo code for all possible MCU platforms. Hence, users have to write their own software library.

## Getting Started

!!!Note
    If this is the first time you work with Arduino, we firmly recommend you to see [Getting Started with Arduino](http://wiki.seeedstudio.com/Getting_Started_with_Arduino/) before the start.

### Play With Arduino

#### Demonstration

As described in Introduction, this sensor performs better in providing qualitative results over a wide scope of target gases. In this demo, we will define 4 statuses for reference in the '.cpp' file. They are:

- a. air fresh -- indicating a good air condition
- b. low pollution -- indicating a rather low concentration of target gases exist.
- c. high pollution(without "Force signal active" message printed on serial monitor) -- you should be aware of the pollution level and consider if some measures could be taken.
- d. high pollution(with "Force signal active" message printed on serial monitor) -- instant measures should be taken to improve the air quality.

We encapsulated the decision structure in a '.cpp' file. You can find information there on how to modify the thresholds.

Let's try it out!

#### Hardware

- **Step 1.** Prepare the below stuffs:

| Seeeduino V4.2 | Base Shield|  Grove - Air Quality Sensor |
|--------------|-------------|-----------------|
|![enter image description here](https://raw.githubusercontent.com/SeeedDocument/Grove_Light_Sensor/master/images/gs_1.jpg)|![enter image description here](https://raw.githubusercontent.com/SeeedDocument/Grove_Light_Sensor/master/images/gs_4.jpg)|![enter image description here](https://github.com/SeeedDocument/Grove_Air_Quality_Sensor_v1.3/raw/master/img/Grove%20Air%20Quality%20Sensor_small.jpg)|
|[Get One Now](http://www.seeedstudio.com/Seeeduino-V4.2-p-2517.html)|[Get One Now](https://www.seeedstudio.com/Base-Shield-V2-p-1378.html)|[Get One Now](https://www.seeedstudio.com/Grove-Air-quality-sensor-v1.3-p-2439.html)|

- **Step 2.** Connect Grove - Air Quality Sensor to port **A0** of Grove-Base Shield.
- **Step 3.** Plug Grove - Base Shield into Seeeduino.
- **Step 4.** Connect Seeeduino to PC via a USB cable.

![](https://github.com/SeeedDocument/Grove_Air_Quality_Sensor_v1.3/raw/master/img/Grove_-_Air_Quality_Sensor_v1.3_Test.jpg)

!!!Note
	If we don't have Grove Base Shield, We also can directly connect Grove - Air Quality Sensor to Seeeduino as below.

| Seeeduino       | Grove - Air Quality Sensor |
|---------------|-------------------------|
| 5V           | Red                     |
| GND           | Black                   |
| Not Conencted | White                   |
| A0            | Yellow                  |

#### Software

- **Step 1.** Download the  [AirQuality_Sensor Library](https://github.com/SeeedDocument/Grove_Air_Quality_Sensor_v1.3/raw/master/res/AirQuality_Sensor.zip).
- **Step 2.** Refer [How to install library](http://wiki.seeedstudio.com/How_to_install_Arduino_Library) to install library for Arduino.
- **Step 3.** Copy the code into Arduino IDE and upload. If you do not know how to upload the code, please check [how to upload code](http://wiki.seeedstudio.com/Upload_Code/).

```c
/*
AirQuality Demo V1.0.
connect to A1 to start testing. it will needs about 20s to start
* By: http://www.seeedstudio.com
*/
#include "AirQuality.h"
#include "Arduino.h"
AirQuality airqualitysensor;
int current_quality =-1;
void setup()
{
    Serial.begin(9600);
    airqualitysensor.init(14);
}
void loop()
{
    current_quality=airqualitysensor.slope();
    if (current_quality >= 0)// if a valid data returned.
    {
        if (current_quality==0)
        Serial.println("High pollution! Force signal active");
        else if (current_quality==1)
        Serial.println("High pollution!");
        else if (current_quality==2)
        Serial.println("Low pollution!");
        else if (current_quality ==3)
        Serial.println("Fresh air");
    }
}
ISR(TIMER2_OVF_vect)
{
    if(airqualitysensor.counter==122)//set 2 seconds as a detected duty
    {

        airqualitysensor.last_vol=airqualitysensor.first_vol;
        airqualitysensor.first_vol=analogRead(A0); // change this value if you use another A port
        airqualitysensor.counter=0;
        airqualitysensor.timer_index=1;
        PORTB=PORTB^0x20;
    }
    else
    {
        airqualitysensor.counter++;
    }
}
```

- **Step 4.** We will see the distance display on terminal as below.

![](https://github.com/SeeedDocument/Grove_Air_Quality_Sensor_v1.3/raw/master/img/AirQualitySensot_Demo.jpg)

To adjust the thresholds and indicating messages, refer to the decision structure below in the .cpp file.

```c
int AirQuality::slope(void)
{
    while(timer_index)
    {
        if(first_vol-last_vol>400||first_vol>700)
        {
            Serial.println("High pollution! Force signal active.");
            timer_index=0;
            avg_voltage();
            return 0;

        }
        else if((first_vol-last_vol>400&&first_vol<700)||first_vol-vol_standard>150)
        {
            Serial.print("sensor_value:");
            Serial.print(first_vol);
            Serial.println("\t High pollution!");
            timer_index=0;
            avg_voltage();
            return 1;

        }
        else if((first_vol-last_vol>200&&first_vol<700)||first_vol-vol_standard>50)
        {
            //Serial.println(first_vol-last_vol);
            Serial.print("sensor_value:");
            Serial.print(first_vol);
            Serial.println("\t Low pollution!");
            timer_index=0;
            avg_voltage();
            return 2;
        }
        else
        {
            avg_voltage();
            Serial.print("sensor_value:");
            Serial.print(first_vol);
            Serial.println("\t Air fresh");
            timer_index=0;
            return 3;
        }
    }
    return -1;
}
```

### Play With Raspberry Pi

#### Hardware

- **Step 1.** Prepare the below stuffs:

| Raspberry pi | GrovePi_Plus |  Grove - Air Quality Sensor |
|--------------|-------------|-----------------|
|![enter image description here](https://github.com/SeeedDocument/wiki_english/raw/master/docs/images/rasp.jpg)|![enter image description here](https://github.com/SeeedDocument/wiki_english/raw/master/docs/images/Grovepi%2B.jpg)|![enter image description here](https://github.com/SeeedDocument/Grove_Air_Quality_Sensor_v1.3/raw/master/img/Grove%20Air%20Quality%20Sensor_small.jpg)|
|[Get One Now](http://www.seeedstudio.com/Seeeduino-V4.2-p-2517.html)|[Get One Now](https://www.seeedstudio.com/Base-Shield-V2-p-1378.html)|[Get One Now](https://www.seeedstudio.com/Grove-Air-quality-sensor-v1.3-p-2439.html)|

- **Step 2.** Plug the GrovePi_Plus into Raspberry.
- **Step 3.** Connect Grove-MOSFET ranger to **A0** port of GrovePi_Plus.
- **Step 4.** Connect the Raspberry to PC through USB cable.

#### Software

- **Step 1.** Navigate to the demos' directory:

```
cd yourpath/GrovePi/Software/Python/
```

- **Step 2.**  To see the code

```
nano grove_air_quality_sensor.py   # "Ctrl+x" to exit #
```

```python
import time
import grovepi

# Connect the Grove Air Quality Sensor to analog port A0
# SIG,NC,VCC,GND
air_sensor = 0

grovepi.pinMode(air_sensor,"INPUT")

while True:
    try:
        # Get sensor value
        sensor_value = grovepi.analogRead(air_sensor)

        if sensor_value > 700:
            print "High pollution"
        elif sensor_value > 300:
            print "Low pollution"
        else:
            print "Air fresh"

        print "sensor_value =", sensor_value
        time.sleep(.5)

    except IOError:
        print "Error"
```

- **Step 3.** Run the demo.

```
sudo python grove_air_quality_sensor.py
```

- **Step 4.** We will see the output display on terminal as below.

![enter image description here](https://github.com/SeeedDocument/Grove_Air_Quality_Sensor_v1.3/raw/master/img/pi_result.png)


## Resources

- **[Library]** [AirQuality Sensor Library](https://github.com/SeeedDocument/Grove_Air_Quality_Sensor_v1.3/raw/master/res/AirQuality_Sensor.zip)
- **[Eagle]** [Grove_-_Air_quality_sensor_v1.3_sch_pcb](https://github.com/SeeedDocument/Grove_Air_Quality_Sensor_v1.3/raw/master/res/Grove_-_Air_quality_sensor_v1.3_sch_pcb.zip)
- **[PDF]** [Grove_-_Air_quality_sensor_v1.3_sch](https://github.com/SeeedDocument/Grove_Air_Quality_Sensor_v1.3/raw/master/res/Grove_-_Air_quality_sensor_v1.3_sch.pdf)
- **[PDF]** [Air_quality_sensor_MP503_Chinese](https://github.com/SeeedDocument/Grove_Air_Quality_Sensor_v1.3/raw/master/res/Air_quality_sensor_MP503%20Chinese.pdf)
- **[PDF]** [Air_quality sensor_MP503_English](https://github.com/SeeedDocument/Grove_Air_Quality_Sensor_v1.3/raw/master/res/Mp503%20English.pdf)

## Projects

**SPCPM (Solar Powered City Pollution Monitor)**: Low maintenance, high output air pollution, sound pollution that put throughout the city without wiring.

<iframe frameborder='0' height='327.5' scrolling='no' src='https://www.hackster.io/100181/spcpm-solar-powered-city-pollution-monitor-ca4072/embed' width='350'></iframe>

**A website to see the environment data around you**:

<iframe frameborder='0' height='327.5' scrolling='no' src='https://www.hackster.io/kevin-lee2/a-website-to-see-the-environment-data-around-you-1aea66/embed' width='350'></iframe>

**Home Control Center using BeagleBone Green Wireless**:

<iframe frameborder='0' height='327.5' scrolling='no' src='https://project.seeedstudio.com/kevin-lee2/home-control-center-using-beaglebone-green-wireless-107a0d/embed' width='350'></iframe>


## Tech Support
Please submit any technical issue into our [forum](http://forum.seeedstudio.com/). 