# KYC-iOS-Release 2.9.2

:point_right: *Take a look [here](Liveness3D.md) if you'd like to use Liveness3D module only.*

### Installation
This framework ment to be installed via [cocoapods](https://cocoapods.org/).

* Add to your `Podfile` specs repositories: `SumSubstance/Specs`, and public one - `CocoaPods/Specs`
* Specify `use_frameworks!` option
* Add dependency `SumSubstanceKYC` to your target

Resulting `Podfile` could look as follows:
```ruby
platform :ios, '9.3'

source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/SumSubstance/Specs.git'

use_frameworks!

target 'MyAwesomeApp' do

  pod 'SumSubstanceKYC'

  # any other dependencies
end
```
* Run `pod install --repo-update`

### Usage 
To instantiate framework call 
```objc
SSEngine *engine = [SSFacade setupForApplicant:applicantID
                                     withToken:authToken
                                        locale:locale
                                  supportEmail:supportEmail
                                       baseUrl:baseUrl
                                   colorConfig:colorConfigOrNil
                                   imageConfig:imageConfigOrNil];
``` 
Where 
* `applicantID` - your applicant identifier
* `authToken` - your Sum&Sub auth token
* `locale` - user locale (preferably `NSLocale.currentLocale.localeIdentifier`, but you can use any)
* `colorConfigOrNil` - nil or subclass of `KYCColorConfig` (for color pallet customization)
* `imageConfigOrNil` - nil or subclass of `KYCImageConfig` (for icons customization)

Then, you should:
* Connect to remote - `[engine connectWithExpirationHandler:verificationResultHandler:]; `
* Create KYC UI - `[SSFacade getChatControllerWithAttributedTitle:titleOrNil]` 
* Refresh auth token (when needed) - `engine.refreshToken = newToken;`

For more usage examples refer to [demo project](https://github.com/SumSubstance/KYC-iOS-Demo).
