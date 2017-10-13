---
title: Gegevensbeveiliging in Azure Security Center | Microsoft Docs
description: In dit document wordt uitgelegd hoe gegevens worden beheerd en beveiligd in Azure Security Center.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 33f2c9f4-21aa-4f0c-9e5e-4cd1223e39d7
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: yurid
ms.openlocfilehash: 6f95cf7631664f4630edbbcdadfd1d98105fdb98
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/11/2017
---
# <a name="azure-security-center-data-security"></a>Gegevensbeveiliging in Azure Security Center
Om klanten te helpen bedreigingen te voorkomen, te detecteren en erop te reageren, verzamelt en verwerkt Azure Security Center gegevens over beveiliging, zoals configuratie-informatie, metagegevens, gebeurtenislogboeken, crashdumpbestanden en nog veel meer. Microsoft voldoet aan strikte nalevings- en beveiligingsrichtlijnen - van het schrijven van code tot de uitvoering van een service.

In dit artikel wordt uitgelegd hoe gegevens worden beheerd en beveiligd in Azure Security Center.

>[!NOTE] 
>Vanaf begin juni 2017 zal Security Center de Microsoft Monitoring Agent gebruiken voor het verzamelen en opslaan van gegevens. Zie [Migratie van Azure Security Center-platform](security-center-platform-migration.md) voor meer informatie. De informatie in dit artikel beschrijft functionaliteit van Security Center na de overstap naar de Microsoft Monitoring Agent.
>


## <a name="data-sources"></a>Gegevensbronnen
Azure Security Center analyseert gegevens uit de volgende bronnen om inzicht in uw beveiligingsstatus te geven, beveiligingsproblemen te identificeren, oplossingen aan te raden en actieve bedreigingen te detecteren:

- Azure Services: gebruikt informatie over de configuratie van de Azure-services die u hebt geïmplementeerd door te communiceren met de resourceprovider van die service.
- Netwerkverkeer: gebruikt steekproefgewijs netwerkverkeermetagegevens uit de infrastructuur van Microsoft, zoals bron-/doel-IP/poort, pakketgrootte en netwerkprotocol.
- Oplossingen van partners: gebruikt beveiligingswaarschuwingen van geïntegreerde partneroplossingen, zoals firewalls en antimalwareoplossingen. 
- Uw virtuele machines en servers: gebruikt configuratiegegevens en informatie over beveiligingsgebeurtenissen, zoals Windows-gebeurtenis- en auditlogboeken, IIS-logboeken, syslog-berichten en crashdumpbestanden van uw virtuele machines. Bovendien kan Azure Security Center wanneer er een waarschuwing wordt gemaakt een momentopname maken van de beïnvloede VM-schijf en machine-artefacten gekoppeld aan de waarschuwing van de VM-schijf, zoals een registerbestand, extraheren voor onderzoeksdoeleinden.


## <a name="data-protection"></a>Gegevensbeveiliging
**Scheiding van gegevens**: gegevens worden op een logische manier apart van elkaar gehouden, in elk onderdeel van de service. Alle gegevens worden gemarkeerd per organisatie. Deze markering blijft aanwezig gedurende de levenscyclus van de gegevens en deze wordt afgedwongen op elke laag van de service.

**Gegevenstoegang**: om beveiligingsaanbevelingen te doen en mogelijke beveiligingsrisico's te onderzoeken, kunnen medewerkers van Microsoft gegevens die zijn verzameld of geanalyseerd door Azure-services openen, waaronder crashdumpbestanden, procesgebeurtenissen, momentopnamen van de VM-schijf en artefacten, die onbedoeld klantgegevens of persoonlijke gegevens bevatten van uw virtuele machines. We voldoen aan de [voorwaarden voor Microsoft Online Services en de Privacyverklaring](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), die stellen dat Microsoft niet de klantgegevens gebruikt of gegevens ervan afleidt voor reclame- of vergelijkbare commerciële doeleinden. We gebruiken klantgegevens alleen indien nodig om u Azure-services te bieden, met inbegrip van doeleinden die compatibel zijn met het leveren van die services. U behoudt alle rechten op de klantgegevens.

**Gegevensgebruik**: Microsoft gebruikt informatie over patronen en bedreigingen die worden gezien tussen meerdere tenants voor het verbeteren van onze mogelijkheden voor voorkoming en detectie; wij doen dit in overeenstemming met de privacyverplichtingen beschreven in onze [Privacyverklaring](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

## <a name="data-location"></a>Gegevenslocatie

**Uw werkruimte(n)**: er wordt een werkruimte opgegeven voor de volgende geografische gebieden, en gegevens die worden verzameld van uw virtuele machines in Azure, waaronder crashdumps en bepaalde typen waarschuwingsgegevens, worden opgeslagen in de dichtstbijzijnde werkruimte. 

| Geografisch gebied van virtuele machine                        | Geografisch gebied van werkruimte |
|-------------------------------|---------------|
| Verenigde Staten, Brazilië, Canada | Verenigde Staten |
| Europa, Verenigd Koninkrijk        | Europa        |
| Azië en Stille Oceaan, Japan, India    | Azië en Stille Oceaan  |
| Australië                     | Australië     |

 
Momentopnamen van de VM-schijf worden opgeslagen in hetzelfde opslagaccount als de VM-schijf.
 
Voor virtuele machines en servers die in andere omgevingen worden uitgevoerd, bijvoorbeeld on-premises, kunt u de werkruimte en de regio opgeven waarin verzamelde gegevens worden opgeslagen. 

**Azure Security Center-opslag**: informatie over beveiligingswaarschuwingen, met inbegrip van waarschuwingen van partners, wordt regionaal opgeslagen op basis van de locatie van de gerelateerde Azure-resource, terwijl informatie over de status van de beveiliging en aanbevelingen centraal wordt opgeslagen in de Verenigde Staten of in Europa, afhankelijk van de locatie van de klant.
Azure Security Center verzamelt tijdelijke kopieën van uw crashdumpbestanden en analyseert deze op bewijs van pogingen tot misbruik en geslaagde aanvallen. Azure Security Center voert deze analyse uit binnen hetzelfde geografische gebied als de werkruimte en verwijdert de tijdelijke kopieën wanneer de analyse is voltooid.

Machine-artefacten worden centraal opgeslagen in dezelfde regio als de virtuele machine. 


## <a name="managing-data-collection-from-virtual-machines"></a>Gegevensverzameling van virtuele machines beheren

Wanneer u Security Center inschakelt in Azure, wordt gegevensverzameling ingeschakeld voor elk van uw Azure-abonnementen. U kunt gegevensverzameling voor uw abonnementen ook inschakelen in het gedeelte Beveiligingsbeleid van Azure Security Center. Wanneer gegevensverzameling is ingeschakeld, levert Azure Security Center de Microsoft Monitoring Agent op alle bestaande, ondersteunde virtuele machines in Azure en op nieuwe virtuele machines die worden gemaakt. De Microsoft Monitoring Agent scant op verschillende aan beveiliging gerelateerde configuraties en legt gebeurtenissen vast in [Event Tracing for Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx)-traceringen (ETW). Bovendien worden door het besturingssysteem gebeurtenislogboekgebeurtenissen gegenereerd tijdens het uitvoeren van de machine. Voorbeelden van dergelijke gegevens zijn: besturingssysteemtype en -versie, besturingssysteemlogboeken (Windows-gebeurtenislogboeken), actieve processen, computernaam, IP-adressen, aangemelde gebruiker en tenant-ID. De Microsoft Monitoring Agent leest vermeldingen in gebeurtenislogboeken en ETW-traceringen en kopieert deze voor analyse naar uw werkruimte(n). De Microsoft Monitoring Agent kopieert ook crashdumpbestanden naar uw werkruimte(n).

Als u de gratis variant van Azure Security Center gebruikt, kunt u het verzamelen van gegevens van virtuele machines ook uitschakelen in het beveiligingsbeleid. Het verzamelen van gegevens is vereist voor abonnementen uit de prijscategorie Standard. De verzameling van momentopnamen en artefacten voor de VM-schijf is nog steeds ingeschakeld, zelfs als het verzamelen van gegevens is uitgeschakeld.


## <a name="see-also"></a>Zie ook
In dit document hebt u geleerd hoe gegevens worden beheerd en beveiligd in Azure Security Center. Zie de volgende onderwerpen voor meer informatie over Azure Security Center:

* [Plannings- en bedieningsgids voor het Azure Beveiligingscentrum](security-center-planning-and-operations-guide.md): leer de ontwerpoverwegingen kennen en plan hiervoor bij de overstap naar Azure Security Center.
* [Security health monitoring in Azure Security Center](security-center-monitoring.md) (Beveiligingsstatus controleren in Azure Security Center): meer informatie over het controleren van de status van uw Azure-resources
* [Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center](security-center-managing-and-responding-alerts.md): leer hoe u beveiligingswaarschuwingen kunt beheren en erop kunt reageren
* [Partneroplossingen controleren met Azure Security Center](security-center-partner-solutions.md): leer hoe u de integriteitsstatus van uw partneroplossingen kunt controleren.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md): raadpleeg veelgestelde vragen over het gebruik van de service
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure
