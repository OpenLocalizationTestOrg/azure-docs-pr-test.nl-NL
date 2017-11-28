---
title: aaaAzure Mobile Engagement Android SDK-integratie
description: Meest recente updates en -procedures voor Android-SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="f18bc-103">Upgradeprocedures</span><span class="sxs-lookup"><span data-stu-id="f18bc-103">Upgrade procedures</span></span>
<span data-ttu-id="f18bc-104">Als u hebt al een oudere versie van onze SDK geïntegreerd in uw toepassing, hebt u tooconsider Hallo volgende punten bij het upgraden van Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="f18bc-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="f18bc-105">Mogelijk hebt u toofollow verschillende procedures als u verschillende versies van Hallo SDK gemist.</span><span class="sxs-lookup"><span data-stu-id="f18bc-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="f18bc-106">Bijvoorbeeld als u migreert vanaf 1.4.0 too1.6.0 hebt toofirst Volg Hallo ' van 1.4.0 too1.5.0 ' procedure vervolgens Hallo ' van 1.5.0 too1.6.0 ' procedure.</span><span class="sxs-lookup"><span data-stu-id="f18bc-106">For example if you migrate from 1.4.0 too1.6.0 you have toofirst follow hello "from 1.4.0 too1.5.0" procedure then hello "from 1.5.0 too1.6.0" procedure.</span></span>

<span data-ttu-id="f18bc-107">Welke Hallo-versie die u bijwerkt, hebt u tooreplace hello `mobile-engagement-VERSION.jar` Hello nieuwe.</span><span class="sxs-lookup"><span data-stu-id="f18bc-107">Whatever hello version you upgrade from, you have tooreplace hello `mobile-engagement-VERSION.jar` with hello new one.</span></span>

## <a name="from-420-too421"></a><span data-ttu-id="f18bc-108">Van 4.2.0 too4.2.1</span><span class="sxs-lookup"><span data-stu-id="f18bc-108">From 4.2.0 too4.2.1</span></span>
<span data-ttu-id="f18bc-109">Deze stap kunt daadwerkelijk worden uitgevoerd op elke versie van Hallo SDK en een beveiligingsverbetering is wanneer u integreert Reach-activiteiten.</span><span class="sxs-lookup"><span data-stu-id="f18bc-109">This step can actually be done on any version of hello SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="f18bc-110">U moet nu toevoegen `exported="false"` tooall Reach-activiteiten.</span><span class="sxs-lookup"><span data-stu-id="f18bc-110">You should now add `exported="false"` tooall Reach activities.</span></span>

<span data-ttu-id="f18bc-111">Reach activiteiten ziet er nu als volgt op uw `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="f18bc-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

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

## <a name="from-400-too410"></a><span data-ttu-id="f18bc-112">Van 4.0.0 too4.1.0</span><span class="sxs-lookup"><span data-stu-id="f18bc-112">From 4.0.0 too4.1.0</span></span>
<span data-ttu-id="f18bc-113">Hallo SDK nu ingang nieuwe machtiging model van Android M.</span><span class="sxs-lookup"><span data-stu-id="f18bc-113">hello SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="f18bc-114">Als u functies van de locatie of grote afbeelding meldingen Lees [in deze sectie](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="f18bc-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="f18bc-115">Bovendien toohello nieuwe machtiging model, er wordt nu ondersteuning voor het configureren van locatie-onderdelen tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="f18bc-115">In addition toohello new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="f18bc-116">We zijn nog steeds compatibel zijn met de Hallo manifest parameters voor de locatie, maar gedeprecieerd.</span><span class="sxs-lookup"><span data-stu-id="f18bc-116">We are still compatible with hello manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="f18bc-117">toouse-runtime-configuratie verwijderen Hallo volgende secties van uw ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="f18bc-117">toouse runtime configuration, remove hello following sections from your ``AndroidManifest.xml``:</span></span>

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

<span data-ttu-id="f18bc-118">en gelezen [procedure wordt dit bijgewerkt](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse runtime-configuratie in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="f18bc-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse runtime configuration instead.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="f18bc-119">Van 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="f18bc-119">From 3.0.0 too4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="f18bc-120">Native pushberichten</span><span class="sxs-lookup"><span data-stu-id="f18bc-120">Native push</span></span>
<span data-ttu-id="f18bc-121">Native pushberichten (GCM/ADM) is nu ook gebruikt voor in de app-meldingen zodat u Hallo native pushreferenties voor elk type pushcampagne moet configureren.</span><span class="sxs-lookup"><span data-stu-id="f18bc-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="f18bc-122">Als dat niet al Volg [deze procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span><span class="sxs-lookup"><span data-stu-id="f18bc-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="f18bc-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="f18bc-123">AndroidManifest.xml</span></span>
<span data-ttu-id="f18bc-124">Reach-integratie is gewijzigd in ``AndroidManifest.xml``.</span><span class="sxs-lookup"><span data-stu-id="f18bc-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="f18bc-125">Vervang deze waarde:</span><span class="sxs-lookup"><span data-stu-id="f18bc-125">Replace this:</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

<span data-ttu-id="f18bc-126">Door</span><span class="sxs-lookup"><span data-stu-id="f18bc-126">By</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
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

<span data-ttu-id="f18bc-127">Er is mogelijk een scherm laden nu wanneer u klikt u op een aankondiging (met tekst of web content) of een poll.</span><span class="sxs-lookup"><span data-stu-id="f18bc-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="f18bc-128">U hebt tooadd dit voor deze toowork campagnes in 4.0.0:</span><span class="sxs-lookup"><span data-stu-id="f18bc-128">You have tooadd this for those campaigns toowork in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="f18bc-129">Resources</span><span class="sxs-lookup"><span data-stu-id="f18bc-129">Resources</span></span>
<span data-ttu-id="f18bc-130">Hallo nieuwe insluiten `res/layout/engagement_loading.xml` -bestand in uw project.</span><span class="sxs-lookup"><span data-stu-id="f18bc-130">Embed hello new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-too300"></a><span data-ttu-id="f18bc-131">Van 2.4.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="f18bc-131">From 2.4.0 too3.0.0</span></span>
<span data-ttu-id="f18bc-132">Hallo hieronder wordt beschreven hoe toomigrate een SDK-integratie van Hallo Capptain service aangeboden door Capptain SAS in een app die is aangedreven door Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="f18bc-132">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="f18bc-133">Als u vanaf een eerdere versie migreert, Raadpleeg Hallo Capptain website toomigrate too2.4.0 eerst en vervolgens toepassen Hallo procedure te volgen.</span><span class="sxs-lookup"><span data-stu-id="f18bc-133">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too2.4.0 first and then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f18bc-134">Capptain Mobile Engagement zijn niet Hallo dezelfde services en Hallo onderstaande procedure alleen highlights hoe toomigrate Hallo client-app.</span><span class="sxs-lookup"><span data-stu-id="f18bc-134">Capptain and Mobile Engagement are not hello same services, and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="f18bc-135">Migreren Hallo SDK in Hallo-app wordt niet uw gegevens migreren vanaf Hallo Capptain servers toohello Mobile Engagement-servers.</span><span class="sxs-lookup"><span data-stu-id="f18bc-135">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="f18bc-136">JAR-bestand</span><span class="sxs-lookup"><span data-stu-id="f18bc-136">JAR file</span></span>
<span data-ttu-id="f18bc-137">Vervang `capptain.jar` door `mobile-engagement-VERSION.jar` in uw `libs` map.</span><span class="sxs-lookup"><span data-stu-id="f18bc-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="f18bc-138">Bronbestanden</span><span class="sxs-lookup"><span data-stu-id="f18bc-138">Resource files</span></span>
<span data-ttu-id="f18bc-139">Elke resource-bestand dat wordt geleverd (voorafgegaan door `capptain_`), is toobe vervangen door nieuwe hello (voorafgegaan door `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="f18bc-139">Every resource file that we provided (prefixed by `capptain_`) has toobe replaced by hello new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="f18bc-140">Als u deze bestanden hebt aangepast, hebt u toore-aanpassing toepassen op nieuwe bestanden hello, **alle Hallo-id's in de bronbestanden Hallo ook zijn gewijzigd**.</span><span class="sxs-lookup"><span data-stu-id="f18bc-140">If you customized those files, you have toore-apply your customization on hello new files, **all hello identifiers in hello resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="f18bc-141">Toepassings-id</span><span class="sxs-lookup"><span data-stu-id="f18bc-141">Application ID</span></span>
<span data-ttu-id="f18bc-142">Nu Engagement maakt gebruik van een verbinding tekenreeks tooconfigure Hallo SDK-id's zoals Hallo toepassings-id.</span><span class="sxs-lookup"><span data-stu-id="f18bc-142">Now Engagement uses a connection string tooconfigure hello SDK identifiers such as hello application identifier.</span></span>

<span data-ttu-id="f18bc-143">U hebt toouse `EngagementAgent.init` methode in uw activiteiten starten als volgt:</span><span class="sxs-lookup"><span data-stu-id="f18bc-143">You have toouse `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="f18bc-144">Hallo-verbindingsreeks voor uw toepassing wordt weergegeven op de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f18bc-144">hello connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="f18bc-145">Verwijder geen enkele aanroep te`CapptainAgent.configure` als `EngagementAgent.init` vervangt deze methode.</span><span class="sxs-lookup"><span data-stu-id="f18bc-145">Please remove any call too`CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="f18bc-146">Hallo `appId` kunnen niet meer worden geconfigureerd met `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="f18bc-146">hello `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="f18bc-147">Verwijder dit gedeelte van uw `AndroidManifest.xml` als u deze hebt:</span><span class="sxs-lookup"><span data-stu-id="f18bc-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="f18bc-148">Java-API</span><span class="sxs-lookup"><span data-stu-id="f18bc-148">Java API</span></span>
<span data-ttu-id="f18bc-149">Elke aanroep tooany Java-klasse van onze SDK heeft toobe gewijzigd; bijvoorbeeld: `CapptainAgent.getInstance(this)` naam moet worden gewijzigd `EngagementAgent.getInstance(this)`, `extends CapptainActivity` naam moet worden gewijzigd `extends EngagementActivity` enzovoort...</span><span class="sxs-lookup"><span data-stu-id="f18bc-149">Every call tooany Java class of our SDK has toobe renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="f18bc-150">Als u met standaard agent voorkeursextensie bestanden zijn geïntegreerd, Hallo standaardbestandsnaam is nu `engagement.agent` en Hallo sleutel `engagement:agent`.</span><span class="sxs-lookup"><span data-stu-id="f18bc-150">If you were integrated with default agent preference files, hello default file name is now `engagement.agent` and hello key is `engagement:agent`.</span></span>

<span data-ttu-id="f18bc-151">Bij het maken van web-aankondigingen Hallo Javascript binder is nu `engagementReachContent`.</span><span class="sxs-lookup"><span data-stu-id="f18bc-151">When creating web announcements, hello Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="f18bc-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="f18bc-152">AndroidManifest.xml</span></span>
<span data-ttu-id="f18bc-153">Een groot aantal wijzigingen hebben plaatsgevonden er, Hallo-service is niet meer gedeeld en veel ontvangers kunnen niet worden geëxporteerd meer.</span><span class="sxs-lookup"><span data-stu-id="f18bc-153">A lot of changes happened there, hello service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="f18bc-154">Hallo servicedeclaratie is nu eenvoudiger; Hallo opzet filter en alle metagegevens erin te verwijderen en toevoegen `exportable=false`.</span><span class="sxs-lookup"><span data-stu-id="f18bc-154">hello service declaration is now simpler; remove hello intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="f18bc-155">Bovendien alles hernoemde toouse engagement is.</span><span class="sxs-lookup"><span data-stu-id="f18bc-155">Plus everything is renamed toouse engagement.</span></span>

<span data-ttu-id="f18bc-156">Nu ziet er als:</span><span class="sxs-lookup"><span data-stu-id="f18bc-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="f18bc-157">Als u wilt dat tooenable test logboeken Hallo meta-gegevens nu zijn toohello toepassing tag verplaatst en de naam is gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="f18bc-157">When you want tooenable test logs, hello meta-data has now been moved toohello application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="f18bc-158">Alle andere metagegevens NET zijn gewijzigd, wordt hier Hallo volledige lijst (natuurlijk rename alleen hello die u gebruikt):</span><span class="sxs-lookup"><span data-stu-id="f18bc-158">All other meta-data have just been renamed, here is hello full list (of course rename only hello ones you use):</span></span>

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

<span data-ttu-id="f18bc-159">Google Play en SmartAd bijhouden is verwijderd van de SDK u net hebt tooremove dit zonder vervanging:</span><span class="sxs-lookup"><span data-stu-id="f18bc-159">Google Play and SmartAd tracking has been removed from SDK you just have tooremove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="f18bc-160">Hallo Reach-activiteiten, worden nu als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="f18bc-160">hello Reach activities are now declared like this:</span></span>

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

<span data-ttu-id="f18bc-161">Als u aangepaste Reach-activiteiten hebt, moet u enige toochange Hallo opzet acties toomatch ofwel `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` of `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span><span class="sxs-lookup"><span data-stu-id="f18bc-161">If you have custom Reach activities, you need only toochange hello intent actions toomatch either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="f18bc-162">Hallo broadcast ontvangers zijn gewijzigd, plus we nu toevoegen `exported=false`.</span><span class="sxs-lookup"><span data-stu-id="f18bc-162">hello broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="f18bc-163">Hier volgt Hallo volledige lijst met ontvangers Hallo met Hallo nieuwe specificatie (natuurlijk rename alleen hello die u gebruikt):</span><span class="sxs-lookup"><span data-stu-id="f18bc-163">Here is hello full list of hello receivers with hello new specification, (of course rename only hello ones you use):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

<span data-ttu-id="f18bc-164">Het bijhouden van de ontvanger is verwijderd, zodat u deze sectie tooremove hebt:</span><span class="sxs-lookup"><span data-stu-id="f18bc-164">Tracking receiver has been removed, so you have tooremove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="f18bc-165">Opmerking dat Hallo declaratie van uw implementatie van Hallo ontvanger broadcast **EngagementMessageReceiver** is gewijzigd in Hallo `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="f18bc-165">Note that hello declaration of your implementation of hello broadcast receiver **EngagementMessageReceiver** has changed in hello `AndroidManifest.xml`.</span></span> <span data-ttu-id="f18bc-166">Dit is omdat Hallo API toosend en verwijderen van willekeurige XMPP van willekeurige XMPP entiteiten berichten en Hallo API toosend en ontvangen van berichten tussen apparaten die zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f18bc-166">This is because hello API toosend and remove arbitrary XMPP messages from arbitrary XMPP entities and hello API toosend and receive messages between devices have been removed.</span></span> <span data-ttu-id="f18bc-167">Zo hebt u ook toodelete Hallo na retouraanroepen uit uw **EngagementMessageReceiver** implementatie:</span><span class="sxs-lookup"><span data-stu-id="f18bc-167">Thus, you have also toodelete hello following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="f18bc-168">en</span><span class="sxs-lookup"><span data-stu-id="f18bc-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="f18bc-169">Verwijder op geen enkele aanroep **EngagementAgent** voor:</span><span class="sxs-lookup"><span data-stu-id="f18bc-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="f18bc-170">en</span><span class="sxs-lookup"><span data-stu-id="f18bc-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="f18bc-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="f18bc-171">Proguard</span></span>
<span data-ttu-id="f18bc-172">Proguard configuratie kan worden beïnvloed door rebranding, Hallo regels zijn nu ziet eruit als:</span><span class="sxs-lookup"><span data-stu-id="f18bc-172">Proguard configuration can be impacted by rebranding, hello rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

