---
title: aaaMigrating van Orchestrator tooAzure Automation | Microsoft Docs
description: Hierin wordt beschreven hoe toomigrate runbooks en de integratie van System Center Orchestrator tooAzure Automation packs.
services: automation
documentationcenter: 
author: bwren
manager: stevenka
editor: tysonn
ms.assetid: 1a7da58c-7a98-49b5-9d9d-001a9f6e631a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2016
ms.author: bwren
ms.openlocfilehash: 797b50067ef2aa68470760e99d494b89ab7baacf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-from-orchestrator-tooazure-automation-beta"></a>Migreren van Orchestrator tooAzure Automation (bèta)
Runbooks in [System Center Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) zijn gebaseerd op activiteiten uit integratiepakketten die specifiek voor Orchestrator zijn geschreven terwijl runbooks in Azure Automation zijn gebaseerd op Windows PowerShell.  [Grafische runbooks](automation-runbook-types.md#graphical-runbooks) in Azure Automation hebt u een vergelijkbare vormgeving tooOrchestrator runbooks met hun activiteiten voor PowerShell-cmdlets, onderliggende runbooks en activa.

Hallo [System Center Orchestrator Migration Toolkit](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) bevat hulpprogramma's voor tooassist u runbooks voor het converteren van Orchestrator tooAzure Automation.  Bovendien tooconverting hello runbooks zelf, moet u converteren Hallo integratiepakketten met Hallo activiteiten die runbooks hello toointegration-modules met Windows PowerShell-cmdlets gebruiken.  

Hieronder volgt Hallo basisproces voor het converteren van Orchestrator runbooks tooAzure Automation.  Elk van deze stappen is beschreven in de volgende secties voor Hallo.

1. Hallo downloaden [System Center Orchestrator Migration Toolkit](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) die Hallo-hulpprogramma's en modules die worden beschreven in dit artikel bevat.
2. Importeren [standaardactiviteiten Module](#standard-activities-module) in Azure Automation.  Dit omvat geconverteerde versies van Orchestrator standaardactiviteiten die kunnen worden gebruikt door geconverteerde runbooks.
3. Importeren [System Center Orchestrator-integratiemodules](#system-center-orchestrator-integration-modules) in Azure Automation voor deze integratiepakketten die wordt gebruikt door uw runbooks die toegang hebben tot System Center.
4. Converteren van aangepaste en derden integratiepakketten met Hallo [Integration Pack Converter](#integration-pack-converter) en importeren in Azure Automation.
5. Converteren van Orchestrator-runbooks met Hallo [Runbook Converter](#runbook-converter) en installeer in Azure Automation.
6. Handmatig vereiste Orchestrator activa maken in Azure Automation sinds Hallo Runbook Converter deze resources niet converteert.
7. Configureer een [Hybrid Runbook Worker](#hybrid-runbook-worker) in uw lokale gegevens center toorun geconverteerd runbooks die toegang lokale bronnen tot.

## <a name="service-management-automation"></a>Service Management Automation
[Service Management Automation](http://technet.microsoft.com/library/dn469260.aspx) (SMA) worden opgeslagen en het uitvoeren van runbooks in uw lokale datacentrum zoals Orchestrator en maakt gebruik van Hallo dezelfde integratiemodules als Azure Automation. Hallo [Runbook Converter](#runbook-converter) Orchestrator runbooks toographical runbooks echter converteert die niet in SMA worden ondersteund.  U kunt nog steeds installeren Hallo [standaard activiteiten Module](#standard-activities-module) en [integratiemodules van System Center Orchestrator](#system-center-orchestrator-integration-modules) in SMA, maar moet u handmatig [herschrijven van uw runbooks](http://technet.microsoft.com/library/dn469262.aspx).

## <a name="hybrid-runbook-worker"></a>Hybrid Runbook Worker
Runbooks in Orchestrator zijn opgeslagen op een databaseserver en uitgevoerd op de runbook-servers, zowel in uw lokale datacentrum.  Runbooks in Azure Automation worden opgeslagen in hello Azure-cloud en kunnen worden uitgevoerd in de lokale data center met een [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md).  Dit is hoe u gewoonlijk geconverteerd van Orchestrator, omdat ze ontworpen toorun op lokale servers zijn runbooks wordt uitgevoerd.

## <a name="integration-pack-converter"></a>Integration Pack Converter
Hallo Integration Pack Converter converteert integratiepakketten die zijn gemaakt met de Hallo [Orchestrator Integration Toolkit (OIT)](http://technet.microsoft.com/library/hh855853.aspx) toointegration modules op basis van Windows PowerShell die kunnen worden geïmporteerd in Azure Automation of Service Management Automation.  

Wanneer u Hallo Integration Pack Converter uitvoert, krijgt u een wizard waarmee u tooselect een integratiepakketbestand (oip).  wizard Hallo en vervolgens een lijst met opgenomen in dat integratiepakket Hallo-activiteiten en kunt u tooselect die wordt gemigreerd.  Wanneer u Hallo wizard hebt voltooid, wordt een integratiemodule met een bijbehorende cmdlet voor elk van de activiteiten in de oorspronkelijke integratiepakket Hallo Hallo gemaakt.

### <a name="parameters"></a>Parameters
Alle eigenschappen van een activiteit in een integratiepakket Hallo zijn geconverteerde tooparameters van de bijbehorende cmdlet Hallo in Hallo integratiemodule.  Windows PowerShell-cmdlets hebben een aantal [algemene parameters](http://technet.microsoft.com/library/hh847884.aspx) die kunnen worden gebruikt met alle cmdlets.  Bijvoorbeeld, Hallo - uitgebreide parameter zorgt ervoor dat een cmdlet toooutput gedetailleerde informatie over de werking ervan.  Er is geen cmdlet heeft misschien een parameter met dezelfde naam als een algemene parameter Hallo.  Als een activiteit een eigenschap met dezelfde naam als een algemene parameter hello heeft, vraagt de wizard Hallo tooprovide u een andere naam voor het Hallo-parameter.

### <a name="monitor-activities"></a>Voor monitoractiviteiten
Bewaken van runbooks in Orchestrator beginnen met een [activiteitsbewaking](http://technet.microsoft.com/library/hh403827.aspx) en wachten toobe aangeroepen door een bepaalde gebeurtenis continu uitvoeren.  Azure Automation biedt geen ondersteuning voor runbooks van de monitor, zodat eventuele monitoractiviteiten in Hallo integratiepakket niet worden geconverteerd.  In plaats daarvan wordt een tijdelijke aanduiding voor cmdlet gemaakt in Hallo integratiemodule voor Hallo monitoractiviteit.  Deze cmdlet heeft geen functionaliteit, maar kunt u een willekeurig geconverteerde runbook deze gebruikt toobe geïnstalleerd.  Dit runbook wordt niet kunnen toorun in Azure Automation, maar kan worden geïnstalleerd zodat u deze kunt wijzigen.

### <a name="integration-packs-that-cannot-be-converted"></a>Integratiepakketten die kunnen niet worden geconverteerd
Integratiepakketten die niet zijn gemaakt met OIT kunnen niet worden geconverteerd met Hallo Integration Pack Converter. Er zijn ook enkele integratiepakketten die is geleverd door Microsoft die op dit moment kan niet worden geconverteerd met dit hulpprogramma.  Geconverteerde versies van deze integratiepakketten zijn [gedownload](#system-center-orchestrator-integration-modules) zodat ze in Azure Automation- of Service Management Automation kunnen worden geïnstalleerd.

## <a name="standard-activities-module"></a>Standaardactiviteiten-Module
Orchestrator bevat een reeks [standaardactiviteiten](http://technet.microsoft.com/library/hh403832.aspx) die niet zijn opgenomen in een integratiepakket, maar worden gebruikt door veel runbooks.  Hallo standaardactiviteiten-module is een integratiemodule met een cmdlet equivalent voor elk van deze activiteiten.  U moet deze integratiemodule in Azure Automation installeren voordat u importeert geconverteerde runbooks die een standaardactiviteit gebruiken.

Bovendien toosupporting runbooks geconverteerd, Hallo-cmdlets in Hallo standaardactiviteiten-module kan worden gebruikt door iemand die bekend zijn met Orchestrator toobuild nieuwe runbooks in Azure Automation.  Tijdens het Hallo-functionaliteit van alle Hallo standaardactiviteiten met cmdlets kan worden uitgevoerd, kunnen ze anders werken.  Hallo Hallo-cmdlets in Hallo geconverteerd standaardactiviteiten module werkt dezelfde als de bijbehorende activiteiten en gebruik Hallo dezelfde parameters.  Dit kan helpen Hallo bestaande Orchestrator runbookauteur in hun overgang tooAzure Automation-runbooks.

## <a name="system-center-orchestrator-integration-modules"></a>System Center Orchestrator-integratiemodules
Microsoft biedt [integratiepakketten](http://technet.microsoft.com/library/hh295851.aspx) voor het bouwen van runbooks tooautomate System Center-onderdelen en andere producten.  Sommige van deze integratiepakketten die momenteel zijn gebaseerd op OIT maar geen momenteel geconverteerde toointegration modules vanwege bekende problemen.  [System Center Orchestrator-integratiemodules](https://www.microsoft.com/download/details.aspx?id=49555) bevat geconverteerde versies van deze integratiepakketten die kunnen worden geïmporteerd in Azure Automation en Service Management Automation.  

Door Hallo RTM-versie van dit hulpprogramma, bijgewerkte versies van integratiepakketten Hallo op basis van OIT die kan worden omgezet met Hallo die Integration Pack Converter wordt gepubliceerd.  Richtlijnen wordt ook tooassist u bij het converteren van runbooks met behulp van activiteiten uit integratiepakketten Hallo niet op basis van OIT worden opgegeven.

## <a name="runbook-converter"></a>Runbook-Converter
Hallo Runbook Converter converteert Orchestrator-runbooks in [grafische runbooks](automation-runbook-types.md#graphical-runbooks) die kunnen worden geïmporteerd in Azure Automation.  

Runbook-Converter is geïmplementeerd als een PowerShell-module met een cmdlet aangeroepen **ConverterenVan SCORunbook** die Hallo conversie uitvoert.  Wanneer u Hallo hulpprogramma installeert, wordt een snelkoppeling tooa PowerShell-sessie die wordt geladen Hallo cmdlet gemaakt.   

Volgende Hallo basisproces tooconvert is een Orchestrator-runbook en importeren in Azure Automation.  Hallo volgende secties bevatten meer informatie over het Hallo-hulpprogramma gebruiken en werken met geconverteerde runbooks.

1. Een of meer runbooks exporteren van Orchestrator.
2. Integratiemodules voor alle activiteiten in Hallo runbook verkrijgen.
3. Orchestrator-runbooks in het geëxporteerde bestand Hallo Hallo converteren.
4. Controleer de gegevens in Logboeken toovalidate Hallo conversie en toodetermine eventuele vereiste handmatige taken.
5. Geconverteerde runbooks in Azure Automation worden geïmporteerd.
6. Alle vereiste activa maken in Azure Automation.
7. Hallo-runbook in Azure Automation toomodify eventuele vereiste activiteiten bewerken.

### <a name="using-runbook-converter"></a>Met behulp van de Converter Runbook
de syntaxis voor het Hallo **ConverterenVan SCORunbook** is als volgt:

    ConvertFrom-SCORunbook -RunbookPath <string> -Module <string[]> -OutputFolder <string>

* RunbookPath - pad toohello export-bestand met Hallo runbooks tooconvert.
* Module - met door komma's gescheiden lijst met integratiemodules met activiteiten in Hallo runbooks.
* OutputFolder - pad toohello map toocreate geconverteerd grafische runbooks.

Hallo volgende voorbeeldopdracht converteert Hallo runbooks in een exportbestand aangeroepen **MyRunbooks.ois_export**.  Deze runbooks Hallo Active Directory en integratiepakketten van Data Protection Manager gebruiken.

    ConvertFrom-SCORunbook -RunbookPath "c:\runbooks\MyRunbooks.ois_export" -Module c:\ip\SystemCenter_IntegrationModule_ActiveDirectory.zip,c:\ip\SystemCenter_IntegrationModule_DPM.zip -OutputFolder "c:\runbooks"


### <a name="log-files"></a>Logboekbestanden
Hallo Runbook Converter maakt Hallo-logboekbestanden in Hallo volgen dezelfde locatie als Hallo runbook geconverteerd.  Als Hallo bestanden al bestaat, wordt deze overschreven met gegevens van de laatste Hallo-conversie.

| File | Inhoud |
|:--- |:--- |
| Runbook Converter - Progress.log |Gedetailleerde stappen van Hallo conversie, met inbegrip van gegevens voor elke activiteit heeft geconverteerd en waarschuwing voor elke activiteit niet geconverteerd. |
| Runbook Converter - Summary.log |Samenvatting van Hallo laatste conversie inclusief eventuele waarschuwingen en taken die u tooperform moet zoals het maken van een variabele is vereist voor het runbook Hallo geconverteerd opvolgen. |

### <a name="exporting-runbooks-from-orchestrator"></a>Exporteren van runbooks van Orchestrator
Hallo Runbook Converter werkt met een exportbestand van Orchestrator met een of meer runbooks.  In het exportbestand hello wordt een bijbehorende Azure Automation-runbook voor elk Orchestrator-runbook gemaakt.  

tooexport Orchestrator, een runbook met de rechtermuisknop op Hallo van Hallo runbook in Runbook Designer en selecteer **exporteren**.  tooexport alle runbooks in een map met de rechtermuisknop op Hallo van Hallo-map en selecteer **exporteren**.

### <a name="runbook-activities"></a>Runbookactiviteiten
Hallo Runbook Converter converteert elke activiteit in Hallo Orchestrator runbook tooa bijbehorende activiteit in Azure Automation.  Voor de activiteiten die kunnen niet worden geconverteerd, wordt een tijdelijke aanduiding voor activiteit gemaakt in Hallo runbook met de waarschuwing.  Nadat u Hallo geconverteerd runbook in Azure Automation importeert, moet u een van deze activiteiten vervangen door geldige activiteiten die Hallo vereist functionaliteit uitvoeren.

Een Orchestrator-activiteiten in Hallo [standaard activiteiten Module](#standard-activities-module) worden geconverteerd.  Er zijn enkele standaard Orchestrator-activiteiten die niet in deze module al en worden niet geconverteerd.  Bijvoorbeeld: **platformgebeurtenis verzenden** heeft geen Azure Automation-equivalent omdat Hallo gebeurtenis specifieke tooOrchestrator.

[Activiteiten volgen die](https://technet.microsoft.com/library/hh403827.aspx) niet worden geconverteerd omdat er geen equivalente toothem in Azure Automation.  Hallo uitzondering zijn monitor activiteiten in [integratiepakketten geconverteerd](#integration-pack-converter) die geconverteerde toohello tijdelijke aanduiding voor activiteit zijn.

Een activiteit uit een [geconverteerd integratiepakket](#integration-pack-converter) worden geconverteerd als u Hallo Hallo pad toohello integratiemodule bieden **modules** parameter.  Voor System Center Integration Packs kunt u Hallo [System Center Orchestrator-integratiemodules](#system-center-orchestrator-integration-modules).

### <a name="orchestrator-resources"></a>Orchestrator-bronnen
Hallo Runbook Converter converteert alleen runbooks, geen andere Orchestrator-bronnen zoals tellers, variabelen of verbindingen.  Prestatiemeteritems worden niet ondersteund in Azure Automation.  Variabelen en verbindingen worden ondersteund, maar moet u ze handmatig maken.  Hallo-logboekbestanden wordt gemeld als Hallo runbook dergelijke resources vereist en geef bijbehorende resources moet u toocreate in Azure Automation voor Hallo runbook toooperate goed geconverteerd.

Een runbook kan bijvoorbeeld een variabele toopopulate een bepaalde waarde gebruiken in een activiteit.  Hallo wordt geconverteerde runbook Hallo activiteit converteren en geef een variabelenactivum in Azure Automation met dezelfde naam als de Orchestrator-variabele Hallo Hallo.  Dit zijn vastgelegd in Hallo **Runbook Converter - Summary.log** bestand dat wordt gemaakt na Hallo conversie.  U moet toomanually deze variabelenactivum maken in Azure Automation voordat u Hallo runbook.

### <a name="input-parameters"></a>Invoerparameters
Runbooks in Orchestrator invoerparameters Hello accepteren **gegevens initialiseren** activiteit.  Als Hallo runbook wordt geconverteerd, deze activiteit bevat wordt er een [invoerparameter](automation-graphical-authoring-intro.md#runbook-input-and-output) in hello Azure Automation runbook is gemaakt voor elke parameter in Hallo-activiteit.  Een [Werkstroomscript besturingselement](automation-graphical-authoring-intro.md#activities) activiteit wordt gemaakt in Hallo geconverteerd runbook die worden opgehaald en elke parameter retourneert.  Alle activiteiten in Hallo runbook die gebruikmaken van een invoerparameter Raadpleeg toohello uitvoer van deze activiteit.

Hallo reden is dat deze strategie wordt gebruikt is toobest mirror Hallo functionaliteit in Hallo Orchestrator runbook.  Activiteiten in een nieuwe grafische runbooks moeten rechtstreeks verwijzen tooinput parameters in met behulp van een Runbook invoer-gegevensbron.

### <a name="invoke-runbook-activity"></a>Activiteit Runbook aanroepen
Runbooks in Orchestrator andere runbooks starten Hello **Runbook aanroepen** activiteit. Als u Hallo runbook wordt geconverteerd deze activiteit en Hallo bevat **wachten op voltooiing** optie is ingesteld, wordt een runbook-activiteit in Hallo geconverteerd runbook is gemaakt.  Als hello **wachten op voltooiing** optie niet is ingesteld, wordt een werkstroom scriptactiviteit gemaakt die gebruikmaakt van **Start AzureAutomationRunbook** toostart hello runbook.  Nadat u Hallo geconverteerd runbook in Azure Automation importeert, moet u deze activiteit met Hallo informatie is opgegeven bij activiteit Hallo wijzigen.

## <a name="related-articles"></a>Verwante artikelen:
* [System Center 2012 - Orchestrator](http://technet.microsoft.com/library/hh237242.aspx)
* [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx)
* [Hybride Runbook Worker](automation-hybrid-runbook-worker.md)
* [Standaard orchestrator-activiteiten](http://technet.microsoft.com/library/hh403832.aspx)
* [Download System Center Orchestrator Migration Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=47323)
