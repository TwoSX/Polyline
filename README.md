<p align="center" >
  <img src="https://raw.githubusercontent.com/raphaelmor/Polyline/assets/polyline.png" title="Polyline logo" float=left>
</p>

[![Build Status](https://travis-ci.org/raphaelmor/Polyline.svg?branch=master)](https://travis-ci.org/raphaelmor/Polyline)
[![CocoaPods](https://img.shields.io/cocoapods/v/Polyline.svg)](http://cocoadocs.org/docsets/Polyline)
![Swift 5](https://img.shields.io/badge/Swift-5.0-green.svg)
[![Licence](http://img.shields.io/badge/Licence-MIT-lightgrey.svg)](https://github.com/raphaelmor/Polyline/blob/master/LICENSE.txt)

Polyline encoder / decoder in Swift

1. [Features](#features)
2. [Requirements](#requirements)
3. [Integration](#integration)
4. [Usage](#usage)
5. [Notes](#notes)
6. [Contributors](#contributors)
7. [License](#license)

## Features

- Encode a `CLLocationCoordinate2D` array to a polyline
- Decode a polyline to an array of `CLLocationCoordinate2D`
- Encode a `CLLocation` array to a polyline
- Decode a polyline to an array of `CLLocation`
- Encode/Decode associated levels (optional)
- 100% Unit Test Coverage
- Complete Documentation
- Continuous integration with [Travis CI](http://travis-ci.org)
- CocoaPod available
- Convert to `MKPolyline`

### Planned for future releases

- Convert to `GMSPolyline`
- Example project
- Filter locations available at a specific level

### Planned when support is available :

- Code Coverage with [Coveralls](https://coveralls.io)

## Requirements

- Xcode 11+
- iOS 10.0+ / Mac OS X 10.12+ / tvOS 10.0+ / watchOS 3.0+ / Linux
- Swift 5.0

---


## Integration
To use this library in your project you can use CocoaPods, Carthage, Swift Package Manager, and/or integrate it manually :

### CocoaPods
You can integrate Polyline in your `Podfile` like this:

```
pod 'Polyline', '~> 5.0'
```

### Carthage
You can integrate Polyline in your `Cartfile` like this:

```
github "raphaelmor/Polyline" ~> 5.0
```

### Swift Package Manager
To integrate Polyline into an application using [Swift Package Manager](https://swift.org/package-manager/) within Xcode:

1. Go to File ‣ Swift Packages ‣ Add Package Dependency.
2. Enter `https://github.com/raphaelmor/Polyline.git` as the package repository and click Next.
3. Set Rules to Version, Up to Next Major, and enter `5.0.2` as the minimum version requirement. Click Next.

Or to integrate Polyline into another Swift package, add the following package to the `dependencies` in your Package.swift file:

```swift
.package(url: "https://github.com/raphaelmor/Polyline.git", from: "5.0.2")
```

### Manual

To install Polyline manually, add Polyline.xcodeproj to an Xcode workspace, then link your application to Polyline.framework.

It is technically possible to install Polyline by adding Polyline.swift and CoreLocation.swift directly to your project, but this approach is not recommended as it may omit important files in the future.

## Usage

### Polyline Encoding

Using `[CLLocationCoordinate2D]` (recommended) :

```swift
let coordinates = [CLLocationCoordinate2D(latitude: 40.2349727, longitude: -3.7707443),
CLLocationCoordinate2D(latitude: 44.3377999, longitude: 1.2112933)]

let polyline = Polyline(coordinates: coordinates)
let encodedPolyline: String = polyline.encodedPolyline

// Or for a functional approach :
let encodedPolyline: String = encodeCoordinates(coordinates)
```

Using `[CLLocation]` :

```swift
let locations = [CLLocation(latitude: 40.2349727, longitude: -3.7707443),
CLLocation(latitude: 44.3377999, longitude: 1.2112933)]

let polyline = Polyline(locations: locations)
let encodedPolyline: String = polyline.encodedPolyline

// Or for a functional approach :
let encodedPolyline: String = encodeLocations(locations)
```

You can encode levels too :

```swift
let levels: [UInt32] = [0,1,2,255]

let polyline = Polyline(coordinates: coordinates, levels: levels)
let encodedLevels: String? = polyline.encodedLevels

// Or for a functional approach :
let encodedLevels: String = encodedLevels(levels)
```


### Polyline Decoding

You can decode to `[CLLocationCoordinate2D]` (recommended) :

```swift
let polyline = Polyline(encodedPolyline: "qkqtFbn_Vui`Xu`l]")
let decodedCoordinates: [CLLocationCoordinate2D]? = polyline.coordinates

// Or for a functional approach :
let coordinates: [CLLocationCoordinate2D]? = decodePolyline("qkqtFbn_Vui`Xu`l]")
```

You can also decode to `[CLLocation]` :

```swift
let polyline = Polyline(encodedPolyline: "qkqtFbn_Vui`Xu`l]")
let decodedLocations: [CLLocation]? = polyline.locations

// Or for a functional approach :
let locations: [CLLocation]? = decodePolyline("qkqtFbn_Vui`Xu`l]")
```

You can decode levels too :

```swift
let polyline = Polyline(encodedPolyline: "qkqtFbn_Vui`Xu`l]", encodedLevels: "BA")
let decodedLevels: [UInt32]? = polyline.levels

// Or for a functional approach :
let levels: [UInt32]? = decodeLevels("BA")
```

### Polyline Precision

Default precision is 1e5 : 0.12345 (5 digit precision used by Google), but you can specify your own precision in all API methods (and functions).

```swift
// OSRM uses a 6 digit precision
let polyline = Polyline(encodedPolyline: "ak{hRak{hR", precision: 1e6)
```



## Notes
This library tries to have consistent results with polylines generated by the [Google Maps iOS SDK](https://developers.google.com/maps/documentation/ios/).
The online tool for [encoding polylines](https://developers.google.com/maps/documentation/utilities/polylineutility) has some minor inconsistencies regarding rounding (for example, 0.000015 is rounded to 0.00002 for latitudes, but 0.00001 for longitudes).

This codes tries to adhere to the [GitHub Swift Style Guide](https://github.com/github/swift-style-guide)

## Contributors

- [Raphaël Mor](http://github.com/raphaelmor) ([@raphaelmor](https://twitter.com/raphaelmor)): Creator
- [Tom Taylor](https://tomtaylor.co.uk): Maintainer
- [Minh Nguyễn](https://github.com/1ec5): Maintainer

## License
Polyline is released under an MIT license. See [LICENSE.txt](https://github.com/raphaelmor/Polyline/blob/master/LICENSE.txt) for more information.
