---
title: aaaGet de slag met Azure Notification Hubs die gebruikmaken van Baidu | Microsoft Docs
description: In deze zelfstudie leert u hoe toouse Azure Notification Hubs toopush meldingen tooAndroid apparaten gebruikmaken van Baidu.
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a>Aan de slag met Azure Notification Hubs die gebruikmaken van Baidu
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Overzicht
Baidu cloud push is een Chinese cloudservice waarmee u toosend push notifications toomobile apparaten kunt. Deze service is handig in China, waar leveren van pushmeldingen tooAndroid is complex vanwege Hallo aanwezigheid van verschillende app stores en push services, Daarnaast toohello beschikbaarheid van Android-apparaten die niet doorgaans verbonden tooGCM (Google zijn Cloud Messaging).

## <a name="prerequisites"></a>Vereisten
Voor deze zelfstudie hebt u het volgende nodig:

* Android SDK (Aannemende dat u Eclipse gebruikt), die u via Hallo downloaden kunt <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android-site</a>
* [Android-SDK voor Mobile Services]
* [Android SDK Baidu Push]

> [!NOTE]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F) voor meer informatie.
> 
> 

## <a name="create-a-baidu-account"></a>Een Baidu-account maken
toouse Baidu, moet u een Baidu-account hebben. Als u al hebt, meldt u zich in toohello [Baidu portal] en toohello volgende stap overslaan. Raadpleeg anders Hallo instructies te volgen over het toocreate een Baidu-account.  

1. Ga toohello [Baidu portal] en klik op Hallo**登录**(**aanmelding**) koppelen. Klik op**立即注册**toostart Hallo account registratieproces.
   
   ![][1]
2. Voer details voor Hallo vereist: telefoon, e-mailadres, wachtwoord en verificatiecode, en klik op **aanmelding**.
   
   ![][2]
3. U ontvangt een e-mailadres toohello e-mailadres dat u hebt ingevoerd met een koppeling tooactivate uw Baidu-account.
   
   ![][3]
4. Aanmelden tooyour e-mailaccount, open Hallo e-mailbericht en op Hallo activering koppeling tooactivate uw Baidu-account.
   
   ![][4]

Zodra u een geactiveerde Baidu-account hebt, meld u bij toohello [Baidu portal].

## <a name="register-as-a-baidu-developer"></a>Registreer u als een Baidu-ontwikkelaar.
1. Zodra u zich hebt aangemeld toohello [Baidu portal], klikt u op**更多 >>** (**meer**).
   
      ![][5]
2. Schuif omlaag in Hallo**站长与开发者服务 (webbeheerder en Ontwikkelaarsservices)** sectie en klik op**百度开放云平台**(**Baidu cloud-platform open**).
   
      ![][6]
3. Klik op volgende pagina Hallo**开发者服务**(**Ontwikkelaarsservices**) in de rechterbovenhoek Hallo.
   
      ![][7]
4. Klik op volgende pagina Hallo**注册开发者**(**ontwikkelaars geregistreerd**) in Hallo-menu op Hallo rechterbovenhoek.
   
      ![][8]
5. Voer uw naam, een beschrijving en een mobiel telefoonnummer in voor het ontvangen van een sms-bericht voor verificatie en klik vervolgens op **送验证码** (**Verificatiecode verzenden**). Internationaal telefoonnummer moet u tooenclose Hallo landcode tussen haakjes. Voor een nummer in de Verenigde Staten moet u bijvoorbeeld de volgende indeling gebruiken: **(1)1234567890**.
   
      ![][9]
6. U ontvangt vervolgens een SMS-bericht met een verificatiecode, zoals wordt weergegeven in Hallo voorbeeld te volgen:
   
      ![][10]
7. Voer de verificatiecode Hallo van Hallo-bericht in**验证码**(**bevestigingscode**).
8. Voltooi ten slotte Hallo developer registratie door Hallo Baidu overeenkomst te accepteren en te klikken**提交**(**indienen**). Hier ziet u Hallo volgende pagina van de registratie is gelukt:
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a>Een Baidu-cloudpushproject maken
Als u een Baidu-cloudpushproject maakt, ontvangt u uw app-id, API-sleutel en een geheime sleutel.

1. Zodra u zich hebt aangemeld toohello [Baidu portal], klikt u op**更多 >>** (**meer**).
   
      ![][5]
2. Schuif omlaag in Hallo**站长与开发者服务**(**webbeheerder en Ontwikkelaarsservices**) sectie en klik op**百度开放云平台**(**Baidu cloud-platform open**).
   
      ![][6]
3. Klik op volgende pagina Hallo**开发者服务**(**Ontwikkelaarsservices**) in de rechterbovenhoek Hallo.
   
      ![][7]
4. Klik op volgende pagina Hallo**云推送**(**Cloud Push**) van Hallo**云服务**(**Cloudservices**) sectie.
   
      ![][12]
5. Nadat u een geregistreerde ontwikkelaar bent, ziet u**管理控制台**(**beheerconsole**) op het bovenste menu Hallo. Klik op **开发者服务管理** (**Beheer van ontwikkelaarsservices**).
   
      ![][13]
6. Klik op volgende pagina Hallo**创建工程**(**Project maken**).
   
      ![][14]
7. Voer een toepassingsnaam in en klik op **创建** (**Maken**).
   
      ![][15]
8. Als u een Baidu Cloud Push-project hebt gemaakt, ziet u een pagina met de **App-id**, de **API-sleutel** en een **geheime sleutel**. Maak een notitie van Hallo API-sleutel en geheime sleutel, die we later gebruiken.
   
      ![][16]
9. Hallo-project voor pushmeldingen configureren door te klikken op**云推送**(**Cloud Push**) in het linkerdeelvenster Hallo.
   
      ![][31]
10. Klik op volgende pagina Hallo Hallo**推送设置**(**Push instellingen**) knop.
    
    ![][32]  
11. Toevoegen op de configuratiepagina Hallo Hallo pakketnaam die u in uw Android-project in Hallo gebruiken wilt**应用包名**(**toepassingspakket**) en klik vervolgens op**保存设置**() **Opslaan**).  
    
    ![][33]

U ziet Hallo**保存成功!** (**Opgeslagen!**).

## <a name="configure-your-notification-hub"></a>Uw Notification Hub configureren
1. Meld u aan toohello [klassieke Azure-Portal], en klik vervolgens op **+ nieuw** Hallo onder welkomstscherm aan.
2. Klik achtereenvolgens op **App Services**, **Service Bus**, **Notification Hub** en **Snelle invoer**.
3. Geef een naam voor uw **Notification Hub**, selecteer Hallo **regio** en Hallo **Namespace** waar deze notification hub wordt gemaakt en klik vervolgens op  **Maak een nieuwe Notification Hub**.  
   
      ![][17]
4. Klik op Hallo naamruimte waarin u uw notification hub hebt gemaakt en klik vervolgens op **Notification Hubs** Hallo bovenaan.
   
      ![][18]
5. Selecteer Hallo notification hub die u gemaakt en klik vervolgens op **configureren** in het bovenste menu Hallo.
   
      ![][19]
6. Schuif omlaag toohello **baidu meldingsinstellingen** sectie en Voer Hallo API-sleutel en geheime sleutel die u hebt verkregen via de Baidu-console Hallo eerder voor uw Baidu-cloudpushproject. Klik op **Opslaan**.
   
      ![][20]
7. Klik op Hallo **Dashboard** tabblad boven Hallo voor Hallo notification hub en klik vervolgens op **verbindingsreeks weergeven**.
   
      ![][21]
8. Maak een notitie van Hallo **DefaultListenSharedAccessSignature** en **DefaultFullSharedAccessSignature** van Hallo **toegang tot verbindingsgegevens** venster.
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a>Verbinding maken met uw app toohello notification hub
1. Maak in Eclipse ADT een nieuw Android-project (**Bestand** > **Nieuw** > **Android-toepassingsproject**).
   
    ![][23]
2. Voer een **toepassingsnaam** en zorg ervoor dat Hallo **minimale vereiste SDK** -versie is ingesteld, te**API 16: Android 4.1**.
   
    ![][24]
3. Klik op **volgende** en doorgaan na Hallo wizard totdat Hallo **activiteit maken** venster wordt weergegeven. Zorg ervoor dat **Blank Activity** is geselecteerd en selecteer vervolgens **voltooien** toocreate een nieuwe Android-toepassing.
   
    ![][25]
4. Zorg ervoor dat Hallo **doel van de Projectbuild** correct is ingesteld.
   
    ![][26]
5. Hallo notification-hubs-0.4.jar bestand downloaden van Hallo **bestanden** tabblad Hallo [Notification-Hubs-Android-SDK op Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4). Toevoegen van Hallo bestand toohello **bibliotheken** map van uw Eclipse-project en vernieuw Hallo *bibliotheken* map.
6. Downloaden en uitpakken Hallo [Android SDK Baidu Push]Open Hallo **bibliotheken** map en kopieer Hallo **pushservice x.y.z** jar-bestand en Hallo **armeabi**  &  **mips** mappen in Hallo **bibliotheken** map van uw Android-toepassing.
7. Open Hallo **AndroidManifest.xml** -bestand van uw Android-project en Hallo machtigingen die door Hallo SDK Baidu vereist zijn toevoegen.
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. Hallo toevoegen **android: name** eigenschap tooyour **toepassing** -element in **AndroidManifest.xml**en vervang *yourprojectname* (voor voorbeeld **com.example.BaiduTest**). Zorg ervoor dat deze naam overeenkomt met Hallo een die u hebt geconfigureerd in Hallo Baidu-console.
   
        <application android:name="yourprojectname.DemoApplication"
9. Hallo na binnen Hallo toepassingselement na Hallo configuratie toevoegen **. MainActivity** activiteit element vervangen *yourprojectname* (bijvoorbeeld **com.example.BaiduTest**):
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. Voeg een nieuwe klasse aangeroepen **ConfigurationSettings.java** toohello project.
    
     ![][28]
    
     ![][29]
11. Hallo code tooit volgende toevoegen:
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    Stel de waarde Hallo van **API_KEY** met wat u eerder hebt opgehaald uit de Baidu-cloudproject hello, **NotificationHubName** met de naam van uw notification hub van Hallo klassieke Azure-Portal en  **NotificationHubConnectionString** defaultlistensharedaccesssignature op van Hallo klassieke Azure-Portal.
12. Voeg een nieuwe klasse aangeroepen **DemoApplication.java**, en voeg Hallo code tooit te volgen:
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. Toevoegen van een andere nieuwe klasse met de naam **MyPushMessageReceiver.java**, en voeg Hallo code tooit te volgen. Het is Hallo-klasse die ingangen Hallo pushmeldingen die afkomstig zijn van Hallo Baidu push-server.
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. Open **MainActivity.java**, en Voeg na toohello hello **onCreate** methode:
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. Open de volgende importinstructies boven Hallo Hallo:
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a>Meldingen tooyour app verzenden
U kunt snel testen ontvangst van meldingen in uw app door meldingen te verzenden in Hallo [Azure-portal](https://portal.azure.com/) met Hallo **verzenden** knop op Hallo notification hub, zoals weergegeven in het volgende scherm Hallo:

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

Pushmeldingen worden gewoonlijk in een back-endservice zoals Mobile Services of ASP.NET verzonden met een compatibele bibliotheek. Als een bibliotheek niet beschikbaar voor uw back-end is, kunt u Hallo REST-API toosend meldingen worden rechtstreeks.

In deze zelfstudie we Houd het eenvoudig en alleen gedemonstreerd hoe u uw clientapp test door meldingen met behulp van Hallo .NET SDK voor notification hubs in een consoletoepassing in plaats van een back-endservice te verzenden. We raden aan Hallo [Notification Hubs gebruiken toopush meldingen toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) Hallo volgende stap voor het verzenden van meldingen vanuit een ASP.NET-back-end zelfstudie. Hallo volgende methoden kan echter worden gebruikt voor het verzenden van meldingen:

* **REST-Interface**: U kunt meldingen ondersteunen op elk back-end-platform Hallo met [REST-interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Microsoft Azure Notification Hubs .NET SDK**: In Hallo Nuget Package Manager voor Visual Studio, voert u [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js**: [hoe toouse Notification Hubs met Node.js](notification-hubs-nodejs-push-notification-tutorial.md).
* **Mobile Apps**: voor een voorbeeld van hoe u meldingen vanuit een back-end voor een Azure App Service Mobile Apps die geïntegreerd met Notification Hubs toosend Zie [Add push notifications tooyour mobiele app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: Zie voor een voorbeeld van hoe toosend meldingen met REST-API's Hallo ' hoe toouse Notification Hubs vanuit Java/PHP ' ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-net-console-app"></a>(Optioneel) Meldingen verzenden vanuit een .NET-console-app
In dit gedeelte behandelen we hoe u een melding vanuit een .NET-console-app kunt verzenden.

1. Maak een nieuwe Visual C#-consoletoepassing:
   
    ![][30]
2. In Hallo venster Package Manager-Console, stelt u Hallo **standaardproject** tooyour nieuwe console toepassingsproject en vervolgens in het consolevenster hello, Hallo volgende opdracht wordt uitgevoerd:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Deze instructie een verwijzing toohello Azure Notification Hubs SDK wordt toegevoegd met behulp van Hallo <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet-pakket</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. Open Hallo bestand **Program.cs** en voeg de volgende Hallo toe met de instructie:
   
        using Microsoft.Azure.NotificationHubs;
4. In uw `Program` klasse Hallo volgende methode toe en vervang *DefaultFullSharedAccessSignatureSASConnectionString* en *NotificationHubName* met Hallo-waarden die u hebt.
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. Toevoegen van de volgende regels in Hallo uw **Main** methode:
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a>Uw app testen
Deze app met een telefoon, alleen verbinding tootest Hallo phone tooyour computer via een USB-kabel. Deze actie wordt uw app naar Hallo gekoppelde telefoon geladen.

tootest deze app met Hallo-emulator op de bovenste werkbalk van Hallo Eclipse, klikt u op **uitvoeren**, en selecteer vervolgens uw app: het Hallo-emulator is geladen wordt gestart en wordt uitgevoerd Hallo app.

Hallo app Hallo 'userId' en 'channelId' opgehaald uit Hallo Baidu Push notification service en voor Hallo notification hub geregistreerd.

een Testmelding toosend, kunt u het foutopsporingstabblad Hallo Hallo klassieke Azure-Portal. Als u gebouwd Hallo .NET-consoletoepassing voor Visual Studio, druk op F5-toets Hallo in Visual Studio toorun Hallo toepassing. de toepassing Hello stuurt een melding die wordt weergegeven in de bovenste systeemvak Hallo van uw apparaat of emulator.

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[Android-SDK voor Mobile Services]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Android SDK Baidu Push]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[klassieke Azure-Portal]: https://manage.windowsazure.com/
[Baidu portal]: http://www.baidu.com/
