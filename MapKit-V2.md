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

CaseAnnotation的設計如下：

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
