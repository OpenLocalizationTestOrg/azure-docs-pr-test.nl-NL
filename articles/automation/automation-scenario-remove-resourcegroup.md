---
title: aaaAutomate verwijderen van de resourcegroepen | Microsoft Docs
description: PowerShell Workflow-versie van een Azure Automation-scenario met inbegrip van runbooks tooremove alle resourcegroepen in uw abonnement.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: 
ms.assetid: b848e345-fd5d-4b9d-bc57-3fe41d2ddb5c
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: magoedte
ms.openlocfilehash: d7ff8064842385d57b0eebdf7b263150c958255f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automate-removal-of-resource-groups"></a>Azure Automation-scenario: de verwijdering van resourcegroepen automatiseren
Veel klanten maken meer dan één resourcegroep. Sommige worden dan bijvoorbeeld gebruikt voor het beheer van productietoepassingen en andere als ontwikkelings-, test- en faseringsomgeving. Hallo-implementatie van deze bronnen te automatiseren is één ding, maar kunnen toodecommission een resourcegroep met een klik op de knop Hallo is een andere. U kunt deze algemene beheertaak stroomlijnen met behulp van Azure Automation. Dit is handig als u werkt met een Azure-abonnement een bestedingslimiet via een ledenaanbieding zoals MSDN of Hallo Microsoft Partner Network Cloud Essentials-programma heeft.

Dit scenario is gebaseerd op een PowerShell-runbook en is ontworpen tooremove een of meer resourcegroepen die u uit uw abonnement opgeeft. de standaardinstelling Hallo van Hallo runbook is tootest voordat u doorgaat. Dit zorgt ervoor dat u niet per ongeluk Hallo resourcegroep verwijdert voordat u klaar toocomplete bent deze procedure.   

## <a name="getting-hello-scenario"></a>Hallo scenario ophalen
Dit scenario bestaat uit een PowerShell-runbook die u van Hallo downloaden kunt [PowerShell Gallery](https://www.powershellgallery.com/packages/Remove-ResourceGroup/1.0/DisplayScript). U kunt het ook importeren rechtstreeks vanuit Hallo [Runbookgalerie](automation-runbook-gallery.md) in hello Azure-portal.<br><br>

| Runbook | Beschrijving |
| --- | --- |
| Remove-ResourceGroup |Hiermee verwijdert u een of meer Azure-resourcegroepen en de bijbehorende bronnen uit het Hallo-abonnement. |

<br>
Hallo na invoerparameters zijn gedefinieerd voor dit runbook:

| Parameter | Beschrijving |
| --- | --- |
| NameFilter (vereist) |Hiermee geeft u een naam filter toolimit Hallo resourcegroepen die u van plan bent over het verwijderen. U kunt meerdere waarden doorgeven met behulp van een met komma's gescheiden lijst.<br>Hallo-filter is niet hoofdlettergevoelig en komt overeen met een resourcegroep met Hallo-tekenreeks. |
| PreviewMode (optioneel) |Hallo runbook toosee welke resourcegroepen worden verwijderd, maar wordt geen actie uitgevoerd worden uitgevoerd.<br>Hallo standaardwaarde is **true** toohelp voorkomen per ongeluk verwijderen van een of meer resourcegroepen toohello runbook doorgegeven. |

## <a name="install-and-configure-this-scenario"></a>Dit scenario installeren en configureren
### <a name="prerequisites"></a>Vereisten
Dit runbook wordt geverifieerd met Hallo [Azure uitvoeren als-account](automation-sec-configure-azure-runas-account.md).    

### <a name="install-and-publish-hello-runbooks"></a>Installeren en Hallo runbooks publiceren
Nadat u Hallo runbook hebt gedownload, kunt u deze importeren met behulp van de procedure Hallo in [runbook procedures importeren](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation). Hallo runbook gepubliceerd nadat deze is geïmporteerd in uw Automation-account.

## <a name="using-hello-runbook"></a>Met behulp van Hallo runbook
Hallo begeleidt volgt u stapsgewijs door Hallo uitvoering van dit runbook en de helpen die u meer vertrouwd raken met hoe het werkt. U gaat alleen testen Hallo runbook in dit voorbeeld Hallo resourcegroep niet werkelijk te verwijderen.  

1. Open uw Automation-account uit hello Azure-portal, en klik op **Runbooks**.
2. Selecteer Hallo **verwijderen ResourceGroup** runbook en klik op **Start**.
3. Wanneer u Hallo runbook start, Hallo **Runbook starten** blade wordt geopend en u kunt de parameters Hallo configureren. Voer Hallo namen van resourcegroepen in uw abonnement dat u voor het testen gebruiken kunt en geen kwaad veroorzaakt als per ongeluk worden verwijderd.<br> ![Remove-ResouceGroup-parameters](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-input-parameters.png)

   > [!NOTE]
   > Zorg ervoor dat **Previewmode** te is ingesteld,**true** tooavoid verwijderen Hallo resourcegroepen geselecteerd.  **Opmerking** dit runbook wordt niet verwijderd Hallo resourcegroep die Hallo Automation-account met dit runbook bevat.  
   >
   >
4. Nadat u alle Hallo parameterwaarden hebt geconfigureerd, klikt u op **OK**, en Hallo runbook zal worden in de wachtrij voor uitvoering.  

tooview hello details van Hallo **verwijderen ResourceGroup** runbooktaak in Azure portal, selecteer Hallo **taken** in Hallo runbook. Hallo taak overzicht Hallo invoerparameters en Hallo uitvoer stream bovendien toogeneral informatie over het Hallo-taak en eventuele uitzonderingen die zijn opgetreden.<br> ![Taakstatus van het runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-status.png).

Hallo **taakoverzicht** berichten van de uitvoer, waarschuwingen en fouten streams Hallo bevat. Selecteer **uitvoer** tooview gedetailleerde resultaten van Hallo runbook-uitvoering.<br> ![Uitvoerresultaten van het runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-output.png)

## <a name="next-steps"></a>Volgende stappen
* beginnen met het opstellen van uw eigen runbook tooget Zie [maken of importeren van een runbook in Azure Automation](automation-creating-importing-runbook.md).
* Zie tooget gestart met PowerShell Workflow-runbooks [Mijn eerste PowerShell Workflow-runbook](automation-first-runbook-textual.md).
