---
title: aaaIntegrating met Operations Management Suite (OMS) | Microsoft Docs
description: Bovendien toousing standaardfuncties van OMS hello, u kunt integreren met andere toepassingen en services tooprovide voor beheer van een hybride beheeromgeving, tooprovide aangepaste scenario's unieke tooyour beheeromgeving of een aangepaste tooprovide de beheerervaring voor uw klanten.  In dit artikel biedt een overzicht van de verschillende opties voor het integreren met OMS en koppelingen tooarticles gedetailleerde technische informatie verstrekt.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fc5f3a8a-77f7-4103-bd7e-744c15ffcca7
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: dce752dcdc6c725bbafd49db4a5055750487ecf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-operations-management-suite-oms"></a>Integratie met Operations Management Suite (OMS)
Operations Management Suite is een oplossing van Microsoft cloud-gebaseerde IT management waarmee u beheren kunt en beveiligen van uw on-premises en cloud-infrastructuur.  Bovendien toousing standaardfuncties van OMS hello, u kunt integreren met andere toepassingen en services tooprovide voor beheer van een hybride beheeromgeving, tooprovide aangepaste scenario's unieke tooyour beheeromgeving of een aangepaste tooprovide de beheerervaring voor uw klanten.  Dit artikel bevat een overzicht van de verschillende opties voor het integreren met OMS-services en koppelingen tooarticles gedetailleerde technische informatie verstrekt. 

## <a name="log-analytics"></a>Log Analytics
Management-gegevens die door logboekanalyse verzameld wordt opgeslagen in een opslagplaats die wordt gehost in Azure.  Alle gegevens die zijn opgeslagen in de opslagplaats Hallo is beschikbaar in het logboek van zoekopdrachten die voorzien in snel analyse op zeer grote hoeveelheden gegevens.  De Integratievereisten van uw mogelijk op toopopulate Hallo-opslagplaats met nieuwe gegevens beschikbaar maakt voor analyse, of gegevens in Hallo opslagplaats tooprovide een nieuwe visualisatie tooextract of toointegrate met een ander hulpprogramma.

Elk gegevensitem in Hallo opslagplaats wordt opgeslagen als een record.  Wanneer u de opslagplaats Hallo vullen, moet u gebruikers met Hallo recordtype die gebruikmaakt van uw oplossing en een beschrijving van de eigenschappen opgeven.  Wanneer u gegevens ophalen, moet u deze informatie over Hallo gegevens waarmee u werkt.

![Hallo OMS-opslagplaats in te vullen](media/operations-management-suite-integration/repository.png)

### <a name="populate-hello-log-analytics-repository"></a>Hallo logboekanalyse opslagplaats vullen
Er zijn meerdere methoden voor het invullen van Hallo OMS-opslagplaats.  Hallo methode die u gebruikt wordt afhankelijk van factoren zoals waar de brongegevens Hallo zich bevindt, Hallo-indeling van het Hallo-gegevens en welke clients moet u toosupport.  Wanneer gegevens worden opgeslagen in de opslagplaats hello, maken het maakt niet uit hoe deze is verzameld.

Hallo beschrijven volgende secties Hallo verschillende opties voor het invullen van Hallo OMS-opslagplaats.

#### <a name="connected-sources-and-data-sources"></a>Verbonden bronnen en gegevensbronnen
Verbonden bronnen zijn Hallo locaties waar gegevens worden opgehaald voor Hallo OMS-opslagplaats.  Gegevensbronnen en oplossingen wordt uitgevoerd op verbonden bronnen en definieer Hallo specifieke gegevens die worden verzameld.  Als uw toepassing gegevens tooone van deze gegevensbronnen schrijft, kunt klikt u vervolgens u verzamelen deze door het configureren van de gegevensbron Hallo.  Bijvoorbeeld, als uw toepassing Syslog-gebeurtenissen gemaakte, kunnen vervolgens zij worden verzameld door Hallo Syslog-gegevensbron op een Linux-agent.

* [Gegevensbronnen in Log Analytics](../log-analytics/log-analytics-data-sources.md)

#### <a name="solutions"></a>Oplossingen
Oplossingen uitbreiden Hallo-mogelijkheden van OMS.  Een oplossing kan verzamelen van gegevens van de verbonden bron Hallo of deze kan op records die al zijn verzameld in Hallo opslagplaats analyse uitvoeren.  Elke oplossing geleverd door Microsoft heeft een afzonderlijke artikel die Hallo details over Hallo-gegevens die worden verzameld.

* [Oplossingen in Log Analytics](../log-analytics/log-analytics-add-solutions.md)

#### <a name="http-data-collector-api"></a>Gegevensverzamelaar voor HTTP-API
Hallo Log Analytics HTTP Data Collector API is een REST-API waarmee u tooadd JSON data toohello Log Analytics-opslagplaats.  Wanneer u een toepassing die geen gegevens via een Hallo andere gegevensbronnen of oplossingen biedt hebt, kunt u deze API gebruikmaken.  Het kan gebruikte toopopulate Hallo opslagplaats vanaf elke client die Hallo API kan aanroepen en niet afhankelijk van de planning voor het verzamelen van een gegevensbron of oplossing Hallo zijn.

* [Log Analytics HTTP-gegevensverzamelaar API](../log-analytics/log-analytics-data-collector-api.md)

### <a name="retrieve-data-from-hello-log-analytics-repository"></a>Gegevens ophalen uit Hallo Log Analytics-bibliotheek
Er zijn meerdere methoden voor het ophalen van gegevens uit Hallo OMS-opslagplaats.  U kunt gebruikers tooretrieve gegevens met Hallo OMS-console en hen voorzien van verschillende soorten visualisaties en analyse.  U kunt ook Hallo-gegevens ophalen uit een extern proces, zoals een andere oplossing voor het beheer.

#### <a name="log-searches"></a>Logboek zoekopdrachten
Alle gegevens die zijn opgeslagen in de OMS-opslagplaats Hallo is beschikbaar via logboek zoekopdrachten.  Gebruikers kunnen hun eigen ad-hoc analyses in Hallo OMS-console of maak een dashboard met een visualisatie in voor een bepaald logboek zoekopdracht.  Oplossingen kunnen aangepaste weergaven met visualisaties op basis van vooraf gedefinieerde zoekopdrachten bevatten.  Hallo Log-API van zoekservice tooaccess gegevens kunt u in Hallo OMS opslagplaats uit een externe toepassing of management-hulpprogramma.  

* [Logboek van zoekopdrachten in Log Analytics](../log-analytics/log-analytics-log-searches.md)
* [Log Analytics logboek search REST-API](../log-analytics/log-analytics-log-search-api.md)
* [Log Analytics-cmdlets](https://msdn.microsoft.com/library/mt188224.aspx)

#### <a name="custom-views"></a>Aangepaste weergaven
Hallo-ontwerper kunt u toocreate aangepaste weergaven in de OMS-console Hallo die gebruikers visualisatie en analyse van gegevens in uw oplossing Hallo bieden.  Elke weergave bevat een tegel die wordt weergegeven op de hoofdpagina Hallo van Hallo-console en een willekeurig aantal visualisatie delen die zijn gebaseerd op het logboek van zoekopdrachten die u definieert.

* [Log Analytics-ontwerper](../log-analytics/log-analytics-view-designer.md)

#### <a name="power-bi"></a>Power BI
Log Analytics kunt automatisch gegevens exporteren vanuit Hallo OMS-opslagplaats in Power BI zodat u van de vorm van visualisaties en hulpmiddelen voor analyse gebruikmaken kunt.  Hiermee deze export worden uitgevoerd volgens een schema zodat Hallo gegevens toodate houden. 

* [Log Analytics gegevens tooPower BI exporteren](../log-analytics/log-analytics-powerbi.md)

## <a name="automation"></a>Automatisering
OMS kunt automatiseren processen tooreact toocollected gegevens of tooperform andere beheerfuncties.  Kan het verzamelen van gegevens van uw toepassing en plaats deze in Hallo OMS-opslagplaats of u Hallo correctie van een bekend probleem in het antwoord toodata gevonden in de opslagplaats Hallo kan automatiseren. 

![Automatisering](media/operations-management-suite-integration/automate.png)

### <a name="runbooks"></a>Runbooks
PowerShell-scripts en werkstromen van Runbooks in Azure Automation worden uitgevoerd in hello Azure-cloud.  U kunt deze toomanage resources in Azure of andere bronnen die toegankelijk zijn vanuit de cloud hello gebruiken.  Runbooks kunnen ook worden uitgevoerd in een lokaal datacenter met Hybrid Runbook Worker.  U kunt een runbook starten vanaf hello Azure-portal of externe processen met behulp van een aantal methoden zoals PowerShell of Hallo Automation-API.

* [Een runbook starten in Azure Automation](../automation/automation-starting-a-runbook.md)
* [Azure Automation-cmdlets](https://msdn.microsoft.com/library/dn690262.aspx)
* [REST-API voor Automation](https://msdn.microsoft.com/library/mt662285.aspx)
* [Automation .NET](https://msdn.microsoft.com//library/mt465763.aspx)

### <a name="alerts"></a>Waarschuwingen
Waarschuwingsregels logboek zoekopdrachten volgens planning tooa automatisch wordt uitgevoerd.  Als de resultaten Hallo overeenkomt met bepaalde kunt criteria Hallo resulterende waarschuwing starten van een runbook in Azure Automation of aanroepen van een webhook die met een extern proces kan starten.  Beide van deze antwoorden kunnen details van Hallo waarschuwing inclusief Hallo-gegevens geretourneerd in Hallo logboek zoekopdracht opnemen.

* [Waarschuwingen in Log Analytics](../log-analytics/log-analytics-alerts.md)
* [Waarschuwing log Analytics-API](../log-analytics/log-analytics-api-alerts.md)

## <a name="backup-and-site-recovery"></a>Back-up en siteherstel
Azure back-up- en Site Recovery-services bieden voor uw Ondernemingsgegevens beveiligen en Hallo beschikbaarheid van servers en toepassingen.  U kunt deze services tooperform gebruikmaken van scenario's zoals back-up bieden voor uw toepassing of u een failover van een virtuele machine start.

* [Azure Backup-cmdlets](https://msdn.microsoft.com/library/mt619253.aspx)
* [Azure Site Recovery REST-API](https://msdn.microsoft.com/library/azure/mt750497.aspx)
* [Azure Site Recovery-Cmdlets](https://msdn.microsoft.com/library/mt637930.aspx)

## <a name="custom-solutions"></a>Aangepaste oplossingen
U kunt integratie logica verpakken in een aangepaste oplossing toorun in uw werkruimte of in een klant werkruimte.  Uw oplossing kan bevatten van Hallo integratie methoden in dit artikel toevoeging tooother resources tooprovide een scenario voor volledig beheer.  Hallo-resources in Hallo oplossing zijn verpakt zo dat wanneer Hallo oplossing wordt verwijderd, alle Hallo resources dat is gemaakt worden verwijderd uit het Hallo OMS-werkruimte en de Azure-abonnement.

Uw oplossing een Automation-runbook toogather en proces-gegevens bevatten en vervolgens vullen Hallo logboekanalyse opslagplaats via Hallo HTTP Data Collector API.  U kunt ook een aangepaste weergave die geeft en analyseert gegevens verzameld Hallo opnemen.  

* Maken van aangepaste oplossingen (binnenkort)    

## <a name="next-steps"></a>Volgende stappen
* Verwijzing Hallo [OMS SDK](operations-management-suite-sdk.md) voor technische informatie over het automatiseren van OMS-services.  

