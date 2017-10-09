1. Open Hallo Android SDK Manager door te klikken op Hallo-pictogram op de werkbalk Hallo van Android Studio of door te klikken op **extra** -> **Android** -> **SDK Manager**Hallo-menu. De doelversie Hallo Hallo Android SDK die wordt gebruikt in uw project vinden, opent u deze door te klikken op **Pakketgegevens weergeven**, en kies **Google APIs**, als deze nog niet is geïnstalleerd.
2. Klik op Hallo **SDK-Tools** tabblad. Als u Google Play Service nog niet hebt geïnstalleerd, klikt u op **Google Play Services** zoals hieronder weergegeven. Klik vervolgens op **toepassen** tooinstall. 
   
    Houd er rekening mee Hallo SDK-pad voor gebruik in een latere stap. 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. Open Hallo **build.gradle** in Hallo app map.
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. Voeg deze regel toe onder *Afhankelijkheden*: 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. Klik op Hallo **Project met Gradle-bestanden** pictogram in het Hallo-werkbalk.
6. Open **AndroidManifest.xml** en voeg deze code toohello *toepassing* label.
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

