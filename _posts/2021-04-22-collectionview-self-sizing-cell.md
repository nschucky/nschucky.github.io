---
layout: post
title: Programmatically UICollectionViewCell with dynamic height - the lazy way
subtitle: working on subtitle, the new subtitle will blow your mind.
tags: [ios, swiftui, swift, uikit]
comments: true
---

> this post was inspired by Giuseppe's article [Self-sizing UICollectionViewCell: the quickest and simplest way](https://medium.com/@giusecapo/self-sizing-uicollectionviewcell-the-quickest-and-simplest-way-94e8d1c89594), I'm basically copying the dude's post, but without storyboards



🚨 I write this while shopping for instacart, that’s what i do part time, that should be self explanatory, this code could be dangerous.

Being lucky as i am, I went from being a full time peasant (there's not many perks on that job, let me tell you) with very little education to owning a 2008 prius and being a premium driver on every food delivery company in San Francisco, I came across this article beautiful [article](https://medium.com/@giusecapo/self-sizing-uicollectionviewcell-the-quickest-and-simplest-way-94e8d1c89594) that prevent me from wasting a lot more of my precious and scarce hours. Being such an intelectual, I avoid using Storyboards, but really, it’s totally fine to use storyboards, I just wanna be cool and accepted in this society.

I’ll be brief...

You can start by initializing a `UICollectionViewController` subclass with

``` swift
init() {
    let layout = UICollectionViewFlowLayout()
    layout.scrollDirection = .vertical
    let width = UIScreen.main.bounds.size.width
    layout.estimatedItemSize = CGSize(width: width, height: 0)
    super.init(collectionViewLayout: layout)
    collectionView.dataSource = self
    collectionView.delegate = self
}

```




...and then in my `UICollectionViewCell` subclass:

``` swift
lazy var widthConstraint: NSLayoutConstraint = {
    let width = contentView.widthAnchor.constraint(equalToConstant: bounds.size.width)
    width.isActive = true
    return width
}()

```

plus

``` swift

override func systemLayoutSizeFitting(_ targetSize: CGSize, withHorizontalFittingPriority horizontalFittingPriority: UILayoutPriority, verticalFittingPriority: UILayoutPriority) -> CGSize {
    widthConstraint.constant = bounds.size.width
    return contentView.systemLayoutSizeFitting(CGSize(width: targetSize.width, height: 1))
}

```


But, don't forget the

``` swift
contentView.translatesAutoresizingMaskIntoConstraints = false
```

In your cell's `init(frame: CGRect)` , and you should be good to go. (🔥)

Still finishing this article, sorry if you ended up here., check my repository with the [Project code](https://github.com/nschucky/SarcasticCollectionView).

Again careful with that code comrades  😬😬😬

Accepting positive, negative and other kinds of feedback (like venmo @nschucky).