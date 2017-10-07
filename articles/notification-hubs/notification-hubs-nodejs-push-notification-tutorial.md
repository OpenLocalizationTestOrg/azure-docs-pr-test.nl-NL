---
title: aaaSending pushmeldingen kunt verzenden met Azure Notification Hubs en Node.js
description: Meer informatie over hoe toouse Notification Hubs toosend pushmeldingen vanuit een Node.js-toepassing.
keywords: push-bericht, push notifications,node.js push, ios push
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a>Pushmeldingen verzenden met Azure Notification Hubs en Node.js
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a>Overzicht
> [!IMPORTANT]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs) voor meer informatie.
> 
> 

Deze handleiding leert u hoe toosend pushmeldingen met Hallo help van Azure Notification Hubs rechtstreeks vanuit een Node.js-toepassing. 

Hallo scenario's worden behandeld zijn push notifications tooapplications verzenden op Hallo volgende platforms:

* Android
* iOS
* Windows Phone
* Universele Windows-Platform 

Zie voor meer informatie over notification hubs Hallo [Vervolgstappen](#next) sectie.

## <a name="what-are-notification-hubs"></a>Wat is Notification Hubs?
Azure Notification Hubs bieden een eenvoudig te gebruiken, meerdere platforms, schaalbare infrastructuur voor het verzenden van pushmeldingen meldingen toomobile apparaten. Zie voor informatie over service-infrastructuur hello, Hallo [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) pagina.

## <a name="create-a-nodejs-application"></a>Een Node.js-toepassing maken
Hallo eerste stap in deze zelfstudie is een nieuwe lege Node.js-toepassing maken. Zie voor instructies over het maken van een Node.js-toepassing [maken en implementeren van een Node.js-toepassing tooAzure website][nodejswebsite], [Node.js-Cloudservice] [ Node.js Cloud Service] met Windows PowerShell of [website met WebMatrix].

## <a name="configure-your-application-toouse-notification-hubs"></a>Configureren van uw toepassing tooUse Notification Hubs
Azure Notification Hubs toouse, moet u toodownload en gebruik Hallo Node.js [azure-pakket](https://www.npmjs.com/package/azure), waaronder een ingebouwde verzameling helper-bibliotheken die met Hallo push notification REST-services communiceren.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Knooppunt Package Manager (NPM) tooobtain Hallo pakket gebruiken
1. Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Linux) en navigeer toohello map waar u uw lege toepassing hebt gemaakt. .
2. Type **npm installeren azure sb** in Hallo-opdrachtvenster.
3. U kunt handmatig uitvoeren Hallo **ls** of **dir** tooverify opdracht die een **knooppunt\_modules** map is gemaakt. Hallo zoeken in die map **azure** , dit pakket bevat Hallo bibliotheken, moet u tooaccess Hallo Notification Hub.

> [!NOTE]
> U kunt meer informatie over het installeren van NPM op Hallo officiële [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm). 
> 
> 

### <a name="import-hello-module"></a>Hallo-module importeren
Met een teksteditor toevoegen na toohello bovenaan Hallo Hallo **server.js** bestand van de toepassing hello:

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a>Een Azure Notification Hub-verbinding instellen
Hallo **NotificationHubService** object kunt u samenwerken met notification hubs. Hallo volgende code maakt een **NotificationHubService** -object voor Hallo nofication hub met de naam **hubname**. Voeg deze toe aan de bovenkant Hallo Hallo **server.js** bestand na Hallo instructie tooimport hello azure module:

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

Hallo verbinding **connectionstring** waarde kan worden verkregen van Hallo [Azure Portal] door Hallo volgende stappen uit te voeren:

1. Klik in het Hallo navigatiedeelvenster links op **Bladeren**.
2. Selecteer **Notification Hubs**, en vervolgens zoeken Hallo-hub gewenste toouse voor Hallo-voorbeeld. U kunt verwijzen toohello [Windows Store aan de slag zelfstudie](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) als u informatie over het maken van een nieuwe Notification Hub nodig.
3. Selecteer **instellingen**.
4. Klik op **toegangsbeleid**. Hier ziet u beide verbindingsreeksen gedeelde en volledige toegang.

![Azure Portal - Notification Hubs](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> U kunt ook ophalen verbindingsreeks Hallo Hallo met **Get-AzureSbNamespace** cmdlet geleverd door [Azure PowerShell](/powershell/azureps-cmdlets-docs) of Hallo **azure sb naamruimte weergeven** opdracht met Hallo [Azure-opdrachtregelinterface (Azure CLI)](../cli-install-nodejs.md).
> 
> 

## <a name="general-architecture"></a>Algemene architectuur
Hallo **NotificationHubService** object beschrijft Hallo instanties van objecten voor het verzenden van pushmeldingen meldingen toospecific apparaten en toepassingen te volgen:

* **Android** -hello gebruiken **GcmService** object, dat beschikbaar is op **notificationHubService.gcm**
* **iOS** -hello gebruiken **ApnsService** -object, dat openen op **notificationHubService.apns**
* **Windows Phone** -hello gebruiken **MpnsService** object, dat beschikbaar is op **notificationHubService.mpns**
* **Universele Windows-Platform** -hello gebruiken **WnsService** object, dat beschikbaar is op **notificationHubService.wns**

### <a name="how-to-send-push-notifications-tooandroid-applications"></a>Hoe: push notifications tooAndroid toepassingen verzenden
Hallo **GcmService** -object biedt een **verzenden** methode die gebruikt toosend push notifications tooAndroid toepassingen worden kan. Hallo **verzenden** methode Hallo volgende parameters accepteert:

* **Labels** -Hallo label-id. Als er is geen code is opgegeven, wordt Hallo-bericht verzonden tooall clients.
* **Nettolading** -Hallo van bericht JSON of raw string nettolading.
* **Callback** -Hallo callback-functie.

Zie voor meer informatie over de indeling van nettolading hello, Hallo **nettolading** sectie Hallo [GCM Server implementeren](http://developer.android.com/google/gcm/server.html#payload) document.

Hallo volgende code gebruikt Hallo **GcmService** exemplaar beschikbaar is gemaakt door Hallo **NotificationHubService** toosend een push notification-tooall ingeschreven clients.

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a>Hoe: push notifications tooiOS toepassingen verzenden
Dezelfde net als bij Android-toepassingen hierboven beschreven, Hallo **ApnsService** -object biedt een **verzenden** methode die gebruikt toosend push notifications tooiOS toepassingen worden kan. Hallo **verzenden** methode Hallo volgende parameters accepteert:

* **Labels** -Hallo label-id. Als er is geen code is opgegeven, wordt Hallo-bericht verzonden tooall clients.
* **Nettolading** - Hallo van bericht JSON of string nettolading.
* **Callback** -Hallo callback-functie.

Zie voor meer informatie Hallo nettolading indeling Hallo **nettolading van de meldingen** sectie Hallo [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.

Hallo volgende code gebruikt Hallo **ApnsService** exemplaar beschikbaar is gemaakt door Hallo **NotificationHubService** toosend een waarschuwing bericht tooall clients:

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a>Hoe: verzenden push notifications tooWindows Phone-toepassingen
Hallo **MpnsService** -object biedt een **verzenden** methode die gebruikt toosend push notifications tooWindows Phone-toepassingen worden kan. Hallo **verzenden** methode Hallo volgende parameters accepteert:

* **Labels** -Hallo label-id. Als er is geen code is opgegeven, wordt Hallo-bericht verzonden tooall clients.
* **Nettolading** -Hallo-bericht van de XML-nettolading.
* **Doelnaam**  -  `toast` voor pop-upmeldingen. `token`voor meldingen van de tegel.
* **NotificationClass** -Hallo prioriteit Hallo-melding. Zie Hallo **elementen voor HTTP-Header** sectie Hallo [Pushmeldingen vanaf een server](http://msdn.microsoft.com/library/hh221551.aspx) document voor geldige waarden.
* **Opties** : optioneel aanvraagheaders.
* **Callback** -Hallo callback-functie.

Voor een lijst met geldige **TargetName**, **NotificationClass** en opties voor header uitchecken Hallo [Pushmeldingen vanaf een server](http://msdn.microsoft.com/library/hh221551.aspx) pagina.

Hallo volgende voorbeeldcode maakt gebruik van Hallo **MpnsService** exemplaar beschikbaar is gemaakt door Hallo **NotificationHubService** toosend een pop-upmelding:

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a>Hoe: verzenden push notifications tooUniversal Windows Platform (UWP)-toepassingen
Hallo **WnsService** -object biedt een **verzenden** methode die gebruikt toosend push notifications tooUniversal Windows-Platform-toepassingen worden kan.  Hallo **verzenden** methode Hallo volgende parameters accepteert:

* **Labels** -Hallo label-id. Als er is geen code is opgegeven, wordt Hallo-bericht verzonden tooall ingeschreven clients.
* **Nettolading** -bericht Hallo de XML-nettolading.
* **Type** -Hallo meldingstype.
* **Opties** : optioneel aanvraagheaders.
* **Callback** -Hallo callback-functie.

Zie voor een lijst van geldige typen en aanvraagheaders [Push notification service aanvraag- en reactieheaders](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).

Hallo volgende code gebruikt Hallo **WnsService** exemplaar beschikbaar is gemaakt door Hallo **NotificationHubService** toosend een pop-up push notification tooa UWP-app:

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a>Volgende stappen
Hallo voorbeeld codefragmenten hierboven kunnen u tooeasily build service infrastructuur toodeliver push notifications tooa grote verscheidenheid aan apparaten. Nu u de basisbeginselen van het gebruik van Notification Hubs met behulp van node.js Hallo hebt geleerd, volgt u deze koppelingen toolearn meer informatie over hoe deze mogelijkheden verder kan worden uitgebreid.

* Zie MSDN-documentatie voor Hallo [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).
* Ga naar Hallo [Azure SDK voor knooppunt] opslagplaats op GitHub voor meer voorbeelden en implementatiegegevens.

[Azure SDK voor knooppunt]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[website met WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Azure Portal]: https://portal.azure.com
