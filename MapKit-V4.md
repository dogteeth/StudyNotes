[關於Bounding Box](https://wiki.openstreetmap.org/wiki/Bounding_Box)

- A bounding box (usually shortened to bbox) is an area defined by two longitudes and two latitudes, where:
- Latitude is a decimal number between -90.0 and 90.0.
- Longitude is a decimal number between -180.0 and 180.0.

- bbox = left,bottom,right,top
- bbox = min Longitude , min Latitude , max Longitude , max Latitude 


- one latitude/one longitutde  = 111 km
- latitude 為南北緯
- longitude 為東西經



[other property for cllocation](https://www.advancedswift.com/user-location-in-swift/)

```swift
// Altitude
let altitude = location.altitude

// Speed
let speed = location.speed

// Course, degrees relative to due north
let source = location.course

// Distance between two CLLocation
// Given another CLLocation, otherLocation
let distance = location.distance(from: otherLocation)

```
