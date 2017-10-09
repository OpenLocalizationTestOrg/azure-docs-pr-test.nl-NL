---
title: aaaCollect en analyseren van de prestatiemeteritems in Azure Log Analytics | Microsoft Docs
description: Prestatiemeteritems worden verzameld met logboekanalyse tooanalyze performance op Windows en Linux-agents.  Dit artikel wordt beschreven hoe tooconfigure verzameling van de prestaties van prestatiemeteritems voor Windows- en Linux-agents, details van deze worden opgeslagen in de OMS-opslagplaats Hallo en hoe tooanalyze ze in Hallo OMS-portal.
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 20e145e4-2ace-4cd9-b252-71fb4f94099e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte
ms.openlocfilehash: 30146fecf8db1d8851b89fdb970f757bbb24abf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-and-linux-performance-data-sources-in-log-analytics"></a>Windows- en Linux prestaties gegevensbronnen in Log Analytics
Prestatiemeters in Windows en Linux bieden inzicht in prestaties Hallo van hardware-onderdelen, besturingssystemen en toepassingen.  Log Analytics kunt verzamelen van prestatiemeteritems met regelmatige tussenpozen voor analyse van de bijna realtime (NRT) in de toevoeging tooaggregating prestatiegegevens voor langere termijn analyse en rapportage.

![Prestatiemeteritems](media/log-analytics-data-sources-performance-counters/overview.png)

## <a name="configuring-performance-counters"></a>Configureren van prestatiemeteritems
Prestatiemeteritems configureren in Hallo OMS-portal Hallo [menu Data in logboekanalyse-instellingen](log-analytics-data-sources.md#configuring-data-sources).

Wanneer u eerst configureren door Windows of Linux-prestatiemeteritems voor een nieuwe OMS-werkruimte, krijgt u maken Hallo optie tooquickly enkele algemene prestatiemeteritems.  Ze worden weergegeven met de volgende tooeach van een selectievakje.  Zorg ervoor dat u wilt dat tooinitially tellers maken zijn geselecteerd en klik vervolgens op **toevoegen Hallo geselecteerd prestatiemeteritems**.

Voor Windows-prestatiemeteritems kunt u een specifiek exemplaar voor elk prestatiemeteritem. Hallo-exemplaar van elk prestatiemeteritem dat u kiest voor Linux-prestatiemeteritems, is van toepassing tooall onderliggende items van Hallo bovenliggende item. Hallo volgende tabel bevat algemene Hallo-exemplaren beschikbaar tooboth Linux- en Windows-prestatiemeteritems.

| Exemplaarnaam | Beschrijving |
| --- | --- |
| \_Totaal |Totaal van alle exemplaren van Hallo |
| \* |Alle exemplaren |
| (/ &#124; / var) |Komt overeen met de exemplaren met de naam: / of /var |

### <a name="windows-performance-counters"></a>Windows-prestatiemeteritems

![Configureren van Windows-prestatiemeteritems](media/log-analytics-data-sources-performance-counters/configure-windows.png)

Volg deze procedure tooadd een nieuwe Windows prestaties teller toocollect.

1. Hallo typenaam van de teller Hallo in het tekstvak Hallo Hallo indeling *object (exemplaar) \counter*.  Wanneer u te typen begint, krijgt u een overeenkomende lijst met algemene prestatiemeteritems.  U kunt een item uit Hallo lijst of typ in een van uw eigen selecteren.  U kunt ook alle instanties voor een bepaald item terugkeren door op te geven *object item*.  

    Wanneer het verzamelen van SQL Server-prestatiemeters van genoemde instanties, alle exemplaar prestatiemeteritems starten met de naam *MSSQL$* en gevolgd door Hallo-naam van het Hallo-exemplaar.  Toocollect hello logboek Cache Hit Ratio meteritem voor alle databases van Hallo Database prestatie-object voor benoemde SQL-exemplaar INST2, Geef bijvoorbeeld `MSSQL$INST2:Databases(*)\Log Cache Hit Ratio`.

2. Klik op  **+**  of druk op **Enter** tooadd hello toohello itemlijst.
3. Wanneer u een item toevoegen, gebruikt het Hallo standaardwaarde van 10 seconden voor de **controle-Interval**.  U kunt deze tooa hogere waarde van too1800 seconden (30 minuten) wijzigen als u wilt dat tooreduce Hallo opslagvereisten prestatiegegevens Hallo verzameld.
4. Wanneer u tellers toe te voegen bent klaar, klikt u op Hallo **opslaan** knop bovenaan Hallo Hallo scherm toosave Hallo configuratie.

### <a name="linux-performance-counters"></a>Linux-prestatiemeteritems

![Configureren van Linux-prestatiemeteritems](media/log-analytics-data-sources-performance-counters/configure-linux.png)

Volg deze procedure tooadd een nieuwe Linux prestaties teller toocollect.

1. Standaard zijn alle configuratiewijzigingen tooall agents automatisch gepusht.  Voor Linux-agents, wordt een configuratiebestand toohello Fluentd gegevensverzamelaar verzonden.  Als u toomodify dit bestand handmatig op elke Linux-agent wenst, schakelt u Hallo vak *toepassen onder configuratie toomy Linux-machines* en volgt u onderstaande Hallo-instructies.
2. Hallo typenaam van de teller Hallo in het tekstvak Hallo Hallo indeling *object (exemplaar) \counter*.  Wanneer u te typen begint, krijgt u een overeenkomende lijst met algemene prestatiemeteritems.  U kunt een item uit Hallo lijst of typ in een van uw eigen selecteren.  
3. Klik op  **+**  of druk op **Enter** tooadd hello toohello itemlijst van andere tellers voor Hallo-object.
4. Alle meteritems voor het gebruik van een object Hallo dezelfde **controle-Interval**.  Hallo standaardwaarde is 10 seconden.  U tooa hoger de waarde van up too1800 seconden (30 minuten) als u wilt dat tooreduce Hallo opslagvereisten prestatiegegevens Hallo verzameld.
5. Wanneer u tellers toe te voegen bent klaar, klikt u op Hallo **opslaan** knop bovenaan Hallo Hallo scherm toosave Hallo configuratie.

#### <a name="configure-linux-performance-counters-in-configuration-file"></a>Linux-prestatiemeteritems in het configuratiebestand configureren
In plaats van Linux-prestatiemeteritems met Hallo OMS-portal configureren, hebt u Hallo-optie voor het bewerken van de configuratiebestanden op Hallo Linux-agent van.  Prestaties metrische gegevens toocollect worden beheerd door Hallo-configuratie in **/etc/opt/microsoft/omsagent/\<werkruimte-id\>/conf/omsagent.conf**.

Elk object of de categorie van prestaties metrische gegevens toocollect moet worden gedefinieerd in het configuratiebestand Hallo als één `<source>` element. Hallo syntaxis volgt Hallo patroon hieronder.

    <source>
      type oms_omi  
      object_name "Processor"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>


Hallo-parameters in dit element worden beschreven in de volgende tabel Hallo.

| Parameters | Beschrijving |
|:--|:--|
| object\_naam | Objectnaam voor Hallo-verzameling. |
| exemplaar\_regex |  Een *reguliere expressie* definiëren welke toocollect exemplaren. Hallo waarde: `.*` bevat alle exemplaren. toocollect processor metrische gegevens voor alleen Hallo \_totaalwaarde, kunt u opgeven `_Total`. Procesgegevens toocollect voor hello alleen crond of sshd exemplaren, kunt u opgeven: ' (crond\|sshd)'. |
| teller\_naam\_regex | Een *reguliere expressie* definiëren welke toocollect tellers (voor Hallo object). toocollect alle meteritems voor het Hallo-object opgeven: `.*`. toocollect wisselen alleen ruimte tellers voor Hallo geheugenobject, bijvoorbeeld: kunt u opgeven:`.+Swap.+` |
| interval | De frequentie op welke Hallo van het object prestatiemeteritems worden verzameld. |


Hallo volgende tabel bevat Hallo-objecten en prestatiemeteritems die u in het Hallo-configuratiebestand opgeven kunt.  Er zijn extra items beschikbaar voor bepaalde toepassingen zoals beschreven in [verzamelen prestatiemeteritems voor Linux-toepassingen in logboekanalyse](log-analytics-data-sources-linux-applications.md).

| Objectnaam | Naam van het meteritem |
|:--|:--|
| Logische schijf | Percentage vrije Inodes |
| Logische schijf | Percentage vrije ruimte |
| Logische schijf | Percentage gebruikte Inodes |
| Logische schijf | Percentage gebruikte ruimte |
| Logische schijf | Gelezen Bytes per seconde |
| Logische schijf | Schijf lezen per seconde |
| Logische schijf | Schijfoverdrachten per seconde |
| Logische schijf | Geschreven Bytes per seconde |
| Logische schijf | Schijf schrijven per seconde |
| Logische schijf | Beschikbare Megabytes |
| Logische schijf | Logische schijf Bytes per seconde |
| Geheugen | Percentage beschikbaar geheugen |
| Geheugen | Percentage beschikbare wisselruimte |
| Geheugen | Percentage gebruikt geheugen |
| Geheugen | Percentage gebruikte wisselruimte |
| Geheugen | Beschikbaar geheugen in megabytes |
| Geheugen | Beschikbare megabytes voor wisselen |
| Geheugen | Paginaleesbewerkingen per seconde |
| Geheugen | Pagina's per seconde |
| Geheugen | Pagina's per seconde |
| Geheugen | Gebruikte wisselruimte in megabytes |
| Geheugen | Gebruikt geheugen in megabytes |
| Netwerk | Totaal aantal verzonden Bytes |
| Netwerk | Totaal aantal ontvangen Bytes |
| Netwerk | Totaal aantal Bytes |
| Netwerk | Totaal aantal verzonden pakketten |
| Netwerk | Totaal aantal ontvangen pakketten |
| Netwerk | Totaal aantal Rx-fouten |
| Netwerk | Totaal aantal Tx-fouten |
| Netwerk | Totaal aantal conflicten |
| Fysieke schijf | Gem. Leestijd schijf |
| Fysieke schijf | Gem. Schijfoverdrachten per seconde |
| Fysieke schijf | Gem. Schrijftijd schijf |
| Fysieke schijf | Fysieke schijf Bytes per seconde |
| Proces | PCT beschermde tijd |
| Proces | Tijd in gebruikersmodus pct |
| Proces | Gebruikt geheugen kB |
| Proces | Virtuele gedeeld geheugen |
| Processor | Percentage DPC-tijd |
| Processor | Percentage niet-actieve tijd |
| Processor | Percentage interrupt-tijd |
| Processor | Percentage wachttijd I/O |
| Processor | Percentage tijd in nice |
| Processor | Percentage tijd in beschermde |
| Processor | Percentage processortijd |
| Processor | Percentage tijd in gebruikersmodus |
| Systeem | Beschikbaar fysiek geheugen |
| Systeem | Vrije ruimte in Wisselgeheugenbestanden |
| Systeem | Beschikbaar virtueel geheugen |
| Systeem | Processen |
| Systeem | Grootte opgeslagen In Pagineringbestanden |
| Systeem | Bedrijfstijd |
| Systeem | Gebruikers |


Hieronder volgt de standaardconfiguratie Hallo voor maatstaven voor prestaties.

    <source>
      type oms_omi
      object_name "Physical Disk"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Logical Disk"
      instance_regex ".*
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Processor"
      instance_regex ".*
      counter_name_regex ".*"
      interval 30s
    </source>

    <source>
      type oms_omi
      object_name "Memory"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>

## <a name="data-collection"></a>Gegevensverzameling
Log Analytics verzamelt alle opgegeven prestatiemeteritems op hun opgegeven controle-interval op alle agents die die meteritem geïnstalleerd hebben.  Hallo gegevens wordt niet geaggregeerd en Hallo onbewerkte gegevens is beschikbaar in alle weergaven van logboek zoeken voor Hallo duur is opgegeven door uw abonnement OMS.

## <a name="performance-record-properties"></a>Eigenschappen van de record Performance
Prestaties records hebben een soort **Perf** en Hallo eigenschappen in de volgende tabel Hallo hebben.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Computer |Computer die gebeurtenis Hallo is verzameld. |
| CounterName |Naam van het prestatiemeteritem Hallo |
| Itempad |Volledig pad van de teller Hallo Hallo vorm \\ \\ \<Computer >\\object(exemplaar)\\teller. |
| Tegenwaarde |Numerieke waarde van Hallo teller. |
| InstanceName |Naam van exemplaar van Hallo-gebeurtenis.  Als er is geen exemplaar leeg. |
| Objectnaam |Naam van prestatieobject Hallo |
| SourceSystem |Agent Hallo gegevenstype is verzameld. <br><br>OpsManager – Windows-agent, ofwel direct verbinding maken of SCOM <br> Linux – alle Linux-agents  <br> AzureStorage – Azure Diagnostics |
| TimeGenerated |Datum en tijd Hallo-gegevens is actieve. |

## <a name="sizing-estimates"></a>Maakt een schatting van schaling
 Een ruwe schatting voor de verzameling van een bepaald item met een interval van 10 seconden is ongeveer 1 MB per dag per exemplaar.  U kunt de opslagvereisten Hallo van een bepaald item schatten Hello formule te volgen.

    1 MB x (number of counters) x (number of agents) x (number of instances)

## <a name="log-searches-with-performance-records"></a>Logboek van zoekopdrachten met prestatiegegevens
Hallo bevat volgende tabel voorbeelden van logboek-zoekopdrachten die prestatiegegevens ophalen.

| Query’s uitvoeren | Beschrijving |
|:--- |:--- |
| Type = Perf |Alle prestatiegegevens |
| Type = Perf Computer = 'Computer' |Alle prestatiegegevens van een bepaalde computer |
| Type = Perf CounterName = 'Huidige wachtrijlengte' |Alle prestatiegegevens voor een bepaald item |
| Type Perf = (ObjectName = Processor) CounterName = '% processortijd' InstanceName = _Totaal &#124; meting Avg(Average) als AVGCPU door Computer |Gemiddelde CPU-gebruik op alle computers |
| Type Perf = (CounterName = '% processortijd') &#124;  meting max(Max) door Computer |Maximale CPU-gebruik op alle computers |
| Type = Perf ObjectName = LogicalDisk CounterName = 'Huidige schijf wachtrijlengte' Computer = "MijnComputernaam" &#124; meting Avg(Average) door InstanceName |Huidige wachtrijlengte voor schijf gemiddeld over alle Hallo exemplaren van een bepaalde computer |
| Type = Perf CounterName = "DiskTransfers per seconde" &#124; meting percentile95(Average) door Computer |95e percentiel van Schijfoverdrachten per seconde op alle computers |
| Type = Perf CounterName = '% processortijd' InstanceName = "_Totaal" &#124; meten avg(CounterValue) per Computer Interval 1 uur |Elk uur gemiddelde CPU-gebruik op alle computers |
| Type = Perf Computer = 'Computer' CounterName = % * InstanceName = _Totaal &#124; meting percentile70(CounterValue) met CounterName Interval 1 uur |Elk uur 70 percentiel van elke percentage prestatiemeteritem percentage voor een bepaalde computer |
| Type = Perf CounterName = '% processortijd' InstanceName = '_Totaal' (Computer = 'Computer') &#124; meten min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) per Computer Interval 1 uur |Elk uur gemiddeld, minimum, maximum en 75 percentiel CPU-gebruik voor een specifieke computer |
| Type = Perf ObjectName = "MSSQL$ INST2: Databases ' InstanceName master = | Alle prestatiegegevens van de prestaties van de Database Hallo object voor de hoofddatabase Hallo van Hallo benoemd exemplaar van SQL Server INST2.  

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo hierboven query's toohello volgende wilt wijzigen.

> | Query’s uitvoeren | Beschrijving |
|:--- |:--- |
| Perf |Alle prestatiegegevens |
| Perf &#124; waar Computer == 'Computer' |Alle prestatiegegevens van een bepaalde computer |
| Perf &#124; Indien CounterName == 'Huidige wachtrijlengte' |Alle prestatiegegevens voor een bepaald item |
| Perf &#124; waar ObjectName == 'Processor' en CounterName == '% processortijd' en InstanceName == "_Totaal" &#124; overzicht van AVGCPU = avg(Average) door Computer |Gemiddelde CPU-gebruik op alle computers |
| Perf &#124; Indien CounterName == "% processortijd" &#124; overzicht van AggregatedValue = max(Max) door Computer |Maximale CPU-gebruik op alle computers |
| Perf &#124; waar ObjectName == 'Logische schijf' en CounterName == 'Huidige wachtrijlengte' en Computer == "MijnComputernaam" &#124; overzicht van AggregatedValue avg(Average) door InstanceName = |Huidige wachtrijlengte voor schijf gemiddeld over alle Hallo exemplaren van een bepaalde computer |
| Perf &#124; Indien CounterName == "DiskTransfers per seconde" &#124; overzicht van AggregatedValue = percentiel (gemiddelde, 95) door Computer |95e percentiel van Schijfoverdrachten per seconde op alle computers |
| Perf &#124; Indien CounterName == '% processortijd' en InstanceName == "_Totaal" &#124; overzicht van AggregatedValue = avg(CounterValue) door bin (TimeGenerated, 1 uur), Computer |Elk uur gemiddelde CPU-gebruik op alle computers |
| Perf &#124; waar Computer == 'Computer' en CounterName startswith_cs '%' en InstanceName == "_Totaal" &#124; overzicht van AggregatedValue percentiel (tegenwaarde 70) door bin (TimeGenerated, 1 uur), CounterName = | Elk uur 70 percentiel van elke percentage prestatiemeteritem percentage voor een bepaalde computer |
| Perf &#124; Indien CounterName == '% processortijd' en InstanceName == '_Totaal' en Computer == 'Computer' &#124; samenvatten ['min(CounterValue)'] min(CounterValue), = ["avg(CounterValue)"] = avg(CounterValue), ['percentile75(CounterValue)'] percentiel (tegenwaarde, 75), = ["max(CounterValue)"] = max(CounterValue) door bin (TimeGenerated, 1 uur), Computer |Elk uur gemiddeld, minimum, maximum en 75 percentiel CPU-gebruik voor een specifieke computer |
| Perf &#124; waar ObjectName == "MSSQL$ INST2: Databases ' en InstanceName == 'master' | Alle prestatiegegevens van de prestaties van de Database Hallo object voor de hoofddatabase Hallo van Hallo benoemd exemplaar van SQL Server INST2.  

## <a name="viewing-performance-data"></a>Weergeven van prestatiegegevens
Wanneer u een zoekopdracht logboek voor prestatiegegevens uitvoert, Hallo **lijst** weergave wordt standaard weergegeven.  tooview hello gegevens in de grafische formulier, klikt u op **metrische gegevens**.  Voor een gedetailleerde grafische weergave, klikt u op Hallo  **+**  volgende tooa teller.  

![Metrische gegevens weergeven die zijn samengevouwen](media/log-analytics-data-sources-performance-counters/metricscollapsed.png)

Zie tooaggregate prestatiegegevens in een zoekopdracht logboek [On demand metrische aggregatie en visualisatie in OMS](http://blogs.technet.microsoft.com/msoms/2016/02/26/on-demand-metric-aggregation-and-visualization-in-oms/).


## <a name="next-steps"></a>Volgende stappen
* [Verzamelen van prestatiemeteritems van Linux-toepassingen](log-analytics-data-sources-linux-applications.md) met inbegrip van MySQL en Apache HTTP-Server.
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) tooanalyze Hallo gegevens verzameld van gegevensbronnen en oplossingen.  
* Verzamelde gegevens te exporteren[Power BI](log-analytics-powerbi.md) voor extra visualisaties en analyse.
