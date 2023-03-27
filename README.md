# PCA for Motorcycle Accidents

This notebook highlights an interesting solution I discovered when working on a professional project to automatically detect motorcycle collisions with an insurance black box. The solution was developed for a company delivering solutions for East Africa where motorcycles transport is the most common form of transportation.

I have permission to share these results. Since much of the work I completed is deemed intellectual property for the company I'm only including a small subsection. 

## Context for the problem

Insurance black boxes were designed for cars. Retrofitting them on to motorcycles means the inbuilt algrorithms have to be modified. In particular:

- Devices have to fitted at awkward angles. This was throwing off the device calibration (i.e. the device does not know which way is forward)
- The devices are placed close to the engine. This means vibration from the engine presents itself as significant noise to the acclerometer.

The insurance boxes have two sensors:

- GPS 
- Acceromter

Notetably there is no gyroscope (you don't need on a car!). The sensors store information locally at 1 second intervals and then push to an Azure SQL database whenever a mobile internet connection can be established.

![Insurance box location](images/motoinsurance.png)

Hopefully my expertly drawn addition helps with understanding where these boxes are located on motorcycles.


