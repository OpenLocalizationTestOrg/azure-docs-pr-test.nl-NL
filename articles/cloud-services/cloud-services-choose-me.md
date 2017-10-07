---
title: aaaAzure compute opties - Cloudservices | Microsoft Docs
description: 'Meer informatie over Azure compute hosting-opties en hoe deze werken: App Service, Cloud Services en virtuele Machines'
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
ms.assetid: ed7ad348-6018-41bb-a27d-523accd90305
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: e7f109a54c61cc2f37644d39a61d2d932a374587
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-choose-cloud-services-or-something-else"></a>Moet ik kiezen cloudservices of iets anders?
Azure Cloud Services Hallo keuze is voor u? Azure biedt verschillende hosting modellen voor het uitvoeren van toepassingen. Elk een andere set services biedt, waarvan één zodat u kiest is afhankelijk van precies wat u probeert toodo.

[!INCLUDE [compute-table](../../includes/compute-options-table.md)]

<a name="tellmecs"></a>

## <a name="tell-me-about-cloud-services"></a>Meer informatie over cloudservices
Cloud-Services is een voorbeeld van [Platform as a Service](https://azure.microsoft.com/overview/what-is-paas/) (PaaS). Zoals [App Service](../app-service-web/app-service-web-overview.md), deze technologie is ontworpen toosupport toepassingen die schaalbare, betrouwbare en goedkope toooperate. Net zoals een App Service wordt gehost op virtuele machines, te zijn Cloud Services, maar u hebt meer controle over Hallo virtuele machines. U kunt uw eigen software installeren op virtuele machines voor Cloud Services en u kunt externe in deze.

![cs_diagram](./media/cloud-services-choose-me/diagram.png)

Meer controle betekent ook minder eenvoudig te gebruiken. Tenzij u nodig hebt Hallo extra controle-opties, is doorgaans sneller en eenvoudiger tooget een webtoepassing en tooCloud Services uitgevoerd in de Web-Apps in App Service vergeleken.

Er zijn twee soorten Cloud Service-rollen. Hallo enige verschil tussen Hallo twee is hoe uw rol wordt gehost op Hallo virtuele machine.

* **Webrol**  
Automatisch implementeert en als host fungeert voor uw app via IIS.

* **Werkrol**  
Maakt geen gebruik van IIS en wordt uw zelfstandige app wordt uitgevoerd.

Een eenvoudige toepassing kan bijvoorbeeld slechts een enkele Webrol, voor een website te gebruiken. Een complexere toepassing mogelijk gebruik van een rol web toohandle binnenkomende aanvragen van gebruikers, geeft deze aanvragen op de werkrol tooa voor verwerking. (Deze communicatie kan gebruiken [Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md) of [Azure wachtrijen](../storage/common/storage-introduction.md).)

Als Hallo voorgaande afbeelding wordt voorgesteld, alle virtuele machines Hallo in één toepassing uitvoeren in Hallo dezelfde cloudservice. Gebruikers toegang Hallo toepassing via één openbaar IP-adres, met aanvragen automatisch taakverdeling over VM's van de toepassing hello. Hallo platform [schaalt en implementeert](cloud-services-how-to-scale.md) Hallo van virtuele machines in een Cloud Services-toepassing op een manier die een potentieel hardwarefout voorkomt.

Hoewel toepassingen in virtuele machines uitvoeren, is het belangrijk toounderstand dat Cloudservices PaaS, niet IaaS biedt. Hier volgt eenrichtingssessie toothink erover: met IaaS, zoals Azure Virtual Machines u maakt eerst en uw toepassing wordt uitgevoerd in Hallo-omgeving configureren en implementeren van uw toepassing in deze omgeving. U bent zelf verantwoordelijk voor het beheren van veel van deze world doen, zoals het implementeren van nieuwe patches versies van het besturingssysteem Hallo in elke virtuele machine. In PaaS, daarentegen, is het alsof er Hallo omgeving bestaat. Hoeft u deze toodo is uw toepassing te implementeren. Hallo-platform die op wordt uitgevoerd, zoals het implementeren van nieuwe versies van het besturingssysteem hello, wordt beheerd voor u.

## <a name="scaling-and-management"></a>Schaalbaarheid en beheer
U kunt virtuele machines niet maken met Cloud-Services. In plaats daarvan het bieden van een configuratiebestand dat Azure aangeeft hoeveel van elk gewenst zoals **drie rolinstanties web** en **twee exemplaren van worker-rol**, en het Hallo-platform deze voor u gemaakt.  U nog steeds kiezen [welke grootte](cloud-services-sizes-specs.md) die back-ups maken van virtuele machines moeten worden, maar u niet expliciet ze zelf maken. Als uw toepassing toohandle een grotere belasting moet, kunt u vragen voor meer virtuele machines en Azure maakt die exemplaren. Als Hallo belasting afneemt, kunt u die exemplaren afgesloten en stoppen betaalt voor hen.

Een Cloud Services-toepassing bestaat meestal beschikbaar toousers via een proces in twee stappen. Een ontwikkelaar eerste [uploads toepassing hello](cloud-services-how-to-create-deploy.md) toohello platform het faseringsgebied. Wanneer ontwikkelaars Hallo gereed toomake Hallo toepassing live, gebruiken ze hello Azure portal tooswap fasering met productie. Dit [schakelen tussen Faseren en productie](cloud-services-nodejs-stage-application.md) kan plaatsvinden zonder uitvaltijd, waarmee een actieve toepassing worden de nieuwe versie van de bijgewerkte tooa zonder de gebruikers te verstoren.

## <a name="monitoring"></a>Bewaking
Cloud-Services biedt ook de bewaking. Als Azure virtuele Machines die het detecteert een mislukte fysieke server en Hallo virtuele machines die werden uitgevoerd op die server op een nieuwe machine opnieuw is opgestart. Maar Cloudservices detecteert ook mislukte VM's en toepassingen, niet alleen hardwarefouten. In tegenstelling tot virtuele Machines, hieraan een agent binnen elke rol web- en werkrollen, en het is daarom toostart kunnen nieuwe VM's en exemplaren van een toepassing als er fouten optreden.

Hallo PaaS aard van Cloudservices heeft andere gevolgen te. Een van de belangrijkste Hallo is waarin toepassingen is gebaseerd op deze technologie worden geschreven toorun correct als een willekeurig exemplaar van de functie web- of worker is mislukt. dit een Cloud-Services die toepassing hoort niet onderhouden in status tooachieve Hallo bestandssysteem van een eigen virtuele machines. In tegenstelling tot VM's zijn gemaakt met Azure Virtual Machines, schrijfbewerkingen aangebracht tooCloud Services VM's zijn niet permanent. Er is niet op een gegevensschijf virtuele Machines. In plaats daarvan een toepassing moet expliciet Cloudservices schrijven alle status tooSQL Database, blobs, tabellen of andere externe opslag. Maken van toepassingen op deze manier zorgt ervoor dat ze gemakkelijker tooscale en beter bestand zijn tegen toofailure beide belangrijke doelstellingen van Cloudservices.

## <a name="next-steps"></a>Volgende stappen
[Een cloud service-app maken in .NET](cloud-services-dotnet-get-started.md)  
[Een cloud service-app maken in Node.js](cloud-services-nodejs-develop-deploy-app.md)  
[Een cloud service-app maken in PHP](../cloud-services-php-create-web-role.md)  
[Een cloud service-app maken in Python](cloud-services-python-ptvs.md)

