javadoc 标记是插入文档注释中的特殊标记，它们用于标识代码中的特殊引用。javadoc 标记由“@”及其后所跟的标记类型和专用注释引用组成。三个部分——@、标记类型、专用注释引用。可以分成两部分：@ 和标记类型、专用注释引用。虽然 @ 和 标记类型之间有时可以用空格符分隔，但是最好始终将它们紧挨着写，以减少出错机会。

__这些是注释类，属性和方法的。__ 简述是注释的第一个‘.’之前的所有内容。

javadoc通常从package、公开类或者接口、公开或者受保护的字段、公开或者受保护的方法提取信息。每条注释应该是以/\**开始以*/结尾。例如
``` java
	/**
	* 
	* @param id the coreID of the person
	* @param userName the name of the person
	
	* you should use the constructor to create a person object
	*/
	public SecondClass(int id,String userName)
	{
	   this.id = id;
	   this.userName = userName;
	}
```
注释应该写在要说明部分的前面，如上所示。并且在其中可以包括html的标记，如果上面没有标记的话，那么you should usr the ......将会在javadoc里面紧跟@param userName....，这样不是我们希望的。一般注释可以分为类注释、方法注释、字段注释等。下面分别作简单的介绍

__类注释__
类注释应该在import语句的后面在类声明的前面，比如
``` java
package com.north.java;
 /**
 * @author ming
 * 
 * this interface is to define a method print()

 * you should implements this interface is you want to print the username

 * @see com.north.ming.MainClass#main(String[])
 */
public interface DoSomething
{
    /**
     * @param name which will be printed  
     * @return nothing will be returned 
     *
     */
    public void print(String name);
}
```
其中@author 和@see都是常用的注释第一个表示作者，第二个表示参考的连接。

__方法注释__
方法注释要紧靠方法的前面，你可以在其中使用@param @return @throws等标签。例如
``` java
     /**
     * 
     * @param i
     * @return true if ..... else false
     * @throws IOException when reading the file ,if something wrong happened
     * then the method will throws a IOException
     */
    public boolean doMethod(int i) throws IOException
    {
        return true;
    }
```
__字段注释__
只有public的字段才需要注释，通常是static德，例如
``` java
    /**
     * the static filed hello
     */
    public static int hello = 1;
```
<br/>
总结：
标记|用于|作用|用法|例子
:--:|:--:|---|---|-----
@author|对类的说明|标明开发该类模块的作者|@author 作者名|可以使用多次，多个作者使用，隔开
@version|对类的说明|标明该类模块的版本|@version 版本号|可以使用多次，但只用第一次生效
@see|对类、属性、方法的说明|参考转向，也就是相关主题|@see 类名；@see #方法名或属性名； @see 类名#方法名或属性名|@see #count(属性); @see #show(boolean b)(方法)
@param|对方法的说明|对方法中某参数的说明|@param 参数名 参数说明| @param b excrescent parameter
@return|对方法的说明|对方法返回值的说明|@return 返回值说明|@return true or false
@exception|对方法的说明|对方法可能抛出的异常进行说明|@exception 异常类名 说明|@exception java.lang.Exception throw when switch is 1
@throws：异常||同exceptioin

还有一种就是：
TODO：//Created on：
这类的注释我只了解到这一个。
