---
title: aaaUnderstand uw Azure gedetailleerde informatie over het gebruik | Microsoft Docs
description: Meer informatie over hoe tooread en begrijpen Hallo secties van gedetailleerde gebruik van uw CSV voor uw Azure-abonnement
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: tonguyen
ms.openlocfilehash: c9284bf94bfa9f36cdd5d39e653a35def7c1aa34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-terms-on-your-microsoft-azure-detailed-usage-charges"></a>Termen in uw Microsoft Azure gedetailleerde gebruikskosten begrijpen 
gedetailleerde informatie over het gebruik kosten CSV-bestand dagelijks bevat Hallo en meter niveau gebruikskosten voor Hallo huidige periode facturering. 

tooget uw bestand gedetailleerde informatie over het gebruik, Zie [hoe tooget uw Azure-facturering factuur- en gebruiksgegevens dagelijks](billing-download-azure-invoice-daily-usage-date.md).
Het is beschikbaar in een indeling met door komma's gescheiden waarden (.csv) dat u in een werkbladtoepassing openen kunt. Als er twee versies beschikbaar zijn, wordt versie 2 downloaden. Dat is de meest recente bestandsindeling Hallo.

Gebruikskosten zijn Hallo totale **maandelijkse** kosten voor een abonnement. De gebruikskosten rekening geen gehouden met eventuele tegoed of kortingen.

## <a name="detailed-terms-and-descriptions-of-your-detailed-usage-file"></a>Gedetailleerde voorwaarden en beschrijvingen van het bestand met gedetailleerde informatie over het gebruik
Hallo beschrijven volgende secties Hallo belangrijke termen die worden weergegeven in versie 2 van Hallo-bestand voor gedetailleerde informatie over het gebruik.

### <a name="statement"></a>Instructie
Hallo bovenste gedeelte van Hallo gedetailleerde informatie over het gebruik CSV toont Hallo Bestandsservices die u hebt gebruikt tijdens het Hallo van deze maand factureringsperiode. Hallo bevat volgende tabel Hallo voorwaarden en beschrijvingen in deze sectie wordt weergegeven.

| Termijn | Beschrijving |
| --- | --- |
|Factureringsperiode |Hallo factureringsperiode wanneer Hallo meters zijn gebruikt |
|De categorie van de meter |Op het hoogste niveau service voor het gebruik van Hallo Hallo identificeert |
|De subcategorie van de meter |Definieert Hallo type Azure-service die kan invloed hebben op Hallo snelheid |
|De naam van de meter |Identificeert Hallo maateenheid voor Hallo meter wordt gebruikt |
|De regio van de meter |Geeft de locatie Hallo van Hallo-datacenter voor bepaalde services die worden berekend op basis van locatie datacenter |
|SKU |Hallo unieke systeem-id voor elk Azure meter identificeert |
|Eenheid |Hallo-eenheid die Hallo-service wordt in rekening gebracht in identificeert. Bijvoorbeeld GB, uur, 10.000 s. |
|Verbruikt aantal |Hallo hoeveelheid Hallo meter gebruikt tijdens het Hallo-factureringsperiode |
|Inbegrepen hoeveelheid |Hallo hoeveelheid Hallo meter die is opgenomen gratis in de huidige factureringsperiode |
|Overschreden hoeveelheid |Toont Hallo verschil tussen Hallo hoeveelheid verbruikt en Hallo hoeveelheid opgenomen. U wordt gefactureerd voor dit bedrag. Voor betalen per gebruik aanbiedingen waarbij geen aantal opgenomen met Hallo aanbieding Hallo dit totaal hetzelfde als de hoeveelheid verbruikte Hallo. |
|Binnen toezegging |Toont Hallo meter kosten die worden afgetrokken van uw toezeggingsbedrag die zijn gekoppeld aan uw aanbieding 6 of 12 maanden. Kosten van de meter worden in chronologische volgorde afgetrokken. |
|Valuta |Hallo valuta gebruikt in uw huidige factureringsperiode |
|Overschrijding |Toont Hallo meter kosten die groter is dan uw toezeggingsbedrag die zijn gekoppeld aan uw aanbieding 6 of 12 maanden |
|Toezeggingstarief |Geeft Hallo streven tarief op basis van de totale toezeggingsbedrag Hallo die zijn gekoppeld aan uw aanbieding 6 of 12 maanden |
|Tarief |u in rekening per eenheid factureerbare gebracht bent Hallo-snelheid |
|Waarde |Hallo-resultaten van de vermenigvuldiging Hallo overschrijding aantal kolom voor Hallo snelheid kolom weergegeven. Er zijn geen kosten in deze kolom als Hallo die verbruikt hoeveelheid niet groter zijn dan hello hoeveelheid opgenomen. |

### <a name="daily-usage"></a>Dagelijkse gebruik

Hallo dagelijkse sectie voor gebruik van CSV-bestand Hallo geeft gebruiksdetails die invloed hebben op Hallo facturering tarieven. Hallo bevat volgende tabel Hallo voorwaarden en beschrijvingen in deze sectie wordt weergegeven.

| Termijn | Beschrijving |
| --- | --- |
|Gebruiksdatum |Hallo datum waarop de meter Hallo is gebruikt |
|De categorie van de meter |Geeft het hoogste niveau Hallo-service waarvoor dit gebruik behoort |
|Id van de meter |Hallo gefactureerd meter-ID die is gebruikt tooprice facturering gebruik |
|De subcategorie van de meter |Definieert hello Azure servicetype dat kan invloed hebben op Hallo snelheid |
|De naam van de meter |Identificeert Hallo maateenheid voor Hallo meter wordt gebruikt |
|De regio van de meter |Geeft de locatie Hallo van Hallo-datacenter voor bepaalde services die worden berekend op basis van locatie datacenter |
|Eenheid |Identificeert Hallo-eenheid die Hallo meter wordt in rekening gebracht. Bijvoorbeeld GB, uur, 10.000 s. |
|Verbruikt aantal |Hallo hoeveelheid Hallo meter die voor die dag is verbruikt |
|Resourcelocatie |Identificeert Hallo datacenter waarop Hallo meter wordt uitgevoerd |
|Verbruikte service |Hello Azure-platform-service die u gebruikt |
|Resourcegroep |Hallo-resourcegroep in welke Hallo geïmplementeerde meter wordt uitgevoerd in. <br/><br/>Zie voor meer informatie [Overzicht van Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
|Exemplaar-id | Hallo-id voor Hallo meter. <br/><br/> Hallo-id bevat Hallo-naam die u voor de meter Hallo opgeeft wanneer deze is gemaakt. Deze naam Hallo van Hallo resource of Hallo volledig gekwalificeerde Resource-ID. Zie voor meer informatie [Azure Resource Manager-API](https://docs.microsoft.com/rest/api/resources/resources). |
|Tags | Label u toohello meter toewijzen. Labels toogroup facturering records gebruiken.<br/><br/>Bijvoorbeeld, kunt u codes toodistribute kosten per afdeling Hallo die gebruikmaakt van de meter Hallo. Services die ondersteuning bieden voor het importeerbereik tags zijn virtuele machines, opslag- en netwerkservices ingericht met behulp van Hallo [Azure Resource Manager-API](https://docs.microsoft.com/rest/api/resources/resources). Zie voor meer informatie [ordenen van uw Azure-resources met labels](http://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/). |
|Aanvullende informatie |Service-specifieke metagegevens. Bijvoorbeeld, een type installatiekopie voor een virtuele machine. |
|Service-informatie 1 |naam van het Hallo-project dat Hallo service deel uitmaakt van tooon uw abonnement |
|Service-informatie 2 |Verouderde veld waarmee optionele servicespecifieke metagegevens wordt vastgelegd |

## <a name="how-do-i-make-sure-that-hello-charges-in-my-detailed-usage-file-are-correct"></a>Hoe maak ik ervoor dat de kosten Hallo in mijn bestand gedetailleerde informatie over het gebruik correct zijn?
Als er een kosten op uw bestand voor gedetailleerde informatie over het gebruik die u graag meer details op, Zie [inzicht in uw factuur voor Microsoft Azure.](./billing-understand-your-bill.md)

## <a name="external"></a>Hoe zit het met externe servicekosten?
Externe services (ook wel bekend als Marketplace orders) worden geleverd door onafhankelijke serviceleveranciers en worden afzonderlijk gefactureerd. Hallo kosten weergegeven op Hallo Azure factuur niet. toolearn meer, Zie [inzicht in uw Azure externe servicekosten](billing-understand-your-azure-marketplace-charges.md).

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?) ophalen van uw probleem snel worden opgelost.
