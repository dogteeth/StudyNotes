取得GPS定位資料
1. import MapKit
2. 做CLlocationManager的object


```Swift

import Mapkit

//製作CLlocationManager的分身
let locationManager:CLlocationManager = CLlocationManager()

//如果user跳去使用別的app，仍然需要持續取得定位。
locationManager.requestWhenInUseAuthorization()

locationManager.desiredAccuracy = kCLlocationAccurayBest

locationManager.distanceFilter = kCLDistanceFilterNone

locationManager.startUpdatingLocation()

```
