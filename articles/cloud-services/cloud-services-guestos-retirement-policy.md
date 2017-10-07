---
title: aaaSupportability en buiten gebruik stellen beleid-handleiding voor Azure Gast OS | Microsoft Docs
description: Bevat informatie over wat wordt ondersteuning van Microsoft met betrekking tot toohello Azure Gast OS door de Cloud-Services gebruikt.
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 919dd781-4dc6-4e50-bda8-9632966c5458
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/26/2017
ms.author: raiye
ms.openlocfilehash: 6a86c42ac95d12bbf116d900b7afb26fc3fe34e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-supportability-and-retirement-policy"></a>Azure Gast OS ondersteuningsmogelijkheden en buiten gebruik stellen beleid
Hallo-informatie op deze pagina is gekoppeld toohello Azure gastbesturingssysteem ([Gastbesturingssysteem](cloud-services-guestos-update-matrix.md)) voor Cloud Services worker en webservice-functies (PaaS). TooVirtual Machines (IaaS) is niet van toepassing.

Microsoft heeft een gepubliceerde [ondersteuningsbeleid voor het Gastbesturingssysteem Hallo](http://support.microsoft.com/gp/azure-cloud-lifecycle-faq). Hallo pagina die u leest nu wordt beschreven hoe Hallo beleid is geïmplementeerd.

Hallo-beleid is

1. Microsoft ondersteunt **Hallo ten minste twee families van de meest recente Hallo Gastbesturingssysteem**. Wanneer een serie buiten gebruik is gesteld, hebben klanten 12 maanden na Hallo officiële buiten gebruik stellen datum tooupdate tooa nieuwere ondersteunde Gast OS-familie.
2. Microsoft ondersteunt **Hallo ten minste twee versies van de meest recente van Hallo ondersteund Gastbesturingssysteem families**.
3. Microsoft ondersteunt **Hallo ten minste twee versies van de meest recente van hello Azure SDK**. Wanneer er een versie van Hallo die SDK is buiten gebruik gesteld, moeten klanten 12 maanden van Hallo officiële buiten gebruik stellen datum tooupdate tooa nieuwere versie.

Tijd tot tijd mogelijk meer dan twee families of releases worden ondersteund. Informatie over het officiële ondersteuning Gastbesturingssysteem wordt weergegeven op Hallo [Azure Gast OS Releases en SDK compatibiliteit Matrix](cloud-services-guestos-update-matrix.md).

## <a name="when-a-guest-os-family-or-version-is-retired"></a>Wanneer een gast OS-familie of de versie is buiten gebruik gesteld
Een nieuwe Gastbesturingssysteem **familie** ergens na Hallo-release van een nieuwe officiële versie van Windows Server-besturingssysteem hello wordt geïntroduceerd. Wanneer een nieuwe Gast OS-familie wordt geïntroduceerd, wordt de oudste Gast OS-familie Hallo intrekken van Microsoft.

Nieuwe Gastbesturingssysteem **versies** over elke maand tooincorporate Hallo nieuwste MSRC updates zijn geïntroduceerd. Vanwege Hallo reguliere maandelijkse updates is een versie van het Gastbesturingssysteem normaal uitgeschakeld 60 dagen na de release. Deze activiteit houdt ten minste twee Gast OS-versies voor iedere familie beschikbaar voor gebruik.

### <a name="process-during-a-guest-os-family-retirement"></a>Verwerken tijdens een buiten gebruik stellen familie Gastbesturingssysteem
Nadat de Hallo buiten gebruik stellen wordt aangekondigd, hebt klanten een overgangsperiode van 12 maanden '' voordat Hallo oudere familie officieel gebruik gesteld buiten. Overgangsduur van deze kan worden uitgebreid goeddunken Hallo van Microsoft. Updates worden opgeslagen op Hallo [Azure Gast OS Releases en SDK compatibiliteit Matrix](cloud-services-guestos-update-matrix.md).

Een geleidelijke buitengebruikstellingsproces begint zes (6) maanden in Hallo overgangsperiode. Gedurende deze tijd:

1. Microsoft stelt klanten van Hallo buiten gebruik stellen.
2. Hallo nieuwere versie van Azure SDK Hallo Hallo buiten gebruik gesteld Gast OS-familie niet wordt ondersteund.
3. Nieuwe implementaties en nieuwe distributies van Cloud Services niet toegestaan op Hallo buiten gebruik gesteld familie

Microsoft blijft toointroduce nieuwe Gastbesturingssysteem versie Hallo nieuwste MSRC updates tot Hallo laatste dag van Hallo overgangsperiode, ook wel 'vervaldatum' hello opnemen. Op de vervaldatum hello, Cloud Services nog steeds uitgevoerd wordt worden niet-ondersteunde onder hello Azure SLA. Microsoft heeft Hallo goeddunken tooforce upgraden, verwijderen of stoppen van deze services na die datum.

### <a name="process-during-a-guest-os-version-retirement"></a>Verwerken tijdens een versie van het besturingssysteem Gast buiten gebruik stellen
Als klanten hun Gastbesturingssysteem tooautomatically update is ingesteld, hebben ze nooit tooworry over het afhandelen van Gast OS-versies. Ze gebruikt wordt altijd in de meest recente Gastbesturingssysteem versie Hallo.

Gast OS-versies worden er elke maand uitgebracht. Elke versie heeft vanwege Hallo frequentie van reguliere releases, een vaste levensduur.

Na 60 dagen in Hallo levensduur is een versie '*uitgeschakeld*'. "Uitgeschakeld" betekent dat Hallo-versie wordt verwijderd uit het Hallo-portal. Hallo-versie kan niet meer worden ingesteld van Hallo CSCFG-configuratiebestand. Bestaande implementaties worden ook actief blijven. Maar nieuwe implementaties en code en configuratie-updates tooexisting implementaties wordt niet toegestaan.

Enige tijd na steeds "uitgeschakeld", versie van het besturingssysteem van de Gast Hallo '*verloopt*' en worden nog steeds uitgevoerd die versie installaties force bijgewerkt en in te stellen tooautomatically update Hallo Gastbesturingssysteem Hallo toekomstige zijn. Verlopen wordt uitgevoerd in batches, zodat Hallo tijdsperiode van deactivering tooexpiration kan variëren.

Deze punten kunnen worden verricht langer op van Microsoft ter discretie tooease klant overgangen. Eventuele wijzigingen worden gecommuniceerd op Hallo [Azure Gast OS Releases en SDK compatibiliteit Matrix](cloud-services-guestos-update-matrix.md).

### <a name="notifications-during-retirement"></a>Meldingen tijdens buiten gebruik stellen
* **Familie buiten gebruik stellen** <br>Microsoft gebruikt blogberichten en de portalmelding. Klanten die nog steeds een buiten gebruik gestelde Gast OS-familie met ontvangt een melding via rechtstreekse communicatie (e-mailbericht, portal berichten, telefonische oproep) tooassigned servicebeheerders. Alle wijzigingen worden toothis pagina en Hallo RSS-feed die Hallo boven aan deze pagina worden geplaatst.
* **Versie buiten gebruik stellen** <br>Alle wijzigingen en Hallo datums die ze optreden, geboekt toothis pagina en Hallo RSS-feed die Hallo boven aan deze pagina, met inbegrip van de release, uitgeschakeld of verlopen. Beheerders van de services ontvangt e-mailberichten als ze implementaties die worden uitgevoerd op een uitgeschakelde Gastbesturingssysteem versie of een groep hebben. Hallo timing van deze e-mailberichten kan variëren. Ze zijn doorgaans ten minste een maand voor deactivering, hoewel deze timing niet een officiële SLA is.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen
**Hoe kan ik het risico van Hallo gevolgen van migratie?**

U wordt aangeraden nieuwste Gast OS-familie voor het ontwerpen van uw Cloud-Services.

1. Start uw migratie tooa nieuwere gezin vroeg plannen.
2. Tijdelijke test implementaties tootest instellen met uw Cloud Service wordt uitgevoerd op de nieuwe Hallo-familie.
3. Stel uw versie van het Gastbesturingssysteem te**automatische** (osVersion = * in Hallo [.cscfg](cloud-services-model-and-package.md#cscfg) bestand) zodat Hallo migratie toonew Gast OS-versies worden automatisch uitgevoerd.

**Wat gebeurt er als mijn webtoepassing diepgaande integratie met Hallo OS vereist?**

Als uw web-toepassingsarchitectuur, is afhankelijk van onderliggende functies van het besturingssysteem hello, gebruikt u ondersteund platformmogelijkheden, zoals [starten van de taken](cloud-services-startup-tasks.md) of andere mechanismen voor uitbreidbaarheid. U kunt ook ook gebruiken [Azure Virtual Machines](https://azure.microsoft.com/documentation/scenarios/virtual-machines/) (IaaS-infrastructuur als een Service), waarbij u bent zelf verantwoordelijk voor het onderliggende besturingssysteem Hallo onderhouden.

## <a name="next-steps"></a>Volgende stappen
Laatste controle Hallo [Gast OS releases](cloud-services-guestos-update-matrix.md).
