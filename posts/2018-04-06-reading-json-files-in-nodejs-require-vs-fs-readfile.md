---
title: "Reading json files in NodeJS: require() vs fs.readFile()"
slug: reading-json-files-in-nodejs-require-vs-fs-readfile
date_published: 2018-04-06T16:24:00.000Z
date_updated: 2018-04-17T08:23:15.000Z
---

Often we save settings or configurations in json files. If you've spent some time using NodeJS, you'd know that there are quite a few ways to read json files in NodeJS

Two of the most common ones are :

The other way is using the fs module.

We can either do it synchronously

Or we can do it asynchronously -

Now obviously the question that comes to mind is which method to use, and if there are any obvious benefits to any one method

Let us discuss the differences -

## Caching : (If the file data changes)

require() will cache the file in the require graph.

So during the lifetime of the node app, if the file.json is changed, you will not get the new data, even if you re-run require('./file.json')

On the other hand fs.readFile or fs.readFileSync will always re-read the file, and pick up changes.

## Encoding : (UTF-8 is used 99% times, but still…)

In require you cannot define the file encoding. 99% of the times, that is not a problem.

Nevertheless if your json is not encoded in Unicode/UTF-8, you’d have to use fs.readFile as it supports encodings such as **ascii** or **latin1** or even **base64** (yes, yes, I hear you, no one saves JSON as base64)

## Sync vs Async

require() is synchronous, and hence blocking in nature.

fs provides both sync and async methods as shown above. If you want to read your JSON file without blocking, then fs.readFile is your only option.

*NOTE: From NodeJS 10.x, import file from './file.json' would be possible because of support for modules, which would allow async reading of json files without fs*

I hope you’ll be able to take an informed decision in your future projects based on the points discussed here.

*Originally published at [gist.github.com](https://gist.github.com/f1467d422bcb8c348bb6677ccd890280).*
