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


```




