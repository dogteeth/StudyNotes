#### cache image
[source link](https://medium.com/flawless-app-stories/reusable-image-cache-in-swift-9b90eb338e8d)

- Using NSCache as a storage
- image rendering pipeline
    - loading: loads compressed images into memory.
    - decoding: converts ecoded image data in per pixel image information.
    - rendering: copies and scales the image data from the image buffer into the frame buffer.
- In memory image cache

```Swift
// Declares in-memory image cache
protocol ImageCacheType: class {
    // Returns the image associated with a given url
    func image(for url: URL) -> UIImage?
    // Inserts the image of the specified url in the cache
    func insertImage(_ image: UIImage?, for url: URL)
    // Removes the image of the specified url in the cache
    func removeImage(for url: URL)
    // Removes all images from the cache
    func removeAllImages()
    // Accesses the value associated with the given key for reading and writing
    subscript(_ url: URL) -> UIImage? { get set }
}
```

#### 壓縮圖片的方式


[來源](https://stackoverflow.com/questions/29137488/how-do-i-resize-the-uiimage-to-reduce-upload-image-size/29138120)


- 直接縮小圖檔
```Swift

let image = UIImage(data: try! Data(contentsOf: URL(string:"http://i.stack.imgur.com/Xs4RX.jpg")!))!

let thumb1 = image.resized(withPercentage: 0.1)
let thumb2 = image.resized(toWidth: 72.0)


extension UIImage {
    func resized(withPercentage percentage: CGFloat, isOpaque: Bool = true) -> UIImage? {
        let canvas = CGSize(width: size.width * percentage, height: size.height * percentage)
        let format = imageRendererFormat
        format.opaque = isOpaque
        return UIGraphicsImageRenderer(size: canvas, format: format).image {
            _ in draw(in: CGRect(origin: .zero, size: canvas))
        }
    }
    func resized(toWidth width: CGFloat, isOpaque: Bool = true) -> UIImage? {
        let canvas = CGSize(width: width, height: CGFloat(ceil(width/size.width * size.height)))
        let format = imageRendererFormat
        format.opaque = isOpaque
        return UIGraphicsImageRenderer(size: canvas, format: format).image {
            _ in draw(in: CGRect(origin: .zero, size: canvas))
        }
    }
}


```

- 判斷檔案大小，進行resize
```Swift

let resizedImage = originalImage.resizedTo1MB()



extension UIImage {

func resized(withPercentage percentage: CGFloat) -> UIImage? {
    let canvasSize = CGSize(width: size.width * percentage, height: size.height * percentage)
    UIGraphicsBeginImageContextWithOptions(canvasSize, false, scale)
    defer { UIGraphicsEndImageContext() }
    draw(in: CGRect(origin: .zero, size: canvasSize))
    return UIGraphicsGetImageFromCurrentImageContext()
}

func resizedTo1MB() -> UIImage? {
    guard let imageData = UIImagePNGRepresentation(self) else { return nil }

    var resizingImage = self
    var imageSizeKB = Double(imageData.count) / 1000.0 // ! Or devide for 1024 if you need KB but not kB

    while imageSizeKB > 1000 { // ! Or use 1024 if you need KB but not kB
        guard let resizedImage = resizingImage.resized(withPercentage: 0.9),
            let imageData = UIImagePNGRepresentation(resizedImage)
            else { return nil }

        resizingImage = resizedImage
        imageSizeKB = Double(imageData.count) / 1000.0 // ! Or devide for 1024 if you need KB but not kB
    }

    return resizingImage
  }
}
```
#### image loading時，加入動畫
```Swift
extension UIImageView {
    fileprivate var activityIndicator : UIActivityIndicatorView {
        get {
            
            let activityIndicator = UIActivityIndicatorView(style: .large)
            activityIndicator.hidesWhenStopped = true
            activityIndicator.center = CGPoint(x:self.frame.width/2, y:self.frame.height/2)
            
            activityIndicator.stopAnimating()
            self.addSubview(activityIndicator)
            return activityIndicator
        }
    }
}

```
#### UIImage 黑白濾鏡
[資料連結](https://stackoverflow.com/questions/40178846/convert-uiimage-to-grayscale-keeping-image-quality)

![vuqcr](https://user-images.githubusercontent.com/18608853/128105728-5481aada-f179-4661-b8a3-59603bfe0091.png)

- CIFilter(name: "CIPhotoEffectNoir")，CIPhotoEffectNoir 可以換成  CIPhotoEffectTonal, CIPhotoEffectMono
```Swift
extension UIImage {
    var noir: UIImage? {
        let context = CIContext(options: nil)
        guard let currentFilter = CIFilter(name: "CIPhotoEffectNoir") else { return nil }
        currentFilter.setValue(CIImage(image: self), forKey: kCIInputImageKey)
        if let output = currentFilter.outputImage,
            let cgImage = context.createCGImage(output, from: output.extent) {
            return UIImage(cgImage: cgImage, scale: scale, orientation: imageOrientation)
        }
        return nil
    }
}
```


