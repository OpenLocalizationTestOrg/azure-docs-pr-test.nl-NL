---
title: aaaAzure Notification Hubs - diagnose richtlijnen
description: Richtlijnen voor hoe toodiagnose algemene met Azure Notification Hubs problemen.
services: notification-hubs
documentationcenter: Mobile
author: ysxu
manager: erikre
editor: 
ms.assetid: b5c89a2a-63b8-46d2-bbed-924f5a4cce61
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: NA
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: e374278f2bfdfad36ba091e8846059cd184c17ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs---diagnosis-guidelines"></a>Azure Notification Hubs - diagnose richtlijnen
## <a name="overview"></a>Overzicht
Een van de meest voorkomende vragen Hallo we graag van Azure Notification Hubs-klanten wordt toofigure uit waarom niet zien ze een melding verzonden vanuit de back-end voor de toepassing weergegeven op het clientapparaat Hallo - waar en waarom meldingen zijn verwijderd en hoe toofix dit. In dit artikel doorlopen we Hallo diverse redenen waarom meldingen mogelijk ophalen verwijderd of niet terechtkomen op Hallo-apparaten. Er wordt ook gezocht via de manieren waarop u kunt analyseren en Hallo hoofdoorzaak te achterhalen. 

Ten eerste is het essentieel toounderstand hoe Azure Notification Hubs meldingen toohello apparaten implementeert.
![][0]

In een typische send notification-stroom Hallo-bericht wordt verzonden vanuit Hallo **toepassing back-end** te**Azure Notification Hub (NH)** sommige verwerking op alle Hallo registraties waarbij rekening wordt gehouden op zijn beurt doet Hallo account geconfigureerd labels & tag expressies toodetermine 'doelen' dat wil zeggen alle Hallo registraties waarvoor tooreceive Hallo push-melding. Deze registraties kunnen overspannen één of alle van onze ondersteunde platformen - iOS, Google, Windows, Windows Phone-Kindle en Baidu voor Android China. Wanneer Hallo doelen zijn ingesteld, NH vervolgens pushes meldingen, verdelen over meerdere batch van registraties toohello apparaat platformspecifiek **Push Notification Service (PNS)** -zoals APNS voor Apple, GCM voor Google enzovoort. NH verifieert met Hallo die respectieve PNS op basis van Hallo referenties die u in de klassieke Azure-Portal Hallo op Hallo Notification Hub configureren pagina instellen. Hallo PNS stuurt Hallo meldingen toohello respectieve **clientapparaten**. Dit is de aanbevolen manier toodeliver pushmeldingen en dat de laatste fase Hallo van de levering van meldingen tussen Hallo platform PNS en Hallo apparaat plaatsvindt Opmerking Hallo-platform. Daarom hebben we vier belangrijke onderdelen - *client*, *toepassing back-end*, *Azure Notification Hubs (NH)* en *Push Notification Services (PNS)* en deze kan ertoe leiden dat meldingen steeds verbroken. Meer informatie over deze architectuur is beschikbaar op [overzicht van Notification Hubs].

Fout toodeliver meldingen situatie kunnen zich voordoen tijdens de eerste Hallo testfase fase dit kan duiden op een configuratieprobleem of het kan gebeuren in productie waarin alle of enkele Hallo meldingen kan worden steeds verbroken die wijzen op een dieper toepassing of messaging-patroon probleem. In de sectie Hallo kijken hieronder we verschillende scenario's voor de verwijderde meldingen variërend van toohello zeldzame voorkomende, die waarvan sommige u duidelijk vindt wellicht en sommige andere niet zo veel. 

## <a name="azure-notifications-hub-mis-configuration"></a>Onjuiste configuratie van Azure Notification hubs
Azure Notification Hubs moet tooauthenticate zichzelf in de context van Hallo van Hallo ontwikkelaarshandleiding toepassing toobe kunnen toosuccessfully verzenden meldingen toohello respectieve PNS. Dit wordt mogelijk gemaakt door Hallo ontwikkelaar een ontwikkelaarsaccount maken met het desbetreffende platform hello (Google, Apple, Windows, enzovoort) en vervolgens registreren hun toepassing waar ze referenties die toobe geconfigureerd in de portal Hallo onder melding moeten krijgen Configuratiesectie hubs. Als er geen meldingen via de eerste stap moet worden tooensure maken dat de juiste referenties Hallo zijn geconfigureerd in Hallo Notification Hub overeenstemming brengen met de toepassing hello gemaakt onder hun platform-specifieke developer-account. Vindt u onze [gestart zelfstudies ophalen] nuttig toogo via dit proces op een manier stap voor stap. Hier volgen enkele veelvoorkomende onjuiste configuraties:

1. **Algemeen**
   
    een) Zorg ervoor dat de naam van uw notification hub (zonder typefouten) is dezelfde Hallo:
   
   * Wanneer u registreert in Hallo-client 
   * Waar u meldingen verzendt vanuit Hallo back-end,  
   * Waar u Hallo PNS referenties hebt geconfigureerd en 
   * Met SAS de referenties die u hebt geconfigureerd op de back-end van een client en Hallo Hallo. 
     
     b) Zorg ervoor dat u Hallo juiste SAS configuratie tekenreeksen op Hallo client- en back-end Hallo van toepassing. Als vuistregel, moet u Hallo **DefaultListenSharedAccessSignature** op Hallo-client en **DefaultFullSharedAccessSignature** op Hallo toepassing back-end (waarmee machtiging toobe kan toosend melding toohello NH)
2. **Configuratie van de Apple Push Notification Service (APNS)**
   
    Moet u twee verschillende hubs - één voor productie onderhouden en een andere voor het testen van doel. Dit betekent dat u gaat toouse in sandbox-omgeving tooa afzonderlijke hub en Hallo-certificaat dat u toouse in productie tooa afzonderlijke hub gaat Hallo-certificaat uploadt. Probeer niet tooupload verschillende typen certificaten toohello dezelfde hub omdat dit kan leiden tot melding fouten Hallo regel omlaag. Als u zelf kunt vinden in de positie waar u verschillende soorten certificaat toohello per ongeluk hebt geüpload dezelfde hub het is raadzaam toodelete Hallo hub en nieuwe start. Als voor een bepaalde reden niet kan toodelete Hallo hub klikt u vervolgens op Hallo zeer minste, verwijdert u alle bestaande Hallo-registraties van Hallo hub. 
3. **Google Cloud Messaging (GCM)-configuratie** 
   
    een) Zorg ervoor dat u 'Google Cloud Messaging voor Android' onder uw cloudproject inschakelen wilt. 
   
    ![][2]
   
    b) Zorg ervoor dat u een sleutel' Server' maakt tijdens het Hallo-referenties zijn verkregen welke NH tooauthenticate met GCM wilt gebruiken. 
   
    ![][3]
   
    c) Zorg ervoor dat u 'Project-ID' op Hallo client is een geheel numeriek entiteit die u van Hallo-dashboard verkrijgen kunt hebt geconfigureerd:
   
    ![][1]

## <a name="application-issues"></a>Problemen met toepassingen
1) **Tags / Tag expressies**

Als u van tags of tag expressies toosegment uw doelgroep gebruikmaakt, is het altijd mogelijk dat wanneer u Hallo melding verzendt, er is geen doel op basis van Hallo tags/tag expressies die u in de aanroep van verzenden opgeeft kan worden gevonden. Het is raadzaam tooreview uw registraties tooensure dat er tags welke overeen bij het verzenden van meldingen en controleer vervolgens de ontvangst ervan de Hallo melding alleen via het Hallo-clients met deze registraties. Bijvoorbeeld Als al uw registraties met NH zijn gemaakt met het label 'Politiek' spreken en u een melding met het label verzendt 'Sport', wordt worden deze niet tooany apparaat verzonden. Een complexe geval kan inhouden: code-expressies waar u alleen geregistreerd met "Tag A" of "Tag B", maar tijdens het verzenden van meldingen, u ontwikkelt voor "Tag A & & Tag B". In Hallo tips onderstaande sectie zelf onderzoeken, manieren waarop u uw registraties en ze hebben Hallo-tags kunt bekijken. 

2) **Sjabloonproblemen**

Als u met behulp van sjablonen en zorg ervoor dat u Hallo richtlijnen beschreven volgt op [sjabloon richtlijnen]. 

3) **Ongeldige registraties**

Ervan uitgaande dat Hallo die Notification Hub correct is geconfigureerd en eventuele tags/tag-expressies zijn gebruikt waardoor correct Hallo zoeken met geldige doelen toowhich Hallo meldingen toobe verzonden moeten, NH wordt uit verschillende verwerken batches parallel - elke batch is geactiveerd verzenden van berichten tooa set met geregistreerde items. 

> [!NOTE]
> Aangezien we hello parallel verwerken, niet wordt gegarandeerd Hallo volgorde in welke Hallo meldingen worden geleverd. 
> 
> 

Azure Notification hubs is nu geoptimaliseerd voor een model voor bericht 'op de meeste eenmaal'. Dit betekent dat we proberen een deactivering duplicatie zodat er geen meldingen meer dan één keer tooa apparaat worden geleverd. tooensure per apparaat-id vóór daadwerkelijk verzenden Hallo-bericht toohello PNS deze we bekijkt hello registraties en zorg ervoor dat slechts één bericht verzonden. Omdat elke batch toohello PNS die op zijn beurt accepteert wordt verzonden en Hallo registraties worden gevalideerd, is het mogelijk dat Hallo PNS detecteert een fout opgetreden bij een of meer van de Hallo registraties in een batch, retourneert een fout tooAzure NH en stopt het verwerken waardoor neer te zetten die batch-volledig. Dit geldt met name met APNS dat gebruikmaakt van een stroom TCP-protocol. Hoewel we eenmaal zijn geoptimaliseerd voor op de meeste Hallo levering in dit geval verwijderen we ontlast registratie van de database en levering van meldingen voor nieuwe pogingen voor de rest Hallo Hallo-apparaten in deze batch.

Krijgt u informatie over de fout voor Hallo mislukte bezorging poging tegen een registratie met hello Azure Notification Hubs REST API's: [Per bericht telemetrie: ophalen Notification Message telemetrie](https://msdn.microsoft.com/library/azure/mt608135.aspx) en [Feedback van PNS](https://msdn.microsoft.com/library/azure/mt705560.aspx). Zie Hallo [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) bijvoorbeeld code.

## <a name="pns-issues"></a>PNS-problemen
Zodra het Hallo-melding is ontvangen door de respectieve Hallo is PNS dan de verantwoordelijkheid toodeliver Hallo melding toohello apparaat. Azure Notification Hubs valt buiten het Hallo-afbeelding hier en heeft geen controle over wanneer of als er Hallo melding toobe toohello apparaat geleverd. Aangezien Hallo platform notification services vrij robuuste, meldingen tooreach Hallo apparaten meestal binnen een paar seconden van Hallo PNS. Hallo PNS echter is beperking vervolgens Azure Notification Hubs is van toepassing als een exponentiële back uitschakelen strategie en als Hallo PNS onbereikbaar is voor een 30 min blijft moeten we hebben een beleid in plaats van tooexpire en deze berichten permanent verwijderen. 

Als een PNS een melding toodeliver probeert maar Hallo apparaat offline is, is Hallo melding opgeslagen door Hallo PNS voor een beperkte periode en toohello apparaat geleverd zodra deze beschikbaar. Slechts één recente melding voor een bepaalde app wordt opgeslagen. Als meerdere meldingen worden verzonden wanneer het Hallo-apparaat offline is, wordt elke nieuwe melding Hallo voorafgaande kennisgeving toobe verwijderd. Dit gedrag alleen Hallo nieuwste melding om te houden is waarnaar wordt verwezen tooas samenvoegen van meldingen in APNS en samenvouwen in GCM (die gebruikmaakt van een samenvouwen sleutel). Als Hallo apparaat gedurende een lange periode offline blijft, worden meldingen die zijn worden opgeslagen voor deze genegeerd. Bron - [APNS richtlijnen] & [GCM richtlijnen]

U kunt met Azure Notification Hubs - een samenvoegen sleutel doorgeven via een HTTP-header met Hallo algemene `SendNotification` API (bijvoorbeeld voor de .NET SDK- `SendNotificationAsync`) toohello wat HTTP-headers die worden doorgegeven als ook duurt is respectieve PNS. 

## <a name="self-diagnose-tips"></a>Tips zelf onderzoeken
Hier bespreken we Hallo verschillende mogelijkheden toodiagnose en hoofdmap ervoor zorgen dat eventuele problemen met de Notification Hub:

### <a name="verify-credentials"></a>Referenties verifiëren
1. **PNS-portal voor ontwikkelaars**
   
    Controleren of ze op Hallo respectieve PNS developer portal (APNS, GCM, WNS enz.) met behulp van onze [gestart zelfstudies ophalen].
2. **Klassieke Azure-portal**
   
    Ga toohello configureren tabblad tooreview en Hallo referenties overeen met die worden verkregen uit Hallo PNS-portal voor ontwikkelaars. 
   
    ![][4]

### <a name="verify-registrations"></a>Registraties controleren
1. **Visual Studio**
   
    Als u Visual Studio voor ontwikkeling gebruiken kunt u verbinding tooMicrosoft Azure en het bekijken en beheren van een aantal Azure-services met inbegrip van Notification hubs vanuit 'Server Explorer'. Dit is vooral handig zijn voor uw omgeving ontwikkelen en testen. 
   
    ![][9]
   
    U kunt weergeven en beheren van alle Hallo registraties van uw hub die mooi voor registratie van het platform, systeemeigen of sjabloon, een labels, PNS-id, registratie-id en het Hallo vervaldatum worden gecategoriseerd. U kunt ook een registratie op Hallo snel - nuttig spreek als u alle codes tooedit wilt bewerken. 
   
    ![][8]
   
   > [!NOTE]
   > Visual Studio functionaliteit tooedit registraties mag alleen worden gebruikt tijdens het ontwikkelen en testen met een beperkt aantal registraties. Als er ontstaat een toofix moet uw registraties in bulk rekening houden met behulp van Hallo registratie-functionaliteit voor exporteren/importeren beschreven hier - [registraties exporteren/importeren](https://msdn.microsoft.com/library/dn790624.aspx)
   > 
   > 
2. **Service Bus explorer**
   
    Veel klanten gebruik service bus explorer beschreven hier - [ServiceBus Explorer] voor weergeven en beheren van de notification hub. Het is een open source-project beschikbaar is via code.microsoft.com - [ServiceBus Explorer-code]

### <a name="verify-message-notifications"></a>Controleer of de melding
1. **Klassieke Azure Portal**
   
    U kunt toohello 'Debug' tabblad toosend meldingen tooyour testclients gaan zonder te hoeven van elke back-end voor de service up en wordt uitgevoerd. 
   
    ![][7]
2. **Visual Studio**
   
    U kunt ook testmeldingen verzenden vanuit Hallo comforts van Visual Studio:
   
    ![][10]
   
    U kunt meer op Hallo Visual Studio Notification Hub Azure explorer-functie hier - lezen 
   
   * [Overzicht van VS Server Explorer]
   * [VS Server Explorer blogbericht - 1]
   * [VS Server Explorer blogbericht - 2]

### <a name="debug-failed-notifications-review-notification-outcome"></a>Fouten opsporen in mislukte meldingen / melding uitkomst controleren
**De eigenschap EnableTestSend**

Wanneer u een melding via Notification Hubs verzenden, in eerste instantie deze zojuist hebt opgehaald in de wachtrij geplaatst voor NH toodo toofigure uit alle doelen verwerking en uiteindelijk NH stuurt vervolgens deze toohello PNS. Dit betekent dat wanneer u van REST-API of een van de Hallo client SDK gebruikmaakt, hello geslaagde rendement van uw verzenden aanroep alleen betekent dat Hallo-bericht zijn met succes in de wachtrij bij Notification Hub geplaatst heeft. Geeft een beter inzicht in wat is er gebeurd wanneer NH uiteindelijk toosend Hallo-bericht tooPNS geen. Als de melding niet dat bij het clientapparaat Hallo binnenkomt is, er is een kans dat wanneer NH toodeliver Hallo-bericht tooPNS probeerde, er een fout bijvoorbeeld Hallo nettolading is overschrijdt Hallo toegestane door Hallo PNS of Hallo-referenties die zijn geconfigureerd in NH zijn Ongeldige enzovoort tooget een inzicht in de Hallo PNS fouten, hebben we een eigenschap met de naam ingevoerd [EnableTestSend functie]. Deze eigenschap wordt automatisch ingeschakeld wanneer u een test van berichten van het Hallo-portal of Visual Studio-client en daarom kunt u gedetailleerde toosee verzenden foutopsporingsinformatie. U kunt deze gebruiken via API's duurt Hallo voorbeeld Hallo .NET SDK waar het is nu beschikbaar en worden toegevoegd tooall client-SDK's uiteindelijk. toouse dit met de REST-aanroep hello, kan een parameter querystring aangedaan 'test' hello einde van de aanroep van verzenden bijvoorbeeld gewoon toevoegen 

    https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test

*Voorbeeld (.NET SDK)*

Stel dat u gebruikmaakt van .NET SDK toosend een systeemeigen toast-melding:

    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
    var result = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(result.State);

`result.State`wordt gewoon status `Enqueued` achter Hallo Hallo kan worden uitgevoerd zonder een inzicht in wat is er gebeurd tooyour push. Nu kunt u Hallo `EnableTestSend` Boole-eigenschap tijdens het initialiseren van Hallo `NotificationHubClient` en gedetailleerde status weergegeven over Hallo PNS fouten opgetreden tijdens het Hallo-bericht verzenden kunnen ophalen. Hallo verzenden aanroep hier duurt extra tijd tooreturn omdat deze alleen retourneert nadat NH Hallo melding tooPNS toodetermine Hallo uitkomst heeft geleverd. 

    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }

*Voorbeelduitvoer*

    DetailedStateAvailable
    windows
    7619785862101227384-7840974832647865618-3
    hello Token obtained from hello Token Provider is wrong

Dit bericht geeft aan of ongeldige referenties zijn geconfigureerd in Hallo notification hub een probleem met de Hallo registraties op Hallo hub en Hallo aanbevolen loop zou worden toodelete deze registratie en maak deze opnieuw voordat u verzendt Hallo Hallo-client te laten Bericht. 

> [!NOTE]
> Houd er rekening mee dat Hallo gebruik van deze eigenschap sterk beperkt is en dus u alleen dit in de omgeving ontwikkelen en testen met een beperkt aantal registraties gebruiken moet. We alleen foutopsporing meldingen verzenden too10 apparaten. We hebben ook een limiet van de verwerking van foutopsporing verzendt toobe 10 per minuut. 
> 
> 

### <a name="review-telemetry"></a>Telemetrie controleren
1. **Gebruik de klassieke Azure-Portal**
   
    Hallo-portal kunt u tooget een snel overzicht van alle Hallo activiteiten op uw Notification Hub. 
   
    a) u kunt een samengevoegde weergave van Hallo registraties, meldingen en fouten per platform weergeven uit de tabblad 'dashboard' Hallo. 
   
    ![][5]
   
    b) u kunt ook veel andere platform specifieke metrische gegevens van Hallo 'Monitor' tabblad tootake uitvoerig stil vooral op specifieke fouten heeft geretourneerd wanneer NH toosend Hallo melding toohello PNS probeert PNS toevoegen. 
   
    ![][6]
   
    c) u moet beginnen met het controleren van Hallo **binnenkomende berichten**, **registratie Operations**, **geslaagde meldingen** en gaat u tooper platform tabblad tooreview Hallo PNS specifieke fouten. 
   
    d) als u ziet Hallo notification hub onjuist geconfigureerd met verificatie-instellingen Hallo vervolgens u PNS verificatiefout. Dit is een goede indicatie toocheck hello PNS-referenties. 

2) **Toegang op programmeerniveau**

Meer informatie hier- 

* [Telemetrie programmatische toegang]
* [Telemetrie toegang via de API-voorbeeld] 

> [!NOTE]
> Meerdere telemetrie-gerelateerde functies, zoals **exporteren/importeren registraties**, **telemetrie toegang via API's** enzovoort zijn alleen beschikbaar in Standard-laag. Als u toouse probeert krijgt deze functies als u in Free of basisstaffel vervolgens u uitzondering bericht toothis effect tijdens het gebruik van Hallo SDK en een HTTP 403 (verboden) wanneer u ze rechtstreeks vanuit Hallo REST-API's. Zorg ervoor dat u hebt verplaatst up tooStandard laag via de klassieke Azure-Portal.  
> 
> 

<!-- IMAGES -->
[0]: ./media/notification-hubs-diagnosing/Architecture.png
[1]: ./media/notification-hubs-diagnosing/GCMConfigure.png
[2]: ./media/notification-hubs-diagnosing/GCMEnable.png
[3]: ./media/notification-hubs-diagnosing/GCMServerKey.png
[4]: ./media/notification-hubs-diagnosing/PortalConfigure.png
[5]: ./media/notification-hubs-diagnosing/PortalDashboard.png
[6]: ./media/notification-hubs-diagnosing/PortalMonitoring.png
[7]: ./media/notification-hubs-diagnosing/PortalTestNotification.png
[8]: ./media/notification-hubs-diagnosing/VSRegistrations.png
[9]: ./media/notification-hubs-diagnosing/VSServerExplorer.png
[10]: ./media/notification-hubs-diagnosing/VSTestNotification.png

<!-- LINKS -->
[overzicht van Notification Hubs]: notification-hubs-push-notification-overview.md
[gestart zelfstudies ophalen]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[sjabloon richtlijnen]: https://msdn.microsoft.com/library/dn530748.aspx 
[APNS richtlijnen]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4
[GCM richtlijnen]: http://developer.android.com/google/gcm/adv.html
[Export/Import Registrations]: http://msdn.microsoft.com/library/dn790624.aspx
[ServiceBus Explorer]: http://msdn.microsoft.com/library/dn530751.aspx
[ServiceBus Explorer-code]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a
[Overzicht van VS Server Explorer]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx 
[VS Server Explorer blogbericht - 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs 
[VS Server Explorer blogbericht - 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ 
[EnableTestSend functie]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx
[Telemetrie programmatische toegang]: http://msdn.microsoft.com/library/azure/dn458823.aspx
[Telemetrie toegang via de API-voorbeeld]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel

