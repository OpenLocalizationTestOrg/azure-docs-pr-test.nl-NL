---
title: een runbook in Azure Automation aaaTesting | Microsoft Docs
description: Voordat u een runbook in Azure Automation publiceren, u kunt het testen tooensure die werkt zoals verwacht.  Dit artikel wordt beschreven hoe een runbook tootest en bekijk de uitvoer ervan weergegeven.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 7f7db785-52c0-4613-aa12-b02fd32a5182
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 8c531f702699d586f8215d4c171cb0ecf94732b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="testing-a-runbook-in-azure-automation"></a>Testen van een runbook in Azure Automation
Wanneer u een runbook test, Hallo [conceptversie](automation-creating-importing-runbook.md#publishing-a-runbook) wordt uitgevoerd en acties die worden uitgevoerd, zijn voltooid. Er wordt geen Taakgeschiedenis gemaakt, maar Hallo [uitvoer](automation-runbook-output-and-messages.md#output-stream) en [waarschuwingen en fouten](automation-runbook-output-and-messages.md#message-streams) stromen worden weergegeven in Hallo Test deelvenster Uitvoer. Berichten toohello [uitgebreide stroom](automation-runbook-output-and-messages.md#message-streams) alleen worden weergegeven in het deelvenster Uitvoer Hallo als hello [variabele $VerbosePreference](automation-runbook-output-and-messages.md#preference-variables) tooContinue is ingesteld.

Hoewel de conceptversie hello wordt uitgevoerd, wordt Hallo runbook nog steeds Hallo werkstroom normaal uitgevoerd en worden eventuele acties op basis van bronnen in de omgeving Hallo uitgevoerd. Daarom kunt testen u runbooks alleen op niet-productiebronnen.

Hallo procedure tootest [type runbook](automation-runbook-types.md) is dezelfde Hallo en er is geen verschil in de testfase tussen Hallo teksteditor en de grafische editor Hallo in hello Azure-portal.  

## <a name="tootest-a-runbook-in-hello-azure-portal"></a>tootest een runbook in hello Azure-portal
U kunt werken met een [runbooktype](automation-runbook-types.md) in hello Azure-portal.

1. Open Hallo conceptversie van Hallo runbook in beide Hallo [teksteditor](automation-edit-textual-runbook.md) of [grafische editor](automation-graphical-authoring-intro.md).
2. Klik op Hallo **Test** blade knop tooopen Hallo-Test.
3. Als Hallo runbook parameters heeft, kunt u ze wordt weergegeven in het linkerdeelvenster Hallo waarin u de waarden toobe gebruikt voor de test Hallo kunt opgeven.
4. Als u wilt dat toorun Hallo testen op een [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md), wijzigt u vervolgens **instellingen uitvoeren** te**Hybrid Worker** en selecteer Hallo-naam van de doelgroep Hallo.  Anders blijven Hallo standaard **Azure** toorun Hallo testen in de cloud Hallo.
5. Klik op Hallo **Start** knop toostart Hallo test.
6. Als Hallo runbook is [PowerShell Workflow](automation-runbook-types.md#powershell-workflow-runbooks) of [grafisch](automation-runbook-types.md#graphical-runbooks), en vervolgens kunt u stoppen of deze onderbreken terwijl deze wordt getest met Hallo knoppen onder Hallo deelvenster Uitvoer. Wanneer u Hallo runbook onderbreekt, is de huidige activiteit Hallo voltooid voordat het wordt onderbroken. Als Hallo runbook is onderbroken, kunt u stoppen of het programma opnieuw.
7. Hallo-uitvoer van runbook in het deelvenster voor testuitvoer Hallo Hallo inspecteren.

## <a name="next-steps"></a>Volgende stappen
* hoe toocreate of importeren van een runbook zien toolearn [maken of importeren van een runbook in Azure Automation](automation-creating-importing-runbook.md)
* Zie toolearn meer informatie over grafisch ontwerpen [grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md)
* tooget gestart met PowerShell workflow-runbooks, Zie [Mijn eerste PowerShell workflow-runbook](automation-first-runbook-textual.md)
* Zie toolearn meer informatie over het configureren van runboks tooreturn statusberichten en fouten, met inbegrip van aanbevolen procedures [Runbook uitvoer en berichten in Azure Automation](automation-runbook-output-and-messages.md)

