---
title: aaaMonitor replicatiestatus van de Active Directory met Azure Log Analytics | Microsoft Docs
description: Hallo Active Directory-replicatiestatus oplossingspakket regelmatig controleert uw Active Directory-omgeving voor eventuele storingen en Hallo resultaten op uw dashboard OMS-rapporten.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 1b988972-8e01-4f83-a7f4-87f62778f91d
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 235e4f7a066ea50b79f681398182b22c91fb6d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-active-directory-replication-status-with-log-analytics"></a>Replicatiestatus van Active Directory met Log Analytics

![AD-replicatie statussymbool](./media/log-analytics-ad-replication-status/ad-replication-status-symbol.png)

Active Directory is een belangrijk onderdeel van een onderneming IT-omgeving. tooensure hoge beschikbaarheid en hoge prestaties, heeft elke domeincontroller in een eigen kopie van Hallo Active Directory-database. Domeincontrollers repliceren met elkaar in volgorde toopropagate wijzigingen over Hallo enterprise. Fouten in dit replicatieproces kunnen tal van problemen veroorzaken in Hallo onderneming.

Hallo AD replicatiestatus oplossingspakket regelmatig controleert uw Active Directory-omgeving voor eventuele storingen en Hallo resultaten op uw dashboard OMS-rapporten.

## <a name="installing-and-configuring-hello-solution"></a>Installeren en configureren van Hallo-oplossing
Gebruik Hallo informatie tooinstall te volgen en Hallo oplossing configureren.

* U moet de agents installeren op domeincontrollers die lid van Hallo domein toobe geëvalueerd zijn. Of moet u agents installeren op servers die lid zijn en Hallo agents toosend AD-replicatie gegevens tooOMS configureren. hoe tooconnect tooOMS van Windows-computers, Zie toounderstand [verbinding maken met Windows-computers tooLog Analytics](log-analytics-windows-agents.md). Als uw domeincontroller al deel van een bestaande System Center Operations Manager-omgeving uitmaakt die u wilt dat tooconnect tooOMS, Zie [verbinding maken met Operations Manager tooLog Analytics](log-analytics-om-agents.md).
* Hallo Active Directory-replicatiestatus oplossing tooyour OMS-werkruimte met behulp van Hallo proces dat wordt beschreven in toevoegen [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).  Er is geen verdere configuratie nodig.

## <a name="ad-replication-status-data-collection-details"></a>AD replicatiestatus Gegevensdetails verzameling
Hallo volgende tabel bevat de methoden van de collectie en andere informatie over hoe gegevens worden verzameld voor de Status van de AD-replicatie.

| Platform | Directe Agent | SCOM-agents | Azure Storage | SCOM vereist? | SCOM-agent gegevens die worden verzonden via de beheergroep | Frequentie van de verzameling |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |elke vijf dagen |

## <a name="optionally-enable-a-non-domain-controller-toosend-ad-data-toooms"></a>Schakel eventueel een niet-domeincontroller toosend AD gegevens tooOMS
Als u niet tooconnect van uw domeincontrollers wilt direct tooOMS, kunt u alle andere OMS verbonden computers in uw domein toocollect gegevens voor Hallo AD replicatiestatus oplossing pack en laat het hello gegevens verzenden.

### <a name="tooenable-a-non-domain-controller-toosend-ad-data-toooms"></a>een niet-domeincontroller toosend AD gegevens tooOMS tooenable
1. Controleer of die Hallo-computer lid is van Hallo-domein dat u wenst dat toomonitor met behulp van Hallo AD replicatiestatus oplossing.
2. [Verbinding maken met de Hallo Windows computer tooOMS](log-analytics-windows-agents.md) of [verbinding maken met behulp van uw bestaande Operations Manager-omgeving tooOMS](log-analytics-om-agents.md), als deze niet al is aangesloten.
3. Instellen op die computer Hallo volgende registersleutel:

   * Sleutel: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management groepen\<ManagementGroupName > \Solutions\ADReplication**
   * Waarde: **IsTarget**
   * Waardegegevens: **true**

   > [!NOTE]
   > Deze wijzigingen worden niet doorgevoerd totdat het opnieuw opstarten Hallo Microsoft Monitoring Agent-service (HealthService.exe).
   >
   >

## <a name="understanding-replication-errors"></a>Wat zijn replicatiefouten opgetreden?
Zodra u AD status replicatiegegevens verzonden tooOMS hebt, ziet u een tegel vergelijkbare toohello installatiekopie op Hallo OMS dashboard waarmee wordt aangegeven hoeveel replicatiefouten die u momenteel hebt te volgen.  
![Tegel Status van de AD-replicatie](./media/log-analytics-ad-replication-status/oms-ad-replication-tile.png)

**Kritieke replicatiefouten** fouten die aan of hoger dan 75% Hallo zijn [tombstone-levensduur](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) voor uw Active Directory-forest.

Wanneer u Hallo tegel klikt, kunt u meer informatie over fouten Hallo kunt weergeven.
![AD replicatiestatus dashboard](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)

### <a name="destination-server-status-and-source-server-status"></a>Doel-serverstatus en de Status van de bron-Server
Deze kolommen bevatten Hallo status van de doelserver en bronservers waarop replicatiefouten zich voordoet. Hallo getal na elke naam van de domeincontroller geeft Hallo aantal replicatiefouten op die domeincontroller.

Hallo-fouten voor zowel doelservers en bronservers worden weergegeven omdat sommige problemen eenvoudiger tootroubleshoot vanuit Hallo bron server perspectief en anderen Hallo bestemming server perspectief.

In dit voorbeeld kunt u zien dat veel doelservers ongeveer hetzelfde aantal fouten hello, maar er is een bronserver (ADDC35) met veel meer fouten dan alle Hallo anderen. Is het waarschijnlijk dat er is een probleem op ADDC35 waardoor het toofail toosend gegevens tooits-replicatiepartners. Hallo problemen op ADDC35 zijn hersteld, mogelijk veel Hallo fouten die worden weergegeven in de server doelgebied Hallo oplossen.

### <a name="replication-error-types"></a>Replicatie fouttypen
Dit gedeelte vindt u informatie over Hallo typen fouten gedetecteerd in uw onderneming. Elke fout heeft een unieke numerieke code en een bericht dat kunt u de hoofdoorzaak Hallo Hallo fout te bepalen.

Hallo ring Hallo boven biedt u een idee van die fouten worden weergegeven, meer en minder vaak in uw omgeving.

Hier ziet u wanneer meerdere domeincontrollers Hallo ondervinden dezelfde Replicatiefout. In dit geval wordt u mogelijk kunnen toodiscover worden of identificeren van een oplossing op één domeincontroller en herhaal vervolgens deze op andere domeincontrollers beïnvloed door Hallo dezelfde fout.

### <a name="tombstone-lifetime"></a>Tombstone-levensduur
Hallo tombstone-levensduur bepaalt hoe lang een verwijderd object, een tombstone tooas waarnaar wordt verwezen, wordt bewaard in Hallo Active Directory-database. Wanneer een verwijderd object geeft Hallo tombstone-levensduur een proces van de verzameling afval deze automatisch verwijderd uit Hallo Active Directory-database.

Hallo standaard tombstone-levensduur is 180 dagen voor de meest recente versies van Windows, maar was 60 dagen op oudere versies, en deze expliciet kan worden gewijzigd door een Active Directory-beheerder.

Het is belangrijk tooknow als er replicatiefouten die bijna hebben bereikt of Hallo tombstone-levensduur hebben. Als twee domeincontrollers een replicatiefout dat behouden na Hallo tombstone-levensduur ondervindt blijft, wordt replicatie uitgeschakeld tussen deze twee domeincontrollers, zelfs als onderliggende Replicatiefout Hallo is opgelost.

Hallo Tombstone-levensduur gebied helpt u identificeren plaatsen waar uitgeschakelde replicatie in gevaar gebeurt is. Elke fout in Hallo **meer dan 100% TSL** categorie vertegenwoordigt een partitie die niet is gerepliceerd tussen de bron- en doelserver server voor op minimaal Hallo tombstone-levensduur voor Hallo-forest.

In dit geval gewoon hersteld Hallo Replicatiefout worden niet voldoende. Ten minste, moet u toomanually tooidentify onderzoeken en opschonen achtergebleven objecten voordat u kunt replicatie opnieuw. Mogelijk moet u zelfs toodecommission een domeincontroller.

In aanvulling tooidentifying replicatiefouten die blijven bestaan uit het verleden Hallo tombstone-levensduur, wilt u er ook toopay aandacht tooany fouten Hallo bereik vallen **50 75% TSL** of **75 100% TSL** categorieën.

Dit zijn de fouten die zijn duidelijk achtergebleven, niet tijdelijk is en dus waarschijnlijk uw tooresolve tussenkomst moet. goed nieuws Hallo is dat ze nog niet is bereikt Hallo tombstone-levensduur. Als u deze problemen snel oplossen en *voordat* ze Hallo tombstone-levensduur bereikt, replicatie met minimale handmatige interventie kan opnieuw worden opgestart.

Zoals eerder opgemerkt, Hallo dashboardtegel voor Hallo AD replicatiestatus oplossing toont Hallo aantal *kritieke* fouten in uw omgeving, die is gedefinieerd als fouten die meer dan 75% van de tombstone-levensduur (met inbegrip van zijn replicatie fouten die meer dan 100% van het TSL zijn). Streven tookeep dit nummer op 0.

> [!NOTE]
> Alle Hallo tombstone-levensduur percentage berekeningen zijn gebaseerd op Hallo werkelijke tombstone-levensduur voor uw Active Directory-forest, zodat u vertrouwen kunt, dat deze percentages kloppen, zelfs als u een aangepaste tombstone-levensduur-waarde ingesteld.
>
>

### <a name="ad-replication-status-details"></a>Details van status van AD-replicatie
Wanneer u een item in een van de lijsten Hallo klikt, ziet u aanvullende informatie over het logboek zoekactie. Hallo resultaten worden gefilterd tooshow enige Hallo fouten gerelateerde toothat item. Bijvoorbeeld, als u klikt u op de eerste domeincontroller Hallo vermeld onder **bestemming serverstatus (ADDC02)**, ziet u de zoekresultaten gefilterd tooshow fouten met die domeincontroller vermeld als de doelserver Hallo:

![AD-replicatiefouten status opgetreden in zoekresultaten](./media/log-analytics-ad-replication-status/oms-ad-replication-search-details.png)

Hier kunt kunt u verder te filteren, Hallo zoekquery wijzigen, enzovoort. Zie voor meer informatie over het gebruik van Hallo logboek zoeken [Meld zoekopdrachten](log-analytics-log-searches.md).

Hallo **HelpLink** veld bevat Hallo-URL van een TechNet-pagina met aanvullende informatie over de specifieke fout. U kunt kopiëren en plakken van deze koppeling in uw browser venster toosee informatie over het oplossen van problemen en het Hallo-fout is hersteld.

U kunt ook klikken op **exporteren** tooexport hello tooExcel resulteert. Exporteren van gegevens hello, kunt u visualiseren van gegevens van de replicatie-fout op een manier die u wilt.

![geëxporteerde AD-replicatiefouten status opgetreden in Excel](./media/log-analytics-ad-replication-status/oms-ad-replication-export.png)

## <a name="ad-replication-status-faq"></a>Replicatiestatus AD Veelgestelde vragen
**V: hoe vaak is AD status replicatiegegevens bijgewerkt?**
A: Hallo informatie wordt elke vijf dagen bijgewerkt.

**V: is er een manier tooconfigure hoe vaak deze gegevens worden bijgewerkt?**
A: niet op dit moment.

**V: moet ik tooadd alle mijn domain controllers toomy OMS-werkruimte in volgorde toosee replicatiestatus?**
A: Nee, slechts één domeincontroller moet worden toegevoegd. Als u meerdere domeincontrollers in uw OMS-werkruimte hebt, gegevens van deze tooOMS verzonden.

**V: ik wil niet tooadd elke domain controllers toomy OMS-werkruimte. Kan ik Hallo AD replicatiestatus oplossing nog steeds gebruiken?**
A: Ja. U kunt Hallo-waarde van een sleutel tooenable register instellen deze. Zie [tooenable een niet-domeincontroller toosend AD gegevens tooOMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

**V: Wat is de naam Hallo van Hallo-proces dat het verzamelen van gegevens Hallo?**
A: AdvisorAssessment.exe

**V: hoe lang duurt het voor gegevens toobe verzameld?**
A: gegevens verzameling tijd afhankelijk Hallo grootte van Hallo Active Directory-omgeving, maar duurt normaal gesproken minder dan 15 minuten.

**V: welk type gegevens worden verzameld?**
A: replicatie gegevens worden verzameld via LDAP.

**V: is er een manier tooconfigure wanneer gegevens worden verzameld?**
A: niet op dit moment.

**V: wat machtigingen doen ik toocollect gegevens nodig?**
A: normale gebruiker machtigingen tooActive Directory zijn voldoende.

## <a name="troubleshoot-data-collection-problems"></a>Gegevens verzamelen problemen oplossen
Hallo AD replicatiestatus oplossingspakket vereist volgorde toocollect gegevens, ten minste één domain controller verbonden toobe tooyour OMS-werkruimte. Totdat u verbinding maakt met een domeincontroller, verschijnt een bericht dat **nog steeds worden gegevens verzameld**.

Als u verbinding maken met een van uw domeincontrollers hulp nodig hebt vindt u documentatie op [verbinding maken met Windows-computers tooLog Analytics](log-analytics-windows-agents.md). Als uw domeincontroller al verbonden tooan bestaande System Center Operations Manager-omgeving is, kunt u ook documentatie op bekijken [verbinding maken met System Center Operations Manager tooLog Analytics](log-analytics-om-agents.md).

Als u niet tooconnect van uw domeincontrollers wilt direct tooOMS of tooSCOM, Zie [tooenable een niet-domeincontroller toosend AD gegevens tooOMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

## <a name="next-steps"></a>Volgende stappen
* Gebruik [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md) tooview gedetailleerde statusgegevens van Active Directory-replicatie.
