#### Standart data type:
- UIID: universally unique identifier
- URI: uniform resource identifier, all URLs is URI
- Binary Data: from images, PDF files, anything that can be serialized into zeroes and ones. and it "Allows External Storage". When use "Allows External Storage", core data heuristically decides on a per-value basis if it should save the data directly in the database or store a URI that points to a separate file. Note: The Allows External Storage option is only available for the binary data attribute type. In addition, if you turn it on, you won't be able to query Core Data using this attribute.

#### Non-standard data type:
- Transformable
- Transformable attributes persist data types that are not listed in Xcode Data Model Inspector. These include types that Apple ships in their frameworks such as UIColor and CLLocationCoordinate2D as well as your own types. (自己的Type！！！！）
- 1): Add NSSecureCoding protocol conformance to the backing data type.
- 2): Create and register an NSSecureUnarchiveFromDataTransformer subclass
- 3): Associate the custom data transformer subclass with the Transformable attribute in the Data Model Editor
- Most data types in Apple's frameworks already confrom to NSSecureCoding.


```Swift

/*
 allowedTopLevelClasses:
 
 This property contains the value of transformedValueClass() if that value isn’t nil. Otherwise, it holds a list of the top level classes that it decodes, which includes NSArray, NSDictionary, NSSet, NSString, NSNumber, NSDate, NSData, NSURL, NSUUID, and NSNull.
 
 Override this property in subclasses to provide an expanded or different set of allowed transformation classes.
 */




/*
 NSSecureUnarchiveFromDataTransformer
 A value transformer that converts data to and from classes that support secure coding.
 
 This class provides a default ValueTransformer implementation for secure decoding. This class attempts to decode data into the classes listed within allowedTopLevelClasses, which includes NSArray, NSDictionary, NSSet, NSString, NSNumber, NSDate, NSData, NSURL, NSUUID, and NSNull.
 
 To archive or unarchive other classes that support NSSecureCoding, create a subclass and override allowedTopLevelClasses to list the classes to transform.
 
 To use NSSecureUnarchiveFromDataTransformer with Core Data, use the name of this class, or the name of a subclass you implement, as the name of the transformer for an entity’s attribute within a Core Data Model. If you use your own transformer subclass, register it with your app before intializing your persistent container with Core Data.
 
 For an example of subclassing NSSecureUnarchiveFromDataTransformer, see Handling Different Data Types in Core Data, which has a ColorToDataTransformer class that transforms UIColor to NSData and the reverse, to support archiving instances of UIColor.
 */


import UIKit

class ColorAttributeTransformer: NSSecureUnarchiveFromDataTransformer {
 
 
  override class var allowedTopLevelClasses: [AnyClass] {
    [UIColor.self]
  }
  

  
  static func register() {
    let className = String(describing: ColorAttributeTransformer.self)
    
    let name = NSValueTransformerName(className)
    
    let transformer = ColorAttributeTransformer()
    ValueTransformer.setValueTransformer(transformer, forName: name)
  }
}
```
<img width="928" alt="Screen Shot 2022-01-03 at 6 40 35 PM" src="https://user-images.githubusercontent.com/18608853/147921781-4746e709-a8aa-4a25-8e31-2c8952f2338f.png">

