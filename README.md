# flutter_ui_framework
flutter项目UI框架搭建

最实用而且现在最流行的框架：
下面几个tab按钮，点击按钮切换到相应的页面。
大家可以看看如图所示：
页面随着tab的切换而切换，随波逐流。
![image](https://github.com/1136346879/Image_Assert/blob/master/flutter_%E6%A1%86%E6%9E%B6.gif)

下面代码具体实现：
1，新建一个flutter项目
2，在main.dart文件中编写app主入口
3，在app主入口中加入主页面的框架index_page
4，然后在index_page中编写，添加需要切换的几个page


main.dart类代码：
```
import 'package:flutter/material.dart';
import './pages/index_page.dart';
//程序主入口
void main() {runApp(MyApp());}
//void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: MaterialApp(
        title: "二元店+",
        debugShowCheckedModeBanner: false,
        theme:ThemeData(
          primaryColor:Colors.pink
        ),
          home:IndexPage()
      ),
    );
  }
}
```

为了测试入口文件，我们在index_page.dart文件里使用了静态组件（也就是继承了StatelessWidget）。因为底部导航栏是要根据用户操作不断变化的，所以我们使用动态组件（StatefulWidget）。

这里我使用了快捷键stful快速生成，如果你要使用这个快速生成需要在android studio 或者VSCode里安装Awesome Flutter Snippets。安装完插件需要重新启动一下VSCode，然后就可以快乐的使用快捷方法生成代码了。（Flutter开发必备，建议安装）

index_page.dart类文件代码：
```
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'home_page.dart';
import 'category_page.dart';
import 'cart_page.dart';
import 'member_page.dart';

class IndexPage extends StatefulWidget {//动态切换页面 用 StatefulWidget
  @override
  _IndexPageState createState() => _IndexPageState();
}

class _IndexPageState extends State<IndexPage> {
  final List<BottomNavigationBarItem> bottomTabs = [
    BottomNavigationBarItem(icon: Icon(CupertinoIcons.home), title: Text("书籍")),
    BottomNavigationBarItem(icon: Icon(CupertinoIcons.car), title: Text("汽车")),
    BottomNavigationBarItem(icon: Icon(CupertinoIcons.shopping_cart), title: Text("购物车")),
    BottomNavigationBarItem(icon: Icon(CupertinoIcons.book), title: Text("会员")),
  ];

  final List pageList = [HomePage(), CategoryPage(), CartPage(), MemberPage()];

  int currentIndex = 0;
  var currentPage;
  @override
  void initState() {
    currentPage = pageList[currentIndex];
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Color.fromRGBO(245, 245, 245, 1.0),//北京
      bottomNavigationBar: BottomNavigationBar(
        type: BottomNavigationBarType.fixed,//类型
        items: bottomTabs,//底部tab
        currentIndex: currentIndex,//当前 index
        onTap: (index) {//点击后调用 setState 方法  然后会重新绘制页面
          setState(() {
            currentIndex = index;//点击的tab
            currentPage = pageList[currentIndex];//当前页面
          });
        },
      ),
      body: currentPage,//主体显示的是当前的页面
    );
  }
}

```
各个页面的文件代码：
MemberPage
```
import 'package:flutter/material.dart';

class MemberPage extends StatelessWidget {//动态切换页面 用 StatefulWidget
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(child:Text("商城会员")),
    );
  }
}
```
HomePage
```
import 'package:flutter/material.dart';

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(child:Text("商城首页")),
    );
  }
}

```
CategoryPage
```
import 'package:flutter/material.dart';

class CategoryPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(child:Text("商品分类")),
    );
  }
}
```
CartPage
```
import 'package:flutter/material.dart';

class CartPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(child:Text("购物车")),
    );
  }
}
```
总结:通过这节课的学习，应该掌握如下知识点：

页面切换的技巧和变量如何定义。
BottomNavigationBar部件的使用，最终作成底部切换效果。

这几个页面 就简单写了几个字，这次就简简单单的编写出App的框架即可，
每个页面的具体内容请看下期内容
代码具体会上传至 github上，如有需要可以下载。
下载地址：
[github源码](https://github.com/1136346879/flutter_ui_framework)
