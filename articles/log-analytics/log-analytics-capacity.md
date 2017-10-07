---
title: aaaCapacity en prestaties oplossing in Azure Log Analytics | Microsoft Docs
description: Gebruik Hallo capaciteit en prestaties oplossing in logboekanalyse toohelp u begrijpt Hallo capaciteit van de Hyper-V-servers.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 51617a6f-ffdd-4ed2-8b74-1257149ce3d4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: c47bb1e8bb9d4460b0241e89a616f3b356844b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-hyper-v-virtual-machine-capacity-with-hello-capacity-and-performance-solution-preview"></a>Plannen van capaciteit voor Hyper-V virtuele machines met Hallo capaciteit en prestaties-oplossing (Preview)

![Symbool van capaciteit en prestaties](./media/log-analytics-capacity/capacity-solution.png)

U kunt Hallo capaciteit en prestaties oplossing in logboekanalyse toohelp u begrijpt Hallo capaciteit van de Hyper-V-servers. Hallo-oplossing biedt inzicht in uw Hyper-V-omgeving door u totale netwerkgebruik (CPU, geheugen en schijfruimte) van hosts Hallo Hallo en Hallo VM's op deze hosts Hyper-V wordt uitgevoerd. Metrische gegevens worden verzameld voor CPU, geheugen en schijven voor alle hosts en Hallo VM's erop worden uitgevoerd.

Hallo-oplossing:

-   Bevat hosts met de hoogste en laagste gebruik van CPU en geheugen
-   Virtuele machines bevat met de hoogste en laagste gebruik van CPU en geheugen
-   Virtuele machines bevat met de hoogste en laagste IOPS en doorvoerlimieten gebruik
-   Geeft aan welke VM's worden uitgevoerd op welke hosts
-   Toont Hallo bovenste schijven met hoge doorvoer, IOP's, en latentie in cluster shared volumes
- Hiermee kunt u toocustomize en filteren op basis van groepen

> [!NOTE]
> Hallo vorige versie van Hallo capaciteit en prestaties oplossing aangeroepen capaciteit Management vereist zowel System Center Operations Manager en System Center Virtual Machine Manager. Deze bijgewerkte oplossing beschikt niet over die afhankelijkheden.


## <a name="connected-sources"></a>Verbonden bronnen

Hallo volgende tabel beschrijft Hallo verbonden gegevensbronnen die worden ondersteund door deze oplossing.

| Verbonden bron | Ondersteuning | Beschrijving |
|---|---|---|
| [Windows-agents](log-analytics-windows-agents.md) | Ja | Hallo oplossing verzamelt gegevens van de capaciteit en prestaties van Windows-agents. |
| [Linux-agents](log-analytics-linux-agents.md) | Nee    | Hallo oplossing verzamelt geen gegevens van de capaciteit en prestaties van rechtstreekse Linux-agents.|
| [SCOM-beheergroep](log-analytics-om-agents.md) | Ja |Hallo oplossing verzamelt gegevens van capaciteit en prestaties van agents in een verbonden SCOM-beheergroep. Een rechtstreekse verbinding tussen Hallo SCOM agent tooOMS is niet vereist. Gegevens doorgestuurd vanuit Hallo management groep toohello OMS-opslagplaats.|
| [Azure Storage-account](log-analytics-azure-storage.md) | Nee | Azure-opslag bevat geen gegevens voor capaciteit en prestaties.|

## <a name="prerequisites"></a>Vereisten

- Windows- of Operations Manager-agents moeten worden geïnstalleerd op Windows Server 2012 Hyper-V-hosts of hoger, niet voor virtuele machines.


## <a name="configuration"></a>Configuratie

Volgende stap tooadd Hallo capaciteit en prestaties oplossing tooyour werkruimte Hallo uitvoeren.

- Hallo capaciteit en prestaties oplossing tooyour OMS-werkruimte met behulp van Hallo proces dat wordt beschreven in toevoegen [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).

## <a name="management-packs"></a>Management packs

Als uw SCOM-beheergroep verbonden tooyour OMS-werkruimte is, wordt klikt u vervolgens Hallo volgende management packs geïnstalleerd in SCOM wanneer u deze oplossing toevoegt. Er is geen configuratie of onderhoud van deze management packs vereist.

- Microsoft.IntelligencePacks.CapacityPerformance

Hallo 1201 gebeurtenis er ongeveer als volgt:


```
New Management Pack with id:"Microsoft.IntelligencePacks.CapacityPerformance", version:"1.10.3190.0" received.
```

Wanneer Hallo capaciteit en prestaties oplossing wordt bijgewerkt, wordt Hallo versienummer gewijzigd.

Zie voor meer informatie over hoe de oplossing management packs worden bijgewerkt, [verbinding maken met Operations Manager tooLog Analytics](log-analytics-om-agents.md).

## <a name="using-hello-solution"></a>Met behulp van Hallo-oplossing

Wanneer u Hallo capaciteit en prestaties oplossing tooyour werkruimte toevoegt, wordt Hallo capaciteit en prestaties toohello Overzichtsdashboard toegevoegd. Deze tegel geeft het aantal Hallo-nummer van de momenteel actieve Hyper-V-hosts en Hallo van actieve virtuele machines die zijn gecontroleerd voor een geselecteerde periode Hallo-tijd weer.

![Tegel capaciteit en prestaties](./media/log-analytics-capacity/capacity-tile.png)


### <a name="review-utilization"></a>Gebruik controleren

Klik op Hallo capaciteit en prestaties tegel tooopen Hallo capaciteit en prestaties dashboard. Hallo dashboard bevat Hallo kolommen in de volgende tabel Hallo. Elke kolom bevat tooten artikelen die overeenkomen met die van de kolom criteria voor Hallo bereik en tijdbereik opgegeven. U kunt een logboek-zoekquery waarmee alle records door te klikken op uitvoeren **alle** onderin Hallo van Hallo kolom of door te klikken op de kolomkop Hallo.

- **Hosts**
    - **Host-CPU-gebruik** ziet u een grafisch weergegeven trend van Hallo CPU-gebruik van de host-computers en een lijst met hosts, op basis van Hallo geselecteerde periode. Beweeg de muisaanwijzer over Hallo grafiek tooview regeldetails voor een bepaald punt in tijd. Klik op Hallo grafiek tooview logboek zoeken voor meer informatie. Klik op elke host naam tooopen logboek zoeken en weergeven van CPU-details voor prestatiemeteritems voor gehoste virtuele machines.
    - **Geheugengebruik host** ziet u een grafisch weergegeven trend van Hallo geheugengebruik van hostcomputers en een lijst met hosts, op basis van Hallo geselecteerde periode. Beweeg de muisaanwijzer over Hallo grafiek tooview regeldetails voor een bepaald punt in tijd. Klik op Hallo grafiek tooview logboek zoeken voor meer informatie. Klik op elke host naam tooopen logboek Zoek- en geheugen details voor prestatiemeteritems voor gehoste virtuele machines.
- **Virtuele machines**
    - **VM CPU-gebruik** ziet u een grafisch weergegeven trend van Hallo CPU-gebruik van virtuele machines en een lijst van virtuele machines, op basis van Hallo geselecteerde periode. Beweeg de muisaanwijzer over Hallo grafiek tooview regeldetails voor een bepaald punt in tijd voor Hallo top 3 VM's. Klik op Hallo grafiek tooview logboek zoeken voor meer informatie. Klik op een VM naam tooopen logboek zoeken en weergave samengevoegd CPU-details voor prestatiemeteritems voor Hallo VM.
    - **VM-geheugengebruik** ziet u een grafisch weergegeven trend van Hallo geheugengebruik van virtuele machines en een lijst van virtuele machines, op basis van Hallo geselecteerde periode. Beweeg de muisaanwijzer over Hallo grafiek tooview regeldetails voor een bepaald punt in tijd voor Hallo top 3 VM's. Klik op Hallo grafiek tooview logboek zoeken voor meer informatie. Klik op een VM naam tooopen logboek zoeken en weergeven van geaggregeerde geheugen details voor prestatiemeteritems voor Hallo VM.
    - **Totaal aantal schijf-IOPS VM** toont een grafisch weergegeven trend van Hallo totale schijf-IOPS voor virtuele machines en een lijst met virtuele machines met Hallo IOP's voor elk, op basis van de geselecteerde periode Hallo. Beweeg de muisaanwijzer over Hallo grafiek tooview regeldetails voor een bepaald punt in tijd voor Hallo top 3 VM's. Klik op Hallo grafiek tooview logboek zoeken voor meer informatie. Klik op een VM naam tooopen logboek Zoek- en samengevoegde schijf-IOPS teller details voor Hallo VM.
    - **De totale schijfruimte doorvoer VM** toont een grafisch weergegeven trend van Hallo totale schijfgrootte doorvoer voor virtuele machines en een lijst met virtuele machines met Hallo totale schijfgrootte doorvoer voor elke, op basis van Hallo periode geselecteerde. Beweeg de muisaanwijzer over Hallo grafiek tooview regeldetails voor een bepaald punt in tijd voor Hallo top 3 VM's. Klik op Hallo grafiek tooview logboek zoeken voor meer informatie. Klik op een VM naam tooopen logboek zoeken en weergeven van cumulatieve totale schijfgrootte doorvoer details voor prestatiemeteritems voor Hallo VM.
- **Geclusterde gedeelde Volumes**
    - **Totale doorvoer** Hallo som van beide leest en schrijft op geclusterde gedeelde volumes bevat.
    - **Totaal aantal IOPS** toont Hallo som van i/o-bewerkingen per seconde op geclusterde gedeelde volumes.
    - **Totale latentie** ziet u de totale latentie Hallo op geclusterde gedeelde volumes.
- **Host dichtheid** Hallo bovenste tegel ziet Hallo kunt u het totale aantal hosts en virtuele machines beschikbaar toohello-oplossing. Klik op Hallo bovenste tegel tooview aanvullende details in het logboek zoeken. Een lijst met alle hosts en Hallo aantal virtuele machines die worden gehost. Klik op een host toodrill Hallo VM resulteert in een logboek zoekopdracht.


![dashboard Hosts blade](./media/log-analytics-capacity/dashboard-hosts.png)

![blade van de virtuele machines dashboard](./media/log-analytics-capacity/dashboard-vms.png)


### <a name="evaluate-performance"></a>Prestaties evalueren

Computeromgevingen met productie verschillen aanzienlijk van tooanother voor één organisatie. Bovendien capaciteit en prestaties werkbelastingen is afhankelijk van hoe uw virtuele machines worden uitgevoerd, en wat u rekening houden met normale. Specifieke procedures toohelp u prestaties meten tooyour omgeving waarschijnlijk niet van toepassing. Zodat meer richtlijnen gegeneraliseerd is beter geschikt toohelp. Microsoft publiceert tal van richtlijnen artikelen toohelp u prestaties meten.

toosummarize, Hallo oplossing verzamelt gegevens van capaciteit en prestaties van een groot aantal bronnen, met inbegrip van prestatiemeteritems. Gebruik van capaciteit en prestaties gegevens die die zijn gepresenteerd in verschillende vlakken in Hallo oplossing en vergelijkt u de resultaten toothose op Hallo [meten van de prestaties van Hyper-V](https://msdn.microsoft.com/library/cc768535.aspx) artikel. Hoewel Hallo artikel kan enige tijd geleden is gepubliceerd, Hallo metrische gegevens, overwegingen en richtlijnen nog steeds geldig zijn. Hallo artikel bevat koppelingen tooother nuttige informatiebronnen.


## <a name="sample-log-searches"></a>Voorbeeldzoekopdrachten in logboeken

Hallo volgende tabel biedt een voorbeeld-logboek zoekt capaciteit en prestaties gegevens verzameld en wordt berekend door deze oplossing.

| Query’s uitvoeren | Beschrijving |
|---|---|
| Alle configuraties van de host geheugen | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="Host Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Alle configuraties voor VM-geheugen | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="VM Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Overzicht van de totale schijf-IOPS over alle VM 's | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Reads/s" OR CounterName="VHD Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Overzicht van de totale doorvoer van de schijf over alle VM 's | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Read MB/s" OR CounterName="VHD Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Overzicht van de totale IOP's over alle CSV 's | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Reads/s" OR CounterName="CSV Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Overzicht van de totale doorvoer over alle CSV 's | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read MB/s" OR CounterName="CSV Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Overzicht van de totale latentie over alle CSV 's | <code> Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read Latency" OR CounterName="CSV Write Latency") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo hierboven query's toohello volgende wilt wijzigen.

> | Query’s uitvoeren | Beschrijving |
|:--- |:--- |
| Alle configuraties van de host geheugen | Perf &#124; waar ObjectName == 'Capaciteit en prestaties' en CounterName == "Host toegewezen geheugen (MB)" &#124; MB samenvatten avg(CounterValue) door InstanceName = |
| Alle configuraties voor VM-geheugen | Perf &#124; waar ObjectName == 'Capaciteit en prestaties' en CounterName == "Toegewezen geheugen (MB) VM" &#124; MB samenvatten avg(CounterValue) door InstanceName = |
| Overzicht van de totale schijf-IOPS over alle VM 's | Perf &#124; waar ObjectName == 'Capaciteit en prestaties' en (CounterName == "VHD leesbewerkingen/s" of CounterName == "VHD-schrijfbewerkingen/s") &#124; overzicht van AggregatedValue = avg(CounterValue) door bin (TimeGenerated, 1 uur), CounterName, InstanceName |
| Overzicht van de totale doorvoer van de schijf over alle VM 's | Perf &#124; waar ObjectName == 'Capaciteit en prestaties' en (CounterName == "VHD lezen MB/s" of CounterName == "VHD schrijven MB/s") &#124; overzicht van AggregatedValue = avg(CounterValue) door bin (TimeGenerated, 1 uur), CounterName, InstanceName |
| Overzicht van de totale IOP's over alle CSV 's | Perf &#124; waar ObjectName == 'Capaciteit en prestaties' en (CounterName == "CSV leesbewerkingen/s" of CounterName == "CSV-schrijfbewerkingen/s") &#124; overzicht van AggregatedValue = avg(CounterValue) door bin (TimeGenerated, 1 uur), CounterName, InstanceName |
| Overzicht van de totale doorvoer over alle CSV 's | Perf &#124; waar ObjectName == 'Capaciteit en prestaties' en (CounterName == "CSV leesbewerkingen/s" of CounterName == "CSV-schrijfbewerkingen/s") &#124; overzicht van AggregatedValue = avg(CounterValue) door bin (TimeGenerated, 1 uur), CounterName, InstanceName |
| Overzicht van de totale latentie over alle CSV 's | Perf &#124; waar ObjectName == 'Capaciteit en prestaties' en (CounterName == 'CSV lezen latentie' of CounterName == 'CSV schrijven latentie') &#124; overzicht van AggregatedValue = avg(CounterValue) door bin (TimeGenerated, 1 uur), CounterName, InstanceName |


## <a name="next-steps"></a>Volgende stappen
* Gebruik [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md) tooview gedetailleerde gegevens voor capaciteit en prestaties.
