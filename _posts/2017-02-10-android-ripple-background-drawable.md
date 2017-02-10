---
layout: post
title: Android Ripple Background Drawable
comments: true
---

If you want to add Ripple effect when user click on your view, add this as a background :

<!--break-->

```xml
<ImageView
	android:background="?attr/selectableItemBackgroundBorderless"
	android:clickable="true"
	/>
```

You may want to add `clickable=true` attribute to make sure that the view can be clicked. This trick only apply to Android v21 (Lolipop) and up. If you want to achieve this effect in earlier version, you need to define the animation & drawable yourself or use a third party library.
