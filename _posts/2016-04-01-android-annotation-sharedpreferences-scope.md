---
layout: post
title: Introducing Hyde
---

Fixing android annotation preference not shared across all activity. *Somehow I miss to read about Scope section*

<!--break-->

If you write / put value in sharedpreference at Activity A and try to read / get it at Activity B and the value is null, maybe you forget to define scope in AA Preference.

Read it here : [Android Annotation SharedPreferences Scope](https://github.com/excilys/androidannotations/wiki/SharedPreferencesHelpers#scope)

**TL;DR** : To make it work like normal SharedPreferences, you should write :

```java
@SharedPref(value=SharedPref.Scope.UNIQUE)
public interface MyPrefs {
...
```
