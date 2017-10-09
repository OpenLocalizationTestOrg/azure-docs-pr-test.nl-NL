---
title: Automation-Runbooktypen aaaAzure | Microsoft Docs
description: 'Beschrijft de verschillende soorten runbooks die u in Azure Automation en overwegingen die u in aanmerking nemen gebruiken kunt moet bij het bepalen van welke type toouse Hallo. '
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9265c975-4281-4819-a84f-d86641277f36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/01/2017
ms.author: bwren
ms.openlocfilehash: c28aa57c77025764b16784372308a4ff2f596914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-runbook-types"></a>Azure Automation-runbooktypen
Azure Automation biedt ondersteuning voor vier typen runbooks die worden kort beschreven in de volgende tabel Hallo.  Hallo secties hieronder vindt u meer informatie over elk type inclusief overwegingen op wanneer toouse elke.

| Type | Beschrijving |
|:--- |:--- |
| [Grafisch](#graphical-runbooks) |Op basis van Windows PowerShell en gemaakt en bewerkt geheel vanuit de grafische editor in Azure-portal. |
| [Grafische PowerShell Workflow](#graphical-runbooks) |Op basis van Windows PowerShell-werkstroom en gemaakt en bewerkt volledig in Hallo grafische editor in Azure-portal. |
| [PowerShell](#powershell-runbooks) |Tekstrunbook op basis van Windows PowerShell-script. |
| [PowerShell-werkstroom](#powershell-workflow-runbooks) |Tekstrunbook op basis van Windows PowerShell-werkstroom. |

## <a name="graphical-runbooks"></a>Grafische runbooks
[Grafische](automation-runbook-types.md#graphical-runbooks) en grafische PowerShell Workflow-runbooks zijn gemaakt en bewerkt met de grafische editor Hallo in hello Azure-portal.  U kunt ze tooa-bestand exporteren en vervolgens importeren in een andere automation-account, maar u kunt maken of bewerken met een ander hulpprogramma.  Grafische runbooks PowerShell-code genereren, maar u rechtstreeks kunt weergeven of wijzigen Hallo code. Grafische runbooks kan niet worden geconverteerd tooone Hallo [tekstindelingen](automation-runbook-types.md), noch een tekstrunbook kan worden geconverteerd toographical indeling. Grafische runbooks kunnen geconverteerde tooGraphical PowerShell Workflow-runbooks zijn tijdens het importeren en vice versa.

### <a name="advantages"></a>Voordelen
* Visual authoring model insert-koppeling configureren  
* Richt u op hoe de gegevens door Hallo-proces loopt  
* Visueel vertegenwoordigen processen voor Apparaatbeheer  
* Andere runbooks bevatten als onderliggende runbooks toocreate hoog niveau werkstromen  
* Modulaire programmering worden gebruikers aangemoedigd  


### <a name="limitations"></a>Beperkingen
* Kan runbook buiten Azure-portal niet bewerken.
* Kan een Code-activiteit met PowerShell code tooperform complexe logica in beslag.
* Kan niet weergeven of Hallo PowerShell-code die is gemaakt door Hallo grafische werkstroom rechtstreeks te bewerken. Houd er rekening mee dat u Hallo-code die u in Code activiteiten maakt kunt weergeven.

## <a name="powershell-runbooks"></a>PowerShell-runbooks
PowerShell-runbooks zijn gebaseerd op Windows PowerShell.  U Hallo-code van Hallo runbook met Hallo-teksteditor in hello Azure-portal voor het rechtstreeks bewerken.  U kunt ook een willekeurige offline teksteditor gebruiken en [hello runbook importeren](http://msdn.microsoft.com/library/azure/dn643637.aspx) in Azure Automation.

### <a name="advantages"></a>Voordelen
* Alle complexe logica met PowerShell-code zonder extra complexiteit Hallo van PowerShell Workflow geïmplementeerd. 
* Start Runbook sneller dan PowerShell Workflow-runbooks omdat toobe gecompileerd voordat u hoeft niet.

### <a name="limitations"></a>Beperkingen
* Moet bekend zijn met het PowerShell-scripts.
* Kan niet worden gebruikt [parallelle verwerking](automation-powershell-workflow.md#parallel-processing) tooperform meerdere acties parallel.
* Kan niet worden gebruikt [controlepunten](automation-powershell-workflow.md#checkpoints) tooresume runbook in geval van een fout.
* PowerShell Workflow-runbooks en grafische runbooks kunnen alleen worden opgenomen als onderliggende runbooks met behulp van Hallo Start AzureAutomationRunbook cmdlet waarmee u een nieuwe taak maakt.

### <a name="known-issues"></a>Bekende problemen
Hieronder vindt u huidige bekende problemen met de PowerShell-runbooks.

* PowerShell-runbooks kunnen niet kan niet ophalen van een niet-versleutelde [variabelenactivum](automation-variables.md) met een null-waarde.
* Kan de PowerShell-runbooks niet ophalen een [variabelenactivum](automation-variables.md) met  *~*  in Hallo-naam.
* Get-Process in een lus in een PowerShell runbook vastlopen na ongeveer 80 iteraties. 
* Een PowerShell-runbook kan mislukken als er wordt een zeer grote hoeveelheid gegevens toohello uitvoerstroom toowrite in één keer geprobeerd.   U kunt gewoonlijk dit probleem omzeilen door het uitvoeren van NET Hallo informatie die u nodig hebt bij het werken met grote objecten.  Bijvoorbeeld, in plaats van het uitvoeren van ongeveer *Get-Process*, kunt u alleen Hallo vereist velden met uitvoeren *Get-Process | Selecteer de procesnaam, CPU*.

## <a name="powershell-workflow-runbooks"></a>PowerShell Workflow-runbooks
PowerShell Workflow-runbooks zijn tekst runbooks op basis van [Windows PowerShell-werkstroom](automation-powershell-workflow.md).  U Hallo-code van Hallo runbook met Hallo-teksteditor in hello Azure-portal voor het rechtstreeks bewerken.  U kunt ook een willekeurige offline teksteditor gebruiken en [hello runbook importeren](http://msdn.microsoft.com/library/azure/dn643637.aspx) in Azure Automation.

### <a name="advantages"></a>Voordelen
* Alle complexe logica met PowerShell Workflow-code implementeren.
* Gebruik [controlepunten](automation-powershell-workflow.md#checkpoints) tooresume runbook in geval van een fout.
* Gebruik [parallelle verwerking](automation-powershell-workflow.md#parallel-processing) tooperform meerdere acties parallel.
* Kan andere grafische runbooks en PowerShell Workflow-runbooks als onderliggende runbooks toocreate hoog niveau werkstromen bevatten.

### <a name="limitations"></a>Beperkingen
* Auteur moet bekend zijn met PowerShell Workflow.
* Runbook moet omgaan met extra complexiteit Hallo van PowerShell Workflow, zoals [gedeserialiseerd objecten](automation-powershell-workflow.md#code-changes).
* Runbook duurt langer toostart dan PowerShell-runbooks omdat het moet toobe gecompileerd voordat u.
* PowerShell-runbooks kunnen alleen worden opgenomen als onderliggende runbooks met behulp van Hallo Start AzureAutomationRunbook cmdlet waarmee u een nieuwe taak maakt.

## <a name="considerations"></a>Overwegingen
U moet rekening worden account Hallo aanvullende overwegingen bij het bepalen van welke type toouse voor een bepaald runbook te volgen.

* U kunt runbooks niet converteren van grafische tootextual type of vice versa.
* Er gelden beperkingen met behulp van runbooks met verschillende typen als een onderliggend runbook.  Zie [onderliggende runbooks in Azure Automation](automation-child-runbooks.md) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
* toolearn meer informatie over het ontwerpen van een grafische runbook, Zie [grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md)
* Hallo toounderstand verschillen tussen PowerShell en PowerShell-werkstromen voor runbooks, Zie [Learning Windows PowerShell Workflow](automation-powershell-workflow.md)
* Voor meer informatie over hoe toocreate of importeren van een Runbook zien [een Runbook maken of importeren](automation-creating-importing-runbook.md)

