#### 地圖的製作

- storyboard 加入 mapView
- import MapKit
這兩部份，即可完成基本地圖出現

#### 在地圖上加入user的座標

- import CoreLocation
- class需要extension CLLocationManagerDelegate
- let locationManager = CLLocationManager()
- locationManager.delegate = self
- locationManager.startUpdatingLocation()
- 再以 didUpdateLocations 的 function 處理 user location資料。

```swift
 override func viewDidLoad() {
        super.viewDidLoad()
        
        items = CoreDataManager.shared.fetchAllItems()

        locationManager.delegate = self
        locationManager.desiredAccuracy = kCLLocationAccuracyKilometer
        locationManager.startUpdatingLocation()
        mapView.showsUserLocation = true
        refreshMapAnnotations()
    }
    
    func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        
        let userLocation = locations[0] as CLLocation
        
        centerUserLocation(userLocation: userLocation)
        
        
    }
    
    func refreshMapAnnotations() {
        
        self.mapView.removeAnnotations(self.mapView.annotations)
        
        guard let safeItems = items else {return}
        for eachItem in safeItems {
            let newAnnotation = CaseAnnotation(
                title: eachItem.caseName,
                item: eachItem,
                coordinate:
                    CLLocationCoordinate2D(
                        latitude: eachItem.latitude,
                        longitude: eachItem.longitude))
            
            mapView.addAnnotation(newAnnotation)
            
        }
        
    }
    
  
    
    func centerUserLocation(userLocation: CLLocation) {
        let TrackingUser = MKUserTrackingButton(mapView: mapView)
        navigationItem.rightBarButtonItem = UIBarButtonItem(customView: TrackingUser)
        
        //數字越大，鳥眼的高度越越高。
        let region = MKCoordinateRegion(center: CLLocationCoordinate2D(latitude: userLocation.coordinate.latitude, longitude: userLocation.coordinate.longitude), latitudinalMeters: 1000, longitudinalMeters: 1000)
        
        mapView.setRegion(region, animated: true)
        
    }
    


```

#### 打開google map
- plist 加入設定
- 加入function



![LSApplicationQueriesSchemes](https://user-images.githubusercontent.com/18608853/120062152-3d884b80-c093-11eb-9e21-a50360b7af5c.png)

```Swift

 func openGoogleMap() {
        
        let latDouble = item?.latitude ?? 0
        let longDouble = item?.longitude ?? 0
        
        if (UIApplication.shared.canOpenURL(URL(string:"comgooglemaps://")!)) {  //if phone has an app
            
            if let url = URL(
                string:
                    
                    //"comgooglemaps://?saddr=&daddr=\(Float(latitude!)),\(Float(longitude!))&directionsmode=driving"
                    
                    "comgooglemaps://?saddr=&daddr=\(latDouble),\(longDouble)"
            ) {
                UIApplication.shared.open(url, options: [:])
            }}
        else {
            //Open in browser
            if let urlDestination = URL.init(string: "https://www.google.co.in/maps/dir/?saddr=&daddr=\(latDouble),\(longDouble)&directionsmode=driving") {
                UIApplication.shared.open(urlDestination)
            }
        }
        
    }
```

