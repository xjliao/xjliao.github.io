---
layout: post
title: 'Objective-c NSMethodSignature NSInvocation'
categories:
- Objective-c
tags:
- Objective-c

---
给某个对象发送消息后者说调用某个对象的方法  
有两种方式:
##第一种方式
delay表示多少秒后执行

{% codeblock lang:objc %}
- (void)performSelector:(SEL)aSelector withObject:(id)anArgument afterDelay:(NSTimeInterval)delay;
{% endcodeblock %} 

##第二种方式:
NSMethodSignature  NSInvocation

实现的第一种方式的delay，需要配合下面使用
{% codeblock lang:objc %}
+ (NSTimer *)timerWithTimeInterval:(NSTimeInterval)ti invocation:(NSInvocation *)invocation repeats:(BOOL)yesOrNo;
{% endcodeblock %} 

##demo  
10秒后执行
{% codeblock lang:objc %}
SEL mySelector = @selector(postRequest);
// 第一种方式
[self performSelector:mySelector withObject:self afterDelay:10];
// 第二种方式
// 需要调用方法所在class
NSMethodSignature *sig = [[InvokeMethodClass class] instanceMethodSignatureForSelector:mySelector];
NSInvocation *iv = [NSInvocation invocationWithMethodSignature:sig];
[iv setSelector:mySelector];
// 需要调用方法所在的target
[iv setTarget:self];
//  timerWithTimeInterval:多少秒后出发 repeats:是否重复执行 
// 如果不适用定时器， 则需要[iv invoke];
[NSTimer timerWithTimeInterval:10 invocation:iv repeats:NO];
    
- (void)postRequest {
	// Do something
}
{% endcodeblock %}