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

### 三种路由传值方式

### 方式一：定义构造方法

#### 1、新路由页面构造函数自定义，接收参数

```dart
class MyPage extends StatelessWidget {

  String data;

  // 自定义构造函数，传入 data 数据
  MyPage(this.data);

  // 默认构造方法
  // const MyPage({Key key}) : super(key: key);  

  // 省略其他代码
}
```

2、`push` 传参、接收 `pop` 参数回传

```dart
// push 返回值是 Future 类型，需要 async...await... 的方式调用
_PushMethod1() async {
    // result 接收页面关闭时回传的参数
    var result = await Navigator.of(context).push(
      MaterialPageRoute(
        builder:(context){
         // 构造函数传参
          return MyPage('push Params');
        }
      )
    );
    print('result = $result');
  }
```

3、`pop` 时参数回传

```dart
......

onTap: (){
    // pop 函数第二个参数是需要回传的值
    Navigator.pop(context,[{'pageName':'MyPage'}]);
},

......
```

总结：需要事先定义好构造函数，不够灵活

#### 方式二：通过路由将参数传递给指定页面

这里参数传递两种场景：**注册路由的方式** 和 **未注册路由的方式**

1、参数传递 -- 注册路由场景

```dart
Navigator.pushNamed(
            context,
            pageB,
            arguments: People("yzq", 25),//需要传递给 PageB 的数据 model
          );
```

或者：

```dart
Navigator.of(context).pushNamed(pageB, 
                                arguments: People("yzq", 25) // 需要传递给 PageB 的数据 model
                                );
```

2、参数传递 -- 未注册路由场景

```dart
Navigator.push(
            context,
            MaterialPageRoute(
              builder: (context) => PageB(),
              settings: RouteSettings(
                arguments: People("yuzhiqiang", 26), // 需要传递给 PageB 的数据 model
              ),
            ),
          );
```

或者：

```dart
Navigator.of(context).push(
            MaterialPageRoute(
                builder: (context) => PageB(),
                settings: RouteSettings(
                    arguments: People("yuzhiqiang", 26), // 需要传递给 PageB 的数据 model
                )
            ),
          );
```

PageB 接收参数 `ModalRoute.of(context).settings.arguments`

```dart
...
Widget build(BuildContext context) {
    /*获取传递过来的参数*/
    People _people = ModalRoute.of(context).settings.arguments;

    return Scaffold(
      xxx
    );
  }
...
```

#### 方式三：通过**onGenerateRoute拦截后传值给具体的 widget**

#### 

##### 



