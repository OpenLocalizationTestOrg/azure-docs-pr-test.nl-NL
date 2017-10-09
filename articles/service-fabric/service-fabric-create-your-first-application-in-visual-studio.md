---
title: aaaCreate een betrouwbare Azure Service Fabric-service met C#
description: Een betrouwbare Service-toepassing die is gebouwd op Azure Service Fabric met Visual Studio maken, implementeren en er foutopsporing op toepassen.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a>Uw eerste stateful betrouwbare Service Fabric-servicetoepassing maken met C#

Meer informatie over hoe toodeploy uw eerste Service Fabric-toepassing voor .NET in Windows over een paar minuten. Wanneer u klaar bent, hebt u een lokaal cluster uitgevoerd met een betrouwbare servicetoepassing.

## <a name="prerequisites"></a>Vereisten

Voordat u begint, zorgt u ervoor dat u [uw ontwikkelingsomgeving hebt ingesteld](service-fabric-get-started.md). Dit omvat het installeren van Service Fabric SDK Hallo en Visual Studio 2017 of 2015.

## <a name="create-hello-application"></a>Hallo-toepassing maken

Start Visual Studio als **beheerder**.

Maak een project met `CTRL`+`SHIFT`+`N`

In Hallo **nieuw Project** dialoogvenster kiezen **Cloud > Service Fabric-toepassing**.

Naam van de toepassing hello **Mijntoepassing** en druk op **OK**.

   
![Dialoogvenster voor nieuw project in Visual Studio][1]

U kunt elk type Service Fabric-toepassing uit het volgende dialoogvenster Hallo maken. Kies voor deze snelstartgids **Stateful service**.

Service voor Hallo **MyStatefulService** en druk op **OK**.

![Dialoogvenster voor nieuwe service in Visual Studio][2]


Visual Studio maakt het toepassingsproject Hallo en Hallo stateful service-project en geeft deze weer in Solution Explorer.

![Solution Explorer na het maken van de stateful service-toepassing][3]

Hallo-toepassingsproject (**Mijntoepassing**) bevat geen code rechtstreeks. Het verwijst naar een reeks serviceprojecten. Daarnaast bevat het project drie andere typen inhoud:

* **Profielen publiceren**  
Profielen voor het implementeren van toodifferent omgevingen.

* **Scripts**  
PowerShell-script voor het implementeren/bijwerken van uw toepassing.

* **Toepassingsdefinitie**  
Hallo ApplicationManifest.xml bestand onder omvat *ApplicationPackageRoot* waarin wordt beschreven samenstelling van uw toepassing. Bijbehorende parameter voor toepassingsbestanden onder zijn *ApplicationParameters*, welke gebruikte toospecify omgeving-specifieke parameters kan worden. Visual Studio selecteert een parameterbestand toepassing die opgegeven in Hallo gekoppeld publicatieprofiel tijdens de implementatie tooa-specifieke omgeving.
    
Zie voor een overzicht van Hallo inhoud van het serviceproject Hallo [aan de slag met Reliable Services](service-fabric-reliable-services-quick-start.md).

## <a name="deploy-and-debug-hello-application"></a>Implementeren en fouten opsporen in de toepassing hello

Nu u een toepassing hebt, kunt u deze uitvoeren.

Druk in Visual Studio op `F5` toodeploy Hallo-toepassing voor foutopsporing.

>[!NOTE]
>Hallo maakt eerst u uitvoeren en implementeren van Hallo toepassing lokaal door Visual Studio een lokaal cluster voor foutopsporing. Dit kan enige tijd duren. status van het Hallo-cluster maken wordt weergegeven in Visual Studio-uitvoervenster Hallo.

Wanneer Hallo cluster klaar is, kunt u een melding krijgt van Hallo lokale cluster system lade manager-toepassing Hello SDK is opgenomen.
   
![Melding van het systeemvak van het lokale cluster][4]

Eenmaal Hallo toepassing wordt gestart, Visual Studio automatisch wordt Hallo **diagnostische logboeken**, waar u de trace-uitvoer van uw services kunt zien.
   
![Diagnostische logboeken][5]

Hallo stateful servicesjabloon we gebruikt gewoon toont een teller waarde en oplopend in stappen in Hallo `RunAsync` methode van **MyStatefulService.cs**.

Vouw een van de Hallo gebeurtenissen toosee meer informatie, zoals Hallo knooppunt waarop Hallo code wordt uitgevoerd. In dit geval is het \_Node\_2. Dit kan anders zijn op uw machine.
   
![Details van de gebeurtenissenviewer][6]

Hallo lokale cluster bevat vijf knooppunten die worden gehost op een enkele computer. In een productieomgeving wordt elk knooppunt gehost op een afzonderlijke fysieke of virtuele machine. foutopsporing toosimulate Hallo verlies van een machine tijdens het Hallo Visual Studio uitoefenen op Hallo dezelfde tijd, laten we bekijken een van de knooppunten op het lokale cluster Hallo Hallo.

In Hallo **Solution Explorer** venster open **MyStatefulService.cs**. 

Hallo zoeken `RunAsync` methode en stel een onderbrekingspunt in op de eerste regel Hallo van Hallo-methode.

![Onderbrekingspunt in de stateful service RunAsync-methode][7]

Hallo starten **Service Fabric Explorer** hulpprogramma door met de rechtermuisknop op Hallo **lokaal Clusterbeheer** lade systeemtoepassing en kies **lokaal Cluster beheren**.

![Start Service Fabric Explorer vanuit lokaal Clusterbeheer Hallo][systray-launch-sfx]

[**Service Fabric Explorer** ](service-fabric-visualizing-your-cluster.md) biedt een visuele weergave van een cluster. Dit omvat Hallo set toepassingen die zijn geïmplementeerd tooit en Hallo set van fysieke knooppunten waaruit het bestaat.

Vouw in het linkerdeelvenster hello, **Cluster > knooppunten** en zoeken Hallo knooppunt waarop uw code wordt uitgevoerd.

Klik op **Acties > uitschakelen (opnieuw opstarten)** toosimulate een machine opnieuw te starten.

![Een knooppunt in Service Fabric Explorer stoppen][sfx-stop-node]

Tijdelijk worden, ziet u uw onderbrekingspunt in Visual Studio bereikt, zoals Hallo berekening u op één knooppunt naadloos uitvoerde overgenomen tooanother wordt.


Vervolgens retourneert toohello diagnostische logboeken en Hallo-berichten te zien. Hallo item is voortgezet en oplopend in stappen, zelfs als Hallo gebeurtenissen daadwerkelijk afkomstig zijn uit een ander knooppunt.

![Details van de gebeurtenissenviewer na een failover][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a>Opruimen van de lokale cluster hello (optioneel)

Vergeet niet dat dit lokale cluster echt bestaat. Hallo debugger wordt gestopt, verwijdert het toepassingsexemplaar van uw en heft de registratie van toepassingstype Hallo. Hallo cluster blijft echter toorun op Hallo achtergrond. Wanneer u klaar toostop Hallo lokale cluster bent, zijn er een aantal opties.

### <a name="keep-application-and-trace-data"></a>Toepassing behouden en gegevens traceren

Hallo cluster afgesloten door met de rechtermuisknop op Hallo **lokaal Clusterbeheer** lade systeemtoepassing en kies vervolgens **lokaal Cluster stoppen**.

### <a name="delete-hello-cluster-and-all-data"></a>Hallo-cluster en alle gegevens verwijderen

Hallo-cluster verwijderen door met de rechtermuisknop op Hallo **lokaal Clusterbeheer** lade systeemtoepassing en kies vervolgens **lokaal Cluster verwijderen**. 

Als u deze optie kiest, Visual Studio wordt opnieuw implementeren Hallo cluster Hallo zodra uw uitvoeren Hallo toepassing. Selecteer deze optie als u niet van plan toouse Hallo lokale cluster gedurende een bepaalde periode bent of als u tooreclaim bronnen nodig.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [betrouwbare services](service-fabric-reliable-services-introduction.md).
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
