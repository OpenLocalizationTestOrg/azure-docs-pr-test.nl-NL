---
title: aaaSending Secure Pushmeldingen met Azure Notification Hubs
description: Meer informatie over hoe toosend beveiligde push-meldingen tooan Android-app van Azure. Codevoorbeelden geschreven in Java en C#.
documentationcenter: android
keywords: push-melding, pushmeldingen, push-berichten, android pushmeldingen
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a>Beveiligde Pushmeldingen verzenden met Azure Notification Hubs
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Overzicht
> [!IMPORTANT]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started) voor meer informatie.
> 
> 

Push notification-ondersteuning in Microsoft Azure kunt u tooaccess een push eenvoudig te gebruiken, meerdere platforms, uitgebreid bericht-infrastructuur, die sterk vereenvoudigd Hallo-implementatie van pushmeldingen voor consumenten- en enterprise-toepassingen voor mobiele platforms.

Vanwege beperkingen voor tooregulatory of beveiliging kunt soms een toepassing tooinclude iets in Hallo-bericht dat via Hallo standaard push notification-infrastructuur kan niet worden verzonden. Deze zelfstudie wordt beschreven hoe tooachieve dezelfde ervaring Hallo door te sturen van gevoelige gegevens via een veilige en geverifieerde verbinding tussen Hallo client Android-apparaat en back-end Hallo app.

Op een hoog niveau is Hallo-stroom als volgt uit:

1. Hallo back-end van app:
   * Winkels beveiligde nettolading in back-enddatabase.
   * Hallo-ID van deze melding toohello Android-apparaat (geen beveiligde gegevens verzonden) verzendt.
2. Hallo-app op Hallo apparaat tijdens het Hallo-bericht ontvangen:
   * Hallo Android-apparaat neemt contact op Hallo back-end aanvragende Hallo beveiligde nettolading.
   * Hallo-app kunt Hallo nettolading weergeven als een melding op Hallo-apparaat.

Het is belangrijk dat in de voorgaande stroom Hallo (en in deze zelfstudie), gaan we ervan uit dat apparaat Hallo toonote slaat geen verificatietoken in lokale opslag nadat Hallo gebruiker zich aanmeldt. Dit garandeert een volledig naadloze ervaring als apparaat Hallo Hallo melding van beveiligde nettolading met dit token kan ophalen. Als uw toepassing slaat geen verificatietokens op Hallo-apparaat, of als deze tokens kunnen verlopen, moet een algemene melding vragen Hallo gebruiker toolaunch Hallo app Hallo apparaat app bij ontvangst van Hallo push-melding worden weergegeven. Hallo-app vervolgens verifieert de gebruiker Hallo en toont de nettolading van de Hallo-meldingen.

Deze zelfstudie laat zien hoe toosend beveiligde pushmeldingen. Dit is gebaseerd op Hallo [gebruikers waarschuwen](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) zelfstudie, dus u eerst te Hallo stappen in deze zelfstudie voltooien moet als u dat nog niet gedaan hebt.

> [!NOTE]
> Deze zelfstudie wordt ervan uitgegaan dat u hebt gemaakt en uw notification hub geconfigureerd zoals beschreven in [aan de slag met Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a>Hallo Android-project wijzigen
Nu dat u uw app back-end toosend alleen Hallo gewijzigd *id* van een push-melding hebt toochange uw Android-app toohandle melding en terugbellen secure uw back-end tooretrieve Hallo bericht toobe weergegeven.
tooachieve deze doelstelling moeten er toomake ervoor dat uw Android-app weet hoe tooauthenticate zelf met uw back-end wanneer het Hallo-pushmeldingen ontvangt.

Er wordt nu Hallo wijzigen *aanmelding* stroom in volgorde toosave Hallo verificatie headerwaarde in Hallo gedeelde voorkeuren van uw app. Vergelijkbaar mechanismen kunnen worden gebruikt toostore een verificatietoken (bijvoorbeeld OAuth tokens) voor die app Hallo toouse zonder gebruikersreferenties hebben.

1. In uw Android-app-project toevoegen na constanten bovenaan Hallo HALLO hallo **MainActivity** klasse:
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. Nog steeds in Hallo **MainActivity** klasse, update Hallo `getAuthorizationHeader()` methode toocontain Hallo code te volgen:
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. Voeg de volgende Hallo `import` instructies boven Hallo Hallo **MainActivity** bestand:
   
        import android.content.SharedPreferences;

Nu wijzigen we Hallo-handler die wordt aangeroepen wanneer het Hallo-melding is ontvangen.

1. In Hallo **MyHandler** klasse wijzigen Hallo `OnReceive()` methode toocontain:
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. Voeg vervolgens Hallo `retrieveNotification()` methode Hallo tijdelijke aanduiding vervangt `{back-end endpoint}` met Hallo backend-eindpunt is verkregen tijdens de implementatie van uw back-end:
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

Deze methode roept uw back-end tooretrieve hello appmelding inhoud met behulp van Hallo referenties opgeslagen in Hallo gedeelde voorkeuren en geeft deze weer als een normale melding. Hallo-melding ziet er toohello app gebruiker net als andere push-melding.

Houd er rekening mee dat het is beter toohandle Hallo gevallen van eigenschap van de header ontbreekt verificatie of afwijzing door Hallo back-end. Hallo specifieke verwerking van deze gevallen afhankelijk zijn van voornamelijk op de doel-gebruikerservaring. Een mogelijkheid is toodisplay een melding met een algemene Hallo tooauthenticate tooretrieve Hallo werkelijke gebruikersmelding wordt gevraagd.

## <a name="run-hello-application"></a>Hallo toepassing uitvoeren
toorun toepassing hello, Hallo te volgen:

1. Zorg ervoor dat **AppBackend** is geïmplementeerd in Azure. Als Visual Studio, voert u Hallo **AppBackend** Web API-toepassing. Een ASP.NET-webpagina wordt weergegeven.
2. Voer in Eclipse Hallo-app op een fysieke Android-apparaat of Hallo-emulator.
3. Voer een gebruikersnaam en wachtwoord in Hallo Android-app gebruikersinterface. Deze kunnen zich een willekeurige tekenreeks, maar ze moet dezelfde waarde Hallo.
4. Klik in Hallo Android-app UI **aanmelden**. Klik vervolgens op **push verzenden**.

