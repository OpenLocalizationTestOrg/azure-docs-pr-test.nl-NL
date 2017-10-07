---
title: aaaAzure Operations Management Suite (OMS)-documentatie - zelfstudie | Microsoft Docs
description: Microsoft Operations Management Suite (OMS) is een cloudoplossing voor IT-beheer van Microsoft waarmee u uw on-premises en cloudinfrastructuur kunt beheren en beveiligen. In dit artikel Hallo verschillende services die worden opgenomen in OMS identificeert en vindt u koppelingen tootheir gedetailleerde inhoud.
services: operations-management-suite
author: carolz
manager: carolz
layout: LandingPage
ms.assetid: 
ms.service: operations-management-suite
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: landing-page
ms.date: 01/23/2017
ms.author: carolz
ms.openlocfilehash: 11a8f5ecb3d84aed90554510fc1bb43320fdebb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>Wat is Operations Management Suite (OMS)?
Microsoft Operations Management Suite (OMS) is een cloudoplossing voor IT-beheer van Microsoft waarmee u uw on-premises en cloudinfrastructuur kunt beheren en beveiligen.  Aangezien OMS wordt geïmplementeerd als een cloudservice, kunt u er al snel mee aan de slag, en dat met minimale investeringen in infrastructuurservices.  Nieuwe functies worden automatisch geleverd, zodat u bespaart op kosten voor lopend onderhoud en upgrades.

Bovendien kunnen tooproviding waardevolle services op een eigen, OMS integreren met System Center-onderdelen, zoals System Center Operations Manager tooextend uw bestaande investeringen in de management in Hallo cloud.  System Center en OMS kunnen samenwerken tooprovide beheer van een volledige hybride-ervaring.

Hallo uit te voeren bieden een hoog niveau Beschrijving van Hallo andere waarde gebieden van OMS en Hallo-services die ze worden geïmplementeerd.  Voordat controleren Hallo documentatie voor elk gedetailleerde, kunt u tooOMS architectuur voor een overzicht van Hallo verschillende OMS onderdelen verwijzen.

## <a name="insight-and-analyticsmediaoperations-management-suite-overviewicon-insight-analyticspng-insight-and-analytics"></a>![Inzicht en analyses](media/operations-management-suite-overview/icon-insight-analytics.png) Inzicht en analyses
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) helpt u om logboek- en prestatiegegevens die worden gegenereerd door besturingssystemen en toepassingen, te verzamelen, aan elkaar de correleren, te vinden en er actie op te ondernemen. Dit biedt u realtime operationeel inzicht met geïntegreerde zoekfunctie en aangepaste dashboards tooreadily miljoenen records analyseren voor alle uw workloads en servers, ongeacht de fysieke locatie.

U kunt eenvoudig oplossingen tooLog analyses die gegevens toobe verzameld definiëren en logica voor de analyse Hallo toevoegen.  Oplossingen mogelijk aanvullende functionaliteit die automatisch wordt geleverd tooagents met minimale of er is geen configuratie bevatten.  Bovendien toousing analyseprogramma's geleverd door afzonderlijke oplossingen, kunt u aangepaste zoekopdrachten uitvoeren via de volledige gegevensset Hallo in volgorde toocorrelate gegevens tussen de systemen en toepassingen.  

## <a name="automation--controlmediaoperations-management-suite-overviewicon-automation-controlpng-automation--control"></a>![Automation en besturing](media/operations-management-suite-overview/icon-automation-control.png) Automation en besturing
Azure Automation automatiseert administratieve processen met [runbooks](../automation/automation-runbook-types.md) die zijn gebaseerd op PowerShell en uitvoeren in hello Azure-cloud.  Runbooks hebben toegang tot andere producten of services die kunnen worden beheerd met PowerShell, met inbegrip van resources in andere clouds zoals Amazon Web Services (AWS).  Runbooks kunnen ook worden uitgevoerd op een server in uw lokale toomanage lokale bronnen in een datacenter.

Azure Automation biedt configuratiebeheer met [PowerShell DSC](../automation/automation-dsc-overview.md).  U kunt maken en beheren van DSC-resources gehost in Azure en ze toocloud en on-premises systemen toodefine toepassen en automatisch afdwingen hun configuratie.

## <a name="protection-and-recoverymediaoperations-management-suite-overviewicon-protection-recoverypng-protection-and-disaster-recovery"></a>![Beveiliging en herstel](media/operations-management-suite-overview/icon-protection-recovery.png) Beveiliging en herstel na noodgevallen
[Azure Backup](http://azure.microsoft.com/documentation/services/backup) beschermt uw toepassingsgegevens en bewaart deze jarenlang, zonder dat u grote investeringen hoeft te doen en met een minimum aan operationele kosten.  Deze kan back-upgegevens van fysieke en virtuele Windows-servers in toevoeging tooapplication werkbelastingen zoals SQL Server en SharePoint.  Het kan ook worden gebruikt door System Center Data Protection Manager (DPM) tooreplicate beveiligde gegevens tooAzure voor redundantie en langetermijnopslag.

[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) bijdraagt tooyour zakelijke continuïteit en noodherstelplan (BCDR) door te organiseren van replicatie, failovers en herstel van on-premises Hyper-V virtuele machines, virtuele VMware-machines en fysieke Windows / Linux-servers. U kunt replicatie van machines tooa secundaire Datacenter of uw datacenter uitbreiden door het repliceren van tooAzure. Site Recovery biedt ook eenvoudige functionaliteit voor failover en herstel voor werkbelastingen. Site Recovery is geïntegreerd met mechanismen voor herstel na noodgevallen, zoals SQL Server AlwaysOn, en biedt plannen voor herstel voor een eenvoudige failover van werkbelastingen die zich gelaagd op meerdere computers bevinden.

## <a name="oms-security-and-compliancemediaoperations-management-suite-overviewicon-security-compliancepng-security-and-compliance"></a>![Beveiliging en naleving in OMS](media/operations-management-suite-overview/icon-security-compliance.png) Beveiliging en naleving
Beveiliging en naleving helpt u identificeren, beoordelen en beveiligingsrisico's tooyour infrastructuur beperken.  Deze functies van OMS worden geïmplementeerd met behulp van meerdere oplossingen in logboekanalyse die logboekgegevens en configuratie van de agent systemen tooassist analyseren u om ervoor te zorgen Hallo actieve beveiliging van uw omgeving.

* Hallo [beveiligings- en Audit oplossing](oms-security-getting-started.md) verzameld en geanalyseerd beveiligingsgebeurtenissen op beheerde systemen tooidentify verdachte activiteit.
* Hallo [antimalwareoplossing](../log-analytics/log-analytics-malware.md) Hallo status van de antimalware-bescherming op beheerde systemen.  
* Hallo systeemupdates oplossing voert een analyse van Hallo beveiligingsupdates en andere updates op uw beheerde systemen, zodat u eenvoudig systemen identificeren waarvoor patches.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* Meer informatie over [Azure Automation](../automation/automation-intro.md).
* Meer informatie over [Azure Backup](http://azure.microsoft.com/documentation/services/backup).
* Meer informatie over [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).

