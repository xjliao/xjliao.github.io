---
layout: post
title: "Swift Advanced Operators"
categories:
- Swift
tags:
- Swift


---
##官方教程
[https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/  Swift_Programming_Language/AdvancedOperators.html#//apple_ref/doc/uid/TP40014097-CH27-ID28](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AdvancedOperators.html#//apple_ref/doc/uid/TP40014097-CH27-ID28)

##高级运算符
除了基本操作符中所讲的运算符，Swift还有许多复杂的高级运算符，包括了C语言和Objective-C中的位运算符和移位运算。

不同于C语言中的数值计算，Swift的数值计算默认是不可溢出的。溢出行为会被捕获并报告为错误。你是故意的？好吧，你可以使用Swift为你准备的另一套默认允许溢出的数值运算符，如可溢出的加号为&+。所有允许溢出的运算符都是以&开始的。

自定义的结构，类和枚举，是否可以使用标准的运算符来定义操作？当然可以！在Swift中，你可以为你创建的所有类型定制运算符的操作。

可定制的运算符并不限于那些预设的运算符，你可以自定义中置，前置，后置及赋值运算符，当然还有优先级和结合性。这些运算符在代码中可以像预设的运算符一样使用，你也可以扩展已有的类型以支持你自定义的运算符
##位运算符
位操作符可以操作数据结构中原始数据的每个比特位。位操作符通常在诸如图像处理和创建设备驱动等底层开发中使用，位操作符在同外部资源的数据进行交互的时候也很有用，比如在使用用户协议进行通信的时候，运用位运算符来对原始数据进行编码和解码
####1、按位取反运算符
按位取反运算符~对一个操作数的每一位都取反。
{% codeblock lang:swift  %}
let initialBits: UInt8 = 0b00001111
let invertedBits = ~initialBits  // 等于 0b11110000
{% endcodeblock %}
####2、按位与运算符
{% codeblock lang:swift  %}
let firstSixBits: UInt8 = 0b11111100
let lastSixBits: UInt8  = 0b00111111
let middleFourBits = firstSixBits & lastSixBits  // 等于 00111100
{% endcodeblock %}