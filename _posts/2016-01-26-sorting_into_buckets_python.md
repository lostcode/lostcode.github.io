---
layout: post
title:  "Sorting items into buckets in Python"
date:   2016-01-26 
categories:
---

Say, you want to sort a list of items, where 

1. the items naturally fall into separate buckets, 
2. you want these buckets to appear in a certain order, 
3. you don't particularly care about the ordering of items *within* these buckets.

For instance, say you have a list of items that have a color attribute and if you want to arrange these items by color. 

    >>> items = ["red:apple", "red:ferrari", "green:apple", "green:grass", "blue:sky", "blue:ocean"]
    >>> def get_sort_key(color):
    ...     # will return tuples like (True, False, False)
    ...     # dependening on which color is passed
    ...     return (
    ...         color == "red",
    ...         color == "green",
    ...         color == "blue"
    ...     )
    >>> sorted(items, key=lambda item: get_sort_key(item.split(":")[0]))
    ['blue:sky', 'blue:ocean', 'green:apple', 'green:grass', 'red:apple', 'red:ferrari']
    >>>


[1] [Bucket Sort](https://en.wikipedia.org/wiki/Bucket_sort) is a sorting technique, which buckets items and then sorts within those buckets. This can probably be thought of the first stage of the bucket sort, where items are inserted into ordered buckets.

[2] This is probably inefficient if you have too many buckets. I'm not a 100% sure how tuples are sorted, but I'm guessing the algorithm makes multiple passes through different stages of the sorted items, one for each entry in tuple (in tuple item order). If so, the complexity comes to O(B * NlogN), where B is the number of buckets and N is the number of items in the list.
