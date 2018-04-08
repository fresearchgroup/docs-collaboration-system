---
id: inappropriatecontentfilter
title: Inappropriate Content Filter
sidebar_label: Inappropriate Content Filter
---

## Inappropriate Content Filter

Import `inappropriate_content_filter` function

```
from InappropriateContentFilter.views import inappropriate_content_filter
```

## Usage

`inappropriate_content_filter` takes two arguments both of which have to be string

It will return data in following format:

```
{ 
	'inappropriate': True, 
	'inappropriate_words': [] 
}
```

It the arguments provided contains any inappropriate words, the value of `inappropriate` key will be `True` and `inappropriate_word` will contain the list of inappropriate words. Otherwise `inappropriate` will be `False` and `inappropriate_words` will be an empty list.
