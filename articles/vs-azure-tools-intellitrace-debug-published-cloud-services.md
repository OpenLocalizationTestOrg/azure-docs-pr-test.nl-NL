---
title: aaaDebugging een gepubliceerde een Azure-cloudservice met Visual Studio en IntelliTrace | Microsoft Docs
description: Meer informatie over hoe toodebug een cloud service met Visual Studio en IntelliTrace
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a>Een gepubliceerde Azure-cloudservice met Visual Studio en IntelliTrace-foutopsporing
U kunt uitgebreide foutopsporingsinformatie voor een rolexemplaar van met IntelliTrace registreren wanneer deze wordt uitgevoerd in Azure. Als u toofind Hallo oorzaak van een probleem moet, kunt u Hallo IntelliTrace-logboeken toostep via uw code vanuit Visual Studio als in Azure werd uitgevoerd. In feite replay IntelliTrace records sleutel code kan worden uitgevoerd en de omgeving gegevens wanneer uw Azure-toepassing wordt uitgevoerd als een cloudservice in Azure, en u kunt gegevens Hallo vastgelegd vanuit Visual Studio. 

U kunt IntelliTrace hebt u Visual Studio Enterprise geïnstalleerd en de doelen van uw Azure-toepassing .NET Framework 4 of hoger gebruiken. IntelliTrace verzamelt gegevens voor uw Azure-functies. Hallo virtuele machines voor deze rollen altijd 64-bits besturingssystemen worden uitgevoerd.

Als alternatief kunt u [foutopsporing op afstand](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach rechtstreeks tooa cloudservice die wordt uitgevoerd in Azure.

> [!IMPORTANT]
> IntelliTrace is bedoeld voor foutopsporing scenario's alleen en mag niet worden gebruikt voor een productie-implementatie.
> 

## <a name="configure-an-azure-application-for-intellitrace"></a>Een Azure-toepassing voor IntelliTrace configureren
tooenable IntelliTrace voor een Azure-toepassing, moet u maken en publiceren van de toepassing hello uit een Azure met Visual Studio-project. Voordat u deze tooAzure publiceert, moet u de IntelliTrace configureren voor uw Azure-toepassing. Als u uw toepassing publiceert zonder IntelliTrace configureren, moet u toorepublish Hallo project. Zie voor meer informatie [publiceren van een Azure cloud services-projecten met Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).

1. Wanneer u bent klaar toodeploy uw Azure-toepassing, Controleer of de doelen van uw project build te worden ingesteld**Debug**.

1. In **Solution Explorer**, met de rechtermuisknop op het project en selecteer in het contextmenu hello, **publiceren**.
   
1. In Hallo **Publish Azure Application** dialoogvenster, selecteer hello Azure-abonnement en selecteert u **volgende**.

1. In Hallo **instellingen** pagina, selecteer Hallo **geavanceerde instellingen** tabblad.

1. Hallo inschakelen **IntelliTrace inschakelen** optie toocollect IntelliTrace-logboeken voor uw toepassing wanneer het wordt gepubliceerd in de cloud Hallo.
   
1. toocustomize hello IntelliTrace basisconfiguratie, selecteer **instellingen** volgende te**IntelliTrace inschakelen**.

    ![Koppeling van IntelliTrace-instellingen](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. In Hallo **IntelliTrace instellingen** dialoogvenster kunt u opgeven welke gebeurtenissen toolog, of de informatie voor het aanroepen van toocollect, welke processen en -modules toocollect logboeken voor en hoeveel ruimte tooallocate toohello opnemen. Zie voor meer informatie over IntelliTrace [foutopsporing met IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).
   
    ![IntelliTrace-instellingen](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

Hallo IntelliTrace-logboek is een circulair logboekbestand van de maximale grootte Hallo opgegeven in de Hallo IntelliTrace-instellingen (standaardgrootte Hallo is 250 MB). IntelliTrace-logboeken zijn verzameld tooa-bestand in het bestandssysteem Hallo van Hallo virtuele machine. Wanneer u Logboeken Hallo aanvraagt, wordt een momentopname is gemaakt op dat moment en de lokale computer tooyour gedownload.

Nadat u gepubliceerde tooAzure hello Azure-cloudservice hebt, kunt u bepalen als IntelliTrace is ingeschakeld vanaf hello Azure knooppunt in **Server Explorer**, zoals weergegeven in Hallo installatiekopie te volgen:

![Server Explorer - IntelliTrace ingeschakeld](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a>IntelliTrace-logboeken voor een rolexemplaar van downloaden
U kunt met behulp van Visual Studio IntelliTrace-logboeken voor een rolexemplaar van downloaden met de volgende stappen:

1. In **Server Explorer**, vouw Hallo **Cloudservices** knooppunt, en zoek rolinstantie waarvan u wilt dat toodownload Logboeken. 

1. Met de rechtermuisknop op de rolinstantie hello en selecteer in het contextmenu Hallo s, **IntelliTrace-logboeken bekijken**. 

    ![Menuoptie voor IntelliTrace-logboeken weergeven](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. Hallo IntelliTrace-logboeken zijn gedownloade tooa bestand in een map op uw lokale computer. Elke keer dat u Hallo IntelliTrace-logboeken aanvragen, wordt een nieuwe momentopname gemaakt. Tijdens het Hallo-logboeken worden gedownload, Visual Studio Hallo geeft voortgang weer van Hallo-bewerking in Hallo **Azure Activity Log** venster. Zoals u in de volgende afbeelding Hallo, kunt u uitbreiden Hallo regelitem voor Hallo bewerking toosee meer details.

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

In Visual Studio kunt u toowork blijven terwijl Hallo IntelliTrace-logboeken worden gedownload. Wanneer het Hallo-logboek is gedownload, wordt het geopend in Visual Studio.

> [!NOTE]
> Hallo IntelliTrace-logboeken bevatten mogelijk uitzonderingen die framework Hallo genereert en daarna worden verwerkt. Interne framework code genereert deze uitzonderingen als een normaal onderdeel van het opstarten van een rol, zodat u ze kunt negeren.
> 
> 

## <a name="next-steps"></a>Volgende stappen
- [Opties voor het opsporen van Azure-cloudservices](vs-azure-tools-debugging-cloud-services-overview.md)
- [Publiceren van een Azure-cloudservice met Visual Studio](vs-azure-tools-publishing-a-cloud-service.md)