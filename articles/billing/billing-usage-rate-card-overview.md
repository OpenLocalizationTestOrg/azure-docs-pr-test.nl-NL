---
title: aaaAzure facturering API's | Microsoft Docs
description: Meer informatie over het gebruik van Azure-facturering en RateCard APIs's die gebruikt tooprovide inzichten in Azure brongebruik en trends zijn.
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/18/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: b3214996cc3279f76fdc7f0dbd2059c3ae7bb15c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-billing-apis-tooprogrammatically-get-insight-into-your-azure-usage"></a>Gebruik Azure Billing-API's tooprogrammatically inzicht verkrijgen in uw Azure-gebruik
Toopull gebruiks- en -gegevens in Azure Billing-API's gebruiken in uw voorkeur hulpprogramma's voor gegevensanalyse. Hello Azure brongebruik en RateCard APIs kunt u nauwkeurige voorspellen en beheren van uw kosten. Hallo API's worden geïmplementeerd als een Resource Provider en een deel van het Hallo-serie API's die worden weergegeven door hello Azure Resource Manager.  

## <a name="azure-invoice-download-api-preview"></a>Azure-factuur downloaden API (Preview)
Eenmaal Hallo [opt-in is voltooid](billing-manage-access.md#opt-in), download facturen met Hallo preview-versie van [factuur API](/rest/api/billing). Hallo-functies:

* **Azure op rollen gebaseerd toegangsbeheer** -toegang configureren beleidsregels op Hallo [Azure-portal](https://portal.azure.com) of via [Azure PowerShell-cmdlets](/powershell/azure/overview) toospecify welke gebruikers of toepassingen toegang kan krijgen gebruiksgegevens van toohello abonnement. Aanroepfuncties moeten standaard tokens van Azure Active Directory voor verificatie gebruiken. Hallo aanroeper tooeither Hallo facturering lezer, de lezer, de eigenaar of bijdrager rol tooget toegang toohello gebruiksgegevens voor een specifieke Azure-abonnement toevoegen.
* **Datum filteren** -gebruik Hallo `$filter` parameter tooget alle Hallo facturen in omgekeerde volgorde door Hallo factuur einddatum. 

> [!NOTE]
> Deze functie is in de eerste versie van de preview en onderwerp toobackward-incompatibele wijzigingen mogelijk zijn. Op dit moment is is het niet beschikbaar voor bepaalde abonnement aanbiedingen (EA, CSP, AIO niet ondersteund) en Duitse Azure.

## <a name="azure-resource-usage-api-preview"></a>Azure-Resource gebruiks-API (Preview)
Gebruik hello Azure [Resource gebruik API](https://msdn.microsoft.com/library/azure/mt219003) tooget uw geschatte Azure verbruiksgegevens. Hallo API bevat:

* **Azure op rollen gebaseerd toegangsbeheer** -toegang configureren beleidsregels op Hallo [Azure-portal](https://portal.azure.com) of via [Azure PowerShell-cmdlets](/powershell/azure/overview) toospecify welke gebruikers of toepassingen toegang kan krijgen gebruiksgegevens van toohello abonnement. Aanroepfuncties moeten standaard tokens van Azure Active Directory voor verificatie gebruiken. Hallo aanroeper tooeither Hallo facturering lezer, de lezer, de eigenaar of bijdrager rol tooget toegang toohello gebruiksgegevens voor een specifieke Azure-abonnement toevoegen.
* **Elk uur of dagelijkse samenvoegingen** - aanroepfuncties kunnen opgeven of ze hun Azure gebruiksgegevens wilt elk uur tijdsintervallen of dagelijks tijdsintervallen. Hallo standaardwaarde is dagelijks.
* **Metagegevens van het exemplaar (inclusief resourcetags)** – ophalen op exemplaarniveau details zoals Hallo volledig gekwalificeerde resource-uri (/subscriptions/ {abonnement-id} /..), groep resourcegegevens en resourcetags Hallo. Deze metagegevens kunt u deterministische en gebruik programmatisch toewijzen door Hallo-tags voor gebruiksvoorbeelden zoals cross in rekening gebracht.
* **Bron-metagegevens** -Resourcedetails zoals de naam van de meter hello, meter categorie meter subcategorie, eenheid en regio geven Hallo aanroeper een beter inzicht in wat is verbruikt. We proberen tooalign resource metagegevens terminologie ook via hello Azure-portal, Azure verbruik CSV, EA CSV, facturering en andere openbare ervaringen, toolet correleren van gegevens over ervaringen.
* **Gebruik voor alle typen bieden** – gebruiksgegevens beschikbaar is voor alle typen zoals betalen naar gebruik, MSDN, bedrag, financieel tegoed en EA bieden.

## <a name="azure-resource-ratecard-api-preview"></a>Azure-Resource RateCard API (Preview)
Gebruik Hallo [API van Azure Resource RateCard](https://msdn.microsoft.com/library/azure/mt219005) tooget Hallo lijst met beschikbare Azure-resources en informatie over de geschatte prijzen voor elk. Hallo API bevat:

* **Azure op rollen gebaseerd toegangsbeheer** -uw beleidsregels configureren op Hallo [Azure-portal](https://portal.azure.com) of via [Azure PowerShell-cmdlets](/powershell/azure/overview) toospecify welke gebruikers of toepassingen toegang kan krijgen toohello RateCard gegevens. Aanroepfuncties moeten standaard tokens van Azure Active Directory voor verificatie gebruiken. Hallo aanroeper tooeither Hallo lezer, de eigenaar of bijdrager rol tooget toegang toohello gebruiksgegevens voor een bepaald Azure-abonnement toevoegen.
* **Ondersteuning voor betalen per gebruik, MSDN, bedrag en financieel tegoed (EA niet ondersteund) biedt** -voor deze API biedt Azure-aanbieding niveau snelheid informatie.  Hallo aanroeper van deze API moet doorgeven in Hallo aanbieding tooget resource Gegevensdetails en tarieven. We kunnen momenteel niet tooprovide EA tarieven omdat EA aanbiedingen tarieven per inschrijving hebt aangepast. 

## <a name="scenarios"></a>Scenario's
Hier volgen enkele Hallo-scenario's die zijn aangebracht met Hallo combinatie van Hallo gebruik en Hallo RateCard APIs mogelijk:

* **Azure besteden tijdens Hallo maand** -gebruik Hallo combinatie van Hallo gebruik en RateCard APIs tooget beter inzicht in uw cloud te besteden aan de tijdens Hallo maand. U kunt elk uur Hallo analyseren en maakt een schatting van dagelijkse buckets van gebruiks- en kosten.
* **Stel waarschuwingen** : Hallo gebruik gebruiken en hello RateCard APIs tooget geschatte cloud verbruik en de kosten en resource of monetaire gebaseerde waarschuwingen instellen.
* **Factuur voorspellen** – Get uw geschatte gebruiks- en cloud besteden en machine learning-algoritmen toopredict welke factuur Hallo achter Hallo Hallo facturering cyclus zou zijn van toepassing.
* **Vooraf verbruik kosten analysis-** – hello RateCard API toopredict hoeveel uw factuur voor het gebruik van uw verwachte niet wanneer u uw werkbelastingen tooAzure verplaatst gebruiken. Als u bestaande workloads in andere clouds of privéclouds hebt, kunt u ook gebruik van uw met hello Azure tarieven tooget een betere schatting van Azure te besteden aan toewijzen. Deze schatting geeft u de mogelijkheid toopivot op aanbieding, en vergelijken en contrast tussen verschillende aanbiedingstypen Hallo dan betalen naar gebruik, Hallo zoals bedrag en financieel tegoed. Hallo API biedt u eveneens Hallo mogelijkheid toosee kosten verschillen per regio en kunt u toodo een wat-als kosten analysis toohelp u implementatie beslissingen nemen.
* **Wat-als-analyse** -
  
  * U kunt bepalen of het meer rendabele toorun werkbelastingen in een andere regio of op een andere configuratie van hello Azure-resource. Azure-resource kosten kunnen verschillen op basis van Hallo u Azure-regio.
  * U kunt ook bepalen als een ander Azure-aanbiedingtype resulteert in een betere rentabiliteit op een Azure-resource.
  
## <a name="partner-solutions"></a>Partneroplossingen
[Microsoft Azure gebruiks- en RateCard API's inschakelen Cloudyn tooProvide ITFM voor klanten](billing-usage-rate-card-partner-solution-cloudyn.md) Hallo integratie ervaring die worden aangeboden door de partner van de Azure-facturering API beschrijft [Cloudyn](https://www.cloudyn.com/microsoft-azure/). In dit artikel wordt gesproken over hun ervaringen en bevat een video ziet u hoe u Cloudyn gebruiken en hello Azure Billing-API's tooget inzicht in gegevens van de Azure-verbruik.

[Cloud Cruiser en Microsoft Azure Billing API-integratie](billing-usage-rate-card-partner-solution-cloudcruiser.md) wordt beschreven hoe [Cloud Cruiser van Express voor Azure Pack](http://www.cloudcruiser.com/partners/microsoft/) rechtstreeks vanuit Windows Azure Pack (WAP)-portal Hallo werkt. U kunt beide Hallo operationele en financiële aspecten van Hallo Microsoft persoonlijke of gehoste openbare Azure-cloud naadloos beheren van één gebruikersinterface.   

## <a name="next-steps"></a>Volgende stappen
* Bekijk Hallo codevoorbeelden op GitHub:
  * [Voorbeeld van de factuur API-code](https://go.microsoft.com/fwlink/?linkid=845124)

  * [Voorbeeld van gebruiks-API-code](https://github.com/Azure-Samples/billing-dotnet-usage-api)

  * [Voorbeeld van RateCard API-code](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)

* Zie toolearn meer informatie over hello Azure Resource Manager [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). 

* Zie voor meer informatie over Hallo-suite met hulpprogramma's die nodig zijn toohelp krijgt u inzicht hebben in de cloud te besteden aan Hallo Gartner artikel [markt-handleiding voor IT financiële Management (ITFM)-hulpprogramma's voor](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

