layout: post
title: How to use UIViewController with SwiftUI Custom TabBar
gh-repo: daattali/beautiful-jekyll
tags: [test]
comments: true
---

After procrastinating for 5 years, here's my first blog post where I'll be covering how to:

- Set a SwiftUI View as the AppCoordinator's `rootViewController`  with **UIHostingController**.
- Use a Custom SwiftUI TabBar with **UIViewController** as child.
- Avoid reloading **UIViewController** when switching tabs.

*Disclaimer*
> Before starting to sync files, you must link an account in the **Synchronize** sub-menu.

## Set a SwiftUI View as your AppCoordinator root

In order to use a SwiftUI in your UIKit AppCoordinator, you'll need to:

 1. Instantiate a **UIHostingController** and set the `rootView` to your SwiftUI View.
 2. Set the **UIWindow's** `rootViewController` to your **UIHostingController** instance.

``` swift
func start() {
	let floatingTabBar = FloatingTabBarView(selectedIndex: 1)
	let mainTabBarView = UIHostingController(rootView: floatingTabBar)
	window.rootViewController = mainTabBarView
	window.makeKeyAndVisible()
}
```