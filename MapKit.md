加入地圖的方式：
1. import MapKit
2. 從library拉地圖的元件到view裹
3. 替元件做一個IBOutlet.
4. 製作function：輸入座標後，就可以在地圖上表示地點。



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
