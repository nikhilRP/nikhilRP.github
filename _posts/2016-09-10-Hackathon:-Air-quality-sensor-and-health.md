---
layout: post
title:  "IoT Hackathon: Air quality sensor and health"
date:   2016-09-10 00:00:00
description: Experience form IoT smart cities hackathon
image: /assets/images/markdown.jpg
headerImage: false
tag:
- hackathon
- Air quality index
blog: true
star: true
author: nikhilrp
---

The IoT for Cities Hackathon is a 27 hour challenge which sees Engineers and Business Developers collaborating together on project for the Internet of Things (IoT) and challenging themselves to create useful products in a short period of time.

Me along with Martin Kirst (a good friend of mine) decided to take part in it, and I am delighted to announce that we won the award for the “Best Smart City Solution”. The event started with a presentation of ideas, followed by the building phase and then the presenting of the project.

## The pitch:
Air quality degradation is not a new problem and a number of steps have been taken to help counteract it. Information about the air quality in someone’s immediate environment can help them make smarter decisions and lifestyle choices.

After doing some basic trend analysis and research on the impact of air quality on human life, we decided to develop a durable air quality sensor, integrated with consumer health data.

The project itself was split into multiple modules:

* Developing the air quality sensor
* Using air quality data from weather stations as a control for real time sensor data
* Determining the impact of air quality on human health
* Providing recommendations based on user health conditions

## The setup:
The internet of things suggests a simple concept: everyday objects used for all sorts of different activities can be connected to the internet (and with each other). Everything ranging from cars, machines, appliances and even things like roads and humans are also a part of this network.

The project had three important components (all provided by the event organizers):

* LoRa IoT development board
* Gas Sensor
* Dust Sensor

### Dust Sensor:
The primary purpose of this sensor is to measure air quality both indoor and outdoor (particles per million (ppm) for NH3, NOx, alcohol, Benzene, smoke, CO2 etc.) The feature that makes them stable working machines is a simple driver circuit, a wide detecting scope, and a fast and high sensitivity response time.

![air quality sensor]({{ site.url }}/assets/images/sensor.jpg)
<i>Board with sensors</i>

### Gas Sensor
Gas sensor is an SNO2 heating sensor, which is highly sensitive to alcohol and mildly sensitive to Benzene components. These hardwearing sensors make a good choice for a project such as this.

The heating tube is made of aluminium oxide and is covered by SnO2. When the current passes through the tube it heats up and the tin dioxide acts like a semiconductor. This allows a large number of electrons to flow through and increases the current flow. When alcohol molecules and the sensor come into close proximity, the ethanol burns transforming into acetic acid, creating a higher current across the sensor. The current change alters the values of the sensor.

## Analytics:
Once the setup was completed, the sensor data was streamed directly to a firebase mobile platform. A simple mobile application was developed to get the data from the platform and provide real time readings to the user. The mobile application also features threshold adjustments for the air quality index according to the user’s health.

![sensor and app]({{ site.url }}/assets/images/sensor-and-app.jpg)
<i>Board with sensors and application</i>

The air quality data from nearby weather stations was gathered from the OpenAQ platform and stored using a web application. This data was primarily used to control and eliminate abnormal readings from the consumer air quality sensor.

## Conclusion:
This work presents a system to understand pollution accumulation levels at various locations and helps structure the readings with the help of real-time analytics. It can also help redirect vehicles and pedestrians to alternative routes with lower pollutant levels, helping reduce vehicular pollution and encouraging a healthier lifestyle.

Based on the analysis conducted, these findings are promising. The proposed system is much more cost-effective compared to other air monitoring devices and technologies, with its most stark functionality being a combination of Internet of Things and Analytics of Things at the same time.

Real-life implementation of this prototype will benefit a large number of people and help create a healthier society – a step in the right direction to creating a SMART CITY.

![Martin and Me]({{ site.url }}/assets/images/winners.jpg)
<i>Martin and me after winning "Best Smart City Solution" award</i>

## References:
* Research on Health and Environmental Effects of Air Quality - https://www.epa.gov/air-research/research-health-and-environmental-effects-air-quality
* Air pollution and cardiovascular disease - http://circ.ahajournals.org/content/109/21/2655
* Air Pollution and Cardiovascular Disease - http://circ.ahajournals.org/content/109/21/2655

![team]({{ site.url }}/assets/images/team.jpg)
<i>With the team</i>
