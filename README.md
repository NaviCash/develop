Swift Package Manager
Swift Package Manager (SwiftPM) is a tool for managing the distribution of Swift code. It simplifies the process of managing Swift package dependencies.

To integrate SVProgressHUD into your project using SwiftPM:

In Xcode, select File > Add Package Dependency.
Enter the following package repository URL: https://github.com/SVProgressHUD/SVProgressHUD.git
Choose the appropriate version (e.g. a specific version, branch, or commit).
Add SVProgressHUD to your target dependencies.
SVProgressHUD requires at least Swift tools version 5.3.

From CocoaPods
CocoaPods is a dependency manager for Objective-C, which automates and simplifies the process of using 3rd-party libraries like SVProgressHUD in your projects. First, add the following line to your Podfile:

pod 'SVProgressHUD'
If you want to use the latest features of SVProgressHUD use normal external source dependencies.

pod 'SVProgressHUD', :git => 'https://github.com/SVProgressHUD/SVProgressHUD.git'
This pulls from the master branch directly.

Second, install SVProgressHUD into your project:

pod install
Carthage
Carthage is a decentralized dependency manager that builds your dependencies and provides you with binary frameworks. To integrate SVProgressHUD into your Xcode project using Carthage, specify it in your Cartfile:

1111111

github "SVProgressHUD/SVProgressHUD"
Run carthage bootstrap to build the framework in your repository's Carthage directory. You can then include it in your target's carthage copy-frameworks build phase. For more information on this, please see Carthage's documentation.

Manually
Drag the SVProgressHUD/SVProgressHUD folder into your project.
Take care that SVProgressHUD.bundle is added to Targets->Build Phases->Copy Bundle Resources.
Add the QuartzCore framework to your project.
Swift
Even though SVProgressHUD is written in Objective-C, it can be used in Swift with no hassle.

If you use CocoaPods add the following line to your Podfile:

use_frameworks!
If you added SVProgressHUD manually, just add a bridging header file to your project with the SVProgressHUD header included.

Usage
(see sample Xcode project in /Demo)

SVProgressHUD is created as a singleton (i.e. it doesn't need to be explicitly allocated and instantiated; you directly call [SVProgressHUD method] / SVProgressHUD.method()).

Use SVProgressHUD wisely! Only use it if you absolutely need to perform a task before taking the user forward. Bad use case examples: pull to refresh, infinite scrolling, sending message.

Using SVProgressHUD in your app will usually look as simple as this.

Objective-C:

[SVProgressHUD show];
dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
    // time-consuming task
    dispatch_async(dispatch_get_main_queue(), ^{
        [SVProgressHUD dismiss];
    });
});
Swift:

SVProgressHUD.show()
DispatchQueue.global(qos: .default).async {
    // time-consuming task
    DispatchQueue.main.async {
        SVProgressHUD.dismiss()
    }
}
Showing the HUD
