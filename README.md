# ESRC for iOS
[![Platform](https://img.shields.io/badge/platform-iOS-orange.svg)](https://github.com/esrc-official/ESRC-iOS)
[![Languages](https://img.shields.io/badge/language-Objective--C%20%7C%20Swift-orange.svg)](https://github.com/esrc-official/ESRC-iOS)
[![Commercial License](https://img.shields.io/badge/License-Commercial-brightgreen.svg)](https://github.com/esrc-official/ESRC-iOS/blob/master/LICENSE.md)

<br />

## Introduction

[ESRC](http://esrc.co.kr) provides the vision API and SDK for your mobile app, enabling real-time recognizing facial expression, heart response and emotion using a camera.

<br />

## Installation

To use our iOS samples, you should first install [ESRC SDK for iOS](https://github.com/esrc-official/ESRC-SDK-iOS) 2.4.6 or higher on your system and should be received License Key by requesting by our email: **esrc@esrc.co.kr** <br /> 

<br />

## Before getting started

### Requirements

The minimum requirements to use our iOS sample are:

- iOS 13.0 or later <br />
- Swift 4 or later, Objective-C <br />
- Xcode 9 or later, macOS Sierra or later <br />

<br />

## Getting started

if you would like to try the sample app specifically fit to your usage, you can do so by following the steps below.

### Step 1: Initialize the ESRC SDK

Initialization binds the ESRC SDK to iOS, thereby allowing it to use a camera in your mobile. To the `initWithApplicationId()` method, pass the **App ID** of your ESRC application to initialize the ESRC SDK and the **ESRCLicenseHandler** to received callback for validation of the App ID.

```swift
ESRC.initWithApplicationId(appId: APP_ID, licenseHandler:  ESRCLicenseHandler() {
    
    func onValidatedLicense() {
        …
    }
    
    func onInvalidatedLicense() {
        …
    }
})
```

> Note: The `ESRC.initWithApplicationId()` method must be called once across your iOS app. It is recommended to initialize the ESRC SDK in the `viewDidAppear()` method of the Application instance.

### Step 2: Start the ESRC SDK

Start the ESRC SDK to recognize your facial expression. To the `start()` method, pass the `ESRCProperty` to select analysis modules and the `ESRCHandler` to handle the results. You should implement the callback method of `ESRCHandler` interface. So, you can receive the results of face, facial landmark, facial expression, heart rate, heart rate variability and engagement. Please refer to **[sample app](https://github.com/esrc-official/ESRC-iOS)**.

```swift
ESRC.start(
    property: ESRCProperty(
        enableMeasureEnv: true,  // Whether analyze measurement environment or not.
        enableFace: true,  // Whether detect face or not.
        enableFacialLandmark: true,  // Whether detect facial landmark or not. If enableFace is false, it is also automatically set to false.
        enableFacialActionUnit: true,  // Whether analyze facial action unit or not. If enableFace or enableFacialLandmark is false, it is also automatically set to false.
        enableBasicFacialExpression: true,  // Whether recognize basic facial expression or not. If enableFace is false, it is also automatically set to false.
        enableValenceFacialExpression: true,  // Whether recognize valence facial expression or not. If enableFace is false, it is also automatically set to false.
        enableRemoteHR: true,  // Whether estimate remote hr or not.
        enableHRV: true,  // Whether analyze HRV or not. If enableRemoteHR is false, it is also automatically
        enableEngagement: true),  // Whether recognize engagement or not. If enableRemoteHR and enableHRV are false, it is also automatically set to false.
    handler: ESRCHandler() {
        func onDetectedFace(face: ESRCFace) {
            // The face is detected.
            // Through the “face” parameter of the onDetectedFace() callback method,
            // you can get the location of the face from the result object
            // that ESRC SDK has passed to the onDetectedFace().
            …
        }
    
        // Please implement other callback method of ESRCHandler interface.
        func onAnalyzedMeasureEnv(measureEnv: ESRCMeasureEnv) { … }
        func onDetectedFacialLandmark(facialLandmark: ESRCFacialLandmark) { … }
        func onAnalyzedFacialActionUnit(facialActionUnit: ESRCFacialActionUnit) { … }
        func onRecognizedFacialExpression(facialExpression: ESRCFacialExpression) { … }
        func didChangedProgressRatioOnRemoteHR(progressRatio: Double) { … }
        func onEstimatedRemoteHR(remoteHR: ESRCRemoteHR) { … }
        func didChangedProgressRatioOnHRV(progressRatio: Double) { … }
        func onAnalyzedHRV(hrv: ESRCHRV) { … }
        func onRecognizedEngagement(engagement: ESRCEngagement) { … }
});
```

### Step 3: Feed the ESRC SDK

Feed `UIImage` on the ESRC SDK. To the `feed()` method, pass the `UIImage` image received using a camera in real-time. Please do it at 10 fps.

```swift
ESRC.feed(frame: frame)
```

### Step 4: Stop the ESRC SDK

When your app is not use the camera or destroyed, stop the ESRC SDK.

```swift
ESRC.stop()
```

<br />

## iOS sample

You can **clone** the project from the [Sample repository](https://github.com/esrc-official/ESRC-iOS).

```
// Clone this repository
git clone git@github.com:esrc-official/ESRC-iOS.git

// Move to the sample
cd ESRC-iOS
```

<br />

## Reference

For further detail on ESRC SDK for iOS, reter to [ESRC SDK for iOS README](https://github.com/esrc-official/ESRC-SDK-iOS/blob/master/README.md).
