

#### 取得user所在，與目標地址，製作路線圖。
[資料來源](https://www.youtube.com/watch?v=UOEx8sb3HeY&list=PLFLnrHt5OblebeFVd6CFapMjkYWQVeumc&index=5)

取得定位資料
1. import MapKit
2. 做CLlocationManager的object，設定值。
3. 需要在plist上取得用戶同意，取得用戶定位資料。



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


#### 雜記

***
[資料來源](https://codertw.com/ios/17724/)
在MKMapView上新增標註可以方便使用者更好地獲取資訊，與地圖進行互動。
標註分為兩種，一種是Annotations，一種是Overlays。
Annotations。標註由經緯度所確定的一個點，比如使用者當前位置，一個被指定的地址，或者一個被收藏的地點。
Overlays。標註由多點連成的線，一個或者多個相鄰或不相鄰的區域。比如路線、交通狀況、或者某個地點的邊界。
和MKMapView中的subView不同，Annotations和Overlays會隨著地圖的移動而移動。

***
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
