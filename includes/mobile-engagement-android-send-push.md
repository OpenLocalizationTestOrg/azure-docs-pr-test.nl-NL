
### <a name="update-manifest-file-to-enable-notifications"></a><span data-ttu-id="a4810-101">Manifestbestand bijwerken om meldingen in te schakelen</span><span class="sxs-lookup"><span data-stu-id="a4810-101">Update manifest file to enable notifications</span></span>
<span data-ttu-id="a4810-102">Kopieer de onderstaande resources voor in-app-meldingen naar uw Manifest.xml tussen de labels `<application>` en `</application>`.</span><span class="sxs-lookup"><span data-stu-id="a4810-102">Copy the in-app messaging resources below into your Manifest.xml between the `<application>` and `</application>` tags.</span></span>

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

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="a4810-103">Een pictogram voor meldingen opgeven</span><span class="sxs-lookup"><span data-stu-id="a4810-103">Specify an icon for notifications</span></span>
<span data-ttu-id="a4810-104">Plak het volgende XML-fragment in het bestand Manifest.xml tussen de labels `<application>` en `</application>`.</span><span class="sxs-lookup"><span data-stu-id="a4810-104">Paste the following XML snippet in your Manifest.xml between the `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="a4810-105">Zo definieert u welk pictogram er bij systeemmeldingen en in in-app-meldingen wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a4810-105">This defines the icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="a4810-106">Het is optioneel voor in-app-meldingen maar verplicht voor systeemmeldingen.</span><span class="sxs-lookup"><span data-stu-id="a4810-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="a4810-107">In Android worden systeemmeldingen met ongeldige pictogrammen geweigerd.</span><span class="sxs-lookup"><span data-stu-id="a4810-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="a4810-108">Controleer of u een pictogram gebruikt dat in een van de **drawable**-mappen (zoals ``engagement_close.png``) voorkomt.</span><span class="sxs-lookup"><span data-stu-id="a4810-108">Make sure you are using an icon that exists in one of the **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="a4810-109">**mipmap**-map wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a4810-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="a4810-110">Gebruik niet het pictogram van het **startprogramma voor toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a4810-110">You should not use the **launcher** icon.</span></span> <span data-ttu-id="a4810-111">Dit heeft een andere resolutie en bevindt zich doorgaans in de mipmap-mappen, die niet worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a4810-111">It has a different resolution and is usually in the mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="a4810-112">Voor echte apps kunt u een pictogram gebruiken dat geschikt is voor meldingen volgens de [Android-ontwerprichtlijnen](http://developer.android.com/design/patterns/notifications.html).</span><span class="sxs-lookup"><span data-stu-id="a4810-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="a4810-113">Om er zeker van te zijn dat de juiste resoluties voor pictogrammen worden gebruikt, kunt u [deze voorbeelden](https://www.google.com/design/icons) bekijken.</span><span class="sxs-lookup"><span data-stu-id="a4810-113">To be sure to use correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="a4810-114">Schuif omlaag naar de sectie **Melding**, klik op een pictogram en klik vervolgens op `PNGS` om de drawable-set voor het pictogram te downloaden.</span><span class="sxs-lookup"><span data-stu-id="a4810-114">Scroll down to the **Notification** section, click an icon, and then click `PNGS` to download the icon drawable set.</span></span> <span data-ttu-id="a4810-115">U kunt zien welke drawable-mappen met welke resolutie moeten worden gebruikt voor elke versie van het pictogram.</span><span class="sxs-lookup"><span data-stu-id="a4810-115">You can see what drawable folders with which resolution to use for each version of the icon.</span></span>
> 
> 

### <a name="enable-your-app-to-receive-gcm-push-notifications"></a><span data-ttu-id="a4810-116">Ontvangen van GCM-pushmeldingen inschakelen voor de app</span><span class="sxs-lookup"><span data-stu-id="a4810-116">Enable your app to receive GCM push notifications</span></span>
1. <span data-ttu-id="a4810-117">Plak het volgende in uw Manifest.xml tussen de labels `<application>` en `</application>` nadat u de **Afzender-id** hebt vervangen dat u hebt opgehaald uit de Firebase-projectconsole.</span><span class="sxs-lookup"><span data-stu-id="a4810-117">Paste the following into your Manifest.xml between the `<application>` and `</application>` tags after replacing the **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="a4810-118">De \n is opzettelijk dus zorg ervoor dat het projectnummer hiermee eindigt.</span><span class="sxs-lookup"><span data-stu-id="a4810-118">The \n is intentional so make sure that you end the project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="a4810-119">Plak de onderstaande code in het bestand Manifest.xml tussen de labels `<application>` en `</application>`.</span><span class="sxs-lookup"><span data-stu-id="a4810-119">Paste the code below into your Manifest.xml between the `<application>` and `</application>` tags.</span></span> <span data-ttu-id="a4810-120">Vervang de pakketnaam <Your package name>.</span><span class="sxs-lookup"><span data-stu-id="a4810-120">Replace the package name <Your package name>.</span></span>
   
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
3. <span data-ttu-id="a4810-121">Voeg de laatste reeks machtigingen die zijn gemarkeerd vóór het label `<application>` toe.</span><span class="sxs-lookup"><span data-stu-id="a4810-121">Add the last set of permissions that are highlighted before the `<application>` tag.</span></span> <span data-ttu-id="a4810-122">Vervang `<Your package name>` door de werkelijke pakketnaam van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4810-122">Replace `<Your package name>` by the actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

