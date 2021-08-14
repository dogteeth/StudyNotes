#### UIImageView Definiton

An UIImageView provides a view-based container for displaying either a single image or for animating a series of images. For animating the images, the UIImageView class provides controls to set the duration and frequency of the animation. You can also start and stop the animation freely.

New image view objects are configured to disregard user events by default. If you want to handle events in a custom subclass of UIImageView, you must explicitly change the value of the userInteractionEnabled property to YES after initializing the object.

When a UIImageView object displays one of its images, the actual behavior is based on the properties of the image and the view. If either of the image’s leftCapWidth or topCapHeight properties are non-zero, then the image is stretched according to the values in those properties. Otherwise, the image is scaled, sized to fit, or positioned in the image view according to the contentMode property of the view. It is recommended (but not required) that you use images that are all the same size. If the images are different sizes, each will be adjusted to fit separately based on that mode.

All images associated with a UIImageView object should use the same scale. If your application uses images with different scales, they may render incorrectly.

#### UIImage與UIImageView的差別
- UIImage比較像是image的本身。
- UIImageView，則是用來處理一個或多個UIImage的View.
