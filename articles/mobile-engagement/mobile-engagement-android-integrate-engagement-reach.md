---
title: aaaAzure Mobile Engagement Android SDK-integratie
description: Meest recente updates en -procedures voor Android-SDK voor Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a><span data-ttu-id="6f723-103">Hoe tooIntegrate Engagement bereiken op Android</span><span class="sxs-lookup"><span data-stu-id="6f723-103">How tooIntegrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6f723-104">U moet volgen Hallo integratie procedure wordt beschreven in Hallo hoe tooIntegrate Engagement op Android-document voordat u deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="6f723-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="6f723-105">Standaard-integratie</span><span class="sxs-lookup"><span data-stu-id="6f723-105">Standard integration</span></span>

<span data-ttu-id="6f723-106">Kopieer de Reach-bronbestanden van Hallo SDK in uw project:</span><span class="sxs-lookup"><span data-stu-id="6f723-106">Copy Reach resource files from hello SDK in your project :</span></span>

* <span data-ttu-id="6f723-107">Hallo-bestanden kopiëren van Hallo `res/layout` map geleverd met Hallo SDK in Hallo `res/layout` map van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="6f723-107">Copy hello files from hello `res/layout` folder delivered with hello SDK into hello `res/layout` folder of your application.</span></span>
* <span data-ttu-id="6f723-108">Hallo-bestanden kopiëren van Hallo `res/drawable` map geleverd met Hallo SDK in Hallo `res/drawable` map van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="6f723-108">Copy hello files from hello `res/drawable` folder delivered with hello SDK into hello `res/drawable` folder of your application.</span></span>

<span data-ttu-id="6f723-109">Bewerk uw `AndroidManifest.xml` bestand:</span><span class="sxs-lookup"><span data-stu-id="6f723-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="6f723-110">Toevoegen van de volgende sectie hello (tussen Hallo `<application>` en `</application>` labels):</span><span class="sxs-lookup"><span data-stu-id="6f723-110">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
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
* <span data-ttu-id="6f723-111">U moet deze machtiging tooreplay systeemmeldingen die niet is geklikt tijdens het opstarten (anders ze op schijf worden behouden, maar niet meer weergegeven, moet u echt tooinclude dit).</span><span class="sxs-lookup"><span data-stu-id="6f723-111">You need this permission tooreplay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have tooinclude this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="6f723-112">Geef een pictogram dat wordt gebruikt voor meldingen (zowel in-app en het systeem die zijn) door te kopiëren en bewerken Hallo sectie volgen (tussen Hallo `<application>` en `</application>` labels):</span><span class="sxs-lookup"><span data-stu-id="6f723-112">Specify an icon used for notifications (both in app and system ones) by copying and editing hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="6f723-113">Deze sectie is **verplichte** als u van plan systeemmeldingen gebruiken bent bij het maken van Reach-campagnes.</span><span class="sxs-lookup"><span data-stu-id="6f723-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="6f723-114">Android wordt voorkomen dat systeemmeldingen zonder pictogrammen wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6f723-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="6f723-115">Dus als u deze sectie weglaat, uw eindgebruikers tooreceive kunnen niet worden ze.</span><span class="sxs-lookup"><span data-stu-id="6f723-115">So if you omit this section, your end users will not be able tooreceive them.</span></span>
> 
> 

* <span data-ttu-id="6f723-116">Als u campagnes met systeemmeldingen met behulp van de grote afbeelding maakt, moet u tooadd Hallo volgende machtigingen (na Hallo `</application>` tag) indien deze ontbreken:</span><span class="sxs-lookup"><span data-stu-id="6f723-116">If you create campaigns with system notifications using big picture, you need tooadd hello following permissions (after hello `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="6f723-117">Op Android M en als uw toepassing gericht op Android-API-niveau 23 of hoger, ``WRITE_EXTERNAL_STORAGE`` machtiging vereist goedkeuring van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6f723-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="6f723-118">Lees [in deze sectie](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="6f723-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="6f723-119">Bereiken voor systeemmeldingen die u ook in Hallo opgeven kunt campagne als Hallo apparaat moet ring en/of trillen.</span><span class="sxs-lookup"><span data-stu-id="6f723-119">For system notifications you can also specify in hello Reach campaign if hello device should ring and/or vibrate.</span></span> <span data-ttu-id="6f723-120">Voor deze toowork, hebt u zeker dat u na machtiging Hallo gedeclareerd toomake (na Hallo `</application>` tag):</span><span class="sxs-lookup"><span data-stu-id="6f723-120">For it toowork, you have toomake sure you declared hello following permission (after hello `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="6f723-121">Zonder deze machtiging Android voorkomt u dat systeemmeldingen worden weergegeven als u dit selectievakje inschakelt Hallo ring of Hallo Trillen optie in Hallo bereiken campagnebeheer.</span><span class="sxs-lookup"><span data-stu-id="6f723-121">Without this permission, Android prevents system notifications from being shown if you checked hello ring or hello vibrate option in hello Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="6f723-122">Native Pushberichten</span><span class="sxs-lookup"><span data-stu-id="6f723-122">Native Push</span></span>
<span data-ttu-id="6f723-123">Nu u de Reach-module hebt geconfigureerd, moet u tooconfigure native pushberichten toobe kunnen tooreceive Hallo campagnes op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6f723-123">Now that you configured Reach module, you need tooconfigure native push toobe able tooreceive hello campaigns on hello device.</span></span>

<span data-ttu-id="6f723-124">We ondersteunen twee services op Android:</span><span class="sxs-lookup"><span data-stu-id="6f723-124">We support two services on Android:</span></span>

* <span data-ttu-id="6f723-125">Google Play-apparaten: Gebruik [Google Cloud Messaging] door de volgende Hallo [hoe tooIntegrate GCM met Engagement begeleiden](mobile-engagement-android-gcm-integrate.md) handleiding.</span><span class="sxs-lookup"><span data-stu-id="6f723-125">Google Play devices: Use [Google Cloud Messaging] by following hello [How tooIntegrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="6f723-126">Amazon-apparaten: Gebruik [Amazon Device Messaging] door de volgende Hallo [hoe tooIntegrate ADM met Engagement begeleiden](mobile-engagement-android-adm-integrate.md) handleiding.</span><span class="sxs-lookup"><span data-stu-id="6f723-126">Amazon devices: Use [Amazon Device Messaging] by following hello [How tooIntegrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="6f723-127">Als u wilt dat tootarget Amazon- en Google Play-apparaten, de mogelijke toohave alles binnen 1 AndroidManifest.xml/APK voor ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="6f723-127">If you want tootarget both Amazon and Google Play devices, its possible toohave everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="6f723-128">Maar bij het indienen van tooAmazon, kunnen ze uw toepassing afwijzen als ze GCM code vinden.</span><span class="sxs-lookup"><span data-stu-id="6f723-128">But when submitting tooAmazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="6f723-129">In dat geval moet u meerdere APKs gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6f723-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="6f723-130">**Uw toepassing is nu gereed tooreceive en weergeven reach-campagnes!**</span><span class="sxs-lookup"><span data-stu-id="6f723-130">**Your application is now ready tooreceive and display reach campaigns!**</span></span>

## <a name="how-toohandle-data-push"></a><span data-ttu-id="6f723-131">Hoe gegevens toohandle push</span><span class="sxs-lookup"><span data-stu-id="6f723-131">How toohandle data push</span></span>
### <a name="integration"></a><span data-ttu-id="6f723-132">Integratie</span><span class="sxs-lookup"><span data-stu-id="6f723-132">Integration</span></span>
<span data-ttu-id="6f723-133">Als u wilt dat uw toepassing toobe kunnen tooreceive Reach-gegevens-pushes, krijgt u toocreate een subklasse zijn van `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` en ernaar wordt verwezen in Hallo `AndroidManifest.xml` bestand (tussen Hallo `<application>` en/of `</application>` labels):</span><span class="sxs-lookup"><span data-stu-id="6f723-133">If you want your application toobe able tooreceive Reach data pushes, you have toocreate a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in hello `AndroidManifest.xml` file (between hello `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="6f723-134">Vervolgens kunt u Hallo overschrijven `onDataPushStringReceived` en `onDataPushBase64Received` retouraanroepen.</span><span class="sxs-lookup"><span data-stu-id="6f723-134">Then you can override hello `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="6f723-135">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6f723-135">Here is an example:</span></span>

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a><span data-ttu-id="6f723-136">Category</span><span class="sxs-lookup"><span data-stu-id="6f723-136">Category</span></span>
<span data-ttu-id="6f723-137">Hallo categorieparameter is optioneel bij het maken van een campagne Push-gegevens en kunt dat u gegevens toofilter pushes.</span><span class="sxs-lookup"><span data-stu-id="6f723-137">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="6f723-138">Dit is handig als u verschillende broadcast ontvangers afhandeling van verschillende soorten gegevens-pushes hebt of als u wilt dat de verschillende typen toopush van `Base64` gegevens en wilt tooidentify hun type voordat ze worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="6f723-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="6f723-139">De retouraanroepen retourparameter</span><span class="sxs-lookup"><span data-stu-id="6f723-139">Callbacks' return parameter</span></span>
<span data-ttu-id="6f723-140">Hier volgen enkele richtlijnen tooproperly ingang Hallo retourparameter van `onDataPushStringReceived` en `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="6f723-140">Here are some guidelines tooproperly handle hello return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="6f723-141">Een ontvanger broadcast moet retourneren `null` in Hallo retouraanroep als het niet weet hoe een data toohandle push.</span><span class="sxs-lookup"><span data-stu-id="6f723-141">A broadcast receiver should return `null` in hello callback if it does not know how toohandle a data push.</span></span> <span data-ttu-id="6f723-142">U moet Hallo categorie toodetermine gebruiken of uw broadcast ontvanger Hallo gegevens-push of niet verwerken moet.</span><span class="sxs-lookup"><span data-stu-id="6f723-142">You should use hello category toodetermine whether your broadcast receiver should handle hello data push or not.</span></span>
* <span data-ttu-id="6f723-143">Een van de Hallo broadcast ontvanger moet retourneren `true` in Hallo retouraanroep als het gegevens-push Hallo accepteert.</span><span class="sxs-lookup"><span data-stu-id="6f723-143">One of hello broadcast receiver should return `true` in hello callback if it accepts hello data push.</span></span>
* <span data-ttu-id="6f723-144">Een van de Hallo broadcast ontvanger moet retourneren `false` in Hallo retouraanroep als Hallo gegevens-push herkent, maar deze om welke reden dan ook negeert.</span><span class="sxs-lookup"><span data-stu-id="6f723-144">One of hello broadcast receiver should return `false` in hello callback if it recognizes hello data push, but discards it for whatever reason.</span></span> <span data-ttu-id="6f723-145">Bijvoorbeeld retourneren `false` wanneer Hallo ontvangen gegevens zijn ongeldig.</span><span class="sxs-lookup"><span data-stu-id="6f723-145">For example, return `false` when hello received data is invalid.</span></span>
* <span data-ttu-id="6f723-146">Als een ontvanger retourneert broadcast `true` terwijl een andere een retourneert `false` voor hello dezelfde gegevens-push, Hallo gedrag niet gedefinieerd is, moet u nooit doen die.</span><span class="sxs-lookup"><span data-stu-id="6f723-146">If one broadcast receiver returns `true` while another one returns `false` for hello same data push, hello behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="6f723-147">Hallo-retourtype wordt alleen gebruikt voor Hallo Reach statistieken:</span><span class="sxs-lookup"><span data-stu-id="6f723-147">hello return type is used only for hello Reach statistics:</span></span>

* <span data-ttu-id="6f723-148">`Replied`Als een van de Hallo broadcast ontvangers ofwel geretourneerd wordt verhoogd `true` of `false`.</span><span class="sxs-lookup"><span data-stu-id="6f723-148">`Replied` is incremented if one of hello broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="6f723-149">`Actioned`alleen als een van de Hallo ontvangers geretourneerd wordt verhoogd `true`.</span><span class="sxs-lookup"><span data-stu-id="6f723-149">`Actioned` is incremented only if one of hello broadcast receivers returned `true`.</span></span>

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="6f723-150">Hoe toocustomize campagnes</span><span class="sxs-lookup"><span data-stu-id="6f723-150">How toocustomize campaigns</span></span>
<span data-ttu-id="6f723-151">toocustomize campagnes, kunt u Hallo-indelingen die beschikbaar zijn in Hallo SDK bereiken wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6f723-151">toocustomize campaigns, you can modify hello layouts provided in hello Reach SDK.</span></span>

<span data-ttu-id="6f723-152">U moet alle Hallo id's die worden gebruikt in Hallo indelingen houden en Hallo typen Hallo weergaven die gebruikmaken van een id in, met name voor tekst en afbeeldingen weergaven houden.</span><span class="sxs-lookup"><span data-stu-id="6f723-152">You should keep all hello identifiers used in hello layouts and keep hello types of hello views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="6f723-153">Sommige weergaven zijn alleen gebruikte toohide of gebieden weergeven, zodat hun type kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="6f723-153">Some views are just used toohide or show areas so their type may be changed.</span></span> <span data-ttu-id="6f723-154">Controleer de broncode Hallo als u toochange Hallo-type van een weergave in de indelingen Hallo opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6f723-154">Please check hello source code if you intend toochange hello type of a view in hello provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="6f723-155">Meldingen</span><span class="sxs-lookup"><span data-stu-id="6f723-155">Notifications</span></span>
<span data-ttu-id="6f723-156">Er zijn twee typen meldingen: systeem en in-app-meldingen die andere indelingsbestanden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6f723-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="6f723-157">Systeemmeldingen</span><span class="sxs-lookup"><span data-stu-id="6f723-157">System notifications</span></span>
<span data-ttu-id="6f723-158">toocustomize systeemmeldingen moet u toouse hello **categorieën**.</span><span class="sxs-lookup"><span data-stu-id="6f723-158">toocustomize system notifications you need toouse hello **categories**.</span></span> <span data-ttu-id="6f723-159">U kunt te gaan[categorieën](#categories).</span><span class="sxs-lookup"><span data-stu-id="6f723-159">You can jump too[Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="6f723-160">In-app-meldingen</span><span class="sxs-lookup"><span data-stu-id="6f723-160">In-app notifications</span></span>
<span data-ttu-id="6f723-161">Een in-app-melding is standaard een weergave die dynamisch worden toegevoegd toohello huidige activiteit gebruiker Bedankt toohello Android interfacemethode `addContentView()`.</span><span class="sxs-lookup"><span data-stu-id="6f723-161">By default, an in-app notification is a view that is dynamically added toohello current activity user interface thanks toohello Android method `addContentView()`.</span></span> <span data-ttu-id="6f723-162">Dit is een melding overlay genoemd.</span><span class="sxs-lookup"><span data-stu-id="6f723-162">This is called a notification overlay.</span></span> <span data-ttu-id="6f723-163">Melding overlays zijn ideaal voor een snelle integratie omdat ze geen toomodify u elke lay-out in uw toepassing vereisen.</span><span class="sxs-lookup"><span data-stu-id="6f723-163">Notification overlays are great for a fast integration because they do not require you toomodify any layout in your application.</span></span>

<span data-ttu-id="6f723-164">toomodify hello uiterlijk van uw notification overlays, kunt u eenvoudig hello bestand wijzigen `engagement_notification_area.xml` tooyour nodig heeft.</span><span class="sxs-lookup"><span data-stu-id="6f723-164">toomodify hello look of your notification overlays, you can simply modify hello file `engagement_notification_area.xml` tooyour needs.</span></span>

> [!NOTE]
> <span data-ttu-id="6f723-165">Hallo bestand `engagement_notification_overlay.xml` is een gebruikte toocreate een overlay melding Hallo waaronder Hallo bestand `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="6f723-165">hello file `engagement_notification_overlay.xml` is hello one that is used toocreate a notification overlay, it includes hello file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="6f723-166">U kunt het ook aanpassen toosuit uw behoeften (bijvoorbeeld voor het systeemvak Hallo binnen Hallo overlay plaatsing).</span><span class="sxs-lookup"><span data-stu-id="6f723-166">You can also customize it toosuit your needs (such as for positioning hello notification area within hello overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="6f723-167">Indeling van de melding als onderdeel van de indeling van een activiteit bevatten</span><span class="sxs-lookup"><span data-stu-id="6f723-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="6f723-168">Overlays zijn ideaal voor een snelle integratie, maar worden onhandig of neveneffecten hebben in bijzondere gevallen.</span><span class="sxs-lookup"><span data-stu-id="6f723-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="6f723-169">Hallo-overlay-systeem kan op een activiteitenniveau van de, zodat u eenvoudig tooprevent bijwerkingen voor speciale activiteiten worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="6f723-169">hello overlay system can be customized at an activity level, making it easy tooprevent side effects for special activities.</span></span>

<span data-ttu-id="6f723-170">U kunt ervoor kiezen tooinclude onze lay-out voor de melding in uw bestaande lay-out met vriendelijke groet toohello Android **omvatten** instructie.</span><span class="sxs-lookup"><span data-stu-id="6f723-170">You can decide tooinclude our notification layout in your existing layout thanks toohello Android **include** statement.</span></span> <span data-ttu-id="6f723-171">Hallo Hieronder volgt een voorbeeld van een gewijzigd `ListActivity` lay-out die net bevat een `ListView`.</span><span class="sxs-lookup"><span data-stu-id="6f723-171">hello following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="6f723-172">**Voordat de Engagement-integratie:**</span><span class="sxs-lookup"><span data-stu-id="6f723-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="6f723-173">**Na de Engagement-integratie:**</span><span class="sxs-lookup"><span data-stu-id="6f723-173">**After Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

<span data-ttu-id="6f723-174">In dit voorbeeld hebben we een bovenliggende container toegevoegd, omdat de oorspronkelijke indeling Hallo een lijstweergave als bovenste niveau element Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6f723-174">In this example we added a parent container since hello original layout used a list view as hello top level element.</span></span> <span data-ttu-id="6f723-175">We hebben ook toegevoegd `android:layout_weight="1"` toobe kunnen tooadd hieronder een lijstweergave in een weergave die zijn geconfigureerd met `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="6f723-175">We also added `android:layout_weight="1"` toobe able tooadd a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="6f723-176">Hallo Engagement bereiken SDK detecteert automatisch die Hallo notification-indeling is opgenomen in deze activiteit en een overlay voor deze activiteit wordt niet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6f723-176">hello Engagement Reach SDK automatically detects that hello notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="6f723-177">Als u een ListActivity in uw toepassing gebruikt, een zichtbaar Reach-overlay wordt voorkomen dat u kruisreagerende tooclicked items in de lijstweergave Hallo meer.</span><span class="sxs-lookup"><span data-stu-id="6f723-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting tooclicked items in hello list view anymore.</span></span> <span data-ttu-id="6f723-178">Dit is een bekend probleem.</span><span class="sxs-lookup"><span data-stu-id="6f723-178">This is a known issue.</span></span> <span data-ttu-id="6f723-179">toowork om dit probleem we raden u tooembed Hallo melding indeling in de indeling van uw eigen lijst activiteit zoals in het vorige voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f723-179">toowork around this problem we suggest you tooembed hello notification layout in your own list activity layout like in hello previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="6f723-180">Het uitschakelen van de melding per activiteit</span><span class="sxs-lookup"><span data-stu-id="6f723-180">Disabling application notification per activity</span></span>
<span data-ttu-id="6f723-181">Als u niet Hallo wilt overlay toobe tooyour activiteit toegevoegd en als u geen Hallo melding lay-out in uw eigen lay-out, kunt u uitschakelen Hallo overlay voor deze activiteit in Hallo `AndroidManifest.xml` door toe te voegen een `meta-data` sectie, zoals in de volgende Hallo Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6f723-181">If you don't want hello overlay toobe added tooyour activity, and if you don't include hello notification layout in your own layout, you can disable hello overlay for this activity in hello `AndroidManifest.xml` by adding a `meta-data` section like in hello following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="6f723-182"><a name="categories"></a>Categorieën</span><span class="sxs-lookup"><span data-stu-id="6f723-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="6f723-183">Als u Hallo opgegeven indelingen wijzigt, wijzigt u Hallo uiterlijk van al uw meldingen.</span><span class="sxs-lookup"><span data-stu-id="6f723-183">When you modify hello provided layouts, you modify hello look of all your notifications.</span></span> <span data-ttu-id="6f723-184">Categorieën kunnen toodefine u die verschillende gericht lijkt (mogelijk gedrag) voor meldingen.</span><span class="sxs-lookup"><span data-stu-id="6f723-184">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="6f723-185">Een categorie kan worden opgegeven wanneer u een Reach-campagne maken.</span><span class="sxs-lookup"><span data-stu-id="6f723-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="6f723-186">Houd er rekening mee dat categorieën ook kunnen u aanpassen aankondigingen en polls, die verderop in dit document wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="6f723-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="6f723-187">tooregister een categorie-handler voor uw meldingen, moet u een aanroep van tooadd wanneer de toepassing hello wordt geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="6f723-187">tooregister a category handler for your notifications, you need tooadd a call when hello application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f723-188">Lees de waarschuwing over Hallo android: proces kenmerk Hallo \<android-sdk-engagement-process\> in Hallo hoe tooIntegrate Engagement op Android onderwerp voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="6f723-188">Please read hello warning about hello android:process attribute \<android-sdk-engagement-process\> in hello How tooIntegrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="6f723-189">Hallo volgende voorbeeld wordt ervan uitgegaan dat u Hallo vorige waarschuwing bevestigd en gebruikt een subklasse zijn van `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="6f723-189">hello following example assumes you acknowledged hello previous warning and use a sub-class of `EngagementApplication`:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

<span data-ttu-id="6f723-190">Hallo `MyNotifier` object is Hallo-implementatie van Hallo melding categorie-handler.</span><span class="sxs-lookup"><span data-stu-id="6f723-190">hello `MyNotifier` object is hello implementation of hello notification category handler.</span></span> <span data-ttu-id="6f723-191">Het is ofwel een implementatie van Hallo `EngagementNotifier` -interface of een subklasse van Hallo standaardimplementatie: `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="6f723-191">It is either an implementation of hello `EngagementNotifier` interface or a sub class of hello default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="6f723-192">Let op Hallo van dezelfde melder verscheidene categorieën kan verwerken, kunt u deze registreren als volgt:</span><span class="sxs-lookup"><span data-stu-id="6f723-192">Note that hello same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="6f723-193">tooreplace hello categorie standaardimplementatie, kunt u uw implementatie zoals registreren in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="6f723-193">tooreplace hello default category implementation, you can register your implementation like in hello following example:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

<span data-ttu-id="6f723-194">Hallo huidige categorie gebruikt in een handler is doorgegeven als een parameter in de meeste methoden kunt u overschrijven `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="6f723-194">hello current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="6f723-195">Deze is doorgegeven als een `String` parameter of indirect in een `EngagementReachContent` object waarvoor een `getCategory()` methode.</span><span class="sxs-lookup"><span data-stu-id="6f723-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="6f723-196">U kunt de meeste Hallo-proces voor het maken van notification wijzigen door gaat herdefiniëren methoden op `EngagementDefaultNotifier`, voor meer geavanceerde aanpassingen van mening bent dat gratis tootake bekijken op Hallo technische documentatie en op Hallo broncode.</span><span class="sxs-lookup"><span data-stu-id="6f723-196">You can change most of hello notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free tootake a look at hello technical documentation and at hello source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="6f723-197">In-app-meldingen</span><span class="sxs-lookup"><span data-stu-id="6f723-197">In-app notifications</span></span>
<span data-ttu-id="6f723-198">Als u alleen toouse alternatieve indelingen voor een specifieke categorie wilt, kunt u dit implementeren als Hallo voorbeeld te volgen in:</span><span class="sxs-lookup"><span data-stu-id="6f723-198">If you just want toouse alternate layouts for a specific category, you can implement this as in hello following example:</span></span>

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

<span data-ttu-id="6f723-199">**Voorbeeld van `my_notification_overlay.xml` :**</span><span class="sxs-lookup"><span data-stu-id="6f723-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="6f723-200">Zoals u ziet, is Hallo overlay weergave-id anders dan Hallo standaard één.</span><span class="sxs-lookup"><span data-stu-id="6f723-200">As you can see, hello overlay view identifier is different than hello standard one.</span></span> <span data-ttu-id="6f723-201">Het is belangrijk dat elke indeling een unieke id voor overlays gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6f723-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="6f723-202">**Voorbeeld van `my_notification_area.xml` :**</span><span class="sxs-lookup"><span data-stu-id="6f723-202">**Example of `my_notification_area.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

<span data-ttu-id="6f723-203">Zoals u ziet, is Hallo melding gebied weergave-id anders dan Hallo standaard één.</span><span class="sxs-lookup"><span data-stu-id="6f723-203">As you can see, hello notification area view identifier is different than hello standard one.</span></span> <span data-ttu-id="6f723-204">Het is belangrijk dat elke indeling wordt gebruikt voor een unieke id voor de melding gebieden.</span><span class="sxs-lookup"><span data-stu-id="6f723-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="6f723-205">Dit eenvoudige voorbeeld van de categorie kunt u een toepassing (of in-app) meldingen weergegeven Hallo boven aan het welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="6f723-205">This simple example of category makes application (or in-app) notifications displayed at hello top of hello screen.</span></span> <span data-ttu-id="6f723-206">Er is niet veranderd Hallo standaard-id's in systeemvak Hallo zelf.</span><span class="sxs-lookup"><span data-stu-id="6f723-206">We did not change hello standard identifiers used in hello notification area itself.</span></span>

<span data-ttu-id="6f723-207">Als u wilt dat er tooredefine hello toochange `EngagementDefaultNotifier.prepareInAppArea` methode.</span><span class="sxs-lookup"><span data-stu-id="6f723-207">If you want toochange that, you have tooredefine hello `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="6f723-208">Het raadzaam toolook op Hallo technische documentatie en op de broncode Hallo van `EngagementNotifier` en `EngagementDefaultNotifier` als u wilt dat dit niveau van Geavanceerd aanpassen.</span><span class="sxs-lookup"><span data-stu-id="6f723-208">It's recommended toolook at hello technical documentation and at hello source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="6f723-209">Systeemmeldingen</span><span class="sxs-lookup"><span data-stu-id="6f723-209">System notifications</span></span>
<span data-ttu-id="6f723-210">Door uit te breiden `EngagementDefaultNotifier`, kunt u overschrijven `onNotificationPrepared` tooalter Hallo melding die is voorbereid door Hallo standaardimplementatie.</span><span class="sxs-lookup"><span data-stu-id="6f723-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` tooalter hello notification that was prepared by hello default implementation.</span></span>

<span data-ttu-id="6f723-211">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6f723-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="6f723-212">In dit voorbeeld wordt een Systeemmelding voor een inhoud wordt weergegeven als een continue gebeurtenis wanneer Hallo 'continue'-categorie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6f723-212">This example makes a system notification for a content being displayed as an ongoing event when hello "ongoing" category is used.</span></span>

<span data-ttu-id="6f723-213">Als u wilt dat toobuild hello `Notification` object vanaf het begin, kunt u terugkeren `false` toohello methode en aanroep `notify` uzelf op Hallo `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="6f723-213">If you want toobuild hello `Notification` object from scratch, you can return `false` toohello method and call `notify` yourself on hello `NotificationManager`.</span></span> <span data-ttu-id="6f723-214">In dat geval is het belangrijk dat u een `contentIntent`, een `deleteIntent` en bericht-id die wordt gebruikt door Hallo `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="6f723-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and hello notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="6f723-215">Hier volgt een voorbeeld van een dergelijke implementatie:</span><span class="sxs-lookup"><span data-stu-id="6f723-215">Here is a correct example of such an implementation:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="6f723-216">Aankondigingen met alleen een melding</span><span class="sxs-lookup"><span data-stu-id="6f723-216">Notification only announcements</span></span>
<span data-ttu-id="6f723-217">Hallo management Hallo klikt u op een melding alleen aankondiging kan worden aangepast door het overschrijven van `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify Hallo voorbereid `Intent`.</span><span class="sxs-lookup"><span data-stu-id="6f723-217">hello management of hello click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify hello prepared `Intent`.</span></span> <span data-ttu-id="6f723-218">Met deze methode kunt u tootune Hallo vlaggen eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="6f723-218">Using this method allows you tootune hello flags easily.</span></span>

<span data-ttu-id="6f723-219">Bijvoorbeeld tooadd hello `SINGLE_TOP` vlag:</span><span class="sxs-lookup"><span data-stu-id="6f723-219">For example tooadd hello `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="6f723-220">Voor oudere Engagement gebruikers, houd er rekening mee dat systeemmeldingen zonder actie URL nu Hallo toepassing start als deze op de achtergrond, zodat deze methode kan worden aangeroepen met een aankondiging zonder actie-URL.</span><span class="sxs-lookup"><span data-stu-id="6f723-220">For legacy Engagement users, please note that system notifications without action URL now launches hello application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="6f723-221">U moet rekening houden met die bij het aanpassen van Hallo opzet.</span><span class="sxs-lookup"><span data-stu-id="6f723-221">You should consider that when customizing hello intent.</span></span>

<span data-ttu-id="6f723-222">U kunt ook implementeren `EngagementNotifier.executeNotifAnnouncementAction` vanaf het begin.</span><span class="sxs-lookup"><span data-stu-id="6f723-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="6f723-223">Levenscyclus van de kennisgeving</span><span class="sxs-lookup"><span data-stu-id="6f723-223">Notification life cycle</span></span>
<span data-ttu-id="6f723-224">Wanneer u de standaardcategorie hello, een aantal methoden levenscyclus worden aangeroepen op Hallo `EngagementReachInteractiveContent` tooreport statistieken en update Hallo campagne status object:</span><span class="sxs-lookup"><span data-stu-id="6f723-224">When using hello default category, some life cycle methods are called on hello `EngagementReachInteractiveContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="6f723-225">Wanneer Hallo melding wordt weergegeven in de toepassing of op de statusbalk hello plaatsen, Hallo `displayNotification` methode (die statistieken) wordt aangeroepen door `EngagementReachAgent` als `handleNotification` retourneert `true`.</span><span class="sxs-lookup"><span data-stu-id="6f723-225">When hello notification is displayed in application or put in hello status bar, hello `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="6f723-226">Als het Hallo-melding wordt gesloten, Hallo `exitNotification` methode wordt aangeroepen, statistiek wordt gerapporteerd en volgende campagnes kunnen nu worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="6f723-226">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="6f723-227">Als u Hallo melding klikt, `actionNotification` is aangeroepen, statistiek gemeld en wordt intentie Hallo die zijn gekoppeld wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="6f723-227">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated intent is launched.</span></span>

<span data-ttu-id="6f723-228">Als uw implementatie van `EngagementNotifier` omleidingen Hallo standaardgedrag, hebt u toocall deze methoden van de levenscyclus van de door u zelf.</span><span class="sxs-lookup"><span data-stu-id="6f723-228">If your implementation of `EngagementNotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="6f723-229">Hallo volgen voorbeelden illustreren bepaalde gevallen waarbij Hallo standaardgedrag wordt overgeslagen:</span><span class="sxs-lookup"><span data-stu-id="6f723-229">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="6f723-230">U kunt niet uitbreiden `EngagementDefaultNotifier`, zoals u categorie verwerking helemaal geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="6f723-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="6f723-231">Voor systeemmeldingen, u Hallo overrode `onNotificationPrepared` en u aangepast `contentIntent` of `deleteIntent` in Hallo `Notification` object.</span><span class="sxs-lookup"><span data-stu-id="6f723-231">For system notifications, you overrode hello `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in hello `Notification` object.</span></span>
* <span data-ttu-id="6f723-232">Voor in-app-meldingen, u overrode `prepareInAppArea`, moet u ervoor dat toomap ten minste `actionNotification` tooone uw U.I-besturingselementen.</span><span class="sxs-lookup"><span data-stu-id="6f723-232">For in-app notifications, you overrode `prepareInAppArea`, be sure toomap at least `actionNotification` tooone of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="6f723-233">Als `handleNotification` er wordt een uitzondering, Hallo inhoud is verwijderd en `dropContent` wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6f723-233">If `handleNotification` throws an exception, hello content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="6f723-234">Dit wordt gemeld in statistieken en volgende campagnes kunnen nu worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="6f723-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="6f723-235">Aankondigingen en polls</span><span class="sxs-lookup"><span data-stu-id="6f723-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="6f723-236">Indelingen</span><span class="sxs-lookup"><span data-stu-id="6f723-236">Layouts</span></span>
<span data-ttu-id="6f723-237">U kunt wijzigen Hallo `engagement_text_announcement.xml`, `engagement_web_announcement.xml` en `engagement_poll.xml` toocustomize tekst aankondigingen, web aankondigingen en polls bestanden.</span><span class="sxs-lookup"><span data-stu-id="6f723-237">You can modify hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files toocustomize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="6f723-238">Deze bestanden delen twee algemene indelingen voor Hallo titel gebieden en Hallo knop.</span><span class="sxs-lookup"><span data-stu-id="6f723-238">These files share two common layouts for hello title area and hello button area.</span></span> <span data-ttu-id="6f723-239">Hallo-indeling voor Hallo titel is `engagement_content_title.xml` en maakt gebruik van Hallo eponymous drawable-bestand voor Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="6f723-239">hello layout for hello title is `engagement_content_title.xml` and uses hello eponymous drawable file for hello background.</span></span> <span data-ttu-id="6f723-240">Hallo lay-out voor de actie en afsluiten knoppen Hallo is `engagement_button_bar.xml` en maakt gebruik van Hallo eponymous drawable-bestand voor Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="6f723-240">hello layout for hello action and exit buttons is `engagement_button_bar.xml` and uses hello eponymous drawable file for hello background.</span></span>

<span data-ttu-id="6f723-241">Hallo vraag lay-out in een poll en hun keuzes dynamisch worden vergroot met behulp van verschillende keren Hallo `engagement_question.xml` indelingsbestand voor Hallo vragen en Hallo `engagement_choice.xml` -bestand voor Hallo keuzes.</span><span class="sxs-lookup"><span data-stu-id="6f723-241">In a poll, hello question layout and their choices are dynamically inflated using several times hello `engagement_question.xml` layout file for hello questions and hello `engagement_choice.xml` file for hello choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="6f723-242">Categorieën</span><span class="sxs-lookup"><span data-stu-id="6f723-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="6f723-243">Alternatieve indelingen</span><span class="sxs-lookup"><span data-stu-id="6f723-243">Alternate layouts</span></span>
<span data-ttu-id="6f723-244">Zoals meldingen, kan de categorie van de campagne Hallo gebruikte toohave alternatieve indelingen voor uw aankondigingen en polls zijn.</span><span class="sxs-lookup"><span data-stu-id="6f723-244">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="6f723-245">Bijvoorbeeld, toocreate een categorie voor een aankondiging tekst, die u kunt uitbreiden `EngagementTextAnnouncementActivity` en verwijst u Hallo `AndroidManifest.xml` bestand:</span><span class="sxs-lookup"><span data-stu-id="6f723-245">For example, toocreate a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it hello `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="6f723-246">Houd er rekening mee die categorie Hallo in Hallo bedoeling filter wordt gebruikt toomake Hallo verschil met Hallo aankondiging standaardactiviteit.</span><span class="sxs-lookup"><span data-stu-id="6f723-246">Note that hello category in hello intent filter is used toomake hello difference with hello default announcement activity.</span></span>

<span data-ttu-id="6f723-247">Hallo bereiken SDK Hallo opzet system tooresolve Hallo juiste activiteit gebruikt voor een specifieke categorie en vallen terug op Hallo standaardcategorie als Hallo omzetting is mislukt.</span><span class="sxs-lookup"><span data-stu-id="6f723-247">hello Reach SDK uses hello intent system tooresolve hello right activity for a specific category and it falls back on hello default category if hello resolution failed.</span></span>

<span data-ttu-id="6f723-248">Hebt u tooimplement `MyCustomTextAnnouncementActivity`, als u alleen toochange Hallo indeling wilt (maar houd Hallo dezelfde id's weergeven), u hoeft alleen toodefine Hallo klasse zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="6f723-248">Then you have tooimplement `MyCustomTextAnnouncementActivity`, if you just want toochange hello layout (but keep hello same view identifiers), you just have toodefine hello class like in hello following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

<span data-ttu-id="6f723-249">tooreplace hello standaardcategorie van aankondigingen van tekst, vervang gewoon `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` door uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="6f723-249">tooreplace hello default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="6f723-250">Web-aankondigingen en polls kunnen worden aangepast op soortgelijke wijze.</span><span class="sxs-lookup"><span data-stu-id="6f723-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="6f723-251">U kunt uitbreiden voor web-aankondigingen `EngagementWebAnnouncementActivity` en de activiteit in Hallo declareren `AndroidManifest.xml` zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="6f723-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="6f723-252">U kunt uitbreiden voor polls `EngagementPollActivity` en uw in Hallo declareren `AndroidManifest.xml` in Hallo voorbeeld te volgen, zoals:</span><span class="sxs-lookup"><span data-stu-id="6f723-252">For polls you can extend `EngagementPollActivity` and declare your in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="6f723-253">Implementatie maken</span><span class="sxs-lookup"><span data-stu-id="6f723-253">Implementation from scratch</span></span>
<span data-ttu-id="6f723-254">U kunt categorieën voor uw activiteiten aankondiging (en de poll) implementeren zonder een Hallo `Engagement*Activity` klassen die worden geleverd door Hallo SDK bereiken.</span><span class="sxs-lookup"><span data-stu-id="6f723-254">You can implement categories for your announcement (and poll) activities without extending one of hello `Engagement*Activity` classes provided by hello Reach SDK.</span></span> <span data-ttu-id="6f723-255">Dit is bijvoorbeeld handig als u wilt dat toodefine een indeling die niet dezelfde bekijkt hello worden gebruikt als standaard Hallo-indelingen.</span><span class="sxs-lookup"><span data-stu-id="6f723-255">This is useful for example if you want toodefine a layout that does not use hello same views as hello standard layouts.</span></span>

<span data-ttu-id="6f723-256">Net als voor geavanceerde melding aanpassing, wordt aangeraden toolook op Hallo broncode van de standaardimplementatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f723-256">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

<span data-ttu-id="6f723-257">Hier volgen enkele dingen tookeep rekening: Reach Hallo activiteit met een specifiek doel (overeenkomende toohello opzet filter), plus een extra parameter Hallo inhouds-id wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="6f723-257">Here are some things tookeep in mind: Reach will launch hello activity with a specific intent (corresponding toohello intent filter) plus an extra parameter which is hello content identifier.</span></span>

<span data-ttu-id="6f723-258">tooretrieve hello inhoudsobject waarin Hallo velden die u hebt opgegeven wanneer het maken van Hallo campagne op Hallo website u kunt dit doen:</span><span class="sxs-lookup"><span data-stu-id="6f723-258">tooretrieve hello content object which contain hello fields you specified when creating hello campaign on hello web site you can do this:</span></span>

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

<span data-ttu-id="6f723-259">U moet voor statistics rapporteert Hallo inhoud wordt weergegeven in Hallo `onResume` gebeurtenis:</span><span class="sxs-lookup"><span data-stu-id="6f723-259">For statistics, you should report hello content is displayed in hello `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="6f723-260">Vervolgens moet u niet vergeten toocall ofwel `actionContent(this)` of `exitContent(this)` op Hallo inhoud object voordat de achtergrond probeert het Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="6f723-260">Then, don't forget toocall either `actionContent(this)` or `exitContent(this)` on hello content object before hello activity goes into background.</span></span>

<span data-ttu-id="6f723-261">Als niet aan te ofwel roepen `actionContent` of `exitContent`, statistieken niet verzonden (d.w.z. geen analytics op Hallo campagne) en meer belangrijker nog, Hallo volgende campagnes wordt niet gewaarschuwd als het toepassingsproces Hallo opnieuw is gestart.</span><span class="sxs-lookup"><span data-stu-id="6f723-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly, hello next campaigns will not be notified until hello application process is restarted.</span></span>

<span data-ttu-id="6f723-262">Afdrukstand of andere configuratiewijzigingen kunnen Hallo code lastig toodetermine maken of Hallo activiteit krijgt de achtergrond of niet, Hallo standaardimplementatie zorgt ervoor dat ervoor Hallo inhoud wordt gerapporteerd als is afgesloten als Hallo gebruiker Hallo-activiteit (via een verlaat drukken `HOME` of `BACK`) maar niet als Hallo afdrukstand wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="6f723-262">Orientation or other configuration changes can make hello code tricky toodetermine whether hello activity goes into background or not, hello standard implementation makes sure hello content is reported as exited if hello user leaves hello activity (either by pressing `HOME` or `BACK`) but not if hello orientation changes.</span></span>

<span data-ttu-id="6f723-263">Hier Hallo interessante deel uitmaakt van Hallo implementatie:</span><span class="sxs-lookup"><span data-stu-id="6f723-263">Here is hello interesting part of hello implementation:</span></span>

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="6f723-264">Zoals u zien kunt als u aangeroepen `actionContent(this)` en klaar bent met het Hallo-activiteit `exitContent(this)` veilig kan worden aangeroepen zonder geen effect.</span><span class="sxs-lookup"><span data-stu-id="6f723-264">As you can see, if you called `actionContent(this)` then finished hello activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
