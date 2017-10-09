---
title: "galerieën aaaRunbook en -module voor Azure Automation | Microsoft Docs"
description: Runbooks en modules van Microsoft en Hallo community beschikbaar zijn voor u tooinstall en gebruiken in uw Azure Automation-omgeving.  Dit artikel wordt beschreven hoe u toegang hebt tot deze bronnen en toocontribute uw runbooks toohello-galerie.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d3fee7b4-630a-4c10-8425-9bf51d7c9e58
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 10b634460edf66dd7548017e3a2f7111b7125f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a>Runbook- en galerieën voor Azure Automation
In plaats van uw eigen runbooks en modules in Azure Automation, kunt u toegang tot allerlei scenario's die al zijn gebouwd door Microsoft en Hallo-community.  U kunt deze scenario's zonder aanpassingen gebruiken of u kunt ze als uitgangspunt gebruiken en ze bewerken voor uw specifieke vereisten.

U kunt runbooks ophalen van Hallo [Runbookgalerie](#runbooks-in-runbook-gallery) en -modules uit Hallo [PowerShell Gallery](#modules-in-powerShell-gallery).  U kunt ook toohello community bijdragen aan scenario's die u ontwikkelt delen.

## <a name="runbooks-in-runbook-gallery"></a>Runbooks in Runbookgalerie
Hallo [Runbookgalerie](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) biedt tal van runbooks van Microsoft en Hallo community die u in Azure Automation importeren kunt. Kunt u een runbook downloaden uit Hallo galerie die wordt gehost in Hallo [TechNet Script Center](https://gallery.technet.microsoft.com/scriptcenter/site/upload), of u kunt runbooks rechtstreeks importeren vanuit galerie Hallo van Hallo klassieke Azure-portal of Azure-portal.

U kunt alleen met de importeren rechtstreeks vanuit de Runbookgalerie Hallo met Hallo klassieke Azure-portal of Azure-portal. U kunt deze functie met Windows PowerShell niet uitvoeren.

> [!NOTE]
> U moet valideren Hallo inhoud van alle runbooks die u niet uit Hallo Runbookgalerie ophalen en uiterst voorzichtig met het installeren en uit te voeren in een productieomgeving. |
> 
> 

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-classic-portal"></a>tooimport een runbook hello Runbookgalerie Hello klassieke Azure-portal
1. In hello Azure-Portal klikt, **nieuw**, **App Services**, **Automation**, **Runbook**, **uit galerie**.
2. Selecteer een categorie tooview gerelateerd runbooks en de details van een runbook tooview selecteren. Wanneer u Hallo runbook die u wilt selecteren, klikt u op de pijlknop-rechts Hallo.
   
    ![Runbook-galerie](media/automation-runbook-gallery/runbook-gallery.png)
3. Bekijkt hello inhoud van Hallo runbook en noteer eventuele vereisten in Hallo beschrijving. Klik op de pijlknop-rechts Hallo wanneer u klaar bent.
4. Voer details voor Hallo runbook en klik vervolgens op Hallo vinkje knop. Hallo runbook-naam wordt al ingevuld.
5. Hallo runbook wordt weergegeven op Hallo **Runbooks** tabblad voor Hallo Automation-Account.

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-portal"></a>tooimport een runbook hello Runbookgalerie Hello Azure-portal
1. Open uw Automation-account in Azure Portal hello.
2. Klik op Hallo **Runbooks** tegel tooopen Hallo lijst van runbooks.
3. Klik op **bladeren galerie** knop.
   
    ![Galerie knop Bladeren](media/automation-runbook-gallery/browse-gallery-button.png)
4. Hallo galerij-item dat u wilt en selecteert u het tooview Zoek de details ervan.
   
    ![Galerie bladeren](media/automation-runbook-gallery/browse-gallery.png)
5. Klik op **weergave bronproject** tooview Hallo item in Hallo [TechNet Script Center](http://gallery.technet.microsoft.com/).
6. tooimport een item, klikt u op tooview de details en klik vervolgens op Hallo **importeren** knop.
   
    ![Knop importeren](media/automation-runbook-gallery/gallery-item-detail.png)
7. Eventueel Hallo-naam van Hallo runbook wijzigen en klik vervolgens op **OK** tooimport hello runbook.
8. Hallo runbook wordt weergegeven op Hallo **Runbooks** tabblad voor Hallo Automation-Account.

### <a name="adding-a-runbook-toohello-runbook-gallery"></a>Toevoegen van een runbook toohello runbook-galerie
Microsoft raadt u tooadd runbooks toohello Runbookgalerie die u denkt dat nuttig tooother klanten.  U kunt een runbook door toevoegen [uploaden toohello Script Center](http://gallery.technet.microsoft.com/site/upload) waarbij rekening wordt gehouden account Hallo volgende details.

* U moet opgeven *Windows Azure* voor Hallo **categorie** en *Automation* voor Hallo **subcategorie** voor Hallo runbook toobe weergegeven in de wizard Hallo.  
* Hallo uploaden moet één .ps1 of .graphrunbook-bestand.  Als Hallo runbook modules, onderliggende runbooks of activa vereist, vervolgens u moet een lijst die in Hallo beschrijving van de verzending van hello en in Hallo gedeelte met opmerkingen over Hallo runbook.  Als u een scenario voor het vereisen van meerdere runbooks hebt, elk afzonderlijk uploaden en namen van Hallo Hallo gerelateerde runbooks in elk van de bijbehorende beschrijvingen. Zorg ervoor dat u dezelfde labels zodat ze worden weergegeven in Hallo Hallo met dezelfde categorie. Een gebruiker heeft tooread Hallo beschrijving tooknow of andere runbooks vereist Hallo scenario toowork zijn.
* Hallo-label "GraphicalPS" toevoegen als u wilt publiceren een **grafisch runbook** (geen grafische werkstroom). 
* Een PowerShell- of PowerShell Workflow codefragment invoegen in het Hallo-beschrijving gebruiken **code sectie invoegen** pictogram.
* Hallo wordt samenvatting voor het uploaden van Hallo weergegeven in Hallo die runbookgalerie resulteert dus moet u gedetailleerde informatie waarmee een gebruiker identificeren Hallo-functionaliteit van Hallo runbook opgeven.
* U moet één toothree Hallo na het uploaden van Tags toohello toewijzen.  Hallo runbook wordt weergegeven in de wizard Hallo onder Hallo categorieën die overeenkomen met de labels.  Alle tags niet op deze lijst worden genegeerd door de wizard Hallo. Als u overeenkomende labels niet opgeeft, Hallo runbook worden vermeld onder Hallo andere categorie.
  
  * Back-up
  * Capaciteitsbeheer
  * Wijzigingsbeheer
  * Naleving
  * Dev / testen omgevingen
  * Noodherstel
  * Bewaking
  * Patchen
  * Inrichten
  * Herstel
  * Levenscyclusbeheer van virtuele machine
* Automation bijgewerkt Hallo galerie eens per uur, zodat u uw bijdragen onmiddellijk niet zien.

## <a name="modules-in-powershell-gallery"></a>Modules in PowerShell Gallery
PowerShell-modules bevatten cmdlets die u in uw runbooks gebruiken kunt en bestaande modules die u in Azure Automation installeren kunt zijn beschikbaar in Hallo [PowerShell Gallery](http://www.powershellgallery.com).  U kunt deze galerie starten vanuit hello Azure-portal en deze rechtstreeks in Azure Automation installeren of u kunt deze downloaden en deze handmatig installeren.  U Hallo modules rechtstreeks vanuit de klassieke Azure-portal Hallo niet installeren, maar kunt u deze downloaden ze net als elke andere module te installeren.

### <a name="tooimport-a-module-from-hello-automation-module-gallery-with-hello-azure-portal"></a>tooimport een module van Hallo Automation Modulegalerie Hello Azure-portal
1. Open uw Automation-account in Azure Portal hello.
2. Klik op Hallo **activa** tegel tooopen Hallo lijst van activa.
3. Klik op Hallo **Modules** tegel tooopen Hallo lijst met modules.
4. Klik op Hallo **bladeren galerie** knop en Hallo bladeren galerie blade wordt gestart.
   
    ![Modulegalerie](media/automation-runbook-gallery/modules-blade.png) <br>
5. Wanneer u Hallo bladeren galerie blade hebt gestart, kunt u zoeken op Hallo velden te volgen:
   
   * Modulenaam
   * Tags
   * Auteur
   * Naam van cmdlet/DSC-resource
6. Een module dat u geïnteresseerd bent in en selecteert u het tooview Zoek de details ervan.  
   Wanneer u een specifieke module inzoomen, vindt u meer informatie over het Hallo-module, een koppeling back toohello PowerShell Gallery eventuele vereiste afhankelijkheden en alle Hallo-cmdlets en/of DSC-resources die module Hallo bevat.
   
    ![Details van de PowerShell-module](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. tooinstall hello module rechtstreeks in Azure Automation, klikt u op Hallo **importeren** knop.
   
    ![Knop importeren-module](media/automation-runbook-gallery/module-import-button.png)
8. Als u op de knop importeren hello, ziet u Hallo modulenaam dat u gaat tooimport. Als alle Hallo-afhankelijkheden zijn geïnstalleerd, Hallo **OK** knop actief zijn. Als u afhankelijkheden ontbreekt, moet u tooimport die voordat u deze module kunt importeren.
9. Klik op **OK** tooimport Hallo-module en Hallo module blade wordt gestart. Als een module tooyour-account voor Azure Automation wordt geïmporteerd, pakt deze metagegevens over Hallo-module en Hallo-cmdlets.
   
    ![Blade voor import-module](media/automation-runbook-gallery/module-import-blade.png)
   
    Dit kan een paar minuten duren, omdat elke activiteit toobe hebt uitgepakt moet.
10. U ontvangt een melding die module hello wordt geïmplementeerd en een melding wanneer deze is voltooid.
11. Nadat het Hallo-module is geïmporteerd, ziet u de beschikbare activiteiten Hallo en kunt u de resources in uw runbooks en Desired State Configuration.

## <a name="requesting-a-runbook-or-module"></a>Een runbook of de module aanvragen
U kunt aanvragen te verzenden[User Voice](https://feedback.azure.com/forums/246290-azure-automation/).  Als u nodig hebt te schrijven van een runbook of een vraag over PowerShell hebt, een vraag tooour boeken [forum](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).

## <a name="next-steps"></a>Volgende stappen
* tooget gestart met runbooks, Zie [maken of importeren van een runbook in Azure Automation](automation-creating-importing-runbook.md)
* toounderstand hello verschillen tussen PowerShell en PowerShell Workflow met runbooks, Zie [Learning PowerShell workflow](automation-powershell-workflow.md)

