---
title: aaaSend platformoverschrijdende meldingen toousers met Notification Hubs (ASP.NET)
description: "Meer informatie over hoe toouse Notification Hubs sjablonen toosend in één aanvraag een platform networkdirect-melding die gericht is op alle platforms."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 11d2131b-f683-47fd-a691-4cdfc696f62b
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: f105b871b809e739dd5c05ea819ad135e842ebb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a>Verzenden van meldingen van de platformoverschrijdende toousers met Notification Hubs
In de vorige zelfstudie Hallo [meldingen verzenden naar gebruikers met Notification Hubs], hebt u geleerd hoe toopush meldingen tooall apparaten door een specifieke geverifieerde gebruiker geregistreerd. In deze zelfstudie zijn meerdere aanvragen vereist toosend een melding tooeach ondersteunde client-platform. Notification Hubs ondersteunt sjablonen waarmee u kunnen opgeven hoe een specifiek apparaat wil tooreceive meldingen. Dit vereenvoudigt het verzenden van meldingen op meerdere platforms. Dit onderwerp wordt beschreven hoe tootake profiteren van sjablonen toosend, in een afzonderlijke aanvraag, een melding platform networkdirect die gericht is op alle platforms. Zie voor meer informatie over sjablonen, [overzicht van Azure Notification Hubs][Templates].
> [!IMPORTANT]
> Projecten van Windows Phone 8.1 en lager worden niet ondersteund met behulp van Visual Studio 2017. Zie [Geschikte platforms voor Visual Studio 2017 en compatibiliteit](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs) voor meer informatie.

> [!NOTE]
> Notification Hubs kunt u een apparaat tooregister meerdere sjablonen met Hallo dezelfde tag. In dit geval bezorgd een binnenkomend bericht als doel dat label in meerdere meldingen resulteert toohello apparaat, één voor elke sjabloon. Dit kunt u toodisplay Hallo hetzelfde bericht in meerdere visual meldingen, zoals beide als een badge en als een pop-upmelding in Windows Store-Apps.
> 
> 

Volgende stappen toosend platformoverschrijdende meldingen met behulp van sjablonen Hallo voltooien:

1. Vouw in Solution Explorer in Visual Studio hello, Hallo **domeincontrollers** map en klik vervolgens open Hallo RegisterController.cs bestand.
2. Hallo codeblok niet vinden in Hallo **plaatsen** methode die een nieuwe registratie maakt vervangen Hallo `switch` inhoud met Hallo code te volgen:
   
        switch (deviceUpdate.Platform)
        {
            case "mpns":
                var toastTemplate = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>$(message)</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
                registration = new MpnsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "wns":
                toastTemplate = @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(message)</text></binding></visual></toast>";
                registration = new WindowsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "apns":
                var alertTemplate = "{\"aps\":{\"alert\":\"$(message)\"}}";
                registration = new AppleTemplateRegistrationDescription(deviceUpdate.Handle, alertTemplate);
                break;
            case "gcm":
                var messageTemplate = "{\"data\":{\"message\":\"$(message)\"}}";
                registration = new GcmTemplateRegistrationDescription(deviceUpdate.Handle, messageTemplate);
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }
   
    Deze code roept Hallo platform-specifieke methode toocreate de registratie van een sjabloon in plaats van de registratie van een systeemeigen. Bestaande registraties moeten niet worden gewijzigd omdat de sjabloon registraties worden afgeleid van systeemeigen registraties.
3. In Hallo **meldingen** controller, vervangen Hallo **sendNotification** methode Hello code te volgen:
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    Deze code wordt een melding verzonden tooall platforms op Hallo dezelfde tijd en zonder toospecify een systeemeigen nettolading. Notification Hubs bouwt en levert de nettolading van de juiste tooevery apparaat Hallo Hello opgegeven *tag* waarde, zoals opgegeven in de sjablonen Hallo geregistreerd.
4. Uw WebApi-back-end-project opnieuw te publiceren.
5. Hallo client-app opnieuw uitvoeren en controleer of de registratie is voltooid.
6. (Optioneel) Hallo app tooa tweede clientapparaat implementeren en vervolgens Hallo app uitvoeren.
   
    Houd er rekening mee dat er een melding wordt weergegeven op elk apparaat.

## <a name="next-steps"></a>Volgende stappen
Nu dat u deze zelfstudie hebt voltooid, meer informatie over Notification Hubs en sjablonen in de volgende onderwerpen:

* **[Gebruik Notification Hubs toosend belangrijk nieuws]** <br/>Demonstreert een ander scenario voor met behulp van sjablonen
* **[Overzicht van Azure Notification Hubs][Templates]**<br/>Overzichtsonderwerp gedetailleerde meer informatie over sjablonen.

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push toousers ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push toousers Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[Gebruik Notification Hubs toosend belangrijk nieuws]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[meldingen verzenden naar gebruikers met Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How toofor Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
