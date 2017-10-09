
### <a name="update-manifest-file-tooenable-notifications"></a><span data-ttu-id="714ca-101">Manifestbestand tooenable meldingen bijwerken</span><span class="sxs-lookup"><span data-stu-id="714ca-101">Update manifest file tooenable notifications</span></span>
<span data-ttu-id="714ca-102">Hallo-app messaging bronnen hieronder kopiëren naar uw Manifest.xml tussen Hallo `<application>` en `</application>` labels.</span><span class="sxs-lookup"><span data-stu-id="714ca-102">Copy hello in-app messaging resources below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

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

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="714ca-103">Een pictogram voor meldingen opgeven</span><span class="sxs-lookup"><span data-stu-id="714ca-103">Specify an icon for notifications</span></span>
<span data-ttu-id="714ca-104">Plakken Hallo na XML-fragment in het bestand Manifest.xml tussen Hallo `<application>` en `</application>` labels.</span><span class="sxs-lookup"><span data-stu-id="714ca-104">Paste hello following XML snippet in your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="714ca-105">Hiermee definieert u Hallo-pictogram dat wordt weergegeven bij systeemmeldingen en in-app-meldingen.</span><span class="sxs-lookup"><span data-stu-id="714ca-105">This defines hello icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="714ca-106">Het is optioneel voor in-app-meldingen maar verplicht voor systeemmeldingen.</span><span class="sxs-lookup"><span data-stu-id="714ca-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="714ca-107">In Android worden systeemmeldingen met ongeldige pictogrammen geweigerd.</span><span class="sxs-lookup"><span data-stu-id="714ca-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="714ca-108">Zorg ervoor dat u een pictogram dat bestaat in een Hallo **drawable** mappen (zoals ``engagement_close.png``).</span><span class="sxs-lookup"><span data-stu-id="714ca-108">Make sure you are using an icon that exists in one of hello **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="714ca-109">**mipmap**-map wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="714ca-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="714ca-110">Gebruik geen Hallo **launcher** pictogram.</span><span class="sxs-lookup"><span data-stu-id="714ca-110">You should not use hello **launcher** icon.</span></span> <span data-ttu-id="714ca-111">Heeft een andere resolutie en bevindt zich doorgaans in de mipmap-mappen hello, die niet worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="714ca-111">It has a different resolution and is usually in hello mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="714ca-112">Voor echte apps kunt u een pictogram gebruiken dat geschikt is voor meldingen volgens de [Android-ontwerprichtlijnen](http://developer.android.com/design/patterns/notifications.html).</span><span class="sxs-lookup"><span data-stu-id="714ca-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="714ca-113">toobe ervoor toouse juiste resoluties voor pictogrammen, kunt u bekijken [deze voorbeelden](https://www.google.com/design/icons).</span><span class="sxs-lookup"><span data-stu-id="714ca-113">toobe sure toouse correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="714ca-114">Schuif omlaag toohello **melding** sectie, klik op een pictogram en klik vervolgens op `PNGS` toodownload Hallo pictogram drawable-set.</span><span class="sxs-lookup"><span data-stu-id="714ca-114">Scroll down toohello **Notification** section, click an icon, and then click `PNGS` toodownload hello icon drawable set.</span></span> <span data-ttu-id="714ca-115">U kunt zien welke drawable-mappen met welke resolutie toouse voor elke versie van het Hallo-pictogram.</span><span class="sxs-lookup"><span data-stu-id="714ca-115">You can see what drawable folders with which resolution toouse for each version of hello icon.</span></span>
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a><span data-ttu-id="714ca-116">Uw app tooreceive GCM-pushmeldingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="714ca-116">Enable your app tooreceive GCM push notifications</span></span>
1. <span data-ttu-id="714ca-117">Plak Hallo volgende in het bestand Manifest.xml tussen Hallo `<application>` en `</application>` labels na het vervangen van Hallo **afzender-ID** ontleend aan uw project Firebase console.</span><span class="sxs-lookup"><span data-stu-id="714ca-117">Paste hello following into your Manifest.xml between hello `<application>` and `</application>` tags after replacing hello **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="714ca-118">Hallo \n is opzettelijk dus zorg ervoor dat Hallo projectnummer Hiermee eindigt.</span><span class="sxs-lookup"><span data-stu-id="714ca-118">hello \n is intentional so make sure that you end hello project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="714ca-119">Plak Hallo onderstaande code in uw Manifest.xml tussen Hallo `<application>` en `</application>` labels.</span><span class="sxs-lookup"><span data-stu-id="714ca-119">Paste hello code below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span> <span data-ttu-id="714ca-120">Vervang de pakketnaam Hallo <Your package name>.</span><span class="sxs-lookup"><span data-stu-id="714ca-120">Replace hello package name <Your package name>.</span></span>
   
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
3. <span data-ttu-id="714ca-121">Toevoegen van de laatste reeks machtigingen die zijn gemarkeerd vóór Hallo Hallo `<application>` label.</span><span class="sxs-lookup"><span data-stu-id="714ca-121">Add hello last set of permissions that are highlighted before hello `<application>` tag.</span></span> <span data-ttu-id="714ca-122">Vervang `<Your package name>` door de werkelijke pakketnaam Hallo van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="714ca-122">Replace `<Your package name>` by hello actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

