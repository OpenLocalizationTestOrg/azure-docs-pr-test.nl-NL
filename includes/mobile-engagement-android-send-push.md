
### <a name="update-manifest-file-tooenable-notifications"></a>Manifestbestand tooenable meldingen bijwerken
Hallo-app messaging bronnen hieronder kopiëren naar uw Manifest.xml tussen Hallo `<application>` en `</application>` labels.

        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
        </activity>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
        </receiver>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
        </receiver>

### <a name="specify-an-icon-for-notifications"></a>Een pictogram voor meldingen opgeven
Plakken Hallo na XML-fragment in het bestand Manifest.xml tussen Hallo `<application>` en `</application>` labels.

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

Hiermee definieert u Hallo-pictogram dat wordt weergegeven bij systeemmeldingen en in-app-meldingen. Het is optioneel voor in-app-meldingen maar verplicht voor systeemmeldingen. In Android worden systeemmeldingen met ongeldige pictogrammen geweigerd.

Zorg ervoor dat u een pictogram dat bestaat in een Hallo **drawable** mappen (zoals ``engagement_close.png``). **mipmap**-map wordt niet ondersteund.

> [!NOTE]
> Gebruik geen Hallo **launcher** pictogram. Heeft een andere resolutie en bevindt zich doorgaans in de mipmap-mappen hello, die niet worden ondersteund.
> 
> 

Voor echte apps kunt u een pictogram gebruiken dat geschikt is voor meldingen volgens de [Android-ontwerprichtlijnen](http://developer.android.com/design/patterns/notifications.html).

> [!TIP]
> toobe ervoor toouse juiste resoluties voor pictogrammen, kunt u bekijken [deze voorbeelden](https://www.google.com/design/icons).
> Schuif omlaag toohello **melding** sectie, klik op een pictogram en klik vervolgens op `PNGS` toodownload Hallo pictogram drawable-set. U kunt zien welke drawable-mappen met welke resolutie toouse voor elke versie van het Hallo-pictogram.
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a>Uw app tooreceive GCM-pushmeldingen inschakelen
1. Plak Hallo volgende in het bestand Manifest.xml tussen Hallo `<application>` en `</application>` labels na het vervangen van Hallo **afzender-ID** ontleend aan uw project Firebase console. Hallo \n is opzettelijk dus zorg ervoor dat Hallo projectnummer Hiermee eindigt.
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. Plak Hallo onderstaande code in uw Manifest.xml tussen Hallo `<application>` en `</application>` labels. Vervang de pakketnaam Hallo <Your package name>.
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
        android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<Your package name>" />
            </intent-filter>
        </receiver>
3. Toevoegen van de laatste reeks machtigingen die zijn gemarkeerd vóór Hallo Hallo `<application>` label. Vervang `<Your package name>` door de werkelijke pakketnaam Hallo van uw toepassing.
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

