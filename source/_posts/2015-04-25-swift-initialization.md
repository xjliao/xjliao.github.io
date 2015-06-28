---
layout: post
title: "Swift initialization"
categories:
- Swift
tags:
- Swift


---
#官方教程
[https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/  Swift_Programming_Language/Initialization.html#//  apple_ref/doc/uid/TP40014097-CH18-ID203](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Initialization.html#//apple_ref/doc/uid/TP40014097-CH18-ID203)
在此只记录比较特殊的情况
#构造过程
{% codeblock lang:swift  %}
init() {
    // perform some initialization here
}
{% endcodeblock %}

demo

{% codeblock lang:swift  %}
struct Fahrenhit {
    var temperature: Double
    init() {
        self.temperature = 32.0
    }
}

var f = Fahrenheit()
println("The default temperature is \(f.temperature)° Fahrenheit")
// prints "The default temperature is 32.0° Fahrenheit"
{% endcodeblock %}
#默认属性值
{% codeblock lang:swift  %}
struct Fahrenheit {
    var temperature = 32.0
}

{% endcodeblock %}
#自定义构造过程
##初始化参数
##无返回值函数