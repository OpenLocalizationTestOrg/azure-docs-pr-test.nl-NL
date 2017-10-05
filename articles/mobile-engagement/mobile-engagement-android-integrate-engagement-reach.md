---
title: Azure Mobile Engagement Android SDK-integratie
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
ms.openlocfilehash: 26ba47b19f3a503693d60d344ad39b9eba74fe99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-reach-on-android"></a><span data-ttu-id="ba849-103">Het integreren van Engagement bereiken op Android</span><span class="sxs-lookup"><span data-stu-id="ba849-103">How to Integrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ba849-104">U moet de integratie procedure beschreven in de manier waarop integreren engagement voor Android-document voordat u deze handleiding volgen.</span><span class="sxs-lookup"><span data-stu-id="ba849-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="ba849-105">Standaard-integratie</span><span class="sxs-lookup"><span data-stu-id="ba849-105">Standard integration</span></span>

<span data-ttu-id="ba849-106">Kopieer Reach-bronbestanden van de SDK in uw project:</span><span class="sxs-lookup"><span data-stu-id="ba849-106">Copy Reach resource files from the SDK in your project :</span></span>

* <span data-ttu-id="ba849-107">Kopieer de bestanden van de `res/layout` map geleverd met de SDK in de `res/layout` map van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ba849-107">Copy the files from the `res/layout` folder delivered with the SDK into the `res/layout` folder of your application.</span></span>
* <span data-ttu-id="ba849-108">Kopieer de bestanden van de `res/drawable` map geleverd met de SDK in de `res/drawable` map van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ba849-108">Copy the files from the `res/drawable` folder delivered with the SDK into the `res/drawable` folder of your application.</span></span>

<span data-ttu-id="ba849-109">Bewerk uw `AndroidManifest.xml` bestand:</span><span class="sxs-lookup"><span data-stu-id="ba849-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="ba849-110">Voeg de volgende sectie (tussen de `<application>` en `</application>` labels):</span><span class="sxs-lookup"><span data-stu-id="ba849-110">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
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
* <span data-ttu-id="ba849-111">U moet deze machtiging aan replay-systeemmeldingen die niet is geklikt tijdens het opstarten (anders ze op schijf worden behouden, maar niet meer weergegeven, moet u echt opnemen).</span><span class="sxs-lookup"><span data-stu-id="ba849-111">You need this permission to replay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have to include this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="ba849-112">Geef een pictogram dat wordt gebruikt voor meldingen (zowel in-app en het systeem die zijn) door te kopiëren en bewerken van de volgende sectie (tussen de `<application>` en `</application>` labels):</span><span class="sxs-lookup"><span data-stu-id="ba849-112">Specify an icon used for notifications (both in app and system ones) by copying and editing the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="ba849-113">Deze sectie is **verplichte** als u van plan systeemmeldingen gebruiken bent bij het maken van Reach-campagnes.</span><span class="sxs-lookup"><span data-stu-id="ba849-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="ba849-114">Android wordt voorkomen dat systeemmeldingen zonder pictogrammen wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ba849-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="ba849-115">Dus als u deze sectie weglaat, wordt uw eindgebruikers niet mogelijk om ze te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="ba849-115">So if you omit this section, your end users will not be able to receive them.</span></span>
> 
> 

* <span data-ttu-id="ba849-116">Als u campagnes met systeemmeldingen met behulp van de grote afbeelding maakt, moet u de volgende machtigingen toevoegen (nadat de `</application>` tag) indien deze ontbreken:</span><span class="sxs-lookup"><span data-stu-id="ba849-116">If you create campaigns with system notifications using big picture, you need to add the following permissions (after the `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="ba849-117">Op Android M en als uw toepassing gericht op Android-API-niveau 23 of hoger, ``WRITE_EXTERNAL_STORAGE`` machtiging vereist goedkeuring van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ba849-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="ba849-118">Lees [in deze sectie](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="ba849-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="ba849-119">Voor systeemmeldingen kunt u ook opgeven in de Reach-campagne als het apparaat moet ring en/of trillen.</span><span class="sxs-lookup"><span data-stu-id="ba849-119">For system notifications you can also specify in the Reach campaign if the device should ring and/or vibrate.</span></span> <span data-ttu-id="ba849-120">Om te werken, hebt u zeker dat u de volgende machtiging gedeclareerd (nadat de `</application>` tag):</span><span class="sxs-lookup"><span data-stu-id="ba849-120">For it to work, you have to make sure you declared the following permission (after the `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="ba849-121">Zonder deze machtiging Android voorkomt u dat systeemmeldingen worden weergegeven als u de ring of de optie vibrate in de Reach-campagnes gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="ba849-121">Without this permission, Android prevents system notifications from being shown if you checked the ring or the vibrate option in the Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="ba849-122">Native Pushberichten</span><span class="sxs-lookup"><span data-stu-id="ba849-122">Native Push</span></span>
<span data-ttu-id="ba849-123">Nu u de Reach-module hebt geconfigureerd, moet u native pushberichten om het ontvangen van de campagnes op het apparaat te kunnen configureren.</span><span class="sxs-lookup"><span data-stu-id="ba849-123">Now that you configured Reach module, you need to configure native push to be able to receive the campaigns on the device.</span></span>

<span data-ttu-id="ba849-124">We ondersteunen twee services op Android:</span><span class="sxs-lookup"><span data-stu-id="ba849-124">We support two services on Android:</span></span>

* <span data-ttu-id="ba849-125">Google Play-apparaten: Gebruik [Google Cloud Messaging] volgens de [hoe GCM integreren met Engagement handleiding](mobile-engagement-android-gcm-integrate.md) handleiding.</span><span class="sxs-lookup"><span data-stu-id="ba849-125">Google Play devices: Use [Google Cloud Messaging] by following the [How to Integrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="ba849-126">Amazon-apparaten: Gebruik [Amazon Device Messaging] volgens de [hoe ADM integreren met Engagement handleiding](mobile-engagement-android-adm-integrate.md) handleiding.</span><span class="sxs-lookup"><span data-stu-id="ba849-126">Amazon devices: Use [Amazon Device Messaging] by following the [How to Integrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="ba849-127">Als u zich richten Amazon- en Google Play-apparaten, de twee mogelijke wilt hebben alles wat binnen 1 AndroidManifest.xml/APK voor ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="ba849-127">If you want to target both Amazon and Google Play devices, its possible to have everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="ba849-128">Maar bij het indienen van Amazon, kunnen ze uw toepassing afwijzen als ze GCM code vinden.</span><span class="sxs-lookup"><span data-stu-id="ba849-128">But when submitting to Amazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="ba849-129">In dat geval moet u meerdere APKs gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ba849-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="ba849-130">**Uw toepassing is nu gereed om te ontvangen en weergeven van reach-campagnes!**</span><span class="sxs-lookup"><span data-stu-id="ba849-130">**Your application is now ready to receive and display reach campaigns!**</span></span>

## <a name="how-to-handle-data-push"></a><span data-ttu-id="ba849-131">Hoe worden gegevens-push verwerkt</span><span class="sxs-lookup"><span data-stu-id="ba849-131">How to handle data push</span></span>
### <a name="integration"></a><span data-ttu-id="ba849-132">Integratie</span><span class="sxs-lookup"><span data-stu-id="ba849-132">Integration</span></span>
<span data-ttu-id="ba849-133">Als u wilt dat uw toepassing te kunnen ontvangen van gegevens-pushes Reach, u moet een subklasse zijn van maken `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` en ernaar wordt verwezen in de `AndroidManifest.xml` bestand (tussen de `<application>` en/of `</application>` labels):</span><span class="sxs-lookup"><span data-stu-id="ba849-133">If you want your application to be able to receive Reach data pushes, you have to create a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in the `AndroidManifest.xml` file (between the `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="ba849-134">Vervolgens kunt u overschrijven de `onDataPushStringReceived` en `onDataPushBase64Received` retouraanroepen.</span><span class="sxs-lookup"><span data-stu-id="ba849-134">Then you can override the `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="ba849-135">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ba849-135">Here is an example:</span></span>

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

### <a name="category"></a><span data-ttu-id="ba849-136">Category</span><span class="sxs-lookup"><span data-stu-id="ba849-136">Category</span></span>
<span data-ttu-id="ba849-137">De categorieparameter is optioneel bij het maken van een campagne Push-gegevens en kunt dat u gegevens wilt filteren pushes.</span><span class="sxs-lookup"><span data-stu-id="ba849-137">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span></span> <span data-ttu-id="ba849-138">Dit is handig als u verschillende broadcast ontvangers afhandeling van verschillende soorten gegevens-pushes hebt of als u wilt pushen van verschillende typen van `Base64` gegevens en wilt u het type waardoor ze identificeren voordat ze worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="ba849-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="ba849-139">De retouraanroepen retourparameter</span><span class="sxs-lookup"><span data-stu-id="ba849-139">Callbacks' return parameter</span></span>
<span data-ttu-id="ba849-140">Hier volgen enkele richtlijnen voor het afhandelen van de retourparameter van goed `onDataPushStringReceived` en `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="ba849-140">Here are some guidelines to properly handle the return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="ba849-141">Een ontvanger broadcast moet retourneren `null` in de callback als het niet weet hoe een gegevens-push verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ba849-141">A broadcast receiver should return `null` in the callback if it does not know how to handle a data push.</span></span> <span data-ttu-id="ba849-142">U moet de categorie gebruiken om te bepalen of uw broadcast ontvanger het gegevens-push of niet verwerken moet.</span><span class="sxs-lookup"><span data-stu-id="ba849-142">You should use the category to determine whether your broadcast receiver should handle the data push or not.</span></span>
* <span data-ttu-id="ba849-143">Een van de ontvanger broadcast moet retourneren `true` in de callback als deze de gegevens-push accepteert.</span><span class="sxs-lookup"><span data-stu-id="ba849-143">One of the broadcast receiver should return `true` in the callback if it accepts the data push.</span></span>
* <span data-ttu-id="ba849-144">Een van de ontvanger broadcast moet retourneren `false` in de callback als het gegevens-push herkent, maar deze om welke reden dan ook negeert.</span><span class="sxs-lookup"><span data-stu-id="ba849-144">One of the broadcast receiver should return `false` in the callback if it recognizes the data push, but discards it for whatever reason.</span></span> <span data-ttu-id="ba849-145">Bijvoorbeeld retourneren `false` wanneer de ontvangen gegevens is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="ba849-145">For example, return `false` when the received data is invalid.</span></span>
* <span data-ttu-id="ba849-146">Als een ontvanger retourneert broadcast `true` terwijl een andere een retourneert `false` voor de dezelfde gegevens-push het gedrag is niet gedefinieerd, moet u nooit die.</span><span class="sxs-lookup"><span data-stu-id="ba849-146">If one broadcast receiver returns `true` while another one returns `false` for the same data push, the behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="ba849-147">Het retourtype wordt alleen gebruikt voor de Reach-statistieken:</span><span class="sxs-lookup"><span data-stu-id="ba849-147">The return type is used only for the Reach statistics:</span></span>

* <span data-ttu-id="ba849-148">`Replied`Als een van de broadcast ontvangers ofwel geretourneerd wordt verhoogd `true` of `false`.</span><span class="sxs-lookup"><span data-stu-id="ba849-148">`Replied` is incremented if one of the broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="ba849-149">`Actioned`alleen als een van de broadcast ontvangers geretourneerd wordt verhoogd `true`.</span><span class="sxs-lookup"><span data-stu-id="ba849-149">`Actioned` is incremented only if one of the broadcast receivers returned `true`.</span></span>

## <a name="how-to-customize-campaigns"></a><span data-ttu-id="ba849-150">Het aanpassen van de campagnes</span><span class="sxs-lookup"><span data-stu-id="ba849-150">How to customize campaigns</span></span>
<span data-ttu-id="ba849-151">U kunt de indelingen die beschikbaar zijn in de SDK bereiken wijzigen voor het aanpassen van campagnes.</span><span class="sxs-lookup"><span data-stu-id="ba849-151">To customize campaigns, you can modify the layouts provided in the Reach SDK.</span></span>

<span data-ttu-id="ba849-152">U moet alle id's die in de indelingen houden en de typen van de weergaven die gebruikmaken van een id in, met name voor tekst en afbeeldingen weergaven houden.</span><span class="sxs-lookup"><span data-stu-id="ba849-152">You should keep all the identifiers used in the layouts and keep the types of the views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="ba849-153">Sommige weergaven worden alleen gebruikt voor het verbergen of weergeven van gebieden, zodat hun type kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="ba849-153">Some views are just used to hide or show areas so their type may be changed.</span></span> <span data-ttu-id="ba849-154">Controleer of de broncode als u van plan bent om te wijzigen van het type van een weergave in de opgegeven indelingen.</span><span class="sxs-lookup"><span data-stu-id="ba849-154">Please check the source code if you intend to change the type of a view in the provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="ba849-155">Meldingen</span><span class="sxs-lookup"><span data-stu-id="ba849-155">Notifications</span></span>
<span data-ttu-id="ba849-156">Er zijn twee typen meldingen: systeem en in-app-meldingen die andere indelingsbestanden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ba849-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="ba849-157">Systeemmeldingen</span><span class="sxs-lookup"><span data-stu-id="ba849-157">System notifications</span></span>
<span data-ttu-id="ba849-158">Om aan te passen systeemmeldingen die u wilt gebruiken, de **categorieën**.</span><span class="sxs-lookup"><span data-stu-id="ba849-158">To customize system notifications you need to use the **categories**.</span></span> <span data-ttu-id="ba849-159">U kunt naar gaan [categorieën](#categories).</span><span class="sxs-lookup"><span data-stu-id="ba849-159">You can jump to [Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="ba849-160">In-app-meldingen</span><span class="sxs-lookup"><span data-stu-id="ba849-160">In-app notifications</span></span>
<span data-ttu-id="ba849-161">Een in-app-melding is standaard een weergave die dynamisch wordt toegevoegd aan de huidige activiteit gebruikersinterface dankzij de Android-methode `addContentView()`.</span><span class="sxs-lookup"><span data-stu-id="ba849-161">By default, an in-app notification is a view that is dynamically added to the current activity user interface thanks to the Android method `addContentView()`.</span></span> <span data-ttu-id="ba849-162">Dit is een melding overlay genoemd.</span><span class="sxs-lookup"><span data-stu-id="ba849-162">This is called a notification overlay.</span></span> <span data-ttu-id="ba849-163">Melding overlays zijn ideaal voor een snelle integratie omdat ze niet vereisen dat u elke lay-out in uw toepassing wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ba849-163">Notification overlays are great for a fast integration because they do not require you to modify any layout in your application.</span></span>

<span data-ttu-id="ba849-164">Voor het wijzigen van het uiterlijk van uw notification overlays u gewoon het bestand kan wijzigen `engagement_notification_area.xml` aan uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="ba849-164">To modify the look of your notification overlays, you can simply modify the file `engagement_notification_area.xml` to your needs.</span></span>

> [!NOTE]
> <span data-ttu-id="ba849-165">Het bestand `engagement_notification_overlay.xml` is de taak die wordt gebruikt voor het maken van een melding overlay, waaronder het bestand `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="ba849-165">The file `engagement_notification_overlay.xml` is the one that is used to create a notification overlay, it includes the file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="ba849-166">U kunt ook aanpassen aan uw behoeften (bijvoorbeeld voor het systeemvak in de overlay plaatsing).</span><span class="sxs-lookup"><span data-stu-id="ba849-166">You can also customize it to suit your needs (such as for positioning the notification area within the overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="ba849-167">Indeling van de melding als onderdeel van de indeling van een activiteit bevatten</span><span class="sxs-lookup"><span data-stu-id="ba849-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="ba849-168">Overlays zijn ideaal voor een snelle integratie, maar worden onhandig of neveneffecten hebben in bijzondere gevallen.</span><span class="sxs-lookup"><span data-stu-id="ba849-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="ba849-169">Het systeem overlay kan worden aangepast op een activiteitenniveau van de, zodat u gemakkelijk om te voorkomen dat bijwerkingen voor speciale activiteiten.</span><span class="sxs-lookup"><span data-stu-id="ba849-169">The overlay system can be customized at an activity level, making it easy to prevent side effects for special activities.</span></span>

<span data-ttu-id="ba849-170">U kunt de indeling van onze melding opnemen in uw bestaande indeling dankzij de Android **omvatten** instructie.</span><span class="sxs-lookup"><span data-stu-id="ba849-170">You can decide to include our notification layout in your existing layout thanks to the Android **include** statement.</span></span> <span data-ttu-id="ba849-171">Hieronder volgt een voorbeeld van een gewijzigde `ListActivity` lay-out die net bevat een `ListView`.</span><span class="sxs-lookup"><span data-stu-id="ba849-171">The following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="ba849-172">**Voordat de Engagement-integratie:**</span><span class="sxs-lookup"><span data-stu-id="ba849-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="ba849-173">**Na de Engagement-integratie:**</span><span class="sxs-lookup"><span data-stu-id="ba849-173">**After Engagement integration :**</span></span>

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

<span data-ttu-id="ba849-174">In dit voorbeeld hebben we een bovenliggende container toegevoegd, omdat de oorspronkelijke indeling een lijstweergave als het bovenste element gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ba849-174">In this example we added a parent container since the original layout used a list view as the top level element.</span></span> <span data-ttu-id="ba849-175">We hebben ook toegevoegd `android:layout_weight="1"` kunnen hieronder een lijstweergave geconfigureerd met een weergave toevoegen `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="ba849-175">We also added `android:layout_weight="1"` to be able to add a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="ba849-176">De SDK Engagement bereiken worden automatisch gedetecteerd dat de indeling van de melding is opgenomen in deze activiteit en een overlay voor deze activiteit wordt niet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ba849-176">The Engagement Reach SDK automatically detects that the notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="ba849-177">Als u een ListActivity in uw toepassing gebruikt, een zichtbaar Reach-overlay wordt voorkomen dat u reageert op meer items in de lijstweergave geklikt.</span><span class="sxs-lookup"><span data-stu-id="ba849-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting to clicked items in the list view anymore.</span></span> <span data-ttu-id="ba849-178">Dit is een bekend probleem.</span><span class="sxs-lookup"><span data-stu-id="ba849-178">This is a known issue.</span></span> <span data-ttu-id="ba849-179">U kunt dit probleem omzeilen raden we u om in te sluiten van de indeling van de melding in de indeling van uw eigen lijst activiteit zoals in het vorige voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ba849-179">To work around this problem we suggest you to embed the notification layout in your own list activity layout like in the previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="ba849-180">Het uitschakelen van de melding per activiteit</span><span class="sxs-lookup"><span data-stu-id="ba849-180">Disabling application notification per activity</span></span>
<span data-ttu-id="ba849-181">Als u niet wilt dat de overlay worden toegevoegd aan de activiteit en als u de indeling van de melding niet in uw eigen lay-out opnemen, kunt u uitschakelen met de overlay voor deze activiteit in de `AndroidManifest.xml` door toe te voegen een `meta-data` sectie, zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ba849-181">If you don't want the overlay to be added to your activity, and if you don't include the notification layout in your own layout, you can disable the overlay for this activity in the `AndroidManifest.xml` by adding a `meta-data` section like in the following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="ba849-182"><a name="categories"></a>Categorieën</span><span class="sxs-lookup"><span data-stu-id="ba849-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="ba849-183">Als u de opgegeven indelingen wijzigt, wijzigt u het uiterlijk van al uw meldingen.</span><span class="sxs-lookup"><span data-stu-id="ba849-183">When you modify the provided layouts, you modify the look of all your notifications.</span></span> <span data-ttu-id="ba849-184">Categorieën kunnen u verschillende gerichte lijkt (mogelijk gedrag) definiëren voor meldingen.</span><span class="sxs-lookup"><span data-stu-id="ba849-184">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="ba849-185">Een categorie kan worden opgegeven wanneer u een Reach-campagne maken.</span><span class="sxs-lookup"><span data-stu-id="ba849-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="ba849-186">Houd er rekening mee dat categorieën ook kunnen u aanpassen aankondigingen en polls, die verderop in dit document wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="ba849-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="ba849-187">Voor het registreren van een categorie-handler voor uw meldingen, moet u een aanroep van toevoegen wanneer de toepassing wordt geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="ba849-187">To register a category handler for your notifications, you need to add a call when the application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba849-188">Lees de waarschuwing voor het kenmerk android: proces \<android-sdk-engagement-process\> in de manier waarop integreren engagement op Android onderwerp voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="ba849-188">Please read the warning about the android:process attribute \<android-sdk-engagement-process\> in the How to Integrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="ba849-189">Het volgende voorbeeld wordt ervan uitgegaan dat u de vorige waarschuwing bevestigd en gebruikt een subklasse zijn van `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="ba849-189">The following example assumes you acknowledged the previous warning and use a sub-class of `EngagementApplication`:</span></span>

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

<span data-ttu-id="ba849-190">De `MyNotifier` object is de implementatie van de meldings-handler categorie.</span><span class="sxs-lookup"><span data-stu-id="ba849-190">The `MyNotifier` object is the implementation of the notification category handler.</span></span> <span data-ttu-id="ba849-191">Het is ofwel een implementatie van de `EngagementNotifier` -interface of een subklasse van de standaardimplementatie: `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="ba849-191">It is either an implementation of the `EngagementNotifier` interface or a sub class of the default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="ba849-192">Houd er rekening mee dat de dezelfde melder verscheidene categorieën kan verwerken, kunt u deze registreren als volgt:</span><span class="sxs-lookup"><span data-stu-id="ba849-192">Note that the same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="ba849-193">Ter vervanging van de standaardimplementatie categorie, kunt u uw implementatie zoals registreren in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ba849-193">To replace the default category implementation, you can register your implementation like in the following example:</span></span>

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

<span data-ttu-id="ba849-194">De huidige categorie gebruikt in een handler is doorgegeven als een parameter in de meeste methoden kunt u overschrijven `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="ba849-194">The current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="ba849-195">Deze is doorgegeven als een `String` parameter of indirect in een `EngagementReachContent` object waarvoor een `getCategory()` methode.</span><span class="sxs-lookup"><span data-stu-id="ba849-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="ba849-196">U kunt de meeste van een proces voor het maken van de melding wijzigen door gaat herdefiniëren methoden op `EngagementDefaultNotifier`, voor meer geavanceerde aanpassing gerust bekijken op de technische documentatie en op de broncode.</span><span class="sxs-lookup"><span data-stu-id="ba849-196">You can change most of the notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free to take a look at the technical documentation and at the source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="ba849-197">In-app-meldingen</span><span class="sxs-lookup"><span data-stu-id="ba849-197">In-app notifications</span></span>
<span data-ttu-id="ba849-198">Als u alleen alternatieve indelingen worden gebruikt voor een specifieke categorie wilt, kunt u dit implementeren als in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ba849-198">If you just want to use alternate layouts for a specific category, you can implement this as in the following example:</span></span>

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

<span data-ttu-id="ba849-199">**Voorbeeld van `my_notification_overlay.xml` :**</span><span class="sxs-lookup"><span data-stu-id="ba849-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="ba849-200">Zoals u ziet is de overlay weergave-id anders dan de standaard één.</span><span class="sxs-lookup"><span data-stu-id="ba849-200">As you can see, the overlay view identifier is different than the standard one.</span></span> <span data-ttu-id="ba849-201">Het is belangrijk dat elke indeling een unieke id voor overlays gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ba849-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="ba849-202">**Voorbeeld van `my_notification_area.xml` :**</span><span class="sxs-lookup"><span data-stu-id="ba849-202">**Example of `my_notification_area.xml` :**</span></span>

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

<span data-ttu-id="ba849-203">Zoals u ziet is de melding gebied weergave-id anders dan de standaard één.</span><span class="sxs-lookup"><span data-stu-id="ba849-203">As you can see, the notification area view identifier is different than the standard one.</span></span> <span data-ttu-id="ba849-204">Het is belangrijk dat elke indeling wordt gebruikt voor een unieke id voor de melding gebieden.</span><span class="sxs-lookup"><span data-stu-id="ba849-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="ba849-205">Dit eenvoudige voorbeeld van de categorie kunt u een toepassing (of in-app) meldingen die aan de bovenkant van het scherm worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ba849-205">This simple example of category makes application (or in-app) notifications displayed at the top of the screen.</span></span> <span data-ttu-id="ba849-206">Er is niet veranderd met de standaard-id's in het systeemvak zelf.</span><span class="sxs-lookup"><span data-stu-id="ba849-206">We did not change the standard identifiers used in the notification area itself.</span></span>

<span data-ttu-id="ba849-207">Als u wijzigen wilt, hebt u definiëren de `EngagementDefaultNotifier.prepareInAppArea` methode.</span><span class="sxs-lookup"><span data-stu-id="ba849-207">If you want to change that, you have to redefine the `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="ba849-208">Het is raadzaam om te zoeken op de technische documentatie en op de broncode van `EngagementNotifier` en `EngagementDefaultNotifier` als u wilt dat dit niveau van Geavanceerd aanpassen.</span><span class="sxs-lookup"><span data-stu-id="ba849-208">It's recommended to look at the technical documentation and at the source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="ba849-209">Systeemmeldingen</span><span class="sxs-lookup"><span data-stu-id="ba849-209">System notifications</span></span>
<span data-ttu-id="ba849-210">Door uit te breiden `EngagementDefaultNotifier`, kunt u overschrijven `onNotificationPrepared` voor het wijzigen van de melding die is voorbereid door de standaardimplementatie.</span><span class="sxs-lookup"><span data-stu-id="ba849-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` to alter the notification that was prepared by the default implementation.</span></span>

<span data-ttu-id="ba849-211">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ba849-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="ba849-212">In dit voorbeeld wordt een Systeemmelding voor een inhoud wordt weergegeven als een continue gebeurtenis geactiveerd wanneer de categorie 'continue' wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ba849-212">This example makes a system notification for a content being displayed as an ongoing event when the "ongoing" category is used.</span></span>

<span data-ttu-id="ba849-213">Als u wilt bouwen de `Notification` object vanaf het begin, kunt u terugkeren `false` aan de methode en de aanroep `notify` uzelf op de `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="ba849-213">If you want to build the `Notification` object from scratch, you can return `false` to the method and call `notify` yourself on the `NotificationManager`.</span></span> <span data-ttu-id="ba849-214">In dat geval is het belangrijk dat u een `contentIntent`, een `deleteIntent` en de bericht-id die wordt gebruikt door `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="ba849-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and the notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="ba849-215">Hier volgt een voorbeeld van een dergelijke implementatie:</span><span class="sxs-lookup"><span data-stu-id="ba849-215">Here is a correct example of such an implementation:</span></span>

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
              manager.notify(getNotificationId(content), myNotification); // notice the call to get the right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="ba849-216">Aankondigingen met alleen een melding</span><span class="sxs-lookup"><span data-stu-id="ba849-216">Notification only announcements</span></span>
<span data-ttu-id="ba849-217">Het beheer van het klikken op een melding alleen aankondiging kan worden aangepast door het overschrijven van `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` te wijzigen van het voorbereide `Intent`.</span><span class="sxs-lookup"><span data-stu-id="ba849-217">The management of the click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` to modify the prepared `Intent`.</span></span> <span data-ttu-id="ba849-218">Met deze methode kunt u eenvoudig de vlaggen afstemmen.</span><span class="sxs-lookup"><span data-stu-id="ba849-218">Using this method allows you to tune the flags easily.</span></span>

<span data-ttu-id="ba849-219">Bijvoorbeeld om toe te voegen de `SINGLE_TOP` vlag:</span><span class="sxs-lookup"><span data-stu-id="ba849-219">For example to add the `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="ba849-220">Voor oudere Engagement gebruikers, houd er rekening mee dat systeemmeldingen zonder actie URL nu de toepassing start als deze op de achtergrond, zodat deze methode kan worden aangeroepen met een aankondiging zonder actie-URL.</span><span class="sxs-lookup"><span data-stu-id="ba849-220">For legacy Engagement users, please note that system notifications without action URL now launches the application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="ba849-221">U moet rekening houden met die bij het aanpassen van het doel.</span><span class="sxs-lookup"><span data-stu-id="ba849-221">You should consider that when customizing the intent.</span></span>

<span data-ttu-id="ba849-222">U kunt ook implementeren `EngagementNotifier.executeNotifAnnouncementAction` vanaf het begin.</span><span class="sxs-lookup"><span data-stu-id="ba849-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="ba849-223">Levenscyclus van de kennisgeving</span><span class="sxs-lookup"><span data-stu-id="ba849-223">Notification life cycle</span></span>
<span data-ttu-id="ba849-224">Wanneer u de standaardcategorie gebruikt, een aantal methoden levenscyclus worden aangeroepen op de `EngagementReachInteractiveContent` object rapport statistieken en de status van de campagne werken:</span><span class="sxs-lookup"><span data-stu-id="ba849-224">When using the default category, some life cycle methods are called on the `EngagementReachInteractiveContent` object to report statistics and update the campaign state:</span></span>

* <span data-ttu-id="ba849-225">Wanneer de melding wordt weergegeven in de toepassing of op de statusbalk plaatsen de `displayNotification` methode (die statistieken) wordt aangeroepen door `EngagementReachAgent` als `handleNotification` retourneert `true`.</span><span class="sxs-lookup"><span data-stu-id="ba849-225">When the notification is displayed in application or put in the status bar, the `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="ba849-226">Als de melding wordt gesloten, de `exitNotification` methode wordt aangeroepen, statistiek wordt gerapporteerd en volgende campagnes kunnen nu worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ba849-226">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="ba849-227">Als u de melding klikt, `actionNotification` is aangeroepen, statistiek gemeld en wordt het bijbehorende doel wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="ba849-227">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated intent is launched.</span></span>

<span data-ttu-id="ba849-228">Als uw implementatie van `EngagementNotifier` het standaardgedrag omzeilt u aan te roepen van deze methoden van de levenscyclus van de door u zelf hebt.</span><span class="sxs-lookup"><span data-stu-id="ba849-228">If your implementation of `EngagementNotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span></span> <span data-ttu-id="ba849-229">De volgende voorbeelden ziet enkele gevallen waarbij het standaardgedrag wordt overgeslagen:</span><span class="sxs-lookup"><span data-stu-id="ba849-229">The following examples illustrate some cases where the default behavior is bypassed:</span></span>

* <span data-ttu-id="ba849-230">U kunt niet uitbreiden `EngagementDefaultNotifier`, zoals u categorie verwerking helemaal geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="ba849-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="ba849-231">Voor systeemmeldingen, overrode u de `onNotificationPrepared` en u aangepast `contentIntent` of `deleteIntent` in de `Notification` object.</span><span class="sxs-lookup"><span data-stu-id="ba849-231">For system notifications, you overrode the `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in the `Notification` object.</span></span>
* <span data-ttu-id="ba849-232">Voor in-app-meldingen, u overrode `prepareInAppArea`, zorg ervoor dat toegewezen ten minste `actionNotification` op een van uw U.I bepaalt.</span><span class="sxs-lookup"><span data-stu-id="ba849-232">For in-app notifications, you overrode `prepareInAppArea`, be sure to map at least `actionNotification` to one of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="ba849-233">Als `handleNotification` er wordt een uitzondering, de inhoud wordt verwijderd en `dropContent` wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ba849-233">If `handleNotification` throws an exception, the content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="ba849-234">Dit wordt gemeld in statistieken en volgende campagnes kunnen nu worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ba849-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="ba849-235">Aankondigingen en polls</span><span class="sxs-lookup"><span data-stu-id="ba849-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="ba849-236">Indelingen</span><span class="sxs-lookup"><span data-stu-id="ba849-236">Layouts</span></span>
<span data-ttu-id="ba849-237">U kunt de `engagement_text_announcement.xml`, `engagement_web_announcement.xml` en `engagement_poll.xml` bestanden voor het aanpassen van tekst aankondigingen, web aankondigingen en polls.</span><span class="sxs-lookup"><span data-stu-id="ba849-237">You can modify the `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files to customize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="ba849-238">Deze bestanden delen twee algemene indeling voor de titel gebieden en de knop.</span><span class="sxs-lookup"><span data-stu-id="ba849-238">These files share two common layouts for the title area and the button area.</span></span> <span data-ttu-id="ba849-239">De indeling voor de titel is `engagement_content_title.xml` en het eponymous drawable-bestand wordt gebruikt voor de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="ba849-239">The layout for the title is `engagement_content_title.xml` and uses the eponymous drawable file for the background.</span></span> <span data-ttu-id="ba849-240">De indeling voor de knoppen met de actie en afsluiten is `engagement_button_bar.xml` en het eponymous drawable-bestand wordt gebruikt voor de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="ba849-240">The layout for the action and exit buttons is `engagement_button_bar.xml` and uses the eponymous drawable file for the background.</span></span>

<span data-ttu-id="ba849-241">In een poll de indeling van de vraag en hun mogelijkheden zijn dynamisch vergroot met behulp van verschillende keren de `engagement_question.xml` lay-bestand voor de vragen en de `engagement_choice.xml` -bestand voor de opties.</span><span class="sxs-lookup"><span data-stu-id="ba849-241">In a poll, the question layout and their choices are dynamically inflated using several times the `engagement_question.xml` layout file for the questions and the `engagement_choice.xml` file for the choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="ba849-242">Categorieën</span><span class="sxs-lookup"><span data-stu-id="ba849-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="ba849-243">Alternatieve indelingen</span><span class="sxs-lookup"><span data-stu-id="ba849-243">Alternate layouts</span></span>
<span data-ttu-id="ba849-244">Zoals meldingen, kan de campagne categorie worden gebruikt voor alternatieve indelingen voor uw aankondigingen en polls hebben.</span><span class="sxs-lookup"><span data-stu-id="ba849-244">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="ba849-245">Bijvoorbeeld: voor het maken van een categorie voor een aankondiging tekst, kunt u uitbreiden `EngagementTextAnnouncementActivity` en verwijst het `AndroidManifest.xml` bestand:</span><span class="sxs-lookup"><span data-stu-id="ba849-245">For example, to create a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it the `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="ba849-246">Houd er rekening mee dat de categorie van het filter opzet wordt gebruikt om het verschil met het standaard aankondiging activiteit maken.</span><span class="sxs-lookup"><span data-stu-id="ba849-246">Note that the category in the intent filter is used to make the difference with the default announcement activity.</span></span>

<span data-ttu-id="ba849-247">De SDK bereiken gebruikt het systeem opzet omzetten van de juiste activiteit voor een specifieke categorie en vallen terug op de standaardcategorie als de omzetting is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ba849-247">The Reach SDK uses the intent system to resolve the right activity for a specific category and it falls back on the default category if the resolution failed.</span></span>

<span data-ttu-id="ba849-248">Hebt u voor het implementeren van `MyCustomTextAnnouncementActivity`, als u alleen wilt wijzigen van de lay-out (maar houd de dezelfde weergave-id's), u hoeft alleen te definiëren van de klasse zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ba849-248">Then you have to implement `MyCustomTextAnnouncementActivity`, if you just want to change the layout (but keep the same view identifiers), you just have to define the class like in the following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class to use R.layout.my_text_announcement
              }
            }

<span data-ttu-id="ba849-249">Ter vervanging van de standaardcategorie van tekst aankondigingen gewoon vervangen `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` door uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="ba849-249">To replace the default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="ba849-250">Web-aankondigingen en polls kunnen worden aangepast op soortgelijke wijze.</span><span class="sxs-lookup"><span data-stu-id="ba849-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="ba849-251">U kunt uitbreiden voor web-aankondigingen `EngagementWebAnnouncementActivity` en declareren van de activiteit in de `AndroidManifest.xml` zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ba849-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in the intent is the data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="ba849-252">U kunt uitbreiden voor polls `EngagementPollActivity` en declareren uw in de `AndroidManifest.xml` zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ba849-252">For polls you can extend `EngagementPollActivity` and declare your in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="ba849-253">Implementatie maken</span><span class="sxs-lookup"><span data-stu-id="ba849-253">Implementation from scratch</span></span>
<span data-ttu-id="ba849-254">U kunt de categorieën voor uw activiteiten aankondiging (en de poll) implementeren zonder het uitbreiden van een van de `Engagement*Activity` klassen die zijn opgegeven door de SDK bereiken.</span><span class="sxs-lookup"><span data-stu-id="ba849-254">You can implement categories for your announcement (and poll) activities without extending one of the `Engagement*Activity` classes provided by the Reach SDK.</span></span> <span data-ttu-id="ba849-255">Dit is bijvoorbeeld handig als u wilt definiëren van een indeling die niet de dezelfde weergaven worden gebruikt als de standaard-indelingen.</span><span class="sxs-lookup"><span data-stu-id="ba849-255">This is useful for example if you want to define a layout that does not use the same views as the standard layouts.</span></span>

<span data-ttu-id="ba849-256">Zoals voor aanpassing van de geavanceerde melding, is het raadzaam om te kijken naar de broncode van de standaardimplementatie.</span><span class="sxs-lookup"><span data-stu-id="ba849-256">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span></span>

<span data-ttu-id="ba849-257">Hier volgen enkele dingen rekening moet houden: Reach de activiteit met een specifiek doel (overeenkomt met de opzet filter), plus een extra parameter die de inhoud-id wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="ba849-257">Here are some things to keep in mind: Reach will launch the activity with a specific intent (corresponding to the intent filter) plus an extra parameter which is the content identifier.</span></span>

<span data-ttu-id="ba849-258">U kunt dit doen voor het ophalen van het inhoudsobject waarin de velden die u hebt opgegeven bij het maken van de campagne op de website:</span><span class="sxs-lookup"><span data-stu-id="ba849-258">To retrieve the content object which contain the fields you specified when creating the campaign on the web site you can do this:</span></span>

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

<span data-ttu-id="ba849-259">U moet voor statistieken, rapporteert de inhoud wordt weergegeven in de `onResume` gebeurtenis:</span><span class="sxs-lookup"><span data-stu-id="ba849-259">For statistics, you should report the content is displayed in the `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark the content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="ba849-260">Vergeet niet om aan te roepen ofwel `actionContent(this)` of `exitContent(this)` op het inhoudsobject voordat de activiteit wordt verplaatst naar achtergrond.</span><span class="sxs-lookup"><span data-stu-id="ba849-260">Then, don't forget to call either `actionContent(this)` or `exitContent(this)` on the content object before the activity goes into background.</span></span>

<span data-ttu-id="ba849-261">Als niet aan te ofwel roepen `actionContent` of `exitContent`, statistieken niet verzonden (d.w.z. geen analytics op de campagne) en belangrijker nog, de volgende campagnes wordt niet gewaarschuwd totdat het toepassingsproces opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="ba849-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on the campaign) and more importantly, the next campaigns will not be notified until the application process is restarted.</span></span>

<span data-ttu-id="ba849-262">De afdrukstand of andere configuratiewijzigingen kunnen de code maken lastig zijn om te bepalen of de activiteit krijgt de achtergrond of niet, de standaardimplementatie wordt gecontroleerd of de inhoud wordt gerapporteerd als is afgesloten als de gebruiker de activiteit verlaat (ofwel door te drukken `HOME`of `BACK`) maar niet als de afdrukstand wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="ba849-262">Orientation or other configuration changes can make the code tricky to determine whether the activity goes into background or not, the standard implementation makes sure the content is reported as exited if the user leaves the activity (either by pressing `HOME` or `BACK`) but not if the orientation changes.</span></span>

<span data-ttu-id="ba849-263">Dit is het interessante deel van de implementatie:</span><span class="sxs-lookup"><span data-stu-id="ba849-263">Here is the interesting part of the implementation:</span></span>

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
                 * called so we don't have to check anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="ba849-264">Zoals u zien kunt als u aangeroepen `actionContent(this)` en vervolgens de activiteit voltooid `exitContent(this)` veilig kan worden aangeroepen zonder geen effect.</span><span class="sxs-lookup"><span data-stu-id="ba849-264">As you can see, if you called `actionContent(this)` then finished the activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
<span data-ttu-id="ba849-265">[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html</span><span class="sxs-lookup"><span data-stu-id="ba849-265">[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html</span></span>
<span data-ttu-id="ba849-266">[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html</span><span class="sxs-lookup"><span data-stu-id="ba849-266">[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html</span></span>
