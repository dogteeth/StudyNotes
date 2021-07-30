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

#### CLLocation & CLLocationCoordinate2D
- CLLocation : A CLLocation object contains the geographical location and altitude of a device, along with values indicating the accuracy of those measurements and when they were collected. In iOS, a location object also contains course information — that is, the speed and heading in which the device was moving. 
- Typically, you don’t create location objects yourself. After you request location updates from your CLLocationManager object, the system uses onboard sensors to gather location data and report that data to your app. Some services also return previously collected location data, which you can use as context to improve your services. You can always retrieve the most recently collected location from the location property of your CLLocationManager object. You may create location objects yourself when you want to cache custom location data or calculate the distance between two geographical coordinates.
- CLLocationCoordinate2D: The latitude and longitude associated with a location, specified using the WGS 84 reference frame.


#### CLLocation埋程式要注意的事
- locationManager要取得gps定位，會花時間。
- 需要取得coordinate的資料才做事情的程式，要放在didUpdateLocations的function裹。 
   - 譬如：table view的資料，依update location後來推薦，即放在didUpdateLocations的function。之後再做reload data.


#### 依userGPS 取得一定區域內的pin
```Swift
func fetchCasesNearBy10kilometer() {
        
        caseNearBy10Kilo.removeAll()
        let baseLatitude:Double = userLocationValue?.latitude ?? 0 //25.084845
        let baseLongitude:Double =  userLocationValue?.longitude ?? 0 //121.567158
        let rangeNearBy:Double = 0.009 * ragneKilo //一公里等於0.009經緯度
        let index = items?.count ?? 0
        
        for a in 0...(index - 1) {
            guard let safeItem = items?[a] else {return}
            
            if safeItem.latitude < baseLatitude + rangeNearBy && safeItem.latitude > baseLatitude - rangeNearBy && safeItem.longitude < baseLongitude + rangeNearBy && safeItem.longitude > baseLongitude - rangeNearBy {
                print(safeItem.caseName ?? "" )
                caseNearBy10Kilo.append(safeItem)
            }
        }
        
```


#### 把所有的pin全部秀在mapView上。

```Swift
func showAnnotations(_ annotations: [MKAnnotation],  animated: Bool)
```
- annotations：The annotations that you want to be visible in the map.
- animated： true if you want the map region change to be animated, or false if you want the map to display the new region immediately without animations.

```Swift
mapView.showAnnotations(annotationArray, animated: true)
```
- 實際的例子：
```Swift

   func refreshMapAnnotations(mapView: MKMapView , items:[Item]?) {
        
        mapView.removeAnnotations(mapView.annotations)
        
        var annotationArray : [MKAnnotation] = []
        
        guard let safeItems = items else {return}
        for eachItem in safeItems {
            let newAnnotation = CaseAnnotation(
                title: eachItem.caseName,
                item: eachItem,
                coordinate:
                    CLLocationCoordinate2D(
                        latitude: eachItem.latitude,
                        longitude: eachItem.longitude)
            )
            annotationArray.append(newAnnotation as MKAnnotation)
        }
        mapView.showAnnotations(annotationArray, animated: true)

    }
```
