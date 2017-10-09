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
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="d438a-103">Automation-Account en resources migreren</span><span class="sxs-lookup"><span data-stu-id="d438a-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="d438a-104">Voor het Automation-accounts en de bijbehorende bronnen (dat wil zeggen activa, runbooks, modules, enzovoort) die u hebt gemaakt in hello Azure-portal en wilt toomigrate van de ene groep tooanother of van één abonnement tooanother, u kunt dit doen eenvoudig met Hallo [verplaatsen van resources](../azure-resource-manager/resource-group-move-resources.md) beschikbare functie in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d438a-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in hello Azure portal and want toomigrate from one resource group tooanother or from one subscription tooanother, you can accomplish this easily with hello [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in hello Azure portal.</span></span> <span data-ttu-id="d438a-105">Echter, voordat u doorgaat met deze actie moet u eerst nagaan Hallo volgende [controlelijst voor het verplaatsen van resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) en daarnaast Hallo onderstaande lijst met specifieke tooAutomation.</span><span class="sxs-lookup"><span data-stu-id="d438a-105">However, before proceeding with this action, you should first review hello following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, hello list below specific tooAutomation.</span></span>   

1. <span data-ttu-id="d438a-106">Hallo bestemming/resourcegroep moet zich in dezelfde regio bevinden als het Hallo-bron.</span><span class="sxs-lookup"><span data-stu-id="d438a-106">hello destination subscription/resource group must be in same region as hello source.</span></span>  <span data-ttu-id="d438a-107">Wat betekent dat Automation-accounts niet verplaatsen tussen regio's.</span><span class="sxs-lookup"><span data-stu-id="d438a-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="d438a-108">Bij het verplaatsen van resources (bijvoorbeeld runbooks, taken, enzovoort), worden zowel Hallo brongroep en de doelgroep Hallo vergrendeld voor Hallo duur van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="d438a-108">When moving resources (e.g. runbooks, jobs, etc.), both hello source group and hello target group are locked for hello duration of hello operation.</span></span> <span data-ttu-id="d438a-109">Schrijf- en verwijderbewerkingen op Hallo groepen worden geblokkeerd totdat Hallo verplaatsen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d438a-109">Write and delete operations are blocked on hello groups until hello move completes.</span></span>  
3. <span data-ttu-id="d438a-110">De runbooks of variabelen die verwijzen naar een resourcegroep of abonnement-ID van het bestaande abonnement Hallo moet toobe bijgewerkt nadat de migratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d438a-110">Any runbooks or variables which reference a resource or subscription ID from hello existing subscription will need toobe updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="d438a-111">Deze functie ondersteunt geen bewegende klassieke automation-resources.</span><span class="sxs-lookup"><span data-stu-id="d438a-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a><span data-ttu-id="d438a-112">toomove Hallo Automation-Account met Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="d438a-112">toomove hello Automation Account using hello portal</span></span>
1. <span data-ttu-id="d438a-113">Van uw Automation-account, klikt u op **verplaatsen** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="d438a-113">From your Automation account, click **Move** at hello top of hello blade.</span></span><br> <span data-ttu-id="d438a-114">![Optie verplaatsen](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="d438a-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="d438a-115">Op Hallo **verplaatsen van resources** blade, notitie deze resources gerelateerde tooboth geeft uw Automation-account en uw groep(en) resource.</span><span class="sxs-lookup"><span data-stu-id="d438a-115">On hello **Move resources** blade, note that it presents resources related tooboth your Automation account and your resource group(s).</span></span>  <span data-ttu-id="d438a-116">Selecteer Hallo **abonnement** en **resourcegroep** van select Hallo optie of Hallo vervolgkeuzelijsten **een nieuwe resourcegroep maken** en voert u een nieuwe Resourcegroepnaam in Hallo-veld is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d438a-116">Select hello **subscription** and **resource group** from hello drop-down lists, or select hello option **create a new resource group** and enter a new resource group name in hello field provided.</span></span>  
3. <span data-ttu-id="d438a-117">Bekijken en selecteer Hallo selectievakje tooacknowledge u *hulpprogramma's en scripts wordt inzicht moeten toobe bijgewerkt toouse nieuwe resource-id nadat resources zijn verplaatst* en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d438a-117">Review and select hello checkbox tooacknowledge you *understand tools and scripts will need toobe updated toouse new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="d438a-118">![Blade voor Resources verplaatsen](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="d438a-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="d438a-119">Deze actie duurt enkele minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="d438a-119">This action will take several minutes toocomplete.</span></span>  <span data-ttu-id="d438a-120">In **meldingen**, u krijgt de status van elke actie die uitgevoerd - validatie, migratie wordt, en klik tot slot wanneer deze is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d438a-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="toomove-hello-automation-account-using-powershell"></a><span data-ttu-id="d438a-121">toomove Hallo Automation-Account met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="d438a-121">toomove hello Automation Account using PowerShell</span></span>
<span data-ttu-id="d438a-122">toomove bestaande Automation-resources tooanother resourcegroep of abonnement, hello gebruiken **Get-AzureRmResource** cmdlet tooget Hallo specifieke Automation-account en vervolgens **verplaatsen AzureRmResource** cmdlet tooperform Hallo verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="d438a-122">toomove existing Automation resources tooanother resource group or subscription, use hello  **Get-AzureRmResource** cmdlet tooget hello specific Automation account and then **Move-AzureRmResource** cmdlet tooperform hello move.</span></span>

<span data-ttu-id="d438a-123">Hallo eerste voorbeeld laat zien hoe toomove een Automation-account tooa nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d438a-123">hello first example shows how toomove an Automation account tooa new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="d438a-124">Nadat u Hallo hierboven codevoorbeeld uitvoert, kunt u zich na vragen aan gebruiker tooverify gewenste tooperform deze actie.</span><span class="sxs-lookup"><span data-stu-id="d438a-124">After you execute hello above code example, you will be prompted tooverify you want tooperform this action.</span></span>  <span data-ttu-id="d438a-125">Nadat u op **Ja** waardoor Hallo script tooproceed, ontvangt u geen meldingen terwijl het Hallo-migratie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="d438a-125">Once you click **Yes** and allow hello script tooproceed, you will not receive any notifications while it's performing hello migration.</span></span>  

<span data-ttu-id="d438a-126">toomove tooa nieuw abonnement, een waarde bevatten voor Hallo *DestinationSubscriptionId* parameter.</span><span class="sxs-lookup"><span data-stu-id="d438a-126">toomove tooa new subscription, include a value for hello *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="d438a-127">Net als bij het vorige voorbeeld hello, kunt u zich na vragen aan gebruiker tooconfirm Hallo verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="d438a-127">As with hello previous example, you will be prompted tooconfirm hello move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d438a-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d438a-128">Next steps</span></span>
* <span data-ttu-id="d438a-129">Zie voor meer informatie over de zwevende resources toonew-resourcegroep of abonnement [verplaatsen van resources toonew resourcegroep of abonnement](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="d438a-129">For more information about moving resources toonew resource group or subscription, see [Move  resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="d438a-130">Voor meer informatie over toegangsbeheer op basis van rollen in Azure Automation te verwijzen[toegangsbeheer op basis van rollen in Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="d438a-130">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="d438a-131">toolearn over PowerShell-cmdlets voor het beheren van uw abonnement, Zie [Azure PowerShell gebruiken met Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="d438a-131">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="d438a-132">toolearn over portal functies voor het beheren van uw abonnement, Zie [hello Azure Portal toomanage bronnen](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d438a-132">toolearn about portal features for managing your subscription, see [Using hello Azure Portal toomanage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
