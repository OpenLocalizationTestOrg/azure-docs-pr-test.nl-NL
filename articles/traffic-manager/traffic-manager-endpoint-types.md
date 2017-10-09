---
title: aaaTraffic Manager Eindpunttypen | Microsoft Docs
description: Dit artikel wordt uitgelegd voor verschillende soorten eindpunten die kunnen worden gebruikt met Azure Traffic Manager
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 4e506986-f78d-41d1-becf-56c8516e4d21
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: kumud
ms.openlocfilehash: 787412ac6207f76791bf3ff753d1df2767b1a964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoints"></a>Traffic Manager-eindpunten
Microsoft Azure Traffic Manager kunt u toocontrol hoe netwerkverkeer is gedistribueerd tooapplication implementaties uitgevoerd in verschillende datacenters. U configureren elke implementatie van toepassing als een 'eindpunt' in Traffic Manager. Wanneer het Traffic Manager een DNS-aanvraag ontvangt, kiest deze een tooreturn beschikbare eindpunt in Hallo DNS-antwoord. Het Traffic manager baseert Hallo keuze op de huidige status van endpoint Hallo en Hallo verkeersroutering methode. Zie voor meer informatie [hoe Traffic Manager werkt](traffic-manager-how-traffic-manager-works.md).

Er zijn drie soorten eindpunt ondersteund door Traffic Manager:
* **Azure-eindpunten** worden gebruikt voor services die worden gehost in Azure.
* **Externe eindpunten** worden gebruikt voor services die worden gehost buiten Azure, on-premises of bij een andere hostingprovider.
* **Genest eindpunten** gebruikte toocombine Traffic Manager-profielen toocreate flexibelere verkeersroutering schema's toosupport Hallo behoeften van grotere, complexe implementaties zijn.

Er is geen beperking op hoe de eindpunten van verschillende typen worden gecombineerd in één Traffic Manager-profiel. Elk profiel kan elke combinatie van eindpunttypen bevatten.

Hallo volgende secties beschrijven elk eindpunttype verdiepen.

## <a name="azure-endpoints"></a>Azure-eindpunten

Azure-eindpunten worden gebruikt voor op basis van een Azure-services in Traffic Manager. Hallo na Azure brontypen die worden ondersteund:

* 'Klassiek' IaaS VM's en PaaS-cloudservices.
* Web Apps
* PublicIPAddress bronnen (dit kunnen verbonden tooVMs rechtstreeks of via een Azure Load Balancer). Hallo publicIpAddress moet een DNS-naam toegewezen toobe gebruikt in een Traffic Manager-profiel hebben.

PublicIPAddress resources zijn Azure Resource Manager-resources. Ze bestaan niet in het klassieke implementatiemodel Hallo. Ze zijn daarom alleen ondersteund in Traffic Manager van Azure Resource Manager-ervaringen. Hallo worden andere endpoint-typen ondersteund via Resource Manager en de Hallo klassieke implementatiemodel.

Wanneer u Azure-eindpunten, detecteert de Traffic Manager als een 'Classic' IaaS VM, cloudservice of een Web-App is gestopt en gestart. Deze status wordt weergegeven in de status van de endpoint Hallo. Zie [Traffic Manager eindpuntcontrole](traffic-manager-monitoring.md#endpoint-and-profile-status) voor meer informatie. Wanneer Hallo onderliggende service is gestopt, voert Traffic Manager geen eindpunt statuscontroles of directe verkeer toohello eindpunt. Er is geen Traffic Manager facturering voor Hallo gebeurtenissen exemplaar is gestopt. Wanneer het Hallo-service opnieuw wordt opgestart, hervat facturering en het Hallo-eindpunt is in aanmerking komende tooreceive verkeer. Deze detectie tooPublicIpAddress eindpunten niet van toepassing.

## <a name="external-endpoints"></a>Externe eindpunten

Externe eindpunten worden gebruikt voor services buiten Azure. Bijvoorbeeld een service die lokaal worden gehost of met een andere provider. Externe eindpunten kunnen worden gebruikt afzonderlijk of in combinatie met Azure-eindpunten in Hallo dezelfde Traffic Manager-profiel. Azure-eindpunten met externe eindpunten combineren, kunt verschillende scenario's:

* In beide een actief-actief of actief / passief failover-model Azure tooprovide verhoogd redundantie voor een bestaande on-premises toepassing te gebruiken.
* tooreduce application latentie voor gebruikers Hallo wereld, breid een bestaande lokale toepassing tooadditional geografische locaties in Azure. Zie voor meer informatie [Traffic Manager 'Prestaties' voor verkeersroutering](traffic-manager-routing-methods.md#performance).
* Gebruik Azure tooprovide extra capaciteit voor een bestaande on-premises toepassing continu of als een 'burst-naar-cloud' oplossing toomeet een piek in de aanvraag.

In bepaalde gevallen is het nuttig toouse externe eindpunten tooreference Azure services (Zie voor voorbeelden Hallo [Veelgestelde vragen over](traffic-manager-faqs.md#traffic-manager-endpoints)). In dit geval wordt statuscontroles gefactureerd snelheid hello Azure-eindpunten, niet Hallo externe eindpunten snelheid. Echter, in tegenstelling tot Azure-eindpunten, als u stoppen of verwijderen van de onderliggende service, Hallo Serverstatus controleren facturering wordt vervolgd totdat u uitschakelen of verwijderen van Hallo eindpunt in Traffic Manager.

## <a name="nested-endpoints"></a>Geneste eindpunten

Geneste eindpunten combineren meerdere Traffic Manager profielen toocreate flexibele verkeersroutering schema's en ondersteuning Hallo behoeften van grotere, complexe implementaties. Met geneste eindpunten, wordt een profiel 'onderliggend item' toegevoegd als een eindpunt tooa 'parent'-profiel. Beide profielen van onderliggende en bovenliggende Hallo kunnen andere eindpunten van elk type, met inbegrip van andere geneste profielen bevatten. Zie voor meer informatie [Traffic Manager-profielen genest](traffic-manager-nested-profiles.md).

## <a name="web-apps-as-endpoints"></a>Web Apps als eindpunten

Enkele aanvullende overwegingen bij het configureren van Web-Apps als eindpunten in Traffic Manager van toepassing:

1. Alleen Web-Apps op Hallo 'Standaard' SKU of boven komen in aanmerking voor gebruik met Traffic Manager. Probeert tooadd een Web-App van een lagere SKU-mislukken. Hallo downgraden resulteert SKU van een bestaande Web-App in Traffic Manager, verkeer toothat Web-App niet meer verzonden.
2. Wanneer een eindpunt een HTTP-aanvraag ontvangt, gebruikt het 'host' Hallo-header in Hallo aanvraag toodetermine welke Web-App moet Hallo service aanvragen. Hallo host-header bevat Hallo DNS-naam die wordt gebruikt tooinitiate Hallo aanvraag, bijvoorbeeld contosoapp.azurewebsites.net. toouse een andere DNS-naam met uw Web-App Hallo DNS-naam moet worden geregistreerd als een aangepaste domeinnaam voor Hallo App. Wanneer u een Web-App-eindpunt toevoegt als een Azure-eindpunt, wordt automatisch Hallo Traffic Manager-profiel DNS-naam voor Hallo App geregistreerd. Deze registratie automatisch verwijderd wanneer het Hallo-eindpunt wordt verwijderd.
3. Elke Traffic Manager-profiel kan maximaal één eindpunt van Web-App van elke Azure-regio hebben. toowork rond voor deze beperking, kunt u een Web-App configureren als een extern eindpunt. Zie voor meer informatie, Hallo [Veelgestelde vragen over](traffic-manager-faqs.md#traffic-manager-endpoints).

## <a name="enabling-and-disabling-endpoints"></a>Inschakelen en uitschakelen van eindpunten

Uitschakelen van een eindpunt in Traffic Manager is nuttig tootemporarily verwijderen verkeer van een eindpunt dat in de onderhoudsmodus of opnieuw wordt geïmplementeerd. Zodra Hallo eindpunt opnieuw actief is, kan het zijn opnieuw worden ingeschakeld.

Eindpunten kunnen worden ingeschakeld en worden uitgeschakeld via Hallo Traffic Manager-portal, PowerShell, CLI of REST API, die allemaal worden ondersteund in zowel het klassieke implementatiemodel Hallo als Resource Manager.

> [!NOTE]
> Uitschakelen van een Azure-eindpunt heeft niets toodo met de implementatiestatus in Azure. Een Azure-service (zoals een virtuele machine of Web-App blijft actief en kunnen tooreceive verkeer zelfs wanneer uitgeschakeld in Traffic Manager. Verkeer kan worden verholpen direct toohello service-exemplaar in plaats van via Hallo Traffic Manager-profiel DNS-naam. Zie voor meer informatie [de werking van Traffic Manager](traffic-manager-how-traffic-manager-works.md).

Hallo huidige geschiktheid van elk eindpunt tooreceive verkeer, is afhankelijk van Hallo volgende factoren:

* status van het profiel hello (ingeschakeld/uitgeschakeld)
* status van de endpoint hello (ingeschakeld/uitgeschakeld)
* Hallo-resultaten van statuscontroles Hallo voor dat eindpunt

Zie voor meer informatie [Traffic Manager eindpuntcontrole](traffic-manager-monitoring.md#endpoint-and-profile-status).

> [!NOTE]
> Aangezien Traffic Manager op Hallo DNS-niveau werkt, is het tooinfluence bestaande verbindingen tooany eindpunt. Wanneer u een eindpunt niet beschikbaar is, stuurt Traffic Manager nieuwe verbindingen tooanother beschikbare eindpunt. Hallo host achter Hallo uitgeschakeld of slecht eindpunt kan echter tooreceive verkeer via bestaande verbindingen blijven totdat deze sessies worden beëindigd. Toepassingen beperken Hallo sessie duur tooallow verkeer toodrain van bestaande verbindingen.

Als alle eindpunten in een profiel zijn uitgeschakeld of als het Hallo-profiel zelf is uitgeschakeld, verzendt een 'NXDOMAIN' antwoord tooa nieuwe DNS-query met Traffic Manager.


## <a name="next-steps"></a>Volgende stappen

* Meer informatie over [de werking van Traffic Manager](traffic-manager-how-traffic-manager-works.md).
* Meer informatie over het Traffic Manager [eindpunt bewakings- en automatische failover](traffic-manager-monitoring.md).
* Meer informatie over het Traffic Manager [verkeersrouteringsmethoden](traffic-manager-routing-methods.md).
