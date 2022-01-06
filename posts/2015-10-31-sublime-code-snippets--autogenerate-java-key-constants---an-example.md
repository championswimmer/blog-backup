---
title: "Sublime Code Snippets : Autogenerate Java key constants - an example"
slug: sublime-code-snippets--autogenerate-java-key-constants---an-example
date_published: 2015-10-31T00:00:00.000Z
date_updated: 2015-10-31T00:00:00.000Z
---

I largely use [Jetbrains](http://jetbrains.com) products for my day to day development work (which is mostly Android). I really love the *Live Template* feature that is available on IntelliJ, for example if I type `psfs` and press `Tab` I get the following on the screen

    public static final String
    

These days, sometimes I use Sublime Text 3 as well, because unless I need all the features of an IDE, it's too heavy to open up, especially if other stuff is running on the laptop. One of those days when I was using Sublime, I needed to create a lot of Database key constants - i.e. in the form of

    public static final String KEY_ONE = "key_one"
    

So it so happens that there exists functionality like live templates on Sublime as well, in form of **Snippets**

To create a new Snippet, go to Tools -> New Snippet.

Ideally you save your snippets in `~/.config/sublime-text-3/Packages/User/MySnippet.sublime-snippet`

Here is an example config for the Snippet that creates Java key constants

    <snippet>
    	<content>public static final String ${1/(.+)/(\U\1)/g} = "${1}";</content>
    	<tabTrigger>jkey</tabTrigger>
    	<scope>source.java</scope>
    	<description>public static final String KEY = "key"</description>
    </snippet>
    

Now when you type `jkey` and press tab, it creates

    public static final String | = "|"
    

The pipes '|' represent the cursor position. When you start typing in lowercase for example `my_key_one`, automatically the variable name updates in uppercase `MY_KEY_ONE`.
