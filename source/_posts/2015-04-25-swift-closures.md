---
layout: post
title: "Swift closures"
categories:
- Swift
tags:
- Swift


--- 
[原文地址:http://fuckingclosuresyntax.com/](http://fuckingclosuresyntax.com/)

How Do I Declare a Closure in Swift?

##As a variable:
{% codeblock lang:swift %}
var closureName: (parameterTypes) -> (returnType)
{% endcodeblock %}

##As an optional variable:
{% codeblock lang:swift %}
var closureName: ((parameterTypes) -> (returnType))?
{% endcodeblock %}
##As a type alias:
{% codeblock lang:swift %}
typealias closureType = (parameterTypes) -> (returnType)
{% endcodeblock %}
##As a constant:
{% codeblock lang:swift %}
let closureName: closureType = { ... }
{% endcodeblock %}
##As an argument to a function call:
{% codeblock lang:swift %}
func({(parameterTypes) -> (returnType) in statements})
{% endcodeblock %}
##As a function parameter:
{% codeblock lang:swift %}
array.sort({ (item1: Int, item2: Int) -> Bool in return item1 < item2 })
{% endcodeblock %}
##As a function parameter with implied types:
{% codeblock lang:swift %}
array.sort({ (item1, item2) -> Bool in return item1 < item2 })
{% endcodeblock %}
##As a function parameter with implied return type:
{% codeblock lang:swift %}
array.sort({ (item1, item2) in return item1 < item2 })
{% endcodeblock %}
##As the last function parameter:
{% codeblock lang:swift %}
array.sort { (item1, item2) in return item1 < item2 }
{% endcodeblock %}
##As the last parameter, referred to by numbers:
{% codeblock lang:swift %}
array.sort { return $0 < $1 }
{% endcodeblock %}
##As the last parameter, with an implied return value:
{% codeblock lang:swift %}
array.sort { $0 < $1 }
{% endcodeblock %}
##As the last parameter, as a reference to an existing function:
{% codeblock lang:swift %}
array.sort(<)
{% endcodeblock %}
This site is not intended to be an exhaustive list of all possible uses of closures.


Unable to access this site due to the profanity in the URL? [http://goshdarnclosuresyntax.com](http://goshdarnclosuresyntax.com) is a more work-friendly mirror.