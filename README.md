# PCA for Motorcycle Accidents

This notebook highlights an interesting solution I discovered when working on a professional project to automatically detect motorcycle collisions with an insurance black box. The solution was developed for a company delivering solutions for East Africa where motorcycles transport is the most common form of transportation.

I have permission to share these results. Since much of the work I completed is deemed intellectual property for the company I'm only including a small subsection. 

## The problem

> Automatically calibrate the insurance box without physical intervention in order to automatically detect when a motorcycle has an accident.

Once the devices are calibrated detecting accidents are trivial - We just need to know when the bike is on it's side. In particular we just need to know when acceleration due to gravity is no longer downwards.


## Context for the problem

Insurance black boxes were designed for cars. Retrofitting them on to motorcycles means the inbuilt algrorithms have to be modified. In particular:

- Devices have to fitted at awkward angles. This was throwing off the device calibration (i.e. the device does not know which way is forward)
- The devices are placed close to the engine. This means vibration from the engine presents itself as significant noise to the acclerometer.
- Motorcycles are much more bumpy then cars.

The insurance boxes have two sensors:

- GPS 
- Acceromter

Notetably there is no gyroscope (you don't need on a car!). The sensors store information locally at 1 second intervals and then push to an Azure SQL database whenever a mobile internet connection can be established.

![Insurance box location](images/motoinsurance.png)

Hopefully my expertly drawn addition helps with understanding where these boxes are located on motorcycles.

## Wider context

Motor vechile accidents are a major problem in East Africa (where the company I developed this solution for is from). Moreover motocycle taxis (or Motos as they are called locally) are a the main form of transport for most of the population.

Table below shows that motorvechile deaths per 100,000 inhabitants are globally highest in Africa. The system being designed will be able to alert emergency services when a moto-taxi has had a serious colision.

| Country/region        |   Deaths per 100k/year |
|:----------------------|-----------------------:|
| Africa                |                   26.6 |
| South-East Asia       |                   20.7 |
| Global                |                   18.2 |
| Eastern Mediterranean |                   18   |
| Western Pacific       |                   16.9 |
| Americas              |                   15.6 |
| Europe                |                    9.3 |

[wiki source](https://en.wikipedia.org/wiki/List_of_countries_by_traffic-related_death_rate)

Kenya is particurally bad globally with 29.1 deaths per 100k inhabitants per year. Which means you have a 0.0291% chance of dying in a vehcile accident (Interesting fact: Obama's dad died in a car collision in Kenya). 

| Country/region   | Continent   |   Deaths per 100k/year |   Percentile |
|:-----------------|:------------|-----------------------:|-------------:|
| Kenya            | Africa      |                   29.1 |     0.936508 |


# The data

Below is a few rows and important columns from the dataset.

| device.name   |   timestamp |   x.acceleration |   y.acceleration |   z.acceleration | engine.ignition.status.1   |
|:--------------|------------:|-----------------:|-----------------:|-----------------:|:---------------------------|
| Bike 07       | 1.65662e+09 |            0.236 |           -0.241 |           -0.128 | False                      |
| Bike 07       | 1.65662e+09 |            0.236 |           -0.241 |           -0.128 | False                      |
| Bike 07       | 1.65662e+09 |            0.132 |            0.067 |           -0.03  | True                       |
| Bike 07       | 1.65662e+09 |            0.146 |            0.097 |           -0.085 | True                       |
| Bike 07       | 1.65662e+09 |           -0.06  |            0.079 |            0.603 | True                       |'

This bike is uncalibrated so the x acceleration is not necessarily the forward acceleration. We need to change the coordinate system of the data points so the x acceleration is describing the acceleration in the forward direction. The interactive graph below shows the data points for a particular bike aligned offaxis.

{% include_relative images/uncalibrated.html %}





