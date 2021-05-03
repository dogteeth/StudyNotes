Singleton
1. 確保整個程式只有一個物件
2. 全局域都可以使用
3. 降低記憶體資源浪費

建構方式
1. initializer前加一個private, 沒有其它人可以init它了。
2. 用shared來代替class的instance, 前面加上static. 加上static之後的所面所有東西，只有這個類可以使用。（類方法的意思）



***
Swift定義：
Instance methods, as described above, are methods that you call on an instance of a particular type. You can also define methods that are called on the type itself. These kinds of methods are called type methods. You indicate type methods by writing the static keyword before the method’s func keyword. 
***

