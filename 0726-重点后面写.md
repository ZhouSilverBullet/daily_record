

1. 代码加入了 leakcanary

   地址：https://github.com/square/leakcanary

```
debugImplementation "com.squareup.leakcanary:leakcanary-android:$project.leakcanary"
```

```kotlin
LeakSentry.config = LeakSentry.config.copy(watchFragmentViews = false)
```

2.  kotlin接口声明

   ```kotlin
   private var listener: (() -> Unit)? = null
   fun setDismissListener(l: () -> Unit) {
       listener = l
   }
   
   //调取的时候使用这个方法
   listener?.invoke()
   ```



3. Wms 可以复习一波，自己写一波这个头部弹出的这种布局



4. kotlin 简化lambda表达式

   Let,with,run,apply,also

    https://blog.csdn.net/u013064109/article/details/78786646#5

   let使用  

   返回最后一行

   ```
   //另一种用途 判断object为null的操作
   object?.let{//表示object不为null的条件下，才会去执行let函数体
   it.todo()
   }
   ```

   

   with使用

   with单独用，要with个对象,对象进行操作

         with(item)	{
           holder.tvNewsTitle.text = StringUtils.trimToEmpty(titleEn)
            holder.tvNewsSummary.text = StringUtils.trimToEmpty(summary)
            holder.tvExtraInf = "难度：$gradeInfo | 单词数：$length | 读后感: $numReviews"
          ... 
          }

   

   run使用

   类似于let和with的结合，对象.run，然后返回**标志（任意类型的）**

   **可以拿这个标记来进行判断中间的一些操作之类的**

   ```kotlin
    
    getItem(position)?.run {
    	//...
    }
   ```

   

   apply使用 

   apply返回传入的对象

   ```kotlin
   ---------使用一---------
   
    var user = User("zhousaito33", "103")
       var user2 = User("zhousaito77", "77")
       /**
        * apply返回传入的一个对象
        */
    val eee = user.apply {
           name = "aaa"
    }
    println("${eee.name}---> ${eee.age}")
   
   ---------使用二---------
   //一般都这么写
   var status = Status()
   status.drinking = true
   status.eating = true
   status.open = true
   
   //通过apply来进行
   var status2 = Status().apply { 
       drinking = true
       eating = true
       open = true
   }
   
   ---------使用三---------
   
   if (!TextUtils.isEmpty(judge.name) && !TextUtils.isEmpty(judge.password) && TextUtils.isEmpty("cc")) {
           //逻辑代码
       }
       
       //相当于
   judge.name?.apply { 
       judge.password
       }?.apply { 
       judge.userId
       }?.apply { 
   
   }
   
   ```

   

   also使用

   和let差不多，只不过最后一行没有返回值了，直接确定了返回值是自己了，这样就相当于链式操作了

# WMS

1. window  WindowManager WindowManagerService 三者的关系

   

   











mac os修改默认打开软件的图标

https://jingyan.baidu.com/article/b87fe19eb386f052183568a2.html