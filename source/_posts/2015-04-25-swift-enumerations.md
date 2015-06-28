---
layout: post
title: "Swift enumerations"
categories:
- Swift
tags:
- Swift

---
[原文地址:https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/  Swift_Programming_Language/Enumerations.html#//apple_ref/doc/uid/TP40014097-CH12-ID145](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Enumerations.html#//apple_ref/doc/uid/TP40014097-CH12-ID145)

##枚举语法
{% codeblock lang:swift  %}
enum SomeEnumeration {
    // enumeration definition goes here
}
{% endcodeblock %}
example
{% codeblock lang:swift  %}
enum CompassPoint {
    case North
    case South
    case East
    case West
}

enum Planet {
  case Mercury, Venus, Earth, Mars, Jupiter, Saturn, Uranus, Neptune
}

var directionToHead = CompassPoint.West
directionToHead = .East
{% endcodeblock %}

##匹配枚举值和Switch语句
{% codeblock lang:swift  %}
directionToHead = .South
switch directionToHead {
case .North:
    println("Lots of planets have a north")
case .South:
    println("Watch out for penguins")
case .East:
    println("Where the sun rises")
case .West:
    println("Where the skies are blue")
}
// 输出 "Watch out for penguins”

let somePlanet = Planet.Earth
switch somePlanet {
case .Earth:
    println("Mostly harmless")
default:
    println("Not a safe place for humans")
}
// 输出 "Mostly harmless”
{% endcodeblock %}

##相关值
{% codeblock lang:swift  %}
enum Barcode {
  case UPCA(Int, Int, Int)
  case QRCode(String)
}

var productBarcode = Barcode.UPCA(8, 85909_51226, 3)
productBarcode = .QRCode("ABCDEFGHIJKLMNOP")

switch productBarcode {
case .UPCA(let numberSystem, let identifier, let check):
    println("UPC-A with value of \(numberSystem), \(identifier), \(check).")
case .QRCode(let productCode):
    println("QR code with value of \(productCode).")
}
// 输出 "QR code with value of ABCDEFGHIJKLMNOP.”

switch productBarcode {
case let .UPCA(numberSystem, identifier, check):
    println("UPC-A with value of \(numberSystem), \(identifier), \(check).")
case let .QRCode(productCode):
    println("QR code with value of \(productCode).")
}
// 输出 "QR code with value of ABCDEFGHIJKLMNOP."

switch productBarcode {
case let .UPCA(numberSystem, identifier, check):
    println("UPC-A with value of \(numberSystem), \(identifier), \(check).")
case let .QRCode(productCode):
    println("QR code with value of \(productCode).")
}
// 输出 "QR code with value of ABCDEFGHIJKLMNOP."
{% endcodeblock %}

##原始值
{% codeblock lang:swift  %}
enum ASCIIControlCharacter: Character {
    case Tab = "t"
    case LineFeed = "n"
    case CarriageReturn = "r"
}

let acc = ASCIIControlCharacter.Tab
println("acc=\(acc.rawValue)")

enum Planet1: Int {
    case Mercury = 1, Venus, Earth, Mars, Jupiter, Saturn, Uranus, Neptune
}

let earthsOrder = Planet1.Earth.rawValue

let positionToFind = 9
if let somePlanet = Planet(rawValue: positionToFind) {
    switch somePlanet {
    case .Earth:
        println("Mostly harmless")
    default:
        println("Not a safe place for humans")
    }
} else {
    println("There isn't a planet at position \(positionToFind)")
}
// 输出 "There isn't a planet at position 9
{% endcodeblock %}