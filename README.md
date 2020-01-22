# godot-plugin-firebase
This plugin is based on https://github.com/FrogSquare/GodotFireBase, so all credit goes to FrogSquare.

I adjusted this plugin so it works with the new Android plugin system for Godot 3.2 (at least alpha 3 is needed).

Steps to follow to make this plugin work:

- download and start Godot 3.2 (alpha 3 or greater). No need to build it on your own (compile, ...).

- in Godot with your project opened select `Project > Install Android Build Template`. This will install the files in your project's directory (by adding `android/...`)

- `git clone https://github.com/mrcrb/godot-plugin-sql` in `[GODOT-PROJECT]/android/` (for this plugin no further configuration is needed)

- `git clone https://github.com/mrcrb/godot-plugin-firebase` in `[GODOT-PROJECT]/android/`

- from Firebase console download `google-services.json` and copy/move it to `[GODOT-PROJECT]/android/build/`

- for AdMob edit `[GODOT-PROJECT]/android/godot-plugin-firebase/assets/godot-firebase-config.json` to match your needs
  - currently AdMob (with Mediation), Analytics, Firestore and Unity Ads is working.
  - to test ads with test ad IDs set `"TestAds" : true`
    - setting this to true ignores the IDs (`BannerAdId`, `InterstitialAdId`, `RewardedVideoAdId`) and fetches [official AdMob test ads](https://developers.google.com/admob/android/test-ads)

- edit `[GODOT-PROJECT]/android/godot-plugin-firebase/gradle.conf`
  - edit your applicationId
 
  `applicationId 'com.mycompany.myappname'`

- edit `[GODOT-PROJECT]/android/godot-plugin-firebase/AndroidManifest.conf`
  - edit the following section to match your AdMob App ID
  
        <meta-data
        android:name="com.google.android.gms.ads.APPLICATION_ID"
        android:value="ca-app-pub-ADMOB-APP-ID"/>

- now you should be able to build
  - in Godot with your project opened select `Project > Export`
  - add an Android Export preset and enable `Use Custom Build`
  - in the project settings (`Project > Project Settings`) add to `Android: Modules` the following line
  
    `org/godotengine/godot/Firebase,org/godotengine/godot/SQLBridge`

That's it. For further instructions on how to call AdMob functions refer to https://github.com/FrogSquare/GodotFireBase. Just remember to change the calls from `FireBase` to `Firebase` (notice the **capital B** is now lower-case in this plugin).

