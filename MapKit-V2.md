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
- 設 delegate to self.這個我不大確定。
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

- callout的action設計，則由同一個protocol下的function來處理。
```Swift

  func mapView(_ mapView: MKMapView,
           annotationView view: MKAnnotationView,
           calloutAccessoryControlTapped control: UIControl) {
        print("good")
    }

```
