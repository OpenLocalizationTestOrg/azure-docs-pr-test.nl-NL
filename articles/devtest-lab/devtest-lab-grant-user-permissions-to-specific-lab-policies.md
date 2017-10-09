---
title: aaaGrant machtigingen toospecific lab gebruikersbeleid | Microsoft Docs
description: Meer informatie over hoe toogrant machtigingen toospecific lab gebruikersbeleid in DevTest Labs op basis van de behoeften van elke gebruiker
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 35647ab837243188f06566cdf365b67fe33a3865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="grant-user-permissions-toospecific-lab-policies"></a><span data-ttu-id="48143-103">Gebruikersmachtigingen verlenen toospecific labbeleidsregels</span><span class="sxs-lookup"><span data-stu-id="48143-103">Grant user permissions toospecific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="48143-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="48143-104">Overview</span></span>
<span data-ttu-id="48143-105">Dit artikel wordt beschreven hoe toouse PowerShell toogrant gebruikers machtigingen tooa bepaalde lab beleid.</span><span class="sxs-lookup"><span data-stu-id="48143-105">This article illustrates how toouse PowerShell toogrant users permissions tooa particular lab policy.</span></span> <span data-ttu-id="48143-106">Op die manier kunnen machtigingen worden toegepast op basis van de behoeften van elke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="48143-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="48143-107">Bijvoorbeeld, kunt u toogrant een bepaalde gebruiker Hallo mogelijkheid toochange Hallo VM instellingen, maar niet Hallo kosten beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="48143-107">For example, you might want toogrant a particular user hello ability toochange hello VM policy settings, but not hello cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="48143-108">Beleid als resources</span><span class="sxs-lookup"><span data-stu-id="48143-108">Policies as resources</span></span>
<span data-ttu-id="48143-109">Zoals beschreven in Hallo [toegangsbeheer op basis van rollen in Azure](../active-directory/role-based-access-control-configure.md) artikel RBAC kunt Geavanceerd toegangsbeheer van resources voor Azure.</span><span class="sxs-lookup"><span data-stu-id="48143-109">As discussed in hello [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="48143-110">Met RBAC kunt u taken scheiden binnen uw team DevOps en alleen Hallo hoeveelheid toousers toegang verlenen die zij nodig hebben tooperform hun werk.</span><span class="sxs-lookup"><span data-stu-id="48143-110">Using RBAC, you can segregate duties within your DevOps team and grant only hello amount of access toousers that they need tooperform their jobs.</span></span>

<span data-ttu-id="48143-111">In DevTest Labs is een beleid een resourcetype waarmee Hallo RBAC actie **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="48143-111">In DevTest Labs, a policy is a resource type that enables hello RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="48143-112">Elk beleid lab is een resource in Hallo beleid brontype en kan worden toegewezen als een bereik tooan RBAC-rol.</span><span class="sxs-lookup"><span data-stu-id="48143-112">Each lab policy is a resource in hello Policy resource type, and can be assigned as a scope tooan RBAC role.</span></span>

<span data-ttu-id="48143-113">Bijvoorbeeld, in volgorde toogrant gebruikers lezen/schrijven machtiging toohello **VM-grootten toegestaan** beleid, maakt u een aangepaste rol die geschikt is voor Hallo **Microsoft.DevTestLab/labs/policySets/policies/** * actie en toewijzen Hallo geschikte gebruikers met toothis aangepaste rol binnen het bereik van Hallo **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="48143-113">For example, in order toogrant users read/write permission toohello **Allowed VM Sizes** policy, you would create a custom role that works with hello **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign hello appropriate users toothis custom role in hello scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="48143-114">toolearn meer informatie over aangepaste rollen in RBAC, Zie Hallo [aangepaste rollen toegangsbeheer](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="48143-114">toolearn more about custom roles in RBAC, see hello [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="48143-115">Maken van een aangepaste lab-functie met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="48143-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="48143-116">In de volgorde tooget gestart, moet u tooread Hallo volgende artikel, waarin wordt uitgelegd hoe tooinstall en configureer hello Azure PowerShell-cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="48143-116">In order tooget started, you’ll need tooread hello following article, which will explain how tooinstall and configure hello Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="48143-117">Zodra u hello Azure PowerShell-cmdlets hebt ingesteld, kunt u Hallo volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="48143-117">Once you’ve set up hello Azure PowerShell cmdlets, you can perform hello following tasks:</span></span>

* <span data-ttu-id="48143-118">Lijst met alle Hallo operations/acties voor een resourceprovider</span><span class="sxs-lookup"><span data-stu-id="48143-118">List all hello operations/actions for a resource provider</span></span>
* <span data-ttu-id="48143-119">Lijst met acties in een bepaalde rol:</span><span class="sxs-lookup"><span data-stu-id="48143-119">List actions in a particular role:</span></span>
* <span data-ttu-id="48143-120">Een aangepaste beveiligingsrol maken</span><span class="sxs-lookup"><span data-stu-id="48143-120">Create a custom role</span></span>

<span data-ttu-id="48143-121">Hallo volgende PowerShell-script ziet u voorbeelden van hoe tooperform deze taken:</span><span class="sxs-lookup"><span data-stu-id="48143-121">hello following PowerShell script illustrates examples of how tooperform these tasks:</span></span>

    ‘List all hello operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="48143-122">Machtigingen tooa gebruiker voor een specifiek beleid met behulp van aangepaste rollen toewijzen</span><span class="sxs-lookup"><span data-stu-id="48143-122">Assigning permissions tooa user for a specific policy using custom roles</span></span>
<span data-ttu-id="48143-123">Als u uw aangepaste rollen hebt gedefinieerd, kunt u deze toousers toewijzen.</span><span class="sxs-lookup"><span data-stu-id="48143-123">Once you’ve defined your custom roles, you can assign them toousers.</span></span> <span data-ttu-id="48143-124">In de volgorde tooassign een aangepaste rol tooa gebruiker, moet u eerst Hallo aanvragen **ObjectId** voor die gebruiker.</span><span class="sxs-lookup"><span data-stu-id="48143-124">In order tooassign a custom role tooa user, you must first obtain hello **ObjectId** representing that user.</span></span> <span data-ttu-id="48143-125">toodo die gebruik Hallo **Get-AzureRmADUser** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="48143-125">toodo that, use hello **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="48143-126">Hallo in Hallo voorbeeld te volgen, **ObjectId** Hallo *SomeUser* gebruiker 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 is.</span><span class="sxs-lookup"><span data-stu-id="48143-126">In hello following example, hello **ObjectId** of hello *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="48143-127">Zodra u Hallo hebt **ObjectId** voor Hallo gebruiker en de naam van een aangepaste rol, kunt u die rol toohello gebruiker Hello toewijzen **New AzureRmRoleAssignment** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="48143-127">Once you have hello **ObjectId** for hello user and a custom role name, you can assign that role toohello user with hello **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="48143-128">In het vorige voorbeeld Hallo Hallo **AllowedVmSizesInLab** beleid wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="48143-128">In hello previous example, hello **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="48143-129">U kunt een van de volgende beleidsregels hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="48143-129">You can use any of hello following polices:</span></span>

* <span data-ttu-id="48143-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="48143-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="48143-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="48143-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="48143-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="48143-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="48143-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="48143-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="48143-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="48143-134">Next steps</span></span>
<span data-ttu-id="48143-135">U hebt verleende machtigingen toospecific labbeleidsregels, hier zijn enkele volgende stappen tooconsider:</span><span class="sxs-lookup"><span data-stu-id="48143-135">Once you've granted user permissions toospecific lab policies, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="48143-136">[Veilige toegang tooa lab](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="48143-136">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="48143-137">[Labbeleidsregels instellen](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="48143-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="48143-138">[Een labsjabloon maken](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="48143-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="48143-139">[Aangepaste artefacten maken voor uw virtuele machines](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="48143-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="48143-140">[Toevoegen van een VM met artefacten tooa lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="48143-140">[Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

