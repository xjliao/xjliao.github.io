title: Objective-C method 'application:didFinishLaunchingWithOptions:' provided by method 'application(_:didFinishLaunchingWithOptions:)' 
date: 2015-07-01 21:10:05
categories:
- Swift
tags:
- Swift

---

##Error
{% codeblock lang:bash %}
AppDelegate.swift:17:10: Objective-C method 'application:didFinishLaunchingWithOptions:' provided by method 'application(_:didFinishLaunchingWithOptions:)' conflicts with optional requirement method 'application(_:didFinishLaunchingWithOptions:)' in protocol 'UIApplicationDelegate'
{% endcodeblock %}

##Solution
{% codeblock lang:swift %}
func application(application: UIApplication!, didFinishLaunchingWithOptions launchOptions: NSDictionary!) -> Bool {  
}
//replaced to
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {  
}
{% endcodeblock %}
