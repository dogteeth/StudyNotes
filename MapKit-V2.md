#### 把Pin放到地圖裹
- IBOutlet的mapView
- import MapKit(mapView需要這個module)
- mapView.addAnnotation(MKAnnotation)

```Swift
func mapAnnotationSetup() {
        guard let items = CoreDataManager.shared.fetchAllItems() else {return}
        for eachItem in items {
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
```

- CaseAnnotation的設計如下：

```Swift
import Foundation
import MapKit

class CaseAnnotation: NSObject, MKAnnotation {
    let title : String?
    let item: Item
    let coordinate: CLLocationCoordinate2D
    
    init(
        title: String?,
        item : Item,
        coordinate : CLLocationCoordinate2D
    ){
        self.title = title
        self.item = item
        self.coordinate = coordinate
        super.init()
    }
       
}
```


#### AnnotationPin的設計
- 在 mapView的function裹做設計。
- mapView(_ mapView: MKMapView, viewFor annotation: MKAnnotation) -> MKAnnotationView?
- 這個func是在protocol：MKMapViewDelegate，要在ViewController 做 extension。
- 設 mapView.delegate = self
- callout的設計，也放在 viewFor這個function裹。
```Swift
 func mapView(_ mapView: MKMapView,
                 viewFor annotation: MKAnnotation) -> MKAnnotationView? {
        
        guard annotation is CaseAnnotation else { return nil }
        
        let identifier = "pin"
        
        var annotationView = mapView.dequeueReusableAnnotationView(withIdentifier: identifier) as? MKPinAnnotationView
         
        annotationView = MKPinAnnotationView(annotation: annotation, reuseIdentifier: identifier)
        
        annotationView?.canShowCallout = true
        annotationView?.rightCalloutAccessoryView = UIButton(type: .detailDisclosure)
        
        annotationView?.clusteringIdentifier = "clusterPin"
        
        return annotationView
    }

```

#### 地圖的大頭針的互動設計

- 點大頭針上的callout action，（同一個protocol下的function來處理）

notes: 重要要讓 view.annotation，需要 downcast as CaseAnnotation, 才能抓出item做passing.
```Swift

  func mapView(_ mapView: MKMapView,
           annotationView view: MKAnnotationView,
           calloutAccessoryControlTapped control: UIControl) {

        guard let caseAnnotation = view.annotation as? CaseAnnotation else { return }
        
        itemForSegue = caseAnnotation.item
        //then peform seque:

    }

```

- 點大頭針即把地圖中心移過去

notes: 抓出 view.annotation 的coordinat, 做處理。

```Swift
func mapView(_ mapView: MKMapView, didSelect view: MKAnnotationView){
        guard let centerCoordinate = view.annotation?.coordinate else {return}
        mapView.setCenter(centerCoordinate, animated: true)
}
```
