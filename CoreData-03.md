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
