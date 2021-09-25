Hi there!
AndroidDnssdDiscoveryEclipse: an eclipse version.
AndroidDnssdDiscovery: a netbeans version of the thing.



Below, how I got the AndroidDnssdDiscoveryEclipse project and how to run it.
* create an android project
* in the AndroidManifest.mf, add:
 <uses-permission android:name="android.permission.INTERNET"/>
 <uses-permission android:name="android.permission.CHANGE_WIFI_MULTICAST_STATE"/>
* after downloading jmdns 3.4.0, I needed to remove duplicate .class inside (at the same time I dropped the test classes):
** run: cp -r ~/jmdns.jar ./
** run: mkdir unjar
** run: cd unjar
** run: jar xf ../jmdns.jar
** run: jar cfm ../jmdns.jar META-INF/MANIFEST.MF javax/
** (create a copy or link for eclipse), run: cd ../AndroidDnssdDiscoveryEclipse && ln -s ../jmdns.jar
* refresh the project in eclipse
* add the jar as a dependency in eclipse by (right click on jmdns.jar and "build path -> add to build path"
* add info in the res/layout/main.xml:
    <TextView android:id="@+id/text"
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:text="" />
* fill the activity
* In eclipse, "run as -> android application"
** if you have a linux pc connected to same network, you should see it listed by your android phone within a few seconds (as it exposes a "_workstation._tcp" service)
** you should also see the service exposed by the phone using "avahi-browse --all" (the service is called AndroidTest)





== OLD VERSION BELOW (before I found the problem with jmdns)

* create an android project
* in the AndroidManifest.mf, add:
 <uses-permission android:name="android.permission.INTERNET"/>
 <uses-permission android:name="android.permission.CHANGE_WIFI_MULTICAST_STATE"/>
* after downloading jmdns 3.4.0 and finding no way to make dex compile the jar, I added the sources with:
** run: cp -r ~/app/jmdns-3.4.0/src/javax/ AndroidDnssdDiscoveryEclipse/src/
** run: rm -rf AndroidDnssdDiscoveryEclipse/src/javax/jmdns/test/
** refresh in eclipse
* add info in the res/layout/main.xml:
    <TextView android:id="@+id/text"
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:text="" />
* fill the activity
* In eclipse, "run as -> android application"
** if you have a linux pc connected to same network, you should see it listed by your android phone within a few seconds (as it exposes a "_workstation._tcp" service)
** you should also see the service exposed by the phone using "avahi-browse --all" (the service is called AndroidTest)
