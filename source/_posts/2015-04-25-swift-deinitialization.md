---
layout: post
title: "Swift deinitialization"
categories:
- Swift
tags:
- Swift


---
##官方教程
[https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/  Swift_Programming_Language/Deinitialization.html#//apple_ref/doc/uid/TP40014097-CH19-ID142](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Deinitialization.html#//apple_ref/doc/uid/TP40014097-CH19-ID142)
##析构过程
Swift 会自动释放不再需要的实例以释放资源。如自动引用计数那一章描述，Swift 通过自动引用计数（ARC）处理实例的内存管理。通常当你的实例被释放时不需要手动地去清理。但是，当使用自己的资源时，你可能需要进行一些额外的清理。例如，如果创建了一个自定义的类来打开一个文件，并写入一些数据，你可能需要在类实例被释放之前关闭该文件。

在类的定义中，每个类最多只能有一个析构函数。析构函数不带任何参数，在写法上不带括号：
{% codeblock lang:swift  %}
deinit {
    // 执行析构过程
}
{% endcodeblock %}
demo
{% codeblock lang:swift  %}
struct Bank {
    static var coinsInBank = 10_000
    static func vendCoins(var numberOfCoinsToVend: Int) -> Int {
        numberOfCoinsToVend = min(numberOfCoinsToVend, coinsInBank)
        return numberOfCoinsToVend
    }
    
    static func receiveCoins(coins: Int) {
        coinsInBank += coins
    }
}


class Player {
    var coinsInPurse: Int
    init(coins: Int) {
        coinsInPurse = Bank.vendCoins(coins)
    }
    
    func winCoins(coins: Int) {
       coinsInPurse += Bank.vendCoins(coins)
    }
    
    deinit {
        Bank.receiveCoins(coinsInPurse)
    }
}

var playerOne: Player? = Player(coins: 100)
println("A new player has joined the game with \(playerOne!.coinsInPurse) coins")
// 输出 "A new player has joined the game with 100  coins"
println("There are now \(Bank.coinsInBank) coins left   in the bank")
// 输出 "There are now 9900 coins left in the bank"

playerOne = nil
println("PlayerOne has left the game")
// 输出 "PlayerOne has left the game"
println("The bank now has \(Bank.coinsInBank) coins")
// 输出 "The bank now has 10000 coins"
{% endcodeblock %}