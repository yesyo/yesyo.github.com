---
layout: post
title: "內凹背景小技巧"
date: 2012-02-12 16:15
comments: true
categories: android
---

我想就從一個 Android 小技巧開始好了，要怎麼描述標題著實讓我苦惱。

是這樣的，在 [Datepicker](http://github.com/yesyo/datepicker "Android DatePicker Widget") 裡，我想讓"今天"這一格有往內凹的感覺。怎麼做呢？當然可以用 photoshop 畫個背景，不過身為一個 programmer (笑)，當然不能碰 photoshop 這種東西(誤)。

於是下面的 xml 就出現了。

``` xml res/drawable/calendar_today_background.xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
	<item>
		<shape>
			<stroke	android:width="1dp" android:color="#202020" />
		</shape>
	</item>

	<item
		android:top="1dp"
		android:right="1dp"
		android:bottom="1dp"
		android:left="1dp">
		<shape>
			<stroke	android:width="1dp" android:color="#2A2A2A"/>
		</shape>
	</item>

	<item
		android:top="2dp"
		android:right="2dp"
		android:bottom="2dp"
		android:left="2dp">
		<shape>
			<solid android:color="#373737" />
			<stroke	android:width="1dp" android:color="#303030"/>
		</shape>
	</item>
</layer-list>
```

[layer list](http://developer.android.com/guide/topics/resources/drawable-resource.html#LayerList "Android Layer List") 會從上畫到下，所以最下面的 drawable item 會畫在最上層。如果下面的 item 跟上面的 item 位置重疊到則會蓋掉上面的 item。

所以上面這段 xml，從最上面的 item 開始依序畫了三個正方形，後一個比前一個縮小一個 [dp](http://developer.android.com/guide/topics/resources/more-resources.html#Dimension "Android dimension")，後兩個就會看起來像是陰影，最後一個再填滿正方形內的顏色。

把這指定給 view 的 background：

``` java MonthView.java
TextView date;
...
date.setBackgroundResource(R.drawable.background_today);
```

就大功告成。

{% img images/android_datepicker.png %}
