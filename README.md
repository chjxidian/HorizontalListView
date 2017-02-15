以前刚学习android不久时，参考第三方实现的一个横向listview。它模仿的是scrollView / gallery，用scroller控制滑动操作。它主要实现的功能是横向滑动的listview。它继承自AdapterView，AdapterView又继承自ViewGroup所以这两者公开的（即方法注释上没有@hide）公共方法和监听器它都可用。vertical listview类似，除特别说明的外。

## 监听器
* RecyclerListener不可见的itemview放入回收站后回调。
* OnScrollListener滑动过程中和滑动停止后回调，两者回调不同的方法。

##方法
* addHeaderView(View view) 给listview添加header view，如果header的高度少于item的高度，会存在下面的问题
* addFooterView(View view) 给listview添加footer view
* setDivider(Drawable/Color) 设置listview的itemview设置分隔线，不能通过xml文件配置，其它用法和vertical listview一样。（如根据itemview是否可以选中来定是否绘制divider）
* setDividerWidth(int width) 设置divider的宽度，如果为0，则不绘制divider
* setSelection(int position) 定位到目标itemview，不带动画效果
* setSelectionFromTop(int position, int offset) 定位到目标itemview，目标itemview离可见区最左边offset
* smoothScrollToPosition(int position) 定位到目标itemview，带动画效果
* setSelector(Drawable/Color) 设置选中项的背景，不能通过xml文件配置。其它一些特点与vertical listview类似。（如果itemview原来有背景，则action up后，会还原成原来的背景，如果没有的话就是用户设置的selector）
* setHeaderDividersEnabled(boolean) 设置是否给header views绘制divider

## 回收机制
这是模仿vertical listview的回收机制，将不可见的itemview放入回收站(RecyclBin)以便复用。此版本已经支持itemview定义不同样式布局，但在使用不同样式布局中，不能使用selection或者smoothscroll方法，因为scroller的滑动要设置滑动距离，不同布局时现在还没想到计算要滑动的长度的方法。如果使用多样式布局，在adapter中还要实现以下方法，这是为了让回收站根据类型来做不同处理，复用不同的itemview，模仿vertical listview。