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

## Use a Custom SwiftUI TabBar with UIViewController as child

First let's create a struct to represent the selected and normal state of the tab bar item

``` swift
public struct BottomBarItem {
    public let selected: String
    public let unselected: String
    
    public init(selected: String, unselected: String) {
        self.selected = selected
        self.unselected = unselected
    }
}
```

Feel free to add more properties to customize the **BottomBarItem**.

``` swift
struct ContentView: View {

    let items: [BottomBarItem] = [
        BottomBarItem(selected: "house.fill", unselected: "house"),
        BottomBarItem(selected: "gamecontroller.fill", unselected: "gamecontroller"),
        BottomBarItem(selected: "car.fill", unselected: "car")
    ]
    
    @State public var selectedIndex: Int = 0
    
    private let viewList = [AnyView(FloatingView()),
                            AnyView(RanOutOfIdeasView()),
                            AnyView(LastView())]
    
    
    var body: some View {
        ZStack {
            viewList[selectedIndex]
            VStack {
                Spacer()
                ZStack {
                    BottomBar(selectedIndex: $selectedIndex, items: items)
                        .cornerRadius(20)
                        .shadow(color: Color.black.opacity(0.1), radius: 10,
                                x: 10,
                                y: 5)
                }.padding(EdgeInsets(top: 0,
                                     leading: 40,
                                     bottom: 20,
                                     trailing: 40))
            }
        }
    }
}
```

## Use a Custom SwiftUI TabBar with **UIViewController** as child

## Avoid calling `viewDidLoad` when switching tabs

If your **UIViewController** makes a network request on `viewDidLoad`, you'll probably want to avoid reloading (or re-rendering) it when you change tabs

> ***Comrades,** constructive and negative feedback are deeply appreciated, I'm also accepting tips to quit smoking.*