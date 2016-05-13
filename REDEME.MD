此分享是对官网不久前上线的 api.openDrawerLayout（ 抽屉式侧滑 window 布局 ）方法做了一个简单的实例，基于这个简单的布局大家可以在这之上再去做更复杂的布局交互，或者直接使用这个到你的应用当中，让你的应用更加的高炫拽。

1. ./index.html

我这里并没有在 index.html 初始时完成以后立马布局侧滑，原因是我得给大家演示了关闭侧滑的方法，而实际我们为了应用体验更加的友好，会在 index.html 需要初始化时就完成这个布局。按照官网的介绍 openDrawerLayout 实际就是在 openWin 方法的基础上新增了 leftPane、rightPane 参数，所以 openWin 的任何方法都是可以在这里使用，比如在打开测试时用的载入动画 animation 字段。

如上所述所以 openDrawerLayout 方法与 openWin 一样只接受一个参数，其中我这里使用到的 name 是主体的 window 名称，对应的主体 url 路径。leftPane 是侧滑的配置 name、url 与主体功能一致。而 animation 这是 "整个" 侧滑布局的动画，并不是侧滑时的动画。除此三个字段以外还有其它好几十个字段，我这就不做演示啦，大家下来自己研究研究。

2. ./html/main.html

这个页面是整个侧滑布局的主体展示部分，很多情况下除了手势滑动侧滑外，还会经常用到手动展开侧滑，我在这个页面使用 JS 封装了关于此需求对应的 openDrawerPane 方法，侧滑布局是针对全局 APP 生效的（即整个应用同时仅运行一个侧滑布局），所以这里关于所有侧滑的方法可以全局去使用，我在 index.html 中 openDrawerLayout 的布局，而现在我是在 main.html 中去使用 openDrawerPane 来展开侧滑。

同第 1 点提到的 "openDrawerLayout 实际就是在 openWin 方法的基础上新增的方法"，所以依照 window 的关闭方式，侧滑布局同样适用，因为我当前就在侧滑布局中，所以直接执行 closeWin 即可关闭侧滑布局，如果你未在侧滑布局中关闭侧滑，那么只需要在 closeWin 时，新增 name 字段，比如我这里写 api.closeWin({name: 'main'}); 结果一模一样。

3.  ./html/leftPane.html

这个页面是整个侧滑布局的侧滑窗格展示部分，该部分被展开时实际就会对应到 main.html openDrawerPane 方法相反的需求，所以一样的，因为侧滑布局全局的理念，我就直接使用侧滑类中的 closeDrawerPane 关闭这个窗格。当然在这个页面也会有关闭侧滑布局的需求，所以同理，直接 closeWin 即可。