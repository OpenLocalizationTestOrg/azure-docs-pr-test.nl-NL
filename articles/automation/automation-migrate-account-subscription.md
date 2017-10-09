---
title: aaaMigrate Automation-Account en Resources | Microsoft Docs
description: "Dit artikel wordt beschreven hoe toomove een Automation-Account in Azure Automation en de bijbehorende resources uit één abonnement tooanother."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a>Automation-Account en resources migreren
Voor het Automation-accounts en de bijbehorende bronnen (dat wil zeggen activa, runbooks, modules, enzovoort) die u hebt gemaakt in hello Azure-portal en wilt toomigrate van de ene groep tooanother of van één abonnement tooanother, u kunt dit doen eenvoudig met Hallo [verplaatsen van resources](../azure-resource-manager/resource-group-move-resources.md) beschikbare functie in hello Azure-portal. Echter, voordat u doorgaat met deze actie moet u eerst nagaan Hallo volgende [controlelijst voor het verplaatsen van resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) en daarnaast Hallo onderstaande lijst met specifieke tooAutomation.   

1. Hallo bestemming/resourcegroep moet zich in dezelfde regio bevinden als het Hallo-bron.  Wat betekent dat Automation-accounts niet verplaatsen tussen regio's.
2. Bij het verplaatsen van resources (bijvoorbeeld runbooks, taken, enzovoort), worden zowel Hallo brongroep en de doelgroep Hallo vergrendeld voor Hallo duur van Hallo-bewerking. Schrijf- en verwijderbewerkingen op Hallo groepen worden geblokkeerd totdat Hallo verplaatsen is voltooid.  
3. De runbooks of variabelen die verwijzen naar een resourcegroep of abonnement-ID van het bestaande abonnement Hallo moet toobe bijgewerkt nadat de migratie is voltooid.   

> [!NOTE]
> Deze functie ondersteunt geen bewegende klassieke automation-resources.
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a>toomove Hallo Automation-Account met Hallo-portal
1. Van uw Automation-account, klikt u op **verplaatsen** Hallo boven aan het Hallo-blade.<br> ![Optie verplaatsen](media/automation-migrate-account-subscription/automation-menu-move.png)<br>
2. Op Hallo **verplaatsen van resources** blade, notitie deze resources gerelateerde tooboth geeft uw Automation-account en uw groep(en) resource.  Selecteer Hallo **abonnement** en **resourcegroep** van select Hallo optie of Hallo vervolgkeuzelijsten **een nieuwe resourcegroep maken** en voert u een nieuwe Resourcegroepnaam in Hallo-veld is opgegeven.  
3. Bekijken en selecteer Hallo selectievakje tooacknowledge u *hulpprogramma's en scripts wordt inzicht moeten toobe bijgewerkt toouse nieuwe resource-id nadat resources zijn verplaatst* en klik vervolgens op **OK**.<br> ![Blade voor Resources verplaatsen](media/automation-migrate-account-subscription/automation-move-resources-blade.png)<br>   

Deze actie duurt enkele minuten toocomplete.  In **meldingen**, u krijgt de status van elke actie die uitgevoerd - validatie, migratie wordt, en klik tot slot wanneer deze is voltooid.     

## <a name="toomove-hello-automation-account-using-powershell"></a>toomove Hallo Automation-Account met behulp van PowerShell
toomove bestaande Automation-resources tooanother resourcegroep of abonnement, hello gebruiken **Get-AzureRmResource** cmdlet tooget Hallo specifieke Automation-account en vervolgens **verplaatsen AzureRmResource** cmdlet tooperform Hallo verplaatsen.

Hallo eerste voorbeeld laat zien hoe toomove een Automation-account tooa nieuwe resourcegroep.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

Nadat u Hallo hierboven codevoorbeeld uitvoert, kunt u zich na vragen aan gebruiker tooverify gewenste tooperform deze actie.  Nadat u op **Ja** waardoor Hallo script tooproceed, ontvangt u geen meldingen terwijl het Hallo-migratie uitvoert.  

toomove tooa nieuw abonnement, een waarde bevatten voor Hallo *DestinationSubscriptionId* parameter.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

Net als bij het vorige voorbeeld hello, kunt u zich na vragen aan gebruiker tooconfirm Hallo verplaatsen.  

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over de zwevende resources toonew-resourcegroep of abonnement [verplaatsen van resources toonew resourcegroep of abonnement](../azure-resource-manager/resource-group-move-resources.md)
* Voor meer informatie over toegangsbeheer op basis van rollen in Azure Automation te verwijzen[toegangsbeheer op basis van rollen in Azure Automation](automation-role-based-access-control.md).
* toolearn over PowerShell-cmdlets voor het beheren van uw abonnement, Zie [Azure PowerShell gebruiken met Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)
* toolearn over portal functies voor het beheren van uw abonnement, Zie [hello Azure Portal toomanage bronnen](../azure-resource-manager/resource-group-portal.md).
