---
title: aaaAgent Health oplossing in OMS | Microsoft Docs
description: Dit artikel is bedoeld toohelp u begrijpt hoe toouse deze oplossing toomonitor Hallo status van de agents rechtstreeks reporting tooOMS of System Center Operations Manager.
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: magoedte
ms.openlocfilehash: 071b14b4ab7af6680ae458eaa331246755c5bb56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#  <a name="agent-health-solution-in-oms"></a>De oplossing Status van agent in OMS
Hallo Health Agent-oplossing in OMS helpt u begrijpen, voor alle reporting rechtstreeks toohello OMS-werkruimte of een tooOMS groep verbonden van System Center Operations Manager management Hallo-agents die niet reageert en verzenden van operationele gegevens.  U kunt ook van bijhouden hoeveel agents zijn geïmplementeerd, waar ze geografisch worden gedistribueerd en andere query's toomaintain bewustzijn van Hallo verdeling van agents die zijn geïmplementeerd in Azure, andere cloudomgevingen of on-premises uitvoeren.    

## <a name="prerequisites"></a>Vereisten
Voordat u deze oplossing implementeren, moet u bevestigen op dit moment ondersteund [Windows-agents](../log-analytics/log-analytics-windows-agents.md) toohello OMS-werkruimte rapportage of rapportages tooan [Operations Manager-beheergroep](../log-analytics/log-analytics-om-agents.md) geïntegreerd met uw OMS-werkruimte.    

## <a name="solution-components"></a>Oplossingsonderdelen
Deze oplossing bestaat uit Hallo resources die zijn toegevoegd tooyour werkruimte en rechtstreeks verbonden zijn met agents of verbonden beheergroep van Operations Manager te volgen.

### <a name="management-packs"></a>Management packs
Als uw System Center Operations Manager-beheergroep verbonden tooan OMS-werkruimte is, worden volgende management packs Hallo in Operations Manager geïnstalleerd.  Deze management packs worden na het toevoegen van deze oplossing ook op rechtstreeks verbonden Windows-computers geïnstalleerd. Er is niets tooconfigure of beheren met deze management packs.

* Microsoft System Center Advisor HealthAssessment Direct Channel Intelligence Pack  (Microsoft.IntelligencePacks.HealthAssessmentDirect)
* Microsoft System Center Advisor HealthAssessment Server Channel Intelligence Pack (Microsoft.IntelligencePacks.HealthAssessmentViaServer).  

Zie voor meer informatie over hoe de oplossing management packs worden bijgewerkt, [verbinding maken met Operations Manager tooLog Analytics](../log-analytics/log-analytics-om-agents.md).

## <a name="configuration"></a>Configuratie
Hallo agentstatus oplossing tooyour OMS-werkruimte met behulp van Hallo proces dat wordt beschreven in toevoegen [oplossingen toevoegen](../log-analytics/log-analytics-add-solutions.md). Er is geen verdere configuratie nodig.


## <a name="data-collection"></a>Gegevensverzameling
### <a name="supported-agents"></a>Ondersteunde agents
Hallo volgende tabel beschrijft Hallo verbonden gegevensbronnen die worden ondersteund door deze oplossing.

| Verbonden bron | Ondersteund | Beschrijving |
| --- | --- | --- |
| Windows-agents | Ja | Er worden heartbeat-gebeurtenissen verzameld van direct verbonden Windows-agents.|
| Beheergroep System Center Operations Manager | Ja | Heartbeat-gebeurtenissen worden verzameld van agents reporting toohello beheergroep elke 60 seconden en vervolgens doorgestuurd tooLog Analytics. Een rechtstreekse verbinding tussen Operations Manager-agents tooLog Analytics is niet vereist. Heartbeat-gebeurtenisgegevens doorgestuurd vanuit Hallo management groep toohello logboekanalyse opslagplaats.|

## <a name="using-hello-solution"></a>Met behulp van Hallo-oplossing
Wanneer u Hallo oplossing tooyour OMS-werkruimte toevoegt, Hallo **agentstatus** tegel tooyour OMS dashboard worden toegevoegd. Deze tegel ziet u Hallo kunt u het totale aantal agents en het aantal niet-reagerende agents Hallo in Hallo afgelopen 24 uur.<br><br> ![De tegel Status van agent in het dashboard](./media/oms-solution-agenthealth/agenthealth-solution-tile-homepage.png)

Klik op Hallo **agentstatus** tegel tooopen hello **agentstatus** dashboard.  Hallo dashboard bevat Hallo kolommen in de volgende tabel Hallo. Elke kolom bevat Hallo top tien gebeurtenissen op het aantal die overeenkomen met die van de kolom criteria voor Hallo tijdbereik opgegeven. U kunt een zoekopdracht logboek waarmee de volledige lijst Hallo door te selecteren uitvoeren **alle** onderin Hallo rechts van elke kolom, of door te klikken op de kolomkop Hallo.

| Kolom | Beschrijving |
|--------|-------------|
| Agent count over time | Een trend van het aantal agents gedurende een periode van zeven dagen voor Linux- en Windows-agents.|
| Count of unresponsive agents | Een lijst met agents die nog niet als een heartbeat Hallo afgelopen 24 uur verzonden.|
| Distribution by OS Type | Een visualisatie van het aantal Windows- en Linux-agents in uw omgeving.|
| Verdeling naar agent-versie | Een partitie van Hallo andere agent-versies geïnstalleerd in uw omgeving en een telling van elkaar.|
| Verdeling naar agent-catgeorie | Een partitie van verschillende categorieën van agents die heartbeat gebeurtenissen verzendt Hallo: directe agents, OpsMgr agents of Hallo OpsMgr Management Server.|
| Verdeling naar beheergroep | Een partitie Hallo verschillende SCOM beheergroepen in uw omgeving.|
| Geo-location of Agents | Een partitie van Hallo verschillende landen waar u de agents en het totale aantal Hallo van agents die zijn geïnstalleerd in elk land hebt.|
| Count of Gateways Installed | het aantal servers waarop Hallo Hallo OMS-Gateway is geïnstalleerd en een lijst van deze servers.|

![Voorbeeld van het dashboard van de oplossing Status van agent](./media/oms-solution-agenthealth/agenthealth-solution-dashboard.png)  

## <a name="log-analytics-records"></a>Log Analytics-records
Hallo-oplossing maakt een type record in Hallo OMS-opslagplaats.  

### <a name="heartbeat-records"></a>Heartbeat-records
Er wordt een record van het type **Heartbeat** gemaakt.  Deze records hebben Hallo eigenschappen in de volgende tabel Hallo.  

| Eigenschap | Beschrijving |
| --- | --- |
| Type | *Heartbeat*|
| Category | De waarde is *Direct Agent*, *SCOM Agent* of *SCOM Management Server*.|
| Computer | De naam van de computer.|
| OSType | Windows- of Linux-besturingssysteem.|
| OSMajorVersion | De primaire versie van het besturingssysteem.|
| OSMinorVersion | De secundaire versie van het besturingssysteem.|
| Versie | De versie van de OMS-agent of Operations Manager-agent.|
| SCAgentChannel | De waarde is *Direct* en/of *SCManagementServer*.|
| IsGatewayInstalled | Als de OMS-gateway is geïnstalleerd, is de waarde *true*, anders is de waarde *false*.|
| ComputerIP | IP-adres van Hallo-computer.|
| RemoteIPCountry | De geografische locatie waar de computer is geïmplementeerd.|
| ManagementGroupName | De naam van de beheergroep van Operations Manager.|
| SourceComputerId | De unieke ID van de computer.|
| RemoteIPLongitude | De lengtegraad van geografische locatie van de computer.|
| RemoteIPLatitude | De breedtegraad van de geografische locatie van de computer.|

Elke agent rapporten tooan Operations Manager-beheerserver stuurt twee heartbeats en de waarde van de eigenschap SCAgentChannel bevat zowel **Direct** en **SCManagementServer** , afhankelijk van wat Log Analytics-gegevensbronnen en oplossingen die u hebt ingeschakeld in uw abonnement OMS. Als u intrekt, zijn gegevens van oplossingen die rechtstreeks van een Operations Manager management server toohello OMS webservice, of vanwege Hallo hoeveelheid gegevens die worden verzameld op Hallo-agent, rechtstreeks vanuit Hallo agent tooOMS webservice worden verzonden. Heartbeat gebeurtenissen zijn die Hallo waarde hebben **SCManagementServer**, Hallo ComputerIP waarde is Hallo IP-adres van beheerserver Hallo omdat Hallo gegevens daadwerkelijk erdoor wordt geüpload.  Voor heartbeats waar SCAgentChannel te is ingesteld**Direct**, het openbare IP-adres van de agent Hallo Hallo is.  

## <a name="sample-log-searches"></a>Voorbeeldzoekopdrachten in logboeken
Hallo bevat volgende tabel voorbeelden logboek zoekt records die door deze oplossing worden verzameld.

| Query’s uitvoeren | Beschrijving |
| --- | --- |
| Type=Heartbeat &#124; distinct Computer |Het totale aantal agents |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-24HOURS |Aantal niet-reagerende agents in Hallo afgelopen 24 uur |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-15MINUTES |Aantal niet-reagerende agents in de afgelopen 15 minuten Hallo |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer IN {Type=Heartbeat TimeGenerated>NOW-24HOURS &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Online computers (in de afgelopen 24 uur Hallo) |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer NOT IN {Type=Heartbeat TimeGenerated>NOW-30MINUTES &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Totaal aantal Agents Offline in de afgelopen 30 minuten (voor Hallo afgelopen 24 uur) |
| Type=Heartbeat &#124; measure countdistinct(Computer) by OSType |Een trend van het aantal agents in de tijd per type besturingssysteem|
| Type=Heartbeat&#124;measure countdistinct(Computer) by OSType |Distribution by OS Type |
| Type=Heartbeat&#124;measure countdistinct(Computer) by Version |Verdeling naar agent-versie |
| Type=Heartbeat&#124;measure count() by Category |Verdeling naar agent-catgeorie |
| Type=Heartbeat&#124;measure countdistinct(Computer) by ManagementGroupName | Verdeling naar beheergroep |
| Type=Heartbeat&#124;measure countdistinct(Computer) by RemoteIPCountry |Geo-location of Agents |
| Type=Heartbeat IsGatewayInstalled=true&#124;Distinct Computer |Het aantal geïnstalleerde OMS-gateways |


>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](../log-analytics/log-analytics-log-search-upgrade.md), Hallo hierboven query's toohello volgende wilt wijzigen.
>
>| Query’s uitvoeren | Beschrijving |
|:---|:---|
| Heartbeat &#124; distinct Computer |Het totale aantal agents |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(24h) |Aantal niet-reagerende agents in Hallo afgelopen 24 uur |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(15m) |Aantal niet-reagerende agents in de afgelopen 15 minuten Hallo |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer in ((Heartbeat &#124; where TimeGenerated > ago(24h) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Online computers (in de afgelopen 24 uur Hallo) |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer !in ((Heartbeat &#124; where TimeGenerated > ago(30m) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Totaal aantal Agents Offline in de afgelopen 30 minuten (voor Hallo afgelopen 24 uur) |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |Een trend van het aantal agents in de tijd per type besturingssysteem|
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |Distribution by OS Type |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by Version |Verdeling naar agent-versie |
| Heartbeat &#124; summarize AggregatedValue = count() by Category |Verdeling naar agent-catgeorie |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by ManagementGroupName | Verdeling naar beheergroep |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by RemoteIPCountry |Geo-location of Agents |
| Heartbeat &#124; where iff(isnotnull(toint(IsGatewayInstalled)), IsGatewayInstalled == true, IsGatewayInstalled == "true") == true &#124; distinct Computer |Het aantal geïnstalleerde OMS-gateways |

## <a name="next-steps"></a>Volgende stappen

* Zie [Understanding alerts in Log Analytics](../log-analytics/log-analytics-alerts.md) voor meer informatie over het genereren van waarschuwingen van Log Analytics.
