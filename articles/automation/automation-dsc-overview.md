---
title: Overzicht van Automation DSC aaaAzure | Microsoft Docs
description: Een overzicht van Azure Automation Desired State Configuration (DSC), de termen en bekende problemen
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: PowerShell dsc, de configuratie van de gewenste status, de powershell dsc-azure
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a>Overzicht van Azure Automation DSC

Azure Automation DSC is een Azure-service waarmee u toowrite, beheren en PowerShell Desired State Configuration (DSC) worden gecompileerd [configuraties](https://msdn.microsoft.com/powershell/dsc/configurations), importeren [DSC-Resources](https://msdn.microsoft.com/powershell/dsc/resources), en toewijzen configuraties tootarget knooppunten, die allemaal in Hallo cloud.

## <a name="why-use-azure-automation-dsc"></a>Waarom Azure Automation DSC gebruiken

Azure Automation DSC biedt verschillende voordelen ten opzichte van DSC buiten Azure.

### <a name="built-in-pull-server"></a>Ingebouwde pull-server

Azure Automation biedt een [DSC-pull-server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) zodat doelknooppunten automatisch configuraties ontvangen, conform toohello gewenst staat, en rapporteren over hun compliance.
Hallo ingebouwde pull-server in Azure Automation Hallo nodig tooset up elimineert en onderhouden van uw eigen pull-server.
Azure Automation kunt richten virtuele of fysieke Windows of Linux machines, in Hallo cloud of on-premises.

### <a name="management-of-all-your-dsc-artifacts"></a>Beheer van alle DSC-artefacten

Azure Automation DSC biedt dezelfde beheerlaag te Hallo[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) zoals Azure Automation voor het PowerShell-scripts biedt.

Hello Azure-portal, of PowerShell, kunt u alle uw DSC-configuraties, bronnen en doelknooppunten kunt beheren.

![Schermopname van hello Azure Automation-blade](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a>Reporting gegevens importeren in Log Analytics

Gedetailleerde status gegevens toohello ingebouwde pull rapportserver wordt verzonden door de knooppunten die worden beheerd met Azure Automation DSC.
Deze gegevens tooyour Microsoft Operations Management Suite (OMS) Log Analytics-werkruimte kunt u Azure Automation DSC toosend configureren.
hoe toosend DSC status gegevens tooyour werkruimte voor logboekanalyse zien toolearn [doorsturen Azure Automation-DSC reporting gegevens tooOMS logboekanalyse](automation-dsc-diagnostics.md).

## <a name="introduction-video"></a>Introductievideo

Voorkeur tooreading bekijken? Hebben bekijkt hello volgende video van mei 2015, wanneer Azure Automation DSC voor het eerst is aangekondigd.

>[!NOTE]
>Tijdens het Hallo-concepten en levenscyclus in deze video worden besproken correct zijn, is Azure Automation DSC veel gevorderd sinds deze video is opgenomen.
>Het is nu algemeen beschikbaar, heeft een veel uitgebreidere gebruikersinterface in hello Azure-portal en biedt ondersteuning voor veel meer mogelijkheden.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a>Volgende stappen

* toolearn hoe tooonboard knooppunten toobe beheerd met Azure Automation DSC raadpleegt [machines voorbereiden voor beheer door Azure Automation DSC](automation-dsc-onboarding.md)
* Zie tooget gestart met behulp van Azure Automation DSC [aan de slag met Azure Automation DSC](automation-dsc-getting-started.md)
* toolearn over het compileren van DSC-configuraties, zodat u deze, kunt u knooppunten tootarget toewijzen kunt, Zie [compileren van configuraties in Azure Automation DSC](automation-dsc-compile.md)
* Zie voor referentiemateriaal voor PowerShell-cmdlet voor Azure Automation DSC, [Azure Automation DSC-cmdlets](/powershell/module/azurerm.automation/#automation)
* Zie voor informatie over prijzen, [prijzen van Azure Automation DSC](https://azure.microsoft.com/pricing/details/automation/)
* Zie voor een voorbeeld van het gebruik van Azure Automation DSC in een pijplijn continue implementatie toosee [continue implementatie tooIaaS virtuele machines met behulp van Azure Automation DSC en Chocolatey](automation-dsc-cd-chocolatey.md)
