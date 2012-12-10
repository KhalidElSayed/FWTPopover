#FWTPopoverView

![FWTPopoverView screenshot](http://grab.by/hc1q)

FWTPopoverView is a pretty flexible custom view that helps when you need to show a popover with a pointing arrow. The idea behind is to expose a very simple and basic API and make easier to extend by accessing its custom objects/blocks entrypoints. FWTPopoverView is pure CG code, so no need to add assets and resolution independent for free.

##Requirements
* XCode 4.4.1 or higher
* iOS 5.0

##Features
FWTPopoverView has very few properties but uses several custom objects.
If you want to adjust/change the appearance of the background you change properties inside the background custom object, the same happens with animations and so on.
On the other side, if you're happy with the default style, you only need to set the contentSize and add your content to the contentView property.

There are two optional blocks executed when the popover is presented/dismissed. 

This project is not yet ARC-ready.

##How to use it: initializing

Generally you don't initialize FWTPopoverView with a frame instead you set the contentSize and then call:

* **presentFromRect: inView: permittedArrowDirection: animated:**

The FWTPopoverView, as default behaviour, check if there's any intersection with the superview and if yes it adjusts its frame position to fit inside the superview bounds. You can change this by setting **adjustPositionInSuperviewEnabled** to NO.

##How to use it: configure

####FWTPopoverBackgroundHelper 
This class needs a quick introduction: the popover image is a runtime image generated by a CAShapeLayer subclass. The layer is not directly added to the view hierarchy instead is rendered in a separate context and then the resulting image is used. The image is stretchable and use a very small chunk of memory.
As with every CAShapeLayer you have access to all shape style properties (clearly they're not animatable this time). The cornerRadius property is used as a property for the path. 

* **drawPathBlock** this block is executed just before return the image. It's a good point to customize or add more drawing stuff to your context 
* **(UIBezierPath *)bezierPathForRect:** returns the path for the current state/frame

####FWTPopoverAnimationHelper
This class is a simple animation properties container.  

####FWTPopoverArrow 
This class encapsulates few arrow specific properties. 

* **direction** (*readonly*) the direction in which the popover arrow is pointing
* **size** the size of the arrow
* **offset** (*readonly*) the distance (measured in points) from the center of the view to the center line of the arrow.
* **cornerOffset** the distance (measured in points) from the center of the arrow to the pointing edge of the arrow


##View hierarchy
For a better understanding it can be useful to see the subviews/sublayers involved. Between braces the available public properties.

- **popoverView** {contentSize, adjustPositionInSuperviewEnabled}
    - **backgroundImageView**
	- **contentView** 

##For your interest
In future release the backgroundHelper will support png images as in UIPopoverBackgroundView.

##Demo
The sample project shows how to use and how to create a custom FWTProgressView.
If you don't have time to read it this is what you need:

``` objective-c

	//	present
	FWTPopoverView *popoverView = [[[FWTPopoverView alloc] init] autorelease];
	popoverView.contentSize = CGSizeMake(240, 140);
    [popoverView presentFromRect:rect
                          inView:self.view
         permittedArrowDirection:FWTPopoverArrowDirectionUp
                        animated:YES];
                        
    // …
    
    //	dismiss
    [popoverView dismissPopoverAnimated:YES];
```

##Licensing
Apache License Version 2.0

##Credits
[Saudi Telecom](http://www.stc.com.sa) Mobile Apps team, who enabled and collaborated with us to extract source code from My STC App for this library

##Support, bugs and feature requests
If you want to submit a feature request, please do so via the issue tracker on github.
If you want to submit a bug report, please also do so via the issue tracker, including a diagnosis of the problem and a suggested fix (in code).
