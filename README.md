# JSONObject2
将json转为YYmodel或者MJExtension需要的类文件（升级版本）

>下载项目，可以在编译运行之后打开使用  
>也可以编译运行之后，将XCode左边的Products目录里，生成的JsonObject.app，拖出来使用（每次就不需要编译运行）

## 类生成的原理
example json：
```json
{
    "status":"1",
    "msg":"这是一个举例说明的json",
    "data": {
        "a":"name",
        "b":"1777777777",
        "c":"1",
    }
}
```

看上述 **json** 里面，一个 **{}** 包含若干字段，其中 **data** 又包含了若干字段。我根据上述 **json** 画出了下图。
`每个 {}就是一个类，不是{}的就是属性`  

![当前框架原理](http://47.89.50.60/CD0FD8D220A3.png)
  

可以看成有一个类  **example {}**，里面有一个**data** ，**data** 里面又包含了几个属性。
在实际项目中，每个`{}`里面包含了若干个`{}`的对象，所以每个类就需要一个数组，数组中装的是当前`{}`包含的其他的`{}`

接着我们要给`{}`生成一个类文件，创建一个类需要类名，父类名，成员属性等。根据需要设置了以下个属性：

> 类名前缀  
> 类名后缀  
> 父类名称  
> 属性列表  
> 被替换的关键字列表（如id等，转换模型需要）  
> []内的{}对应的class名称列表。（转换模型需要）  
> 其他json对象列表

调用initWithObject方法，传入json和使用解析model的框架类型即可，具体可看XHModelClass和XHModelParser里面的代码