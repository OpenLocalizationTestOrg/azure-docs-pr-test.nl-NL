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
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a><span data-ttu-id="e0555-103">Verzenden van meldingen van de platformoverschrijdende toousers met Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="e0555-103">Send cross-platform notifications toousers with Notification Hubs</span></span>
<span data-ttu-id="e0555-104">In de vorige zelfstudie Hallo [meldingen verzenden naar gebruikers met Notification Hubs], hebt u geleerd hoe toopush meldingen tooall apparaten door een specifieke geverifieerde gebruiker geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="e0555-104">In hello previous tutorial [Notify users with Notification Hubs], you learned how toopush notifications tooall devices registered by a specific authenticated user.</span></span> <span data-ttu-id="e0555-105">In deze zelfstudie zijn meerdere aanvragen vereist toosend een melding tooeach ondersteunde client-platform.</span><span class="sxs-lookup"><span data-stu-id="e0555-105">In that tutorial, multiple requests were required toosend a notification tooeach supported client platform.</span></span> <span data-ttu-id="e0555-106">Notification Hubs ondersteunt sjablonen waarmee u kunnen opgeven hoe een specifiek apparaat wil tooreceive meldingen.</span><span class="sxs-lookup"><span data-stu-id="e0555-106">Notification Hubs supports templates, which let you specify how a specific device wants tooreceive notifications.</span></span> <span data-ttu-id="e0555-107">Dit vereenvoudigt het verzenden van meldingen op meerdere platforms.</span><span class="sxs-lookup"><span data-stu-id="e0555-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="e0555-108">Dit onderwerp wordt beschreven hoe tootake profiteren van sjablonen toosend, in een afzonderlijke aanvraag, een melding platform networkdirect die gericht is op alle platforms.</span><span class="sxs-lookup"><span data-stu-id="e0555-108">This topic demonstrates how tootake advantage of templates toosend, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="e0555-109">Zie voor meer informatie over sjablonen, [overzicht van Azure Notification Hubs][Templates].</span><span class="sxs-lookup"><span data-stu-id="e0555-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e0555-110">Projecten van Windows Phone 8.1 en lager worden niet ondersteund met behulp van Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e0555-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="e0555-111">Zie [Geschikte platforms voor Visual Studio 2017 en compatibiliteit](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e0555-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="e0555-112">Notification Hubs kunt u een apparaat tooregister meerdere sjablonen met Hallo dezelfde tag.</span><span class="sxs-lookup"><span data-stu-id="e0555-112">Notification Hubs allows a device tooregister multiple templates with hello same tag.</span></span> <span data-ttu-id="e0555-113">In dit geval bezorgd een binnenkomend bericht als doel dat label in meerdere meldingen resulteert toohello apparaat, één voor elke sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e0555-113">In this case, an incoming message targeting that tag results in multiple notifications delivered toohello device, one for each template.</span></span> <span data-ttu-id="e0555-114">Dit kunt u toodisplay Hallo hetzelfde bericht in meerdere visual meldingen, zoals beide als een badge en als een pop-upmelding in Windows Store-Apps.</span><span class="sxs-lookup"><span data-stu-id="e0555-114">This enables you toodisplay hello same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="e0555-115">Volgende stappen toosend platformoverschrijdende meldingen met behulp van sjablonen Hallo voltooien:</span><span class="sxs-lookup"><span data-stu-id="e0555-115">Complete hello following steps toosend cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="e0555-116">Vouw in Solution Explorer in Visual Studio hello, Hallo **domeincontrollers** map en klik vervolgens open Hallo RegisterController.cs bestand.</span><span class="sxs-lookup"><span data-stu-id="e0555-116">In hello Solution Explorer in Visual Studio, expand hello **Controllers** folder, then open hello RegisterController.cs file.</span></span>
2. <span data-ttu-id="e0555-117">Hallo codeblok niet vinden in Hallo **plaatsen** methode die een nieuwe registratie maakt vervangen Hallo `switch` inhoud met Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0555-117">Locate hello block of code in hello **Put** method that creates a new registration replace hello `switch` content with hello following code:</span></span>
   
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
   
    <span data-ttu-id="e0555-118">Deze code roept Hallo platform-specifieke methode toocreate de registratie van een sjabloon in plaats van de registratie van een systeemeigen.</span><span class="sxs-lookup"><span data-stu-id="e0555-118">This code calls hello platform-specific method toocreate a template registration instead of a native registration.</span></span> <span data-ttu-id="e0555-119">Bestaande registraties moeten niet worden gewijzigd omdat de sjabloon registraties worden afgeleid van systeemeigen registraties.</span><span class="sxs-lookup"><span data-stu-id="e0555-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="e0555-120">In Hallo **meldingen** controller, vervangen Hallo **sendNotification** methode Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0555-120">In hello **Notifications** controller, replace hello **sendNotification** method with hello following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="e0555-121">Deze code wordt een melding verzonden tooall platforms op Hallo dezelfde tijd en zonder toospecify een systeemeigen nettolading.</span><span class="sxs-lookup"><span data-stu-id="e0555-121">This code sends a notification tooall platforms at hello same time and without having toospecify a native payload.</span></span> <span data-ttu-id="e0555-122">Notification Hubs bouwt en levert de nettolading van de juiste tooevery apparaat Hallo Hello opgegeven *tag* waarde, zoals opgegeven in de sjablonen Hallo geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="e0555-122">Notification Hubs builds and delivers hello correct payload tooevery device with hello provided *tag* value, as specified in hello registered templates.</span></span>
4. <span data-ttu-id="e0555-123">Uw WebApi-back-end-project opnieuw te publiceren.</span><span class="sxs-lookup"><span data-stu-id="e0555-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="e0555-124">Hallo client-app opnieuw uitvoeren en controleer of de registratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e0555-124">Run hello client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="e0555-125">(Optioneel) Hallo app tooa tweede clientapparaat implementeren en vervolgens Hallo app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e0555-125">(Optional) Deploy hello client app tooa second device, then run hello app.</span></span>
   
    <span data-ttu-id="e0555-126">Houd er rekening mee dat er een melding wordt weergegeven op elk apparaat.</span><span class="sxs-lookup"><span data-stu-id="e0555-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0555-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0555-127">Next Steps</span></span>
<span data-ttu-id="e0555-128">Nu dat u deze zelfstudie hebt voltooid, meer informatie over Notification Hubs en sjablonen in de volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="e0555-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="e0555-129">**[Gebruik Notification Hubs toosend belangrijk nieuws]**</span><span class="sxs-lookup"><span data-stu-id="e0555-129">**[Use Notification Hubs toosend breaking news]**</span></span> <br/><span data-ttu-id="e0555-130">Demonstreert een ander scenario voor met behulp van sjablonen</span><span class="sxs-lookup"><span data-stu-id="e0555-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="e0555-131">**[Overzicht van Azure Notification Hubs][Templates]**</span><span class="sxs-lookup"><span data-stu-id="e0555-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="e0555-132">Overzichtsonderwerp gedetailleerde meer informatie over sjablonen.</span><span class="sxs-lookup"><span data-stu-id="e0555-132">Overview topic has more detailed information on templates.</span></span>

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
