---
layout: post
title: How to use UIViewController with a SwiftUI Custom TabBar
subtitle: Clever subtitle to come...
tags: [ios, swiftui, swift, uikit]
comments: true
---

After procrastinating for 5 years, here's my first blog post, where I'll be covering how to:

- Set a SwiftUI View as the AppCoordinator's `rootViewController` with **UIHostingController**.
- Use a Custom SwiftUI TabBar with **UIViewController** as child.
- Avoid reloading **UIViewController** when switching tabs.

> ***IMPORTANT**: This post is dedicated to all Tesla owners in California who don't have a custom license plate. You’re the resistance in our doomed civilization!*

> ***ALSO IMPORTANT**: My poor vocabulary will probably annoy you, but since you’re already here, keep reading, I’ll be brief.*


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

## Use a Custom SwiftUI TabBar with **UIViewController** as child

## Avoid calling `viewDidLoad` when switching tabs

If your **UIViewController** makes a network request on `viewDidLoad`, you'll probably want to avoid reloading (or re-rendering) it when you change tabs

> ***Comrades,** constructive and negative feedback are deeply appreciated, I'm also accepting tips to quit smoking.*