---
title: "Sets in Golang"
subtitle: ""
date: 2020-08-13T07:15:49-07:00
lastmod: 2020-08-13T07:15:49-07:00

tags:
  - Golang

featuredImage: ""
featuredImagePreview: ""

toc: false
lightgallery: false
---

Go natively doesn't support a set datatype like Python. However, it does provide the building blocks to create your own set implementation pretty easily.

The magic bit? The **empty struct**.

[Dave Cheney](https://dave.cheney.net/2014/03/25/the-empty-struct) goes into a lot of good detail about why the empty struct is such a neat thing. But for this post, I'll be covering how you can use the empty struct to do set operations.
<!--more-->

Say you wanted to make a set of strings and take action like. adding, removing, and checking membership of those strings all while guaranteeing a fundamental property of sets: no duplicates.

How can you do this?

The TL;DR is that you can make a set by creating a map where the key is whatever you want to store in the set, and the value being the empty struct. The empty struct takes no space, so it is the most efficient way to create a set-like structure in Go. 

Here's an example of how to create a set of strings:

```go
// I usually first like to define an `empty` variable to represent my empty struct
var empty struct{}

// Create a map that represents the set structure
uniqueStrings := make(map[string]empty)
```

Once you have this, here are some common set operations

```go
// Add "foo" to the set
uniqueStrings["foo"] = empty

// Remove "foo" fom the set
delete(uniqueStrings, "foo")

// Check if "bar" is in the set
if _, ok := uniqueStrings["bar"]; ok {
  fmt.Println("bar is in the set!")
}
```

You might ask, *"Why not just put strings into a slice/list?"*

Well, that is because membership checking and removing elements from a slice is a `O(n)` operation and using a map gives you `O(1)` for inserting, removing, AND membership checking.

And that's it! Hopefully this provided you with some info on how to make sure own set implementation in Go! Coming from Python, I thought it was lacking that Go didn't have a native set type, but then I realized how easy it was to create your own!
