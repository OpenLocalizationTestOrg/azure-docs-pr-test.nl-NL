---
title: aaaWhat is een Azure Automation | Microsoft Docs
description: Informatie over welke waarde Azure Automation biedt en antwoorden toocommon vragen zodat u kunt aan de slag maakt, met behulp van runbooks en Azure Automation DSC.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: wat is automation, azure automation en voorbeelden van azure automation
ms.assetid: 0cf1f3e8-dd30-4f33-b52a-e148e97802a9
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/10/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 1e5a90e272d6b2beb7b5007e2fea2c110dbd79b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-overview"></a>Overzicht van Azure Automation
Microsoft Azure Automation biedt een manier voor gebruikers tooautomate Hallo handmatige, langlopende, foutgevoelige en regelmatig herhaalde taken die vaak worden uitgevoerd in een cloud en enterprise-omgeving. Dit bespaart tijd en verhoogt de betrouwbaarheid van regelmatige beheertaken Hallo en deze worden zelfs gepland toobe automatisch uitgevoerd met regelmatige tussenpozen. U kunt processen automatiseren met behulp van runbooks of configuratiebeheer automatiseren met behulp van Desired State Configuration. In dit artikel wordt een kort overzicht gegeven van Azure Automation en worden enkele veelgestelde vragen beantwoord. U kunt tooother artikelen in deze bibliotheek voor meer gedetailleerde informatie over de verschillende onderwerpen Hallo verwijzen.

## <a name="automating-processes-with-runbooks"></a>Processen automatiseren met runbooks
Een runbook is een set taken waarmee een geautomatiseerd proces in Azure Automation wordt uitgevoerd. Kan het een eenvoudig proces, zoals een virtuele machine wordt gestart en het maken van een logboekvermelding zijn of moet u wellicht een complex runbook waarin andere kleinere runbooks tooperform een complex proces aan meerdere resources of zelfs meerdere clouds en on-premises omgevingen.  

Bijvoorbeeld, wellicht u een bestaand handmatig proces voor het afkappen van een SQL-database als deze de maximale grootte omvat meerdere stappen zoals verbinding toohello-server, verbinding maken met database toohello nadert, Hallo huidige grootte van de database ophalen, controleren als drempelwaarde heeft overschreden en vervolgens afkappen en gebruiker waarschuwen. In plaats van het handmatig uitvoeren van deze stappen, kunt u een runbook maken waarmee al deze taken als één proces worden uitgevoerd. U zou Hallo runbook starten, Geef informatie op Hallo vereist zoals Hallo SQL-servernaam, databasenaam en e-mail van de ontvanger en u hoeft verder niets doen terwijl het Hallo-proces is voltooid. 

## <a name="what-can-runbooks-automate"></a>Wat kan met runbooks worden geautomatiseerd?
Runbooks in Azure Automation zijn gebaseerd op Windows PowerShell of Windows PowerShell Workflow, zodat ze alles kunnen dat PowerShell kan. Als een toepassing of service een API heeft, kan een runbook hiermee werken. Als u een PowerShell-module voor de toepassing hello hebt, kunt u die module in Azure Automation laden en die cmdlets opnemen in uw runbook. Azure Automation-runbooks uitgevoerd in hello Azure-cloud en hebben toegang tot alle cloud-resources of externe bronnen die toegankelijk zijn vanuit Hallo cloud. Met behulp van [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md), runbooks kunnen worden uitgevoerd in uw lokale gegevens center toomanage lokale bronnen. 

## <a name="getting-runbooks-from-hello-community"></a>Runbooks ophalen uit het Hallo-community
Hallo [Runbookgalerie](automation-runbook-gallery.md#runbooks-in-runbook-gallery) bevat runbooks van Microsoft en Hallo-community u ofwel ongewijzigd in uw omgeving kunt of pas ze aan voor uw eigen doeleinden. Ze zijn ook nuttig tooas verwijzingen toolearn hoe toocreate uw eigen runbooks. U kunt zelfs uw eigen runbooks toohello galerie waarvan u denkt dat andere gebruikers nuttig kunnen bijdragen. 

## <a name="creating-runbooks-with-azure-automation"></a>Runbooks maken met Azure Automation
U kunt [maken van uw eigen runbooks](automation-creating-importing-runbook.md) van scratchruimte of wijzigen van runbooks uit Hallo [Runbookgalerie](http://msdn.microsoft.com/library/azure/dn781422.aspx) voor uw eigen vereisten. Er zijn vier verschillende [runbooktypen](automation-runbook-types.md) waaruit u kunt kiezen op basis van uw vereisten en PowerShell-ervaring. Als u liever toowork rechtstreeks met de Hallo PowerShell-code, dan kunt u een [PowerShell-runbook](automation-runbook-types.md#powershell-runbooks) of [PowerShell Workflow-runbook](automation-runbook-types.md#powershell-workflow-runbooks) dat u offline of Hello bewerkt [teksteditor](http://msdn.microsoft.com/library/azure/dn879137.aspx) in hello Azure-portal. Als u liever tooedit een runbook zonder toohello onderliggende code weergegeven en kunt u een [grafisch runbook](automation-runbook-types.md#graphical-runbooks) met Hallo [grafische editor](automation-graphical-authoring-intro.md) in hello Azure-portal. 

Voorkeur tooreading bekijken? Bekijkt hello onderstaande video van de Microsoft Ignite-sessie in mei 2015 hebben. Opmerking: Tijdens het Hallo concepten en functies in deze video worden besproken correct zijn, dat Azure Automation is veel gevorderd sinds deze video is opgenomen, het heeft nu een uitgebreidere gebruikersinterface in hello Azure-portal en de aanvullende mogelijkheden ondersteunt.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3451/player]
> 
> 

## <a name="automating-configuration-management-with-desired-state-configuration"></a>Configuratiebeheer automatiseren met Desired State Configuration
[PowerShell DSC](https://technet.microsoft.com/library/dn249912.aspx) is een beheerplatform waarmee u toomanage, implementeren en afdwingen van configuratie voor fysieke hosts en virtuele machines met een declaratieve PowerShell-syntaxis. U kunt configuraties definiëren op een centrale DSC-pull-server die met doelmachines automatisch kunnen worden opgehaald en toegepast. DSC biedt een set van PowerShell-cmdlets waarmee u toomanage configuraties en resources kunt.  

[Azure Automation DSC](automation-dsc-overview.md) is een cloudoplossing voor PowerShell DSC waarmee services worden geboden die zijn vereist voor bedrijfsomgevingen.  U kunt uw DSC-resources in Azure Automation beheren en configuraties toovirtual of fysieke machines waarmee deze worden opgehaald uit een DSC-Pull-Server in Azure-cloud Hallo toepassen.  Het biedt ook rapportageservices waarmee u wordt geïnformeerd over belangrijke gebeurtenissen zoals wanneer knooppunten zijn afgeweken van de toegewezen configuratie en wanneer een nieuwe configuratie is toegepast. 

## <a name="creating-your-own-dsc-configurations-with-azure-automation"></a>Uw eigen DSC-configuraties maken met Azure Automation
[DSC-configuraties](automation-dsc-overview.md) Hallo gewenste status van een knooppunt opgeven.  Meerdere knooppunten kunnen toepassen Hallo dezelfde configuratie tooassure dat ze allemaal dezelfde status houden.  U kunt een configuratie maken met een teksteditor op uw lokale machine en deze vervolgens importeren in Azure Automation, waar u deze kunt compileren en op knooppunten kunt toepassen.

## <a name="getting-modules-and-configurations"></a>Modules en configuraties ophalen
U kunt krijgen [PowerShell-modules](automation-runbook-gallery.md#modules-in-powershell-gallery) die cmdlets bevatten die u in uw runbooks en DSC-configuraties uit Hallo gebruiken kunt [PowerShell Gallery](http://www.powershellgallery.com/). U kunt deze galerie starten vanuit hello Azure-portal en modules rechtstreeks in Azure Automation importeren, of u kunt downloaden en deze handmatig importeren. U geen Hallo-modules installeren rechtstreeks vanuit hello Azure-portal, maar kunt u deze downloaden ze net als elke andere module te installeren. 

## <a name="example-practical-applications-of-azure-automation"></a>Voorbeeld van praktische toepassingen van Azure Automation
Hier volgen enkele voorbeelden van wat Hallo soorten automatiseringsscenario's met Azure Automation zijn. 

* Virtuele machines in verschillende Azure-abonnementen maken en kopiëren. 
* Bestandskopieën van een lokale computer tooan Azure Blob Storage-container plannen. 
* Beveiligingsfuncties automatiseren zoals aanvragen van een client weigeren wanneer een Denial of Service-aanval wordt gedetecteerd. 
* Ervoor zorgen dat machines voortdurend zijn aangepast aan geconfigureerd beveiligingsbeleid.
* Continue implementatie van toepassingscode beheren in cloud- en on-premises infrastructuur. 
* Een Active Directory-forest in Azure bouwen voor uw testomgeving. 
* Een tabel in een SQL-database afkappen als de database bijna de maximale grootte heeft bereikt. 
* Omgevingsinstellingen voor een Azure-website extern bijwerken. 

## <a name="how-does-azure-automation-relate-tooother-automation-tools"></a>Hoe Azure Automation tooother automatiseringsprogramma's in verhouding?
[Service Management Automation (SMA)](http://technet.microsoft.com/library/dn469260.aspx) beoogde tooautomate beheertaken in de privécloud Hallo is. Het wordt lokaal in uw datacentrum geïnstalleerd als een onderdeel van het [Microsoft Azure-pakket](https://www.microsoft.com/en-us/server-cloud/). SMA en Azure Automation hello gebruiken dezelfde runbookindeling op basis van Windows PowerShell en Windows PowerShell Workflow, maar biedt geen ondersteuning voor SMA [grafische runbooks](automation-graphical-authoring-intro.md).  

[System Center 2012 Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) is bedoeld voor automatisering van on-premises resources. Het maakt gebruik van een andere runbookindeling dan Azure Automation en Service Management Automation en heeft een grafische interface toocreate runbooks zonder dat er scripts nodig. De runbooks bestaan uit activiteiten uit integratiepakketten die specifiek voor Orchestrator zijn geschreven. 

## <a name="where-can-i-get-more-information"></a>Waar vind ik meer informatie?
Een aantal bronnen beschikbaar zijn voor u toolearn meer over Azure Automation en het maken van uw eigen runbooks. 

* U bevindt zich nu in de **Azure Automation-bibliotheek**. Hallo artikelen in deze bibliotheek bieden volledige documentatie over Hallo-configuratie en het beheer van Azure Automation en over het ontwerpen van uw eigen runbooks. 
* [Azure PowerShell-cmdlets](http://msdn.microsoft.com/library/jj156055.aspx) bevat informatie voor het automatiseren van Azure-bewerkingen met behulp van Windows PowerShell. Deze cmdlets toowork Runbooks gebruiken met Azure-resources. 
* [Management Blog](https://azure.microsoft.com/blog/tag/azure-automation/) Hallo meest recente informatie bevat over Azure Automation en andere beheertechnologieën van Microsoft. Moet u zich abonneren toothis blog toostay up toodate Hello nieuwste van hello Azure Automation-team. 
* [Automation-Forum](http://go.microsoft.com/fwlink/p/?LinkId=390561) kunt u toopost vragen over Azure Automation toobe beantwoord door Microsoft en Hallo Automation-community. 
* [Azure Automation Cmdlets](https://msdn.microsoft.com/library/mt244122.aspx) biedt informatie over het automatiseren van beheertaken. Het bevat cmdlets toomanage Automation-accounts, -assets, runbooks en-DSC.

## <a name="can-i-provide-feedback"></a>Mag ik feedback geven?
**Ja, feedback is welkom.** Als u een Azure Automation-runbookoplossing of een integratiemodule zoekt, plaatst u een scriptaanvraag in Scriptcentrum. Als u feedback wilt geven of functieaanvragen hebt voor Azure Automation, plaatst u deze op [UserVoice](http://feedback.windowsazure.com/forums/34192--general-feedback). Bedankt! 

