#ScrollingNavbar  

[ScrollingNavbar原文连接](https://github.com/mygithubzhangyafeng/AMScrollingNavbar#enable-the-scrolling-with-autolayout)

描述：
可滚动UINavigationBar（UIScrollView或类似的滚动视图(例如UITableView或UIWebView)。它的工作原理就像导航栏在Chrome或为iOS7 Facebook的应用程序。

###设置：
* Import ```UIViewController+ScrollingNavbar.h``` in your controller
* 实现一下2个方法
<pre><code>
	- (void)viewWillDisappear:(BOOL)animated
	{
    	[super viewWillDisappear:animated];
	    [self showNavBarAnimated:NO];
	}
</code></pre>
* 确保viewController释放的时候stop scrolling
<pre><code>
    - (void)dealloc 
	{
	      [self stopFollowingScrollView];
	}
</code></pre>



###确保scrollView使用了Autolayout
版本1.1引入了Autolayout-friendly设置视图的方式,强烈推荐使用该方法:

* 用autolayout设置你的view
* Create an outlet of the top constraint of the first view sitting below the navigation bar
* 确保scrollview使用了这个方法
<pre>
[self followScrollView:self.scrollView usingTopConstraint:self.topLayoutConstraint];
</pre>




###=================================================
###方法2不使用autolayout的方式
### 确保scrollview没使用autolayout
这个版本不需要autolayout，你只需要叫followScrollView方法来激活滚动效果，UIView的实例将会被跟踪。
<pre>[self followScrollView:self.scrollView];</pre>

你也可以对手势（ that reveals the navigation bar.）的响应设置一个等待效果
<pre>
[self followScrollView:self.scrollView withDelay:60];
</pre>

Make sure to have a barTintColor for your UINavigationBar, or you won't see the fade-in and fade-out effects. Also make sure that you are not using a translucent navigation bar. E.g., in your controller:
<pre>
[self.navigationController.navigationBar setTranslucent:NO];
</pre>
###＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝
###Using it with UITableViewController or UICollectionViewController
If you are not using a plain UIViewController you have to enable this property:
<pre>
[self setUseSuperview:YES];
</pre>

###Delegate
You can implement the AMScrollingNavbarDelegate protocol to receive these messages:
<pre>
- (void)navigationBarDidChangeToCollapsed:(BOOL)collapsed;
- (void)navigationBarDidChangeToExpanded:(BOOL)expanded;
</pre>
