title: Fragment 部分 API 用法
date: 2014-10-19 19:36:52
category: 技术
tags:  Fragment
description: Fragment 中 isAdded(), isDetached(),isHidden(),isInLayout(),isRemoving(),isResumed(),isVisible() 的用法。

---
`public final boolean isAdded()`

如果该Fragment对象被添加到了它的Activity中，那么它返回true，否则返回false。

`public final boolean isDetached()`

如果该Fragment已经明确的从UI中分离，那么它返回true。也就是说,在该Fragment对象上使用

`public final boolean isHidden()`

如果该Fragment对象已经被隐藏，那么它返回true。默认情况下，Fragment是被显示的。能够用onHiddenChanged(boolean)回调方法获取该Fragment对象状态的改变，要注意的是隐藏状态与其他状态是正交的---也就是说，要把该Fragment对象显示给用户，Fragment对象必须是被启动并不被隐藏。

`Public final boolean isInLayout()`

如果布局通过<fragment>标签被包含在Activity层次树中，那么它就返回true。当Fragment是通过<fragment>标签来创建的时候，这个方法始终会返回true。从之前的状态恢复旧的Fragment对象，并且该对象没有显示在当前状态的布局中的情况除外。

`Public final boolean isRemoving()`

如果当前的Fragment对象正在从它的Activity中被删除，那么就返回true。这删除过程不是该Fragment对象的Activity的结束过程，而是把Fragment对象从它所在的Activity中删除的过程。

`public final boolean isResumed()`

如果Fragment对象是在恢复状态中，该方法会返回true。在onResume()和onPause()回调期间，这个方法都返回true。

`Public final boolean isVisible()`

如果该Fragment对象对用户可见，那么就返回true。这就意味着它：1.已经被添加到Activity中；2.它的View对象已经被绑定到窗口中；3.没有被隐藏。