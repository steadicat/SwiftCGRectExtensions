Swift CGRect Extensions
=======================

A collection of `CGRect`, `CGPoint` and `CGSize` convenience functions for Swift on OS X and iOS.

The goal is to provide clear functions for the most commonly used rect operations, even if the code savings are minimal. The reason is that function names communicate the programmer's intent more clearly than setting properties with ad-hoc calculations.

Pull requests and suggestions are welcome.

Features
--------

- Operators for adding, scaling sizes, applying `CGAffineTransform`
- Shortcut properties for corner and center points
- Offsetting, insetting and extending methods with multiple ways of specifying arguments
- Aligning and centering sizes in rects
- Copying rects with some values changed without going through a variable
- Respects the different coordinate systems on iOS and OS X
- Unit tested

Integration
-----------

### CocoaPods ###

Add the following to your Podfile:

    pod 'CGRectExtensions'

Then run `pod install` as usual and `import CGRectExtensions` in your Swift code.

### Manual Installation ###

If you don't use CocoaPods, copy the CGRectExtensions.swift file into your project.

Examples
--------

**These examples are also available as a Playground in the Xcode project.**

```swift
import Foundation
import CGRectExtensions

let rect = CGRect(1, 2, 100, 200) // shorter constructor

let minY = rect.minY // shortcut properties

let topCenter = rect.topCenter // OS-dependent coordinate system

let oppositeOrigin = rect.origin + rect.size // adding

let corneredRect = rect.with(x: 0, y: 0) // modified copy

let nextPageRect = rect.rectByOffsetting(dx: 100) // offsetting

let paddedRect = rect.rectByInsetting(top: 66, left: 10, right: 10) // insetting

let quarterSize = rect.size * 0.5 // scaling sizes
let corner = rect.rectByAligning(quarterSize, corner: .MinXEdge, .MinYEdge) // aligning sizes

let halfWidthSize = rect.size * (0.5, 1) // scaling sizes
let centeredRect = rect.rectByCentering(halfWidthSize) // centering sizes

let scaledRect = rect * CGAffineTransformMakeScale(2.0, 3.0)
```

Mutating functions are also available. These are especially convenient since Swift allows modifying a `struct` property directly.

```swift
import Cocoa
import CGRectExtensions

let view = NSView()
view.frame.size = CGSize(width: 100, height: 200)

view.frame.bottomLeft = CGPoint(x: 1, y: 2)

view.frame.offset(25, 25)

view.frame.inset(top: 66, left: 10, right: 10)

view.frame.setSizeCentered(CGSize(50, 50))

view.frame.setSizeCentered(CGSize(50, 50), alignTo: .MinXEdge)

view.frame.setSizeAligned(CGSize(50, 50), corner: .MinXEdge, .MinYEdge)

view.frame *= CGAffineTransformMakeScale(2.0, 3.0)
```
