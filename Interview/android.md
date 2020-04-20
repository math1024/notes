[TOC]



##### Handler的post和sendMessage方法的区别和应用场景

* 都会调用sendMessageAtTime方法进行消息的发送
* post方法的消息是在post传递的Runnable对象的run方法中处理
* 而调用sendMessage方法需要重写handleMessage方法或者给handler设置callback

