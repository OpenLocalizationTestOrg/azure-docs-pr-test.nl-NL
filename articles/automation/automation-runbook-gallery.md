---
title: "Runbook- en galerieën voor Azure Automation | Microsoft Docs"
description: Runbooks en modules van Microsoft en de community zijn beschikbaar voor u installeren en gebruiken in uw Azure Automation-omgeving.  Dit artikel wordt beschreven hoe u toegang hebt tot deze bronnen en bij te dragen van uw runbooks aan de galerie.
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
ms.openlocfilehash: 04cfafc9e7a037d915f63723fd0b67a07954460b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a>Runbook- en galerieën voor Azure Automation
In plaats van uw eigen runbooks en modules in Azure Automation, kunt u toegang tot allerlei scenario's die al zijn gebouwd door Microsoft en de community.  U kunt deze scenario's zonder aanpassingen gebruiken of u kunt ze als uitgangspunt gebruiken en ze bewerken voor uw specifieke vereisten.

U krijgt runbooks uit de [Runbookgalerie](#runbooks-in-runbook-gallery) en -modules van de [PowerShell Gallery](#modules-in-powerShell-gallery).  U kunt ook bijdragen aan de community delen scenario's die u ontwikkelt.

## <a name="runbooks-in-runbook-gallery"></a>Runbooks in Runbookgalerie
De [Runbookgalerie](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) biedt tal van runbooks van Microsoft en de community die u in Azure Automation importeren kunt. Kunt u een runbook downloaden uit de galerie die wordt gehost in de [TechNet Script Center](https://gallery.technet.microsoft.com/scriptcenter/site/upload), of u kunt rechtstreeks runbooks importeren uit de galerie van de klassieke Azure-portal of een Azure-portal.

U kunt alleen met de importeren rechtstreeks vanuit de Runbookgalerie met behulp van de klassieke Azure-portal of Azure-portal. U kunt deze functie met Windows PowerShell niet uitvoeren.

> [!NOTE]
> U moet controleren of de inhoud van alle runbooks die u niet uit de Runbookgalerie ophalen en uiterst voorzichtig met het installeren en uit te voeren in een productieomgeving. |
> 
> 

### <a name="to-import-a-runbook-from-the-runbook-gallery-with-the-azure-classic-portal"></a>Een runbook importeren vanuit de galerie Runbook met de klassieke Azure portal
1. In de Azure-Portal klikt, **nieuw**, **App Services**, **Automation**, **Runbook**, **uit galerie**.
2. Selecteer een categorie om verwante runbooks weer te geven en selecteer een runbook om de details ervan weer te geven. Wanneer u het runbook dat u wilt selecteren, klikt u op de pijl naar rechts.
   
    ![Runbook-galerie](media/automation-runbook-gallery/runbook-gallery.png)
3. Controleer de inhoud van het runbook en Let op eventuele vereisten in de beschrijving. Wanneer u klaar bent, klikt u op de pijl naar rechts.
4. Geef de runbookdetails en klik op knop met het vinkje. De runbooknaam wordt al ingevuld.
5. Het runbook wordt weergegeven op de **Runbooks** tabblad voor het Automation-Account.

### <a name="to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal"></a>Een runbook importeren vanuit de galerie Runbook met de Azure-portal
1. Open uw Automation-account in Azure Portal.
2. Klik op de tegel **Runbooks** om de lijst met runbooks te openen.
3. Klik op **bladeren galerie** knop.
   
    ![Galerie knop Bladeren](media/automation-runbook-gallery/browse-gallery-button.png)
4. Ga naar het galerij-item u wilt en selecteert u deze om de details ervan weer te geven.
   
    ![Galerie bladeren](media/automation-runbook-gallery/browse-gallery.png)
5. Klik op **weergave bronproject** om weer te geven van het item in de [TechNet Script Center](http://gallery.technet.microsoft.com/).
6. Voor het importeren van een item, klikt u op de bijbehorende details weergeven en klik vervolgens op de **importeren** knop.
   
    ![Knop importeren](media/automation-runbook-gallery/gallery-item-detail.png)
7. U kunt desgewenst de naam van het runbook wijzigen en klik vervolgens op **OK** voor het importeren van het runbook.
8. Het runbook wordt weergegeven op de **Runbooks** tabblad voor het Automation-Account.

### <a name="adding-a-runbook-to-the-runbook-gallery"></a>Een runbook toe te voegen aan de runbookgalerie
Microsoft raadt u runbooks toevoegen aan de Runbook-galerie die u denkt dat handig kan zijn voor andere klanten.  U kunt een runbook door toevoegen [uploaden naar het Script Center](http://gallery.technet.microsoft.com/site/upload) rekening houdend met de volgende details.

* U moet opgeven *Windows Azure* voor de **categorie** en *Automation* voor de **subcategorie** voor het runbook moet worden weergegeven in de wizard.  
* Het uploaden moet één .ps1 of .graphrunbook-bestand.  Als het runbook is vereist voor alle modules, onderliggende runbooks of activa, moet klikt u aanbieden die in de beschrijving van de verzending en in het gedeelte met opmerkingen van het runbook.  Als u een scenario voor het vereisen van meerdere runbooks hebt, elk afzonderlijk uploaden en de namen van de gerelateerde runbooks in elk van de bijbehorende beschrijvingen. Zorg ervoor dat de dezelfde codes te gebruiken, zodat ze worden weergegeven in dezelfde categorie. Een gebruiker moet lees de beschrijving als u wilt weten dat er andere runbooks vereist zijn het scenario om te werken.
* Voeg het label 'GraphicalPS' als u wilt publiceren een **grafisch runbook** (geen grafische werkstroom). 
* Een PowerShell- of PowerShell Workflow codefragment invoegen in het gebruik van de beschrijving **code sectie invoegen** pictogram.
* De samenvatting voor het uploaden wordt weergegeven in de resultaten Runbookgalerie zodat u moet bieden gedetailleerde informatie waarmee een gebruiker die de functionaliteit van het runbook te identificeren.
* U moet één tot drie van de volgende codes toewijzen aan het uploaden.  Het runbook wordt weergegeven in de wizard onder de categorieën die overeenkomen met de labels.  Alle tags niet op deze lijst worden genegeerd door de wizard. Als u geen overeenkomende labels opgeeft, wordt het runbook wordt weergegeven onder de andere categorie.
  
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
* De galerie-Automation updates eenmaal een uur, zodat u uw bijdragen onmiddellijk niet zien.

## <a name="modules-in-powershell-gallery"></a>Modules in PowerShell Gallery
PowerShell-modules bevatten cmdlets die u in uw runbooks gebruiken kunt en bestaande modules die u in Azure Automation installeren kunt zijn beschikbaar in de [PowerShell Gallery](http://www.powershellgallery.com).  U kunt deze galerie starten vanuit de Azure-portal en deze rechtstreeks in Azure Automation installeren of u kunt deze downloaden en deze handmatig installeren.  U kunt de modules niet rechtstreeks vanuit de klassieke Azure portal installeren, maar u kunt ze downloaden ze net als elke andere module te installeren.

### <a name="to-import-a-module-from-the-automation-module-gallery-with-the-azure-portal"></a>Een module importeren uit de galerie met Automation-Module met de Azure-portal
1. Open uw Automation-account in Azure Portal.
2. Klik op de **activa** tegel om de lijst van assets te openen.
3. Klik op de **Modules** tegel te openen van de lijst met modules.
4. Klik op de **bladeren galerie** knop en de blade bladeren galerie wordt gestart.
   
    ![Modulegalerie](media/automation-runbook-gallery/modules-blade.png) <br>
5. Nadat u de blade bladeren galerie hebt gestart, kunt u zoeken door de volgende velden:
   
   * Modulenaam
   * Tags
   * Auteur
   * Naam van cmdlet/DSC-resource
6. Zoek een module die u geïnteresseerd bent in en selecteert u deze om de details ervan weer te geven.  
   Wanneer u een specifieke module inzoomen, kunt u meer informatie weergeven over de module, een koppeling naar de PowerShell-galerie, inclusief eventuele vereiste afhankelijkheden en alle van de cmdlets en/of de DSC-resources met de module.
   
    ![Details van de PowerShell-module](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. Voor het installeren van de module rechtstreeks in Azure Automation, klikt u op de **importeren** knop.
   
    ![Knop importeren-module](media/automation-runbook-gallery/module-import-button.png)
8. Als u op de knop importeren, ziet u de naam van de module die u wilt importeren. Als alle afhankelijkheden zijn geïnstalleerd, de **OK** knop actief zijn. Als u afhankelijkheden ontbreekt, moet u die importeren voordat u deze module kunt importeren.
9. Klik op **OK** voor het importeren van de module en de module-blade wordt gestart. Wanneer u een module Azure Automation importeert in uw account, pakt deze metagegevens over de module en de cmdlets.
   
    ![Blade voor import-module](media/automation-runbook-gallery/module-import-blade.png)
   
    Dit kan enkele minuten duren, omdat elke activiteit moet worden geëxtraheerd.
10. U ontvangt een melding dat de module wordt geïmplementeerd en een melding wanneer deze is voltooid.
11. Nadat de module is geïmporteerd, ziet u de beschikbare activiteiten en kunt u de resources in uw runbooks en Desired State Configuration.

## <a name="requesting-a-runbook-or-module"></a>Een runbook of de module aanvragen
U kunt aanvragen verzenden [User Voice](https://feedback.azure.com/forums/246290-azure-automation/).  Als u nodig hebt te schrijven van een runbook of een vraag over PowerShell hebt, een vraag te posten onze [forum](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).

## <a name="next-steps"></a>Volgende stappen
* Om te beginnen met runbooks, Zie [maken of importeren van een runbook in Azure Automation](automation-creating-importing-runbook.md)
* Zie voor informatie over de verschillen tussen PowerShell en PowerShell Workflow met runbooks, [Learning PowerShell workflow](automation-powershell-workflow.md)

