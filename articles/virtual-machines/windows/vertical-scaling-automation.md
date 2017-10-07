---
title: Azure Automation-toovertically aaaUse schalen Windows virtuele machines | Microsoft Docs
description: Een virtuele Windows-Machine verticaal te schalen in antwoord toomonitoring waarschuwingen met Azure Automation
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f964713-fb67-4bcc-8246-3431452ddf7d
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: kasing
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 24d07f3e2e217668f18676e6d6873be4f9770349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a>Windows-VM's met Azure Automation verticaal te schalen

Verticale schaling is Hallo proces oplopende of aflopende volgorde Hallo resources van een machine in het antwoord toohello werkbelasting. In Azure kunt dit doen door de tekengrootte Hallo Hallo virtuele Machine te wijzigen. Dit kan helpen in de volgende scenario's Hallo

* Als de virtuele Machine Hallo niet vaak wordt gebruikt, kunt u het formaat omlaag tooa kleinere grootte tooreduce uw maandelijkse kosten
* Als Hallo virtuele Machine een piekbelasting ziet is, kan het formaat is gewijzigd tooa groter formaat tooincrease worden de capaciteit

Hallo-overzicht voor Hallo stappen tooaccomplish dit omdat is hieronder

1. Uw virtuele Machines van Azure Automation tooaccess instellen
2. Hallo verticale schaal van Azure Automation-runbooks importeert in uw abonnement
3. Een webhook tooyour runbook toevoegen
4. Een waarschuwing tooyour virtuele Machine toevoegen

> [!NOTE]
> Vanwege de grootte van Hallo Hallo eerste virtuele Machine, Hallo grootten deze kan worden geschaald, mogelijk beperkt vanwege toohello beschikbaarheid van Hallo andere grootten in Hallo cluster huidige virtuele Machine wordt geïmplementeerd in. In Hallo gepubliceerd automation-runbooks gebruikt in dit artikel we zorgt voor deze aanvraag en slechts worden opgeschaald binnen Hallo hieronder paren van VM-grootte. Dit betekent dat een Standard_D1v2 virtuele Machine wordt niet plotseling tooStandard_G5 vergroot of verkleind tooBasic_A0.
> 
> | VM-grootten paar schalen |  |
> | --- | --- |
> | Basic_A0 |Basic_A4 |
> | Standard_A0 |Standard_A4 |
> | Standard_A5 |Standard_A7 |
> | Standard_A8 |Standard_A9 |
> | Standard_A10 |Standard_A11 |
> | Standard_D1 |Standard_D4 |
> | Standard_D11 |Standard_D14 |
> | Standard_DS1 |Standard_DS4 |
> | Standard_DS11 |Standard_DS14 |
> | Standard_D1v2 |Standard_D5v2 |
> | Standard_D11v2 |Standard_D14v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a>Uw virtuele Machines van Azure Automation tooaccess instellen
u moet toodo Hallo-eerst is een Azure Automation-account dat Hallo runbooks gebruikt tooscale fungeert als host voor een virtuele Machine maken. Hallo Automation-service is onlangs geïntroduceerd Hallo 'Uitvoeren als-account' functie waardoor Hallo Service-Principal instellen voor het automatisch uitvoeren van runbooks Hallo van Hallo gebruiker namens heel eenvoudig. U kunt meer lezen over deze in de onderstaande Hallo-artikel:

* [Runbooks verifiëren met een Azure Uitvoeren als-account](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Hallo verticale schaal van Azure Automation-runbooks importeert in uw abonnement
Hallo runbooks die nodig zijn voor het verticaal schalen van uw virtuele Machine al in de galerie van Azure Automation-Runbook Hallo zijn gepubliceerd. U moet tooimport bij uw abonnement. U leert hoe tooimport runbooks door te lezen Hallo volgende artikel.

* [Runbook- en galerieën voor Azure Automation](../../automation/automation-runbook-gallery.md)

Hallo-runbooks die toobe geïmporteerd moeten worden weergegeven in onderstaande afbeelding voor Hallo

![Importeren van runbooks](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a>Een webhook tooyour runbook toevoegen
Zodra u Hallo runbooks hebt geïmporteerd moet u een webhook toohello runbook tooadd zodat deze kan worden geactiveerd door een waarschuwing van een virtuele Machine. Hallo-details van het maken van een webhook voor uw Runbook kunnen hier worden gelezen

* [Azure Automation-webhooks.](../../automation/automation-webhooks.md)

Zorg ervoor dat u Hallo webhook kopiëren voordat het Hallo-webhook dialoogvenster te sluiten als u dit in de volgende sectie Hallo moet.

## <a name="add-an-alert-tooyour-virtual-machine"></a>Een waarschuwing tooyour virtuele Machine toevoegen
1. Instellingen voor virtuele Machine selecteren
2. Selecteer 'Waarschuwingsregels'
3. Selecteer 'Waarschuwing toevoegen'
4. Selecteer een waarschuwing voor het Hallo van metrische toofire op
5. Selecteer een voorwaarde die tijdens wordt voldaan Hallo waarschuwing toofire veroorzaken
6. Selecteer een drempelwaarde voor Hallo voorwaarde in stap 5. toobe voldaan
7. Selecteer een periode gedurende welke Hallo monitoring-service wordt gecontroleerd voor Hallo voorwaarde en de drempelwaarde in stap 5 en 6
8. In het Hallo-webhook die u hebt gekopieerd uit de vorige sectie hello te plakken.

![Waarschuwing tooVirtual Machine 1 toevoegen](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Waarschuwing tooVirtual Machine 2 toevoegen](./media/vertical-scaling-automation/add-alert-webhook-2.png)

