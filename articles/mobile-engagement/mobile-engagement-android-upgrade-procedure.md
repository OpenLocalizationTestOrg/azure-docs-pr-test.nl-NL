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
# <a name="upgrade-procedures"></a>Upgradeprocedures
Als u hebt al een oudere versie van onze SDK geïntegreerd in uw toepassing, hebt u tooconsider Hallo volgende punten bij het upgraden van Hallo SDK.

Mogelijk hebt u toofollow verschillende procedures als u verschillende versies van Hallo SDK gemist. Bijvoorbeeld als u migreert vanaf 1.4.0 too1.6.0 hebt toofirst Volg Hallo ' van 1.4.0 too1.5.0 ' procedure vervolgens Hallo ' van 1.5.0 too1.6.0 ' procedure.

Welke Hallo-versie die u bijwerkt, hebt u tooreplace hello `mobile-engagement-VERSION.jar` Hello nieuwe.

## <a name="from-420-too421"></a>Van 4.2.0 too4.2.1
Deze stap kunt daadwerkelijk worden uitgevoerd op elke versie van Hallo SDK en een beveiligingsverbetering is wanneer u integreert Reach-activiteiten.

U moet nu toevoegen `exported="false"` tooall Reach-activiteiten.

Reach activiteiten ziet er nu als volgt op uw `AndroidManifest.xml`:

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

## <a name="from-400-too410"></a>Van 4.0.0 too4.1.0
Hallo SDK nu ingang nieuwe machtiging model van Android M.

Als u functies van de locatie of grote afbeelding meldingen Lees [in deze sectie](mobile-engagement-android-integrate-engagement.md#android-m-permissions).

Bovendien toohello nieuwe machtiging model, er wordt nu ondersteuning voor het configureren van locatie-onderdelen tijdens runtime.
We zijn nog steeds compatibel zijn met de Hallo manifest parameters voor de locatie, maar gedeprecieerd. toouse-runtime-configuratie verwijderen Hallo volgende secties van uw ``AndroidManifest.xml``:

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

en gelezen [procedure wordt dit bijgewerkt](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse runtime-configuratie in plaats daarvan.

## <a name="from-300-too400"></a>Van 3.0.0 too4.0.0
### <a name="native-push"></a>Native pushberichten
Native pushberichten (GCM/ADM) is nu ook gebruikt voor in de app-meldingen zodat u Hallo native pushreferenties voor elk type pushcampagne moet configureren.

Als dat niet al Volg [deze procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).

### <a name="androidmanifestxml"></a>AndroidManifest.xml
Reach-integratie is gewijzigd in ``AndroidManifest.xml``.

Vervang deze waarde:

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

Door

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

Er is mogelijk een scherm laden nu wanneer u klikt u op een aankondiging (met tekst of web content) of een poll.
U hebt tooadd dit voor deze toowork campagnes in 4.0.0:

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a>Resources
Hallo nieuwe insluiten `res/layout/engagement_loading.xml` -bestand in uw project.

## <a name="from-240-too300"></a>Van 2.4.0 too3.0.0
Hallo hieronder wordt beschreven hoe toomigrate een SDK-integratie van Hallo Capptain service aangeboden door Capptain SAS in een app die is aangedreven door Azure Mobile Engagement. Als u vanaf een eerdere versie migreert, Raadpleeg Hallo Capptain website toomigrate too2.4.0 eerst en vervolgens toepassen Hallo procedure te volgen.

> [!IMPORTANT]
> Capptain Mobile Engagement zijn niet Hallo dezelfde services en Hallo onderstaande procedure alleen highlights hoe toomigrate Hallo client-app. Migreren Hallo SDK in Hallo-app wordt niet uw gegevens migreren vanaf Hallo Capptain servers toohello Mobile Engagement-servers.
> 
> 

### <a name="jar-file"></a>JAR-bestand
Vervang `capptain.jar` door `mobile-engagement-VERSION.jar` in uw `libs` map.

### <a name="resource-files"></a>Bronbestanden
Elke resource-bestand dat wordt geleverd (voorafgegaan door `capptain_`), is toobe vervangen door nieuwe hello (voorafgegaan door `engagement_`).

Als u deze bestanden hebt aangepast, hebt u toore-aanpassing toepassen op nieuwe bestanden hello, **alle Hallo-id's in de bronbestanden Hallo ook zijn gewijzigd**.

### <a name="application-id"></a>Toepassings-id
Nu Engagement maakt gebruik van een verbinding tekenreeks tooconfigure Hallo SDK-id's zoals Hallo toepassings-id.

U hebt toouse `EngagementAgent.init` methode in uw activiteiten starten als volgt:

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

Hallo-verbindingsreeks voor uw toepassing wordt weergegeven op de Azure Portal.

Verwijder geen enkele aanroep te`CapptainAgent.configure` als `EngagementAgent.init` vervangt deze methode.

Hallo `appId` kunnen niet meer worden geconfigureerd met `AndroidManifest.xml`.

Verwijder dit gedeelte van uw `AndroidManifest.xml` als u deze hebt:

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a>Java-API
Elke aanroep tooany Java-klasse van onze SDK heeft toobe gewijzigd; bijvoorbeeld: `CapptainAgent.getInstance(this)` naam moet worden gewijzigd `EngagementAgent.getInstance(this)`, `extends CapptainActivity` naam moet worden gewijzigd `extends EngagementActivity` enzovoort...

Als u met standaard agent voorkeursextensie bestanden zijn geïntegreerd, Hallo standaardbestandsnaam is nu `engagement.agent` en Hallo sleutel `engagement:agent`.

Bij het maken van web-aankondigingen Hallo Javascript binder is nu `engagementReachContent`.

### <a name="androidmanifestxml"></a>AndroidManifest.xml
Een groot aantal wijzigingen hebben plaatsgevonden er, Hallo-service is niet meer gedeeld en veel ontvangers kunnen niet worden geëxporteerd meer.

Hallo servicedeclaratie is nu eenvoudiger; Hallo opzet filter en alle metagegevens erin te verwijderen en toevoegen `exportable=false`.

Bovendien alles hernoemde toouse engagement is.

Nu ziet er als:

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

Als u wilt dat tooenable test logboeken Hallo meta-gegevens nu zijn toohello toepassing tag verplaatst en de naam is gewijzigd:

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

Alle andere metagegevens NET zijn gewijzigd, wordt hier Hallo volledige lijst (natuurlijk rename alleen hello die u gebruikt):

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

Google Play en SmartAd bijhouden is verwijderd van de SDK u net hebt tooremove dit zonder vervanging:

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

Hallo Reach-activiteiten, worden nu als volgt gedefinieerd:

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

Als u aangepaste Reach-activiteiten hebt, moet u enige toochange Hallo opzet acties toomatch ofwel `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` of `com.microsoft.azure.engagement.reach.intent.action.POLL`.

Hallo broadcast ontvangers zijn gewijzigd, plus we nu toevoegen `exported=false`. Hier volgt Hallo volledige lijst met ontvangers Hallo met Hallo nieuwe specificatie (natuurlijk rename alleen hello die u gebruikt):

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

Het bijhouden van de ontvanger is verwijderd, zodat u deze sectie tooremove hebt:

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

Opmerking dat Hallo declaratie van uw implementatie van Hallo ontvanger broadcast **EngagementMessageReceiver** is gewijzigd in Hallo `AndroidManifest.xml`. Dit is omdat Hallo API toosend en verwijderen van willekeurige XMPP van willekeurige XMPP entiteiten berichten en Hallo API toosend en ontvangen van berichten tussen apparaten die zijn verwijderd. Zo hebt u ook toodelete Hallo na retouraanroepen uit uw **EngagementMessageReceiver** implementatie:

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

en

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

Verwijder op geen enkele aanroep **EngagementAgent** voor:

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

en

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a>Proguard
Proguard configuratie kan worden beïnvloed door rebranding, Hallo regels zijn nu ziet eruit als:

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

