---
title: aaaOperations Management Suite beveiligings- en gegevensbeveiliging Audit-oplossing | Microsoft Docs
description: In dit document wordt uitgelegd hoe gegevens worden beheerd en bewaakt in de oplossing Beveiliging en controle in Operations Management Suite.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a>Gegevensbeveiliging in de oplossing Beveiliging en controle in Operations Management Suite
toohelp klanten detecteren, voorkomen van en reageren toothreats, [Operations Management Suite (OMS) beveiligings- en Audit oplossing](operations-management-suite-overview.md) verzamelt en verwerkt gegevens over uw resources, waaronder:

* Beveiligingslogboek
* ETW-gebeurtenissen (Event Tracing for Windows)
* Controlegebeurtenissen AppLocker
* Windows Firewall-logboek
* Advanced Threat Analytics-gebeurtenissen
* Resultaten van de evaluatie van de basislijn
* Resultaten van de antimalware-evaluatie
* Resultaten van de evaluatie van updates/patching
* Syslogs stromen die expliciet zijn ingeschakeld op het Hallo-agent

Wij maken sterk verbintenissen tooprotect Hallo privacy en beveiliging van deze gegevens. Microsoft toostrict naleving en beveiliging richtlijnen voldoet, van een service toooperating coderen.
In dit artikel wordt uitgelegd hoe gegevens worden beheerd en beveiligd in Beveiliging en controle in OMS.

## <a name="data-sources"></a>Gegevensbronnen
OMS beveiligings- en Audit oplossing analyseren van gegevens op uw virtuele Machines en fysieke computers waarop Hallo OMS-Agent is geïnstalleerd. Met de oplossing Beveiliging en controle in OMS worden configuratiegegevens over beveiligingsgebeurtenissen verzameld, zoals Windows-gebeurtenissen, controlelogboeken, IIS-logboeken en syslog-berichten. Voorbeelden van dergelijke gegevens zijn: besturingssysteemtype en -versie, actieve processen, computernaam, IP-adressen, aangemelde gebruiker en tenant-id.  

## <a name="data-protection"></a>Gegevensbeveiliging
**Gegevensscheiding**: gegevens worden voor elk onderdeel in de gehele Hallo service logisch gescheiden gehouden. Alle gegevens worden gemarkeerd per organisatie. Deze labels zich blijft voordoen gedurende de levenscyclus van Hallo gegevens en het wordt afgedwongen op elke laag van Hallo-service. 

**Toegang tot gegevens**: tooprovide beveiligingsaanbevelingen en onderzoeken van mogelijke bedreigingen, medewerkers van Microsoft mogelijk toegang tot gegevens verzameld of geanalyseerd door services. We ons houden toohello [Microsoft Online servicevoorwaarden](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) en [privacyverklaring](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), die dat Microsoft wordt niet klantgegevens gebruiken of gegevens worden opgehaald van het voor adverteren of vergelijkbare status commerciële doeleinden. beveiligingsaanbevelingen voor de tooprovide en onderzoeken van mogelijke bedreigingen, medewerkers van Microsoft mogelijk toegang tot gegevens verzameld of geanalyseerd door services. We gebruiken klantgegevens alleen als de benodigde tooprovide u met Azure-services, met inbegrip van de toepassing compatibel is met deze services bieden. U behoudt alle rechten tooyour eigen gegevens.

**Gebruik**: Microsoft patronen gebruikt en dreigingen gezien over meerdere tenants tooenhance onze mogelijkheden voor preventie en detectie; zo doen dat in overeenstemming met Hallo privacy verbintenissen beschreven in onze [Privacy Instructie](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

> [!NOTE]
> Locatie van gegevens is geconfigureerd op het niveau Hallo OMS werkruimte, tijdens het Hallo werkruimte maken, die deel uitmaakt van Hallo initiële OMS beveiligings- en Audit configuratieproces.
> 
> 

## <a name="see-also"></a>Zie ook
In dit document hebt u geleerd hoe gegevens worden beheerd en bewaakt in OMS. toolearn meer informatie over OMS beveiligings- en Audit-oplossing, Zie:

* [Overzicht van Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Bewaking en reageren tooSecurity waarschuwingen in de beveiliging van Operations Management Suite en Audit-oplossing](oms-security-responding-alerts.md)
* [Resources bewaken in de oplossing Beveiliging en controle van Operations Management Suite ](oms-security-monitoring-resources.md)

