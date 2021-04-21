# How to use UIViewController with SwiftUI Custom TabBar

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

## Use a Custom SwiftUI TabBar with UIViewController as child


``` swift
let  items: [BottomBarItem] = [
	BottomBarItem(selected: "house.fill", unselected: "house"),
	BottomBarItem(selected: "gamecontroller.fill", unselected: "gamecontroller"),
	BottomBarItem(selected: "car.fill", unselected: "car")
]

@State  public  var  selectedIndex: Int = 0

private  let  viewList = [AnyView(FloatingView()),
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
			.shadow(color: Color.black.opacity(0.1), radius: 10, x: 10, y: 5)

		}.padding(EdgeInsets(top: 0, leading: 40, bottom: 20, trailing: 40))

}

}

}
```

>  ***Comrades,** revisions and tips to quit smoking are deeply appreciated.*

If your **UIViewController** makes a network request on `viewDidLoad`, you'll probably want to avoid reloading (or re-rendering) it when switching tabs

## Create files and folders

The file explorer is accessible using the button in left corner of the navigation bar. You can create a new file by clicking the **New file** button in the file explorer. You can also create folders by clicking the **New folder** button.

## Switch to another file

All your files and folders are presented as a tree in the file explorer. You can switch from one to another by clicking a file in the tree.

## Rename a file

You can rename the current file by clicking the file name in the navigation bar or by clicking the **Rename** button in the file explorer.

## Delete a file

You can delete the current file by clicking the **Remove** button in the file explorer. The file will be moved into the **Trash** folder and automatically deleted after 7 days of inactivity.

## Export a file

You can export the current file by clicking **Export to disk** in the menu. You can choose to export the file as plain Markdown, as HTML using a Handlebars template or as a PDF.


# Synchronization

Synchronization is one of the biggest features of StackEdit. It enables you to synchronize any file in your workspace with other files stored in your **Google Drive**, your **Dropbox** and your **GitHub** accounts. This allows you to keep writing on other devices, collaborate with people you share the file with, integrate easily into your workflow... The synchronization mechanism takes place every minute in the background, downloading, merging, and uploading file modifications.

There are two types of synchronization and they can complement each other:

- The workspace synchronization will sync all your files, folders and settings automatically. This will allow you to fetch your workspace on any other device.
	> To start syncing your workspace, just sign in with Google in the menu.

- The file synchronization will keep one file of the workspace synced with one or multiple files in **Google Drive**, **Dropbox** or **GitHub**.
	> Before starting to sync files, you must link an account in the **Synchronize** sub-menu.

## Open a file

You can open a file from **Google Drive**, **Dropbox** or **GitHub** by opening the **Synchronize** sub-menu and clicking **Open from**. Once opened in the workspace, any modification in the file will be automatically synced.

## Save a file

You can save any file of the workspace to **Google Drive**, **Dropbox** or **GitHub** by opening the **Synchronize** sub-menu and clicking **Save on**. Even if a file in the workspace is already synced, you can save it to another location. StackEdit can sync one file with multiple locations and accounts.

## Synchronize a file

Once your file is linked to a synchronized location, StackEdit will periodically synchronize it by downloading/uploading any modification. A merge will be performed if necessary and conflicts will be resolved.

If you just have modified your file and you want to force syncing, click the **Synchronize now** button in the navigation bar.

> **Note:** The **Synchronize now** button is disabled if you have no file to synchronize.

## Manage file synchronization

Since one file can be synced with multiple locations, you can list and manage synchronized locations by clicking **File synchronization** in the **Synchronize** sub-menu. This allows you to list and remove synchronized locations that are linked to your file.


# Publication

Publishing in StackEdit makes it simple for you to publish online your files. Once you're happy with a file, you can publish it to different hosting platforms like **Blogger**, **Dropbox**, **Gist**, **GitHub**, **Google Drive**, **WordPress** and **Zendesk**. With [Handlebars templates](http://handlebarsjs.com/), you have full control over what you export.

> Before starting to publish, you must link an account in the **Publish** sub-menu.

## Publish a File

You can publish your file by opening the **Publish** sub-menu and by clicking **Publish to**. For some locations, you can choose between the following formats:

- Markdown: publish the Markdown text on a website that can interpret it (**GitHub** for instance),
- HTML: publish the file converted to HTML via a Handlebars template (on a blog for example).

## Update a publication

After publishing, StackEdit keeps your file linked to that publication which makes it easy for you to re-publish it. Once you have modified your file and you want to update your publication, click on the **Publish now** button in the navigation bar.

> **Note:** The **Publish now** button is disabled if your file has not been published yet.

## Manage file publication

Since one file can be published to multiple locations, you can list and manage publish locations by clicking **File publication** in the **Publish** sub-menu. This allows you to list and remove publication locations that are linked to your file.


# Markdown extensions

StackEdit extends the standard Markdown syntax by adding extra **Markdown extensions**, providing you with some nice features.

> **ProTip:** You can disable any **Markdown extension** in the **File properties** dialog.


## SmartyPants

SmartyPants converts ASCII punctuation characters into "smart" typographic punctuation HTML entities. For example:

|                |ASCII                          |HTML                         |
|----------------|-------------------------------|-----------------------------|
|Single backticks|`'Isn't this fun?'`            |'Isn't this fun?'            |
|Quotes          |`"Isn't this fun?"`            |"Isn't this fun?"            |
|Dashes          |`-- is en-dash, --- is em-dash`|-- is en-dash, --- is em-dash|


## KaTeX

You can render LaTeX mathematical expressions using [KaTeX](https://khan.github.io/KaTeX/):

The *Gamma function* satisfying $\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$ is via the Euler integral

$$
\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.
$$

> You can find more information about **LaTeX** mathematical expressions [here](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference).


## UML diagrams

You can render UML diagrams using [Mermaid](https://mermaidjs.github.io/). For example, this will produce a sequence diagram:

```mermaid
sequenceDiagram
Alice ->> Bob: Hello Bob, how are you?
Bob-->>John: How about you John?
Bob--x Alice: I am good thanks!
Bob-x John: I am good thanks!
Note right of John: Bob thinks a long<br/>long time, so long<br/>that the text does<br/>not fit on a row.

Bob-->Alice: Checking with John...
Alice->John: Yes... John, how are you?
```

And this will produce a flow chart:

```mermaid
graph LR
A[Square Rect] -- Link text --> B((Circle))
A --> C(Round Rect)
B --> D{Rhombus}
C --> D
```

## Use a Custom SwiftUI TabBar with UIViewController as child

  

First let's create a struct to represent the selected and normal state of the tab bar item

``` swift

public  struct  BottomBarItem {
	public  let selected: String
	public  let unselected: String

	public  init(selected: String, unselected: String) {
		self.selected = selected
		self.unselected = unselected
	}
}

```

Feel free to add more properties to customize the **BottomBarItem**.

To create the actual TabBar, We'll use a a View that takes the `selectedIndex` and an array of **BottomBarItem's** and setup the layout for the TabBar

``` swift
public  struct  BottomBar : View {
	@Binding  public  var  selectedIndex: Int
	public  let  items: [BottomBarItem]
	
	public init(selectedIndex: Binding<Int>, items: [BottomBarItem]) {
		self._selectedIndex = selectedIndex
		self.items = items
	}

	func itemView(at index: Int) -> some View {
		Button(action: {
			self.selectedIndex = index
		}) {
			BottomBarItemView(isSelected: index == selectedIndex, item: items[index])
		}
	}

	public  var  body: some  View {
		ZStack {
			HStack(alignment: .center) {
				Spacer()
				self.itemView(at: 0)
				Spacer()
				self.itemView(at: 1)
				Spacer()
				self.itemView(at: 2)
				Spacer()
			}.padding([.horizontal]).padding(.bottom,0).padding(.top,0)
		}
		.background(Color.black)
	}
}
```

Now, you'll have an opportunity to customize each tab bar item, using the **BottomBarItem**, you can add UI Components and set them based on the model's properties:

``` swift
public  struct  BottomBarItemView: View {
	public  let  isSelected: Bool
	public  let  item: BottomBarItem
	
	public  var  body: some  View {
		HStack {
			Image(systemName: isSelected ? item.selected : item.unselected)
			.imageScale(.large)
		}
		.padding()
	}
}
```

Finally, to display the TabBar  we will create another view 

``` swift 
struct  ContentView: View {
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
						.shadow(color: Color.black.opacity(0.1), radius: 10, x: 10, y: 5)

}.padding(EdgeInsets(top: 0,

leading: 40,

bottom: 20,

trailing: 40))

}

}

}

}
```