加入地圖的方式：
1. import MapKit, CoreLocation
2. 從library拉地圖的元件到view裹
3. 替元件做一個IBOutlet, ex mapView
4. 製作function：輸入座標後，就可以在地圖上表示地點。

授權
- 取得CLLocationManager()的 instance
- 以instance呼叫授權。

地圖標示
- 取得MKPointAnnotation()的 instance
- 以instance，取得coordinate的method,即可將instace定位在特定的座標
- 以addAnnotation這個method, 把MKPointAnnotation的 instance加入 map.即完成。


```Swift
let locationManager  = CLLocationManager()
locationManager.requestWhenInUseAuthorization()

let pin = MKPointAnnotation()
pin.coordinate = CLLocationCoordinate2D(latitude: XXXXX, longitude: XXXXX)
pin.title = "XXXX"
mapView.addAnnotation(pin)

mapView.setCenter(pin.coordinate, animated: false)

```

做成function，如這個例子，傳入座標，即可出現在地圖上。。



```Swift

func markMap(longitude long:Double, latitude lat:Double){
        
        let annotation = MKPointAnnotation()
        annotation.coordinate = CLLocationCoordinate2D(latitude: lat, longitude: long)
       
        //title後的變數名稱，會出現在地圖圖釘的標示裹。
        annotation.title = caseNameString
        
        mapView.addAnnotation(annotation)
        
        //設定地圖的大小。數字越小，地圖放的越大。
        let region = MKCoordinateRegion(center: annotation.coordinate, latitudinalMeters: 5000, longitudinalMeters: 5000)
        
        mapView.setRegion(region, animated: true)   
    }


```
加入地圖的方式：
1. import MapKit, CoreLocation
2. 從library拉地圖的元件到view裹
3. 替元件做一個IBOutlet, ex mapView
4. 製作function：輸入座標後，就可以在地圖上表示地點。

#### 授權
- import CoreLocation
- notes: Info.plist，要設定 Privacy-whenInUse
- 製作CLLocationManager()的instance
- 以instance呼叫 requestWhenInUseAuthorization 的 method

#### CLLocationManager的操作
- 取得CLLocationManager的instance -> locationManager
- extension CLLocationManagerDelegate, 同時 locationManager要設 delegate ＝ self。
- locationManager 設定三件事： 1. desiredAccuracy, 2. distanceFilter, 3.startUpdatingLocation
- 呼叫function "didUpdateLocations"，設定，當取回location的值後，即停止更新（這個要依不同狀況自行更改）。同時在地圖上註記所在位置。

- 註記所在位置的方式：(從後頭往回寫）
>> <1>在mapView上畫一個鳥眼區域 -> mapView.setRegion(region, animated: true)
>> <2>鳥眼區域的設定 -> let region = MKCoordinateRegion(center: coordinate, span: span)
>> <3>設定鳥眼區域需要兩個變數，2D地理定位CLLocationCoordinate2D，鳥眼高度距離MKCoordinateSpan(latitudeDelta: 1, longitudeDelta: 1)，數字越大，高度越高。顯示的區域越大。

notes:
1. 取得user的location(CLLocation的2D定位，longitude, latitude, (CLLocationCoordinate2D)
2. 以user所在location為中心，設定鳥眼區域（MKCoordinateRegion）,鳥眼高度（MKCoordinateSpan）
3. 最後，將區域加入地圖。



範例：

```swift

import UIKit
import MapKit
import CoreLocation

class ViewController: UIViewController, CLLocationManagerDelegate {
    
    @IBOutlet weak var mapView: MKMapView!
    
    let locationManager = CLLocationManager()
    
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        locationManager.delegate = self
        locationManager.desiredAccuracy = kCLLocationAccuracyKilometer
        
        locationManager.distanceFilter = kCLDistanceFilterNone
        
        locationManager.startUpdatingLocation()
        
        mapView.showsUserLocation = true
        
        // Do any additional setup after loading the view.
    }
    
    func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        if let location  = locations.first {
            locationManager.stopUpdatingLocation()
            render(location)
        }
    }
    
    func render(_ location: CLLocation) {
        
        let coordinate = CLLocationCoordinate2D(latitude: location.coordinate.latitude, longitude: location.coordinate.longitude)
        
        //數字越大，鳥眼的高度越越高。
        let span = MKCoordinateSpan(latitudeDelta: 1, longitudeDelta: 1)
        let region = MKCoordinateRegion(center: coordinate, span: span)
        
        mapView.setRegion(region, animated: true)
        
        let pin = MKPointAnnotation()
        pin.coordinate = coordinate
        mapView.addAnnotation(pin)
    }
    
}

```






地圖標示
- 取得MKPointAnnotation()的 instance
- 以instance，取得coordinate的method,即可將instace定位在特定的座標
- 以addAnnotation這個method, 把MKPointAnnotation的 instance加入 map.即完成。


```Swift
let locationManager  = CLLocationManager()
locationManager.requestWhenInUseAuthorization()

let pin = MKPointAnnotation()
pin.coordinate = CLLocationCoordinate2D(latitude: XXXXX, longitude: XXXXX)
pin.title = "XXXX"
mapView.addAnnotation(pin)

mapView.setCenter(pin.coordinate, animated: false)

```

做成function，如這個例子，傳入座標，即可出現在地圖上。。



```Swift

func markMap(longitude long:Double, latitude lat:Double){
        
        let annotation = MKPointAnnotation()
        annotation.coordinate = CLLocationCoordinate2D(latitude: lat, longitude: long)
       
        //title後的變數名稱，會出現在地圖圖釘的標示裹。
        annotation.title = caseNameString
        
        mapView.addAnnotation(annotation)
        
        //設定地圖的大小。數字越小，地圖放的越大。
        let region = MKCoordinateRegion(center: annotation.coordinate, latitudinalMeters: 5000, longitudinalMeters: 5000)
        
        mapView.setRegion(region, animated: true)   
    }


```


#### 取得user所在，與目標地址，製作路線圖。
[資料來源](https://www.youtube.com/watch?v=UOEx8sb3HeY&list=PLFLnrHt5OblebeFVd6CFapMjkYWQVeumc&index=5)

製作方式：
1. import MapKit
2. 做CLlocationManager的object，設定值。
3. 需要在plist上取得用戶同意，取得用戶定位資料。 

注意事項：
1. Privacy-Location when in use。用戶的狀態有三種，Authorized, Denied, Restricted. Denied的狀態時，可以再次提醒用戶，需要同意才能進行。若是Restricted, 則無需再詢問，因為這是該用戶的當下設定己被限制，譬如企業內的用戶等。
2. Generally it's a good idea to add all your annotations up-front. Annotations are light weight, but annotation views are not. MKMapView reuses annotation views similar to how UITableView reuses cells.
3. map view type: mapType = .Standard .Sattellite .Hybrid
4.可以決定地圖出現的區域大小。用 MKCoordinateRegion, MKCoordinateSpan(Span用的是CLLocationDegrees



```Swift

import Mapkit

//製作CLlocationManager的分身
let locationManager:CLLocationManager = CLlocationManager()

//如果user跳去使用別的app，仍然需要持續取得定位。
locationManager.requestWhenInUseAuthorization()

locationManager.desiredAccuracy = kCLLocationAccuracyBest

locationManager.distanceFilter = kCLDistanceFilterNone

locationManager.startUpdatingLocation()


//顯示user的所在地

mapView.showsUserLocation = true

```
另外的notes

1. CLLocationManagerDelegate，
2. MKMapViewDelegate
3. .desiredAccuracy = kCLLocationAccuracyBest，有多種選擇，越精細花的電力越大。kCLlocationAccurracyNearestTenMeters



顯示前再次檢查是否有授權，如果沒有，做提醒。

```Swift

func checkLocationAuthorization() {
  switch CLLocatioManager.authorizationStatus() {
  case .authorizedWhenInUse:
    mapView.showUserLocation = true
    locationManager.startUpdatingLocation()
    centerOnUsersLocation()
  case .notDetermined:
    locationManager.requestWhenInUseAuthorization()
  case .denied:
    locationDeniedAlert()
  case .restricted
    ///
  default:
    break
  }
}
```


一次性的取得User的座標
```Swift

func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
  guard let userLocation = location.last else { return }
  
  manager.stopUpdatingLocation()
  usersLastLocation = userLocation
  
  print(userLocation.coordinate.latitude)
  print(userLocation.coordinate.longitude)

}

```

取得路線圖

```Swift

func getCoordinatesForLocationsText() {
  
  //Clear old pins and route first
  let annotations = self.mapView.annotations
  mapview.removeAnnotaions(annotations)
  let overlays = mapView.overlays
  mapView.removeOverlays(overlays)
  
  
  //user輸入text
  
  guard let startAddress = startTextField.text
    !startAddress.isEmpty else {
      print("no start address text, error")
      return
    }
    
  guard let endAddress = endTextField.text
    !endAddress.isEmpty else {
      print("no end address text, error")
      return
    }
    
  
  var startPin: CustomPin?
  var endPin: CustomPin?

  //Get coordinates for the first location
  
  CLGeocoder().geocodeAddressString(startAddress) { (placemarks, error) in
    if error != nil {
      print("CLGeocoder error")
      return
    }
    
    //回傳的placemarks是一個array, 因為符合地址的座標，可能一個也可能是多個。
    if let placemark = placemarks?[0] {
      
      //把取得的座標，轉成字串，做使用。
      let startLatitudeString = String(format: "%.04f", placemark.location?.coordinate.latitude ?? 0.0)
      let startLongitudeString = String(format: "%.04f", placemark.location?.coordinate.longtitude ?? 0.0)

      print( /* 說明文字   */  ）
      
      let startLatitude = placemark.location?.coordinate.latitude ?? 0.0
      let starLongititude = placemark.location?.coordinate.longitude ?? 0.0
      let coordinate = CLLocationCoordinate2D(latitude: startLatitude, longitude: startLongitude)
      
      let pin =  CustomPin(pintTitle: startAddress, pinSubTitle: startAddress, location: coordinate)
      startPin = pin
      
      
      // 

    } 
  }
}

```

```Swift

import Foundation
import MapKit

class CustomPin: NSObject, MKAnnotation {

  var coordinate : CLLocationCoordinate2D
  var title: String?
  var subtitle: String?
  
  init(pinTitle: String, pinSubTitle: String, location: CLLocationCoordinate2D) {
    self.title = pinTitle
    self.subtitle = pinSubTitle
    self.coordinate = location
  }
}

```


***
#### 雜記
***

[資料來源](https://codertw.com/ios/17724/)
在MKMapView上新增標註可以方便使用者更好地獲取資訊，與地圖進行互動。
標註分為兩種，一種是Annotations，一種是Overlays。
Annotations。標註由經緯度所確定的一個點，比如使用者當前位置，一個被指定的地址，或者一個被收藏的地點。
Overlays。標註由多點連成的線，一個或者多個相鄰或不相鄰的區域。比如路線、交通狀況、或者某個地點的邊界。
和MKMapView中的subView不同，Annotations和Overlays會隨著地圖的移動而移動。


自訂地圖羅盤：
showCompass = true
由於，地圖本身有個預設地圖，移動地圖方向就會出現，所以要把它false，自己再做一個。


```Swift
 let compassButton = MKCompassButton(mapView: mapView)
        compassButton.compassVisibility = .visible
        
        /* 
         *  設定compass的位置，CGPoint(x, y)
         * self.view.bounds.width --> 營幕的寛度。
         */
        compassButton.frame.origin = CGPoint(x: self.view.bounds.width - 50, y: 20)
        //mapView是自定的var 
        mapView.addSubview(compassButton)

```


其它功能：
showTraffic
showScale



#### 地圖上加入指方向的箭頭。
```Swift
  let TrackingUser = MKUserTrackingButton(mapView: mapView)
  navigationItem.leftBarButtonItem = UIBarButtonItem(customView: TrackingUser)
```

