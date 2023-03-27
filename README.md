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

# The data

| device.name   |   timestamp |   x.acceleration |   y.acceleration |   z.acceleration | engine.ignition.status.1   |
|:--------------|------------:|-----------------:|-----------------:|-----------------:|:---------------------------|
| Bike 07       | 1.65662e+09 |            0.236 |           -0.241 |           -0.128 | False                      |
| Bike 07       | 1.65662e+09 |            0.236 |           -0.241 |           -0.128 | False                      |
| Bike 07       | 1.65662e+09 |            0.132 |            0.067 |           -0.03  | True                       |
| Bike 07       | 1.65662e+09 |            0.146 |            0.097 |           -0.085 | True                       |
| Bike 07       | 1.65662e+09 |           -0.06  |            0.079 |            0.603 | True                       |'



