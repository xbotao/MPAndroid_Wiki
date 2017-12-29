
In case you are using _Proguard_, you will need to **whitelist MPAndroidChart**, which requires to add the following line to your Proguard configuration file:

```
-keep class com.github.mikephil.charting.** { *; }
```
If you don't do this, animations might not work.

If you are having issues with the [Realm.io](http://realm.io) classes, add the following to your config file:

```
-dontwarn io.realm.**
```

[Additional information on Proguard](http://developer.android.com/tools/help/proguard.html).