# Add dependencies

1) add uSDK.xcframwork
2) add StoreKit dependencies

3) add Appsflyer https://github.com/AppsFlyerSDK/AppsFlyerFramework
Step 1
In Xcode go to: File -> Swift Packages -> Add Package Dependency...
Step 2
Enter the AppsFlyer SDK GitHub repository - https://github.com/AppsFlyerSDK/AppsFlyerFramework



# uSDK


import AppsFlyerLib
import StoreKit
import uSDK

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
      
      AppsFlyerLib.shared().appsFlyerDevKey = "jPTLjzLcSczAjnbN8QV56K"
      AppsFlyerLib.shared().appleAppID = "COPY-HERE-APPSTORE-ID"
     
      UADManager.shared().configure(context: UIApplication.shared, apikey: "YOUR API KEY")
      AppsFlyerLib.shared().deepLinkDelegate = UADManager.shared().deeplinkDelegate as? DeepLinkDelegate
      
      SKAdNetwork.registerAppForAdNetworkAttribution()

}


func application(_ application: UIApplication, continue userActivity: NSUserActivity, restorationHandler: @escaping ([UIUserActivityRestoring]?) -> Void) -> Bool {
  AppsFlyerLib.shared().continue(userActivity, restorationHandler: nil)
  return true
}

func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
  AppsFlyerLib.shared().handleOpen(url, options: options)
  return true
}



# edit info.plist

<array>
    <dict>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        </array>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
    </dict>
</array>

<key>SKAdNetworkItems</key>
<array>
    <dict>
        <key>SKAdNetworkIdentifier</key>
        <string>cad8qz2s3j.skadnetwork</string>
    </dict>
</array>

<key>NSUserTrackingUsageDescription</key>
<string>App would like to access IDFA for tracking purpose</string>

# Associate Domain onelink
PROJECT -> Target -> Signign & Capabilities -> Associated Domains
Add   "applinks:{here your subdomain}.onelink.me"



