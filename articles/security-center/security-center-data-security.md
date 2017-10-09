---
title: Security Center-gegevensbeveiliging aaaAzure | Microsoft Docs
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
ms.openlocfilehash: 30f8b11272dc5df6d485608abdaa62ba57e63f23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-data-security"></a>Gegevensbeveiliging in Azure Security Center
toohelp klanten detecteren, voorkomen van en reageren toothreats, Azure Security Center verzamelt en beveiliging gerelateerde gegevens, inclusief informatie over de configuratie, metagegevens, gebeurtenislogboeken, crashdumpbestanden en meer verwerkt. Microsoft toostrict naleving en beveiliging richtlijnen voldoet, van een service toooperating coderen.

In dit artikel wordt uitgelegd hoe gegevens worden beheerd en beveiligd in Azure Security Center.

>[!NOTE] 
>Begin juni 2017 vanaf kan Security Center Hallo Microsoft Monitoring Agent toocollect gebruiken en opslaan van gegevens. Zie [Azure Security Center-Platform migratie](security-center-platform-migration.md) toolearn meer. Hallo-informatie in dit artikel beschrijft Security Center functionaliteit na de overgang toohello Microsoft Monitoring Agent.
>


## <a name="data-sources"></a>Gegevensbronnen
Azure Security Center analyseert gegevens van Hallo bronnen tooprovide zichtbaarheid in uw beveiligingsstatus te volgen, kwetsbaarheden identificeren en oplossingen het beste actieve bedreigingen te detecteren:

- Azure-Services: Informatie over Hallo configuratie van Azure-services die u hebt geïmplementeerd door de communicatie met die service resourceprovider gebruikt.
- Netwerkverkeer: gebruikt steekproefgewijs netwerkverkeermetagegevens uit de infrastructuur van Microsoft, zoals bron-/doel-IP/poort, pakketgrootte en netwerkprotocol.
- Oplossingen van partners: gebruikt beveiligingswaarschuwingen van geïntegreerde partneroplossingen, zoals firewalls en antimalwareoplossingen. 
- Uw virtuele machines en servers: gebruikt configuratiegegevens en informatie over beveiligingsgebeurtenissen, zoals Windows-gebeurtenis- en auditlogboeken, IIS-logboeken, syslog-berichten en crashdumpbestanden van uw virtuele machines. Bovendien wanneer een waarschuwing is gemaakt, mag Azure Security Center een momentopname van Hallo VM schijf is van invloed op een genereren en machine artefacten gerelateerde toohello waarschuwing extraheren uit Hallo VM schijf, zoals een registerbestand voor forensische doeleinden.


## <a name="data-protection"></a>Gegevensbeveiliging
**Gegevensscheiding**: gegevens worden voor elk onderdeel in de gehele Hallo service logisch gescheiden gehouden. Alle gegevens worden gemarkeerd per organisatie. Deze labels zich blijft voordoen gedurende de levenscyclus van Hallo gegevens en het wordt afgedwongen op elke laag van Hallo-service.

**Toegang tot gegevens**: In volgorde tooprovide aanbevelingen voor beveiliging en het onderzoeken van mogelijke bedreigingen, medewerkers van Microsoft kunnen toegang krijgen tot gegevens die worden verzameld of geanalyseerd door Azure-services, waaronder crashdumpbestanden, het maken van gebeurtenissen, VM verwerken schijf momentopnamen en artefacten, waaronder mogelijk per ongeluk gegevens van de klant of persoonlijke gegevens van uw virtuele machines. We ons houden toohello [privacyverklaring voor Microsoft Online Services-voorwaarden en](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), die dat Microsoft wordt niet klantgegevens gebruiken of gegevens worden opgehaald van het voor commerciële doeleinden reclame of vergelijkbare status. We gebruiken klantgegevens alleen als de benodigde tooprovide u met Azure-services, met inbegrip van de toepassing compatibel is met deze services bieden. U behoudt alle rechten tooCustomer gegevens.

**Gebruik**: Microsoft patronen gebruikt en dreigingen gezien over meerdere tenants tooenhance onze mogelijkheden voor preventie en detectie; zo doen dat in overeenstemming met Hallo privacy verbintenissen beschreven in onze [Privacy Instructie](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

## <a name="data-location"></a>Gegevenslocatie

**Uw Workspace(s)**: een werkruimte is opgegeven voor Hallo geografische gebieden te volgen en gegevens van uw virtuele machines van Azure, met inbegrip van crashdumps en bepaalde typen waarschuwingen gegevens verzameld in Hallo dichtstbijzijnde werkruimte worden opgeslagen. 

| Geografisch gebied van virtuele machine                        | Geografisch gebied van werkruimte |
|-------------------------------|---------------|
| Verenigde Staten, Brazilië, Canada | Verenigde Staten |
| Europa, Verenigd Koninkrijk        | Europa        |
| Azië en Stille Oceaan, Japan, India    | Azië en Stille Oceaan  |
| Australië                     | Australië     |

 
VM schijf momentopnamen worden opgeslagen in Hallo hetzelfde opslagaccount als Hallo VM schijf.
 
Voor virtuele machines en servers in andere omgevingen met bijvoorbeeld on-premises kunt u Hallo werkruimte en de regio waar verzamelde gegevens worden opgeslagen. 

**Azure Security Center opslag**: informatie over beveiligingswaarschuwingen, met inbegrip van waarschuwingen van de partner, regionaal wordt opgeslagen op basis van locatie toohello Hallo gerelateerde Azure-resource dat informatie over de status van de beveiliging en aanbeveling wordt centraal worden opgeslagen in Hallo Verenigde Staten of volgens de locatie van de toocustomer-Europa.
Azure Security Center verzamelt tijdelijke kopieën van uw crashdumpbestanden en analyseert deze op bewijs van pogingen tot misbruik en geslaagde aanvallen. Azure Security Center voert deze analyse binnen dezelfde Geo Hallo zoals Hallo werkruimte en verwijderingen Hallo kortstondige kopieën wanneer de analyse is voltooid.

Machine artefacten worden opgeslagen in een centraal in dezelfde regio Hallo zoals Hallo VM. 


## <a name="managing-data-collection-from-virtual-machines"></a>Gegevensverzameling van virtuele machines beheren

Wanneer u Security Center inschakelt in Azure, wordt gegevensverzameling ingeschakeld voor elk van uw Azure-abonnementen. U kunt ook gegevensverzameling inschakelen voor uw abonnementen in Hallo beveiligingsbeleid sectie van Azure Security Center. Wanneer gegevensverzameling is ingeschakeld, wordt Azure Security Center bepalingen Hallo Microsoft Monitoring Agent op alle bestaande ondersteunde virtuele machines in Azure en nieuwe bestanden die zijn gemaakt. Hallo Microsoft Monitoring agent scant op verschillende beveiliging gerelateerde configuraties en gebeurtenissen in [Event Tracing for Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) traceringen (ETW). Hallo-besturingssysteem verhoogt bovendien logboekgebeurtenissen tijdens Hallo Hallo machine uitgevoerd. Voorbeelden van dergelijke gegevens zijn: besturingssysteemtype en -versie, besturingssysteemlogboeken (Windows-gebeurtenislogboeken), actieve processen, computernaam, IP-adressen, aangemelde gebruiker en tenant-ID. Hallo Microsoft Monitoring Agent logboekvermeldingen leest en ETW traceert en kopieert ze tooyour workspace(s) voor analyse. Hallo Microsoft Monitoring Agent ook crashdump bestanden tooyour workspace(s) gekopieerd.

Als u van Azure Security Center gratis gebruikmaakt, kunt u ook het verzamelen van virtuele machines in Hallo beveiligingsbeleid uitschakelen. Verzamelen van gegevens is vereist voor abonnementen op Hallo Standard-laag. De verzameling van momentopnamen en artefacten voor de VM-schijf is nog steeds ingeschakeld, zelfs als het verzamelen van gegevens is uitgeschakeld.


## <a name="see-also"></a>Zie ook
In dit document hebt u geleerd hoe gegevens worden beheerd en beveiligd in Azure Security Center. toolearn meer informatie over Azure Security Center, Zie:

* [Azure Security Center Planning- en Bedieningsgids](security-center-planning-and-operations-guide.md) : meer informatie hoe tooplan en Hallo ontwerpoverwegingen tooadopt Azure Security Center begrijpen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) : meer informatie over hoe toomonitor Hallo status van uw Azure-resources
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) : meer informatie hoe toomanage en gereageerd had toosecurity waarschuwingen
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) : meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure
