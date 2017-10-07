---
title: beheer van aaaAlert in Microsoft monitoring producten | Microsoft Docs
description: Een waarschuwing geeft een probleem aan dat de aandacht van een beheerder vereist.  In dit artikel worden beschreven Hallo verschillen in hoe waarschuwingen worden gemaakt en beheerd in System Center Operations Manager (SCOM) en Log Analytics en aanbevolen procedures bij het gebruik van de twee producten Hallo voor een strategie voor een hybride beheer van waarschuwingen.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6572c3f8-78ca-4fa9-8fe1-d0b488590788
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 526a3d92f3b6a5d6dec2f3979a934cc94c13f2e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-alerts-with-microsoft-monitoring"></a>Het beheren van waarschuwingen met het bewaken van Microsoft
Een waarschuwing geeft een probleem aan dat de aandacht van een beheerder vereist.  Er toch duidelijke verschillen tussen System Center Operations Manager (SCOM) en Log Analytics in Operations Management Suite (OMS) in termen van hoe waarschuwingen worden gemaakt, hoe ze worden beheerd en geanalyseerd, en hoe u wordt gewaarschuwd dat een kritiek probleem is gedetecteerd.

## <a name="alerts-in-operations-manager"></a>Waarschuwingen in Operations Manager
Waarschuwingen in SCOM worden gegenereerd door afzonderlijke regels of monitors tooindicate een specifiek probleem.  Een monitor kan een waarschuwing genereren als krijgt de foutstatus wanneer een regel een waarschuwing tooindicate genereert sommige Kritiek probleem dat is niet direct gerelateerd toohello status van een beheerd object.  Management packs bevatten tal van werkstromen die waarschuwingen genereren voor Hallo toepassing of service die ze beheren.  Onderdeel van het proces van het configureren van een nieuw management pack Hallo afstemmen het tooensure dat niet wordt overspoeld met waarschuwingen voor problemen die u niet van essentieel belang.

![Weergave van de SCOM-waarschuwing](media/operations-management-suite-monitoring-alerts/scom-alert-view.png)

SCOM biedt volledige waarschuwingenbeheer waarschuwingen met een status die kan worden gewijzigd door beheerders, terwijl ze tooresolve Hallo probleem werkt.  Wanneer deze Hallo probleem is opgelost, stelt Hallo beheerder Hallo waarschuwing tooclosed op dat moment wordt deze niet meer weergegeven in weergaven worden actieve waarschuwingen weergegeven.  Waarschuwingen die zijn gegenereerd uit monitors kunnen automatisch worden opgelost wanneer Hallo monitor weer probleemloos kan worden uitgevoerd tooa.

![Waarschuwingsstatus](media/operations-management-suite-monitoring-alerts/scom-alert-status.png)

## <a name="alerts-in-log-analytics"></a>Waarschuwingen in Log Analytics
Een waarschuwing in Log Analytics wordt gemaakt van een logboek-query die automatisch wordt uitgevoerd met regelmatige tussenpozen.  U kunt geen waarschuwingsregel maken van een logboek-query.  Als Hallo query resultaten die overeenkomen met de Hallo criteria die u opgeeft retourneert, wordt een waarschuwing gemaakt.  Dit kan een specifieke query die u een waarschuwing maakt als er een bepaalde gebeurtenis wordt gedetecteerd, of kunt u een meer algemene query of zoekt een foutgebeurtenis tooa bepaalde toepassing betrekking heeft.

Log Analytics waarschuwingen zijn toohello OMS-opslagplaats als een gebeurtenis geschreven en kunnen worden opgehaald met een logboek-query.  Ze hoeft geen status zoals SCOM gebeurtenissen zodat u aangeven kunt wanneer Hallo probleem is opgelost.

![OMS-waarschuwing](media/operations-management-suite-monitoring-alerts/oms-alert.png)

Wanneer SCOM wordt gebruikt als gegevensbron voor logboekanalyse, worden SCOM waarschuwingen toohello OMS-opslagplaats geschreven als ze zijn gemaakt en gewijzigd.  

![SCOM-waarschuwing](media/operations-management-suite-monitoring-alerts/scom-alert.png)

Hallo [waarschuwing beheeroplossing](http://technet.microsoft.com/library/mt484092.aspx) biedt een overzicht van actieve waarschuwingen en enkele algemene query's tooretrieve verschillende sets van waarschuwingen.  Dit biedt u effectiever analyse van uw waarschuwingen dan een rapport in SCOM.  U kunt inzoomen op Hallo samenvattingen toodetailed gegevens en tooretrieve verschillende sets van waarschuwingen voor ad-hocquery's maken.

![Oplossing voor beheer van waarschuwingen](media/operations-management-suite-monitoring-alerts/alert-management.png)

## <a name="notifications"></a>Meldingen
Meldingen in SCOM verzenden u een e-mail of tekst in het antwoord tooalerts die aan bepaalde criteria voldoen.  U kunt verschillende meldingsabonnementen die andere mensen gewaarschuwd, afhankelijk van criteria zoals Hallo-object wordt bewaakt, ernst van waarschuwing hello, Hallo soort problemen die worden gedetecteerd of Hallo Hallo maken tijd van de dag.

Enkele abonnementen kunnen worden gebruikt tooimplement strategie voor een volledige aanmelding voor een groot aantal management packs.

![SCOM-waarschuwingen](media/operations-management-suite-monitoring-alerts/alerts-overview-scom.png)

Log Analytics kunt u een melding via e-mail dat er een waarschuwing is gemaakt door in te stellen van een e-meldingsactie op elke [waarschuwingsregel](http://technet.microsoft.com/library/mt614775.aspx).  Deze beschikt niet over de functionaliteit van de Hallo SCOM Hallo abonneren toomultiple waarschuwingen met een enkele regel.  U moet ook toocreate uw eigen regels voor waarschuwingen omdat OMS geen biedt een vooraf geconfigureerde.

![Waarschuwingen in Log Analytics](media/operations-management-suite-monitoring-alerts/alerts-overview-oms.png)

U beheren geen SCOM-waarschuwingen in logboekanalyse volledig echter omdat u alleen in Hallo Operations-Console wijzigen kunt.  Log Analytics is nuttig als onderdeel van een waarschuwing management verwerken echter voor analyseprogramma's bieden die alleen SCOM beschikt niet over.

## <a name="alert-remediation"></a>Waarschuwing herstel
[Herstel](http://technet.microsoft.com/library/mt614775.aspx) tooan poging tooautomatically juiste Hallo probleem geïdentificeerd door een waarschuwing verwijst.

SCOM kunt u toorun diagnoses en herstelbewerkingen antwoord tooa monitor invoeren van een slechte status.  Dit gebeurt gelijktijdige toohello-monitor maken Hallo waarschuwing.  Diagnoses en herstelbewerkingen worden doorgaans geïmplementeerd als een script dat op het Hallo-agent wordt uitgevoerd.  Een diagnostische pogingen toogather meer informatie over Hallo gedetecteerd probleem tijdens een herstelpoging gedaan toocorrect Hallo probleem.

Log Analytics kunt u toostart een [Azure Automation-runbook](https://azure.microsoft.com/documentation/services/automation/) of een webhook aanroepen in antwoord tooa logboekanalyse waarschuwing.  Runbooks kunnen complexe logica geïmplementeerd in PowerShell bevatten.  Hallo-script wordt uitgevoerd in Azure en toegang tot alle Azure-resources of externe bronnen beschikbaar vanuit de cloud Hallo.  Azure Automation heeft Hallo mogelijkheid tooexecute runbooks op een server in uw lokale datacentrum, maar deze functie is momenteel niet beschikbaar bij het starten van runbook Hallo in antwoord tooLog Analytics waarschuwingen.

Zowel herstelbewerkingen in SCOM en runbooks in OMS kunt PowerShell-scripts bevatten, maar herstelbewerkingen zijn moeilijker toocreate en beheren omdat ze moeten zijn opgenomen in een management pack.  Runbooks worden opgeslagen in Azure Automation dat voorziet in functies voor schrijven, testen en het beheer van runbooks.

Als u SCOM als gegevensbron voor Log Analytics gebruiken, kunt u een Log Analytics-waarschuwing met behulp van een query logboek tooretrieve SCOM waarschuwingen opgeslagen in Hallo OMS-opslagplaats maken.  Deze manier kunt u een Azure Automation-runbook toorun in antwoord tooa SCOM waarschuwing.  Omdat Hallo runbook wordt uitgevoerd in Azure, zou dit natuurlijk niet een geschikte strategie voor herstelbewerkingen van lokale problemen zijn.

## <a name="next-steps"></a>Volgende stappen
* Meer details op Hallo van [waarschuwingen in System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh212913.aspx).

