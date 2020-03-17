# 路由

---

### 路由定义

* 路由（Route）在移动开发中通常指页面（Page）；
* Route 在 Android 中通常指一个 `Activity`；
* Route 在 iOS 中通常指一个`ViewController`；

### 路由管理

管理页面之间如何跳转，通常也成为导航管理；

无论是 iOS、Android、Flutter 路由管理都维护了一个路由栈；入栈（push）打开一个页面，出栈（pop）关闭一个页面；

### Flutter中的路由

demo

```dart
Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
      ... //省略无关代码
      FlatButton(
         child: Text("open new route"),
         textColor: Colors.blue,
         onPressed: () {
          //导航到新路由   
          Navigator.push( context,
           MaterialPageRoute(builder: (context) {
              return NewRoute();
           }));
          },
         ),
       ],
 )
```

#### MaterialPageRoute 路由

`MaterialPageRoute` 是一个路由页面，构造函数：

```dart
 MaterialPageRoute({
    WidgetBuilder builder,     // 是一个回调函数，返回值是Route需要显示的 widget
    RouteSettings settings,    // 配置路由名称，是否是初始路由（首页）
    bool maintainState = true,  // 是否保活，true：保活 false：释放，路由没用的时候是否资源， 场景是什么 ？？？
    bool fullscreenDialog = false, // 是否 present 页面
  })
```

#### Navigator 路由管理组件

* `Future push(BulidContext context, Route route)`  
   打开页面，返回值 `Future` 接收新路由关闭时的返回数据；
* `bool pop(BuildContext context, [result])`
  关闭页面，`result` 为页面关闭时返回给上一个页面的数据 
* `Navigator.replace`，`Navigator.popUntil` ...

#### 三种路由传值方式

##### 方式一：定义构造方法

##### 方式二：将参数传递给制定路由

##### 方式三：通过**onGenerateRoute拦截后传值给具体的 widget**

##### 

##### 



