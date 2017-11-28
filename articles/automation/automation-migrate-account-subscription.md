---
title: Automation-Account en Resources migreren | Microsoft Docs
description: In dit artikel wordt beschreven hoe een Automation-Account in Azure Automation en de bijbehorende bronnen van een abonnement te verplaatsen naar een andere.
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
ms.openlocfilehash: 687da15bdaf854254321b59350f47549781676f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="cb6a8-103">Automation-Account en resources migreren</span><span class="sxs-lookup"><span data-stu-id="cb6a8-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="cb6a8-104">Voor het Automation-accounts en de bijbehorende bronnen (dat wil zeggen activa, runbooks, modules, enzovoort) die u hebt gemaakt in de Azure portal en wilt migreren van een resourcegroep naar een andere of van een abonnement naar een andere, u kunt dit doen eenvoudig met de [verplaatsen van resources](../azure-resource-manager/resource-group-move-resources.md) functie is beschikbaar in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in the Azure portal and want to migrate from one resource group to another or from one subscription to another, you can accomplish this easily with the [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in the Azure portal.</span></span> <span data-ttu-id="cb6a8-105">Echter, voordat u doorgaat met deze actie moet u eerst nagaan de volgende [controlelijst voor het verplaatsen van resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) en daarnaast de lijst hieronder die specifiek zijn voor Automation.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-105">However, before proceeding with this action, you should first review the following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, the list below specific to Automation.</span></span>   

1. <span data-ttu-id="cb6a8-106">De bestemming/resourcegroep moet zich in dezelfde regio bevinden als de bron.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-106">The destination subscription/resource group must be in same region as the source.</span></span>  <span data-ttu-id="cb6a8-107">Wat betekent dat Automation-accounts niet verplaatsen tussen regio's.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="cb6a8-108">Bij het verplaatsen van resources (bijvoorbeeld runbooks, taken, enzovoort), worden zowel de bronnengroep als de doelgroep vergrendeld voor de duur van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-108">When moving resources (e.g. runbooks, jobs, etc.), both the source group and the target group are locked for the duration of the operation.</span></span> <span data-ttu-id="cb6a8-109">Schrijven en verwijderen van bewerkingen op de groepen die worden geblokkeerd totdat de verplaatsing is voltooid.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-109">Write and delete operations are blocked on the groups until the move completes.</span></span>  
3. <span data-ttu-id="cb6a8-110">De runbooks of variabelen die verwijzen naar een resourcegroep of abonnement-ID van het bestaande abonnement moet worden bijgewerkt nadat de migratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-110">Any runbooks or variables which reference a resource or subscription ID from the existing subscription will need to be updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="cb6a8-111">Deze functie ondersteunt geen bewegende klassieke automation-resources.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="to-move-the-automation-account-using-the-portal"></a><span data-ttu-id="cb6a8-112">Verplaatsen van het Automation-Account via de portal</span><span class="sxs-lookup"><span data-stu-id="cb6a8-112">To move the Automation Account using the portal</span></span>
1. <span data-ttu-id="cb6a8-113">Van uw Automation-account, klikt u op **verplaatsen** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-113">From your Automation account, click **Move** at the top of the blade.</span></span><br> <span data-ttu-id="cb6a8-114">![Optie verplaatsen](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="cb6a8-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="cb6a8-115">Op de **verplaatsen van resources** blade, Let op: dit geeft de bronnen die betrekking hebben op uw Automation-account en uw groep(en) resource.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-115">On the **Move resources** blade, note that it presents resources related to both your Automation account and your resource group(s).</span></span>  <span data-ttu-id="cb6a8-116">Selecteer de **abonnement** en **resourcegroep** uit de vervolgkeuzelijst, of Selecteer de optie **een nieuwe resourcegroep maken** en voert u een nieuwe Resourcegroepnaam in het veld dat is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-116">Select the **subscription** and **resource group** from the drop-down lists, or select the option **create a new resource group** and enter a new resource group name in the field provided.</span></span>  
3. <span data-ttu-id="cb6a8-117">Bekijk en schakel het selectievakje in om te bevestigen dat u *over hulpprogramma's en scripts moet worden bijgewerkt om de nieuwe resource-id's gebruiken nadat resources zijn verplaatst* en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-117">Review and select the checkbox to acknowledge you *understand tools and scripts will need to be updated to use new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="cb6a8-118">![Blade voor Resources verplaatsen](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="cb6a8-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="cb6a8-119">Deze actie duurt enkele minuten in beslag.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-119">This action will take several minutes to complete.</span></span>  <span data-ttu-id="cb6a8-120">In **meldingen**, u krijgt de status van elke actie die uitgevoerd - validatie, migratie wordt, en klik tot slot wanneer deze is voltooid.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="to-move-the-automation-account-using-powershell"></a><span data-ttu-id="cb6a8-121">Verplaatsen van het Automation-Account met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb6a8-121">To move the Automation Account using PowerShell</span></span>
<span data-ttu-id="cb6a8-122">U kunt bestaande Automation-resources verplaatsen naar een andere resourcegroep of abonnement met de **Get-AzureRmResource** cmdlet ophalen van de specifieke Automation-account en vervolgens **verplaatsen AzureRmResource** cmdlet uit te voeren van de verplaatsing.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-122">To move existing Automation resources to another resource group or subscription, use the  **Get-AzureRmResource** cmdlet to get the specific Automation account and then **Move-AzureRmResource** cmdlet to perform the move.</span></span>

<span data-ttu-id="cb6a8-123">Het eerste voorbeeld laat zien hoe een Automation-account verplaatsen naar een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-123">The first example shows how to move an Automation account to a new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="cb6a8-124">Nadat u het bovenstaande voorbeeld uitvoert, wordt u gevraagd om te controleren of dat u wilt dat deze actie uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-124">After you execute the above code example, you will be prompted to verify you want to perform this action.</span></span>  <span data-ttu-id="cb6a8-125">Nadat u op **Ja** en toestaan dat het script om door te gaan, ontvangt u geen meldingen tijdens het uitvoeren van de migratie.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-125">Once you click **Yes** and allow the script to proceed, you will not receive any notifications while it's performing the migration.</span></span>  

<span data-ttu-id="cb6a8-126">Als u wilt verplaatsen naar een nieuw abonnement, een waarde bevatten voor de *DestinationSubscriptionId* parameter.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-126">To move to a new subscription, include a value for the *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="cb6a8-127">Net als bij het vorige voorbeeld, wordt u gevraagd om te bevestigen dat de verplaatsing.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-127">As with the previous example, you will be prompted to confirm the move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="cb6a8-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cb6a8-128">Next steps</span></span>
* <span data-ttu-id="cb6a8-129">Zie voor meer informatie over het verplaatsen van resources naar de nieuwe resourcegroep of abonnement [resources verplaatsen naar de nieuwe resourcegroep of abonnement](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="cb6a8-129">For more information about moving resources to new resource group or subscription, see [Move  resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="cb6a8-130">Zie [Op rollen gebaseerd toegangsbeheer in Azure Automation](automation-role-based-access-control.md) voor meer informatie over het op rollen gebaseerd toegangsbeheer in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="cb6a8-130">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="cb6a8-131">Zie voor meer informatie over PowerShell-cmdlets voor het beheren van uw abonnement, [Azure PowerShell gebruiken met Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="cb6a8-131">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="cb6a8-132">Zie voor meer informatie over portal functies voor het beheren van uw abonnement, [om resources te beheren met behulp van de Azure Portal](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cb6a8-132">To learn about portal features for managing your subscription, see [Using the Azure Portal to manage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
