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
# <a name="how-toointegrate-engagement-reach-on-android"></a>Hoe tooIntegrate Engagement bereiken op Android
> [!IMPORTANT]
> U moet volgen Hallo integratie procedure wordt beschreven in Hallo hoe tooIntegrate Engagement op Android-document voordat u deze handleiding.
> 
> 

## <a name="standard-integration"></a>Standaard-integratie

Kopieer de Reach-bronbestanden van Hallo SDK in uw project:

* Hallo-bestanden kopiëren van Hallo `res/layout` map geleverd met Hallo SDK in Hallo `res/layout` map van uw toepassing.
* Hallo-bestanden kopiëren van Hallo `res/drawable` map geleverd met Hallo SDK in Hallo `res/drawable` map van uw toepassing.

Bewerk uw `AndroidManifest.xml` bestand:

* Toevoegen van de volgende sectie hello (tussen Hallo `<application>` en `</application>` labels):
  
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
* U moet deze machtiging tooreplay systeemmeldingen die niet is geklikt tijdens het opstarten (anders ze op schijf worden behouden, maar niet meer weergegeven, moet u echt tooinclude dit).
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* Geef een pictogram dat wordt gebruikt voor meldingen (zowel in-app en het systeem die zijn) door te kopiëren en bewerken Hallo sectie volgen (tussen Hallo `<application>` en `</application>` labels):
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> Deze sectie is **verplichte** als u van plan systeemmeldingen gebruiken bent bij het maken van Reach-campagnes. Android wordt voorkomen dat systeemmeldingen zonder pictogrammen wordt weergegeven. Dus als u deze sectie weglaat, uw eindgebruikers tooreceive kunnen niet worden ze.
> 
> 

* Als u campagnes met systeemmeldingen met behulp van de grote afbeelding maakt, moet u tooadd Hallo volgende machtigingen (na Hallo `</application>` tag) indien deze ontbreken:
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * Op Android M en als uw toepassing gericht op Android-API-niveau 23 of hoger, ``WRITE_EXTERNAL_STORAGE`` machtiging vereist goedkeuring van een gebruiker. Lees [in deze sectie](mobile-engagement-android-integrate-engagement.md#android-m-permissions).
* Bereiken voor systeemmeldingen die u ook in Hallo opgeven kunt campagne als Hallo apparaat moet ring en/of trillen. Voor deze toowork, hebt u zeker dat u na machtiging Hallo gedeclareerd toomake (na Hallo `</application>` tag):
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  Zonder deze machtiging Android voorkomt u dat systeemmeldingen worden weergegeven als u dit selectievakje inschakelt Hallo ring of Hallo Trillen optie in Hallo bereiken campagnebeheer.

## <a name="native-push"></a>Native Pushberichten
Nu u de Reach-module hebt geconfigureerd, moet u tooconfigure native pushberichten toobe kunnen tooreceive Hallo campagnes op Hallo-apparaat.

We ondersteunen twee services op Android:

* Google Play-apparaten: Gebruik [Google Cloud Messaging] door de volgende Hallo [hoe tooIntegrate GCM met Engagement begeleiden](mobile-engagement-android-gcm-integrate.md) handleiding.
* Amazon-apparaten: Gebruik [Amazon Device Messaging] door de volgende Hallo [hoe tooIntegrate ADM met Engagement begeleiden](mobile-engagement-android-adm-integrate.md) handleiding.

Als u wilt dat tootarget Amazon- en Google Play-apparaten, de mogelijke toohave alles binnen 1 AndroidManifest.xml/APK voor ontwikkeling. Maar bij het indienen van tooAmazon, kunnen ze uw toepassing afwijzen als ze GCM code vinden.

In dat geval moet u meerdere APKs gebruiken.

**Uw toepassing is nu gereed tooreceive en weergeven reach-campagnes!**

## <a name="how-toohandle-data-push"></a>Hoe gegevens toohandle push
### <a name="integration"></a>Integratie
Als u wilt dat uw toepassing toobe kunnen tooreceive Reach-gegevens-pushes, krijgt u toocreate een subklasse zijn van `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` en ernaar wordt verwezen in Hallo `AndroidManifest.xml` bestand (tussen Hallo `<application>` en/of `</application>` labels):

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

Vervolgens kunt u Hallo overschrijven `onDataPushStringReceived` en `onDataPushBase64Received` retouraanroepen. Hier volgt een voorbeeld:

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

### <a name="category"></a>Category
Hallo categorieparameter is optioneel bij het maken van een campagne Push-gegevens en kunt dat u gegevens toofilter pushes. Dit is handig als u verschillende broadcast ontvangers afhandeling van verschillende soorten gegevens-pushes hebt of als u wilt dat de verschillende typen toopush van `Base64` gegevens en wilt tooidentify hun type voordat ze worden geparseerd.

### <a name="callbacks-return-parameter"></a>De retouraanroepen retourparameter
Hier volgen enkele richtlijnen tooproperly ingang Hallo retourparameter van `onDataPushStringReceived` en `onDataPushBase64Received`:

* Een ontvanger broadcast moet retourneren `null` in Hallo retouraanroep als het niet weet hoe een data toohandle push. U moet Hallo categorie toodetermine gebruiken of uw broadcast ontvanger Hallo gegevens-push of niet verwerken moet.
* Een van de Hallo broadcast ontvanger moet retourneren `true` in Hallo retouraanroep als het gegevens-push Hallo accepteert.
* Een van de Hallo broadcast ontvanger moet retourneren `false` in Hallo retouraanroep als Hallo gegevens-push herkent, maar deze om welke reden dan ook negeert. Bijvoorbeeld retourneren `false` wanneer Hallo ontvangen gegevens zijn ongeldig.
* Als een ontvanger retourneert broadcast `true` terwijl een andere een retourneert `false` voor hello dezelfde gegevens-push, Hallo gedrag niet gedefinieerd is, moet u nooit doen die.

Hallo-retourtype wordt alleen gebruikt voor Hallo Reach statistieken:

* `Replied`Als een van de Hallo broadcast ontvangers ofwel geretourneerd wordt verhoogd `true` of `false`.
* `Actioned`alleen als een van de Hallo ontvangers geretourneerd wordt verhoogd `true`.

## <a name="how-toocustomize-campaigns"></a>Hoe toocustomize campagnes
toocustomize campagnes, kunt u Hallo-indelingen die beschikbaar zijn in Hallo SDK bereiken wijzigen.

U moet alle Hallo id's die worden gebruikt in Hallo indelingen houden en Hallo typen Hallo weergaven die gebruikmaken van een id in, met name voor tekst en afbeeldingen weergaven houden. Sommige weergaven zijn alleen gebruikte toohide of gebieden weergeven, zodat hun type kan worden gewijzigd. Controleer de broncode Hallo als u toochange Hallo-type van een weergave in de indelingen Hallo opgegeven.

### <a name="notifications"></a>Meldingen
Er zijn twee typen meldingen: systeem en in-app-meldingen die andere indelingsbestanden gebruiken.

#### <a name="system-notifications"></a>Systeemmeldingen
toocustomize systeemmeldingen moet u toouse hello **categorieën**. U kunt te gaan[categorieën](#categories).

#### <a name="in-app-notifications"></a>In-app-meldingen
Een in-app-melding is standaard een weergave die dynamisch worden toegevoegd toohello huidige activiteit gebruiker Bedankt toohello Android interfacemethode `addContentView()`. Dit is een melding overlay genoemd. Melding overlays zijn ideaal voor een snelle integratie omdat ze geen toomodify u elke lay-out in uw toepassing vereisen.

toomodify hello uiterlijk van uw notification overlays, kunt u eenvoudig hello bestand wijzigen `engagement_notification_area.xml` tooyour nodig heeft.

> [!NOTE]
> Hallo bestand `engagement_notification_overlay.xml` is een gebruikte toocreate een overlay melding Hallo waaronder Hallo bestand `engagement_notification_area.xml`. U kunt het ook aanpassen toosuit uw behoeften (bijvoorbeeld voor het systeemvak Hallo binnen Hallo overlay plaatsing).
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a>Indeling van de melding als onderdeel van de indeling van een activiteit bevatten
Overlays zijn ideaal voor een snelle integratie, maar worden onhandig of neveneffecten hebben in bijzondere gevallen. Hallo-overlay-systeem kan op een activiteitenniveau van de, zodat u eenvoudig tooprevent bijwerkingen voor speciale activiteiten worden aangepast.

U kunt ervoor kiezen tooinclude onze lay-out voor de melding in uw bestaande lay-out met vriendelijke groet toohello Android **omvatten** instructie. Hallo Hieronder volgt een voorbeeld van een gewijzigd `ListActivity` lay-out die net bevat een `ListView`.

**Voordat de Engagement-integratie:**

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

**Na de Engagement-integratie:**

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

In dit voorbeeld hebben we een bovenliggende container toegevoegd, omdat de oorspronkelijke indeling Hallo een lijstweergave als bovenste niveau element Hallo gebruikt. We hebben ook toegevoegd `android:layout_weight="1"` toobe kunnen tooadd hieronder een lijstweergave in een weergave die zijn geconfigureerd met `android:layout_height="fill_parent"`.

Hallo Engagement bereiken SDK detecteert automatisch die Hallo notification-indeling is opgenomen in deze activiteit en een overlay voor deze activiteit wordt niet worden toegevoegd.

> [!TIP]
> Als u een ListActivity in uw toepassing gebruikt, een zichtbaar Reach-overlay wordt voorkomen dat u kruisreagerende tooclicked items in de lijstweergave Hallo meer. Dit is een bekend probleem. toowork om dit probleem we raden u tooembed Hallo melding indeling in de indeling van uw eigen lijst activiteit zoals in het vorige voorbeeld Hallo.
> 
> 

##### <a name="disabling-application-notification-per-activity"></a>Het uitschakelen van de melding per activiteit
Als u niet Hallo wilt overlay toobe tooyour activiteit toegevoegd en als u geen Hallo melding lay-out in uw eigen lay-out, kunt u uitschakelen Hallo overlay voor deze activiteit in Hallo `AndroidManifest.xml` door toe te voegen een `meta-data` sectie, zoals in de volgende Hallo Voorbeeld:

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <a name="categories"></a>Categorieën
Als u Hallo opgegeven indelingen wijzigt, wijzigt u Hallo uiterlijk van al uw meldingen. Categorieën kunnen toodefine u die verschillende gericht lijkt (mogelijk gedrag) voor meldingen. Een categorie kan worden opgegeven wanneer u een Reach-campagne maken. Houd er rekening mee dat categorieën ook kunnen u aanpassen aankondigingen en polls, die verderop in dit document wordt beschreven.

tooregister een categorie-handler voor uw meldingen, moet u een aanroep van tooadd wanneer de toepassing hello wordt geïnitialiseerd.

> [!IMPORTANT]
> Lees de waarschuwing over Hallo android: proces kenmerk Hallo \<android-sdk-engagement-process\> in Hallo hoe tooIntegrate Engagement op Android onderwerp voordat u doorgaat.
> 
> 

Hallo volgende voorbeeld wordt ervan uitgegaan dat u Hallo vorige waarschuwing bevestigd en gebruikt een subklasse zijn van `EngagementApplication`:

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

Hallo `MyNotifier` object is Hallo-implementatie van Hallo melding categorie-handler. Het is ofwel een implementatie van Hallo `EngagementNotifier` -interface of een subklasse van Hallo standaardimplementatie: `EngagementDefaultNotifier`.

Let op Hallo van dezelfde melder verscheidene categorieën kan verwerken, kunt u deze registreren als volgt:

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

tooreplace hello categorie standaardimplementatie, kunt u uw implementatie zoals registreren in Hallo voorbeeld te volgen:

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

Hallo huidige categorie gebruikt in een handler is doorgegeven als een parameter in de meeste methoden kunt u overschrijven `EngagementDefaultNotifier`.

Deze is doorgegeven als een `String` parameter of indirect in een `EngagementReachContent` object waarvoor een `getCategory()` methode.

U kunt de meeste Hallo-proces voor het maken van notification wijzigen door gaat herdefiniëren methoden op `EngagementDefaultNotifier`, voor meer geavanceerde aanpassingen van mening bent dat gratis tootake bekijken op Hallo technische documentatie en op Hallo broncode.

##### <a name="in-app-notifications"></a>In-app-meldingen
Als u alleen toouse alternatieve indelingen voor een specifieke categorie wilt, kunt u dit implementeren als Hallo voorbeeld te volgen in:

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

**Voorbeeld van `my_notification_overlay.xml` :**

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

Zoals u ziet, is Hallo overlay weergave-id anders dan Hallo standaard één. Het is belangrijk dat elke indeling een unieke id voor overlays gebruiken.

**Voorbeeld van `my_notification_area.xml` :**

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

Zoals u ziet, is Hallo melding gebied weergave-id anders dan Hallo standaard één. Het is belangrijk dat elke indeling wordt gebruikt voor een unieke id voor de melding gebieden.

Dit eenvoudige voorbeeld van de categorie kunt u een toepassing (of in-app) meldingen weergegeven Hallo boven aan het welkomstscherm. Er is niet veranderd Hallo standaard-id's in systeemvak Hallo zelf.

Als u wilt dat er tooredefine hello toochange `EngagementDefaultNotifier.prepareInAppArea` methode. Het raadzaam toolook op Hallo technische documentatie en op de broncode Hallo van `EngagementNotifier` en `EngagementDefaultNotifier` als u wilt dat dit niveau van Geavanceerd aanpassen.

##### <a name="system-notifications"></a>Systeemmeldingen
Door uit te breiden `EngagementDefaultNotifier`, kunt u overschrijven `onNotificationPrepared` tooalter Hallo melding die is voorbereid door Hallo standaardimplementatie.

Bijvoorbeeld:

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

In dit voorbeeld wordt een Systeemmelding voor een inhoud wordt weergegeven als een continue gebeurtenis wanneer Hallo 'continue'-categorie wordt gebruikt.

Als u wilt dat toobuild hello `Notification` object vanaf het begin, kunt u terugkeren `false` toohello methode en aanroep `notify` uzelf op Hallo `NotificationManager`. In dat geval is het belangrijk dat u een `contentIntent`, een `deleteIntent` en bericht-id die wordt gebruikt door Hallo `EngagementReachReceiver`.

Hier volgt een voorbeeld van een dergelijke implementatie:

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

##### <a name="notification-only-announcements"></a>Aankondigingen met alleen een melding
Hallo management Hallo klikt u op een melding alleen aankondiging kan worden aangepast door het overschrijven van `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify Hallo voorbereid `Intent`. Met deze methode kunt u tootune Hallo vlaggen eenvoudig.

Bijvoorbeeld tooadd hello `SINGLE_TOP` vlag:

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

Voor oudere Engagement gebruikers, houd er rekening mee dat systeemmeldingen zonder actie URL nu Hallo toepassing start als deze op de achtergrond, zodat deze methode kan worden aangeroepen met een aankondiging zonder actie-URL. U moet rekening houden met die bij het aanpassen van Hallo opzet.

U kunt ook implementeren `EngagementNotifier.executeNotifAnnouncementAction` vanaf het begin.

##### <a name="notification-life-cycle"></a>Levenscyclus van de kennisgeving
Wanneer u de standaardcategorie hello, een aantal methoden levenscyclus worden aangeroepen op Hallo `EngagementReachInteractiveContent` tooreport statistieken en update Hallo campagne status object:

* Wanneer Hallo melding wordt weergegeven in de toepassing of op de statusbalk hello plaatsen, Hallo `displayNotification` methode (die statistieken) wordt aangeroepen door `EngagementReachAgent` als `handleNotification` retourneert `true`.
* Als het Hallo-melding wordt gesloten, Hallo `exitNotification` methode wordt aangeroepen, statistiek wordt gerapporteerd en volgende campagnes kunnen nu worden verwerkt.
* Als u Hallo melding klikt, `actionNotification` is aangeroepen, statistiek gemeld en wordt intentie Hallo die zijn gekoppeld wordt gestart.

Als uw implementatie van `EngagementNotifier` omleidingen Hallo standaardgedrag, hebt u toocall deze methoden van de levenscyclus van de door u zelf. Hallo volgen voorbeelden illustreren bepaalde gevallen waarbij Hallo standaardgedrag wordt overgeslagen:

* U kunt niet uitbreiden `EngagementDefaultNotifier`, zoals u categorie verwerking helemaal geïmplementeerd.
* Voor systeemmeldingen, u Hallo overrode `onNotificationPrepared` en u aangepast `contentIntent` of `deleteIntent` in Hallo `Notification` object.
* Voor in-app-meldingen, u overrode `prepareInAppArea`, moet u ervoor dat toomap ten minste `actionNotification` tooone uw U.I-besturingselementen.

> [!NOTE]
> Als `handleNotification` er wordt een uitzondering, Hallo inhoud is verwijderd en `dropContent` wordt aangeroepen. Dit wordt gemeld in statistieken en volgende campagnes kunnen nu worden verwerkt.
> 
> 

### <a name="announcements-and-polls"></a>Aankondigingen en polls
#### <a name="layouts"></a>Indelingen
U kunt wijzigen Hallo `engagement_text_announcement.xml`, `engagement_web_announcement.xml` en `engagement_poll.xml` toocustomize tekst aankondigingen, web aankondigingen en polls bestanden.

Deze bestanden delen twee algemene indelingen voor Hallo titel gebieden en Hallo knop. Hallo-indeling voor Hallo titel is `engagement_content_title.xml` en maakt gebruik van Hallo eponymous drawable-bestand voor Hallo achtergrond. Hallo lay-out voor de actie en afsluiten knoppen Hallo is `engagement_button_bar.xml` en maakt gebruik van Hallo eponymous drawable-bestand voor Hallo achtergrond.

Hallo vraag lay-out in een poll en hun keuzes dynamisch worden vergroot met behulp van verschillende keren Hallo `engagement_question.xml` indelingsbestand voor Hallo vragen en Hallo `engagement_choice.xml` -bestand voor Hallo keuzes.

#### <a name="categories"></a>Categorieën
##### <a name="alternate-layouts"></a>Alternatieve indelingen
Zoals meldingen, kan de categorie van de campagne Hallo gebruikte toohave alternatieve indelingen voor uw aankondigingen en polls zijn.

Bijvoorbeeld, toocreate een categorie voor een aankondiging tekst, die u kunt uitbreiden `EngagementTextAnnouncementActivity` en verwijst u Hallo `AndroidManifest.xml` bestand:

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

Houd er rekening mee die categorie Hallo in Hallo bedoeling filter wordt gebruikt toomake Hallo verschil met Hallo aankondiging standaardactiviteit.

Hallo bereiken SDK Hallo opzet system tooresolve Hallo juiste activiteit gebruikt voor een specifieke categorie en vallen terug op Hallo standaardcategorie als Hallo omzetting is mislukt.

Hebt u tooimplement `MyCustomTextAnnouncementActivity`, als u alleen toochange Hallo indeling wilt (maar houd Hallo dezelfde id's weergeven), u hoeft alleen toodefine Hallo klasse zoals in het volgende voorbeeld Hallo:

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

tooreplace hello standaardcategorie van aankondigingen van tekst, vervang gewoon `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` door uw implementatie.

Web-aankondigingen en polls kunnen worden aangepast op soortgelijke wijze.

U kunt uitbreiden voor web-aankondigingen `EngagementWebAnnouncementActivity` en de activiteit in Hallo declareren `AndroidManifest.xml` zoals in het volgende voorbeeld Hallo:

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

U kunt uitbreiden voor polls `EngagementPollActivity` en uw in Hallo declareren `AndroidManifest.xml` in Hallo voorbeeld te volgen, zoals:

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a>Implementatie maken
U kunt categorieën voor uw activiteiten aankondiging (en de poll) implementeren zonder een Hallo `Engagement*Activity` klassen die worden geleverd door Hallo SDK bereiken. Dit is bijvoorbeeld handig als u wilt dat toodefine een indeling die niet dezelfde bekijkt hello worden gebruikt als standaard Hallo-indelingen.

Net als voor geavanceerde melding aanpassing, wordt aangeraden toolook op Hallo broncode van de standaardimplementatie Hallo.

Hier volgen enkele dingen tookeep rekening: Reach Hallo activiteit met een specifiek doel (overeenkomende toohello opzet filter), plus een extra parameter Hallo inhouds-id wordt gestart.

tooretrieve hello inhoudsobject waarin Hallo velden die u hebt opgegeven wanneer het maken van Hallo campagne op Hallo website u kunt dit doen:

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

U moet voor statistics rapporteert Hallo inhoud wordt weergegeven in Hallo `onResume` gebeurtenis:

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

Vervolgens moet u niet vergeten toocall ofwel `actionContent(this)` of `exitContent(this)` op Hallo inhoud object voordat de achtergrond probeert het Hallo-activiteit.

Als niet aan te ofwel roepen `actionContent` of `exitContent`, statistieken niet verzonden (d.w.z. geen analytics op Hallo campagne) en meer belangrijker nog, Hallo volgende campagnes wordt niet gewaarschuwd als het toepassingsproces Hallo opnieuw is gestart.

Afdrukstand of andere configuratiewijzigingen kunnen Hallo code lastig toodetermine maken of Hallo activiteit krijgt de achtergrond of niet, Hallo standaardimplementatie zorgt ervoor dat ervoor Hallo inhoud wordt gerapporteerd als is afgesloten als Hallo gebruiker Hallo-activiteit (via een verlaat drukken `HOME` of `BACK`) maar niet als Hallo afdrukstand wordt gewijzigd.

Hier Hallo interessante deel uitmaakt van Hallo implementatie:

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

Zoals u zien kunt als u aangeroepen `actionContent(this)` en klaar bent met het Hallo-activiteit `exitContent(this)` veilig kan worden aangeroepen zonder geen effect.

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
