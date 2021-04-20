---
layout: post
title: How to use UIViewController with a SwiftUI Custom TabBar
subtitle: Each post also has a subtitle, but i couldn't think of one
tags: [ios, swiftui, swift, uikit]
comments: true
---

It's 4/20 4:20 PM in California and after procrastinating for 5 years, here's my first blog post where I'll be covering how to:

- Set a SwiftUI View as the AppCoordinator's `rootViewController`  with **UIHostingController**.
- Use a Custom SwiftUI TabBar with **UIViewController** as child.
- Avoid reloading **UIViewController** when switching tabs.

*Disclaimer*
> This post is dedicated to all Tesla owners in California who doesn’t have a custom license plate, you’re the resistance in our doomed civilization!

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