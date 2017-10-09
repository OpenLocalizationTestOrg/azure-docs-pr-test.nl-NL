---
title: de gegevensbronnen aaaConfigure in OMS Log Analytics | Microsoft Docs
description: "Gegevensbronnen definiëren dat Log Analytics verzamelt van agents en andere bronnen verbonden Hallo-gegevens.  In dit artikel wordt beschreven Hallo concept van hoe Log Analytics maakt gebruik van gegevensbronnen, wordt uitgelegd Hallo gedetailleerde informatie over de tooconfigure, en bevat een samenvatting van Hallo verschillende gegevensbronnen beschikbaar."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 67710115-c861-40f8-a377-57c7fa6909b4
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: ebe8d29a2442a654b98004f624181ff406868e2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-in-log-analytics"></a>Gegevensbronnen in Log Analytics
Log Analytics verzamelt gegevens van Hallo verbonden bronnen in de OMS-werkruimte en slaat ze op in de OMS-opslagplaats.  Hallo-gegevens die worden verzameld van elk wordt gedefinieerd door Hallo gegevensbronnen die u configureert.  Gegevens in de OMS-opslagplaats hello wordt opgeslagen als een reeks records.  Records van een bepaald type elke gegevensbron gemaakt met elk type met een eigen set eigenschappen.

![Meld u gegevensverzameling Analytics](./media/log-analytics-data-sources/overview.png)

Gegevensbronnen zijn anders dan de OMS-oplossingen die ook gegevens verzamelen van verbonden bronnen en records maken in Hallo OMS-opslagplaats.  Oplossingen tooyour werkruimte van Hallo galerie met oplossingen kunnen worden toegevoegd en biedt doorgaans aanvullende analyse hulpprogramma's in Hallo OMS-portal.  

## <a name="summary-of-data-sources"></a>Samenvatting van gegevensbronnen
Hallo-gegevensbronnen die momenteel beschikbaar in Log Analytics zijn worden weergegeven in de volgende tabel Hallo.  Elk heeft een koppeling tooa apart artikel bieden details voor de gegevensbron.

| Gegevensbron | Gebeurtenistype | Beschrijving |
|:--- |:--- |:--- |
| [Aangepaste logboeken](log-analytics-data-sources-custom-logs.md) |\<Logboeknaam\>_CL |Tekstbestanden op Windows of Linux-agents met de informatie in het foutenlogboek. |
| [Windows-gebeurtenislogboeken](log-analytics-data-sources-windows-events.md) |Gebeurtenis |Gebeurtenissen verzameld van Hallo-gebeurtenislogboek op Windows-computers. |
| [Windows-prestatiemeteritems](log-analytics-data-sources-performance-counters.md) |Perf |Prestatiemeteritems van Windows-computers worden verzameld. |
| [Linux-prestatiemeteritems](log-analytics-data-sources-performance-counters.md) |Perf |Prestatiemeteritems worden verzameld van Linux-computers. |
| [IIS-logboeken](log-analytics-data-sources-iis-logs.md) |W3CIISLog |Internet Information Services registreert W3C-indeling. |
| [Syslog](log-analytics-data-sources-syslog.md) |Syslog |Syslog-gebeurtenissen op Windows of Linux-computers. |

## <a name="configuring-data-sources"></a>Gegevensbronnen configureren
Configureren van gegevensbronnen van Hallo **gegevens** menu van logboekanalyse **instellingen**.  Een willekeurige configuratie geleverd tooall verbonden bronnen in de OMS-werkruimte.  U uitsluiten niet alle agents momenteel van deze configuratie.

![Windows-gebeurtenissen configureren](./media/log-analytics-data-sources/configure-events.png)

1. Klik in Hallo OMS-console op Hallo **instellingen** tegel of Hallo **instellingen** knop Hallo boven aan het welkomstscherm.
2. Selecteer **gegevens**.
3. Klik op Hallo data source tooconfigure.
4. Volg Hallo koppeling toohello documentatie voor elke gegevensbron in Hallo bovenstaande tabel voor meer informatie op hun configuratie.

> [!NOTE]
> U kunt Log Analytics-gegevensbronnen op dit moment in hello Azure-portal configureren.

## <a name="data-collection"></a>Gegevensverzameling
Data source-configuraties worden afgeleverd tooagents die rechtstreeks verbonden zijn met tooLog Analytics binnen enkele minuten duren.  Hallo opgegeven gegevens worden verzameld van Hallo agent en bezorgd rechtstreeks tooLog Analytics in intervallen specifieke tooeach-gegevensbron.  Zie de documentatie Hallo voor elke gegevensbron voor deze specifieke informatie.

Voor System Center Operations Manager (SCOM) agents in een verbonden beheergroep, data source-configuraties omgezet in management packs en beheergroep toohello om de 5 minuten bezorgd standaard.  Hallo agent downloadt Hallo management pack zoals elke andere en verzamelt Hallo opgegeven gegevens. Afhankelijk van Hallo data source Hallo gegevens er worden dat een tooa beheerserver waarop Hallo gegevens toohello logboekanalyse stuurt verzonden of Hallo agent Hallo gegevens tooLog Analytics zonder tussenkomst van de beheerserver hello wordt verzonden. Raadpleeg te[verzameling Gegevensdetails voor OMS-functies en oplossingen](log-analytics-add-solutions.md#data-collection-details) voor meer informatie.  Meer informatie vindt u details van de verbinding van SCOM en OMS en Hallo frequentie wijzigen dat de configuratie wordt geleverd bij [integratie met System Center Operations Manager configureren](log-analytics-om-agents.md).

Als Hallo-agent kan geen tooconnect tooLog Analytics of Operations Manager, blijft toocollect gegevens die u ermee kunt wanneer deze een verbinding tot stand brengt.  Gegevens kunnen verloren gaan als Hallo hoeveelheid gegevens die de maximale cachegrootte Hallo voor Hallo client bereikt of als Hallo-agent niet kunnen tooestablish een verbinding binnen 24 uur.

## <a name="log-analytics-records"></a>Log Analytics-records
Alle gegevens die worden verzameld door Log Analytics wordt opgeslagen in de OMS-opslagplaats Hallo als records.  Records verzameld door andere gegevensbronnen hebben hun eigen set eigenschappen en worden aangeduid met hun **Type** eigenschap.  Zie Hallo-documentatie voor elke gegevensbron en de oplossing voor meer informatie over elk recordtype.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [oplossingen](log-analytics-add-solutions.md) die functionaliteit tooLog Analytics toevoegen en verzamelen van gegevens ook in Hallo OMS-opslagplaats.
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) tooanalyze Hallo gegevens verzameld van gegevensbronnen en oplossingen.  
* Configureer [waarschuwingen](log-analytics-alerts.md) tooproactively zullen u informeren over essentiële gegevens verzameld van gegevensbronnen en oplossingen.
