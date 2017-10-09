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
# <a name="grant-user-permissions-toospecific-lab-policies"></a>Gebruikersmachtigingen verlenen toospecific labbeleidsregels
## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe toouse PowerShell toogrant gebruikers machtigingen tooa bepaalde lab beleid. Op die manier kunnen machtigingen worden toegepast op basis van de behoeften van elke gebruiker. Bijvoorbeeld, kunt u toogrant een bepaalde gebruiker Hallo mogelijkheid toochange Hallo VM instellingen, maar niet Hallo kosten beleidsregels.

## <a name="policies-as-resources"></a>Beleid als resources
Zoals beschreven in Hallo [toegangsbeheer op basis van rollen in Azure](../active-directory/role-based-access-control-configure.md) artikel RBAC kunt Geavanceerd toegangsbeheer van resources voor Azure. Met RBAC kunt u taken scheiden binnen uw team DevOps en alleen Hallo hoeveelheid toousers toegang verlenen die zij nodig hebben tooperform hun werk.

In DevTest Labs is een beleid een resourcetype waarmee Hallo RBAC actie **Microsoft.DevTestLab/labs/policySets/policies/**. Elk beleid lab is een resource in Hallo beleid brontype en kan worden toegewezen als een bereik tooan RBAC-rol.

Bijvoorbeeld, in volgorde toogrant gebruikers lezen/schrijven machtiging toohello **VM-grootten toegestaan** beleid, maakt u een aangepaste rol die geschikt is voor Hallo **Microsoft.DevTestLab/labs/policySets/policies/** * actie en toewijzen Hallo geschikte gebruikers met toothis aangepaste rol binnen het bereik van Hallo **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.

toolearn meer informatie over aangepaste rollen in RBAC, Zie Hallo [aangepaste rollen toegangsbeheer](../active-directory/role-based-access-control-custom-roles.md).

## <a name="creating-a-lab-custom-role-using-powershell"></a>Maken van een aangepaste lab-functie met behulp van PowerShell
In de volgorde tooget gestart, moet u tooread Hallo volgende artikel, waarin wordt uitgelegd hoe tooinstall en configureer hello Azure PowerShell-cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).

Zodra u hello Azure PowerShell-cmdlets hebt ingesteld, kunt u Hallo volgende taken uitvoeren:

* Lijst met alle Hallo operations/acties voor een resourceprovider
* Lijst met acties in een bepaalde rol:
* Een aangepaste beveiligingsrol maken

Hallo volgende PowerShell-script ziet u voorbeelden van hoe tooperform deze taken:

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

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a>Machtigingen tooa gebruiker voor een specifiek beleid met behulp van aangepaste rollen toewijzen
Als u uw aangepaste rollen hebt gedefinieerd, kunt u deze toousers toewijzen. In de volgorde tooassign een aangepaste rol tooa gebruiker, moet u eerst Hallo aanvragen **ObjectId** voor die gebruiker. toodo die gebruik Hallo **Get-AzureRmADUser** cmdlet.

Hallo in Hallo voorbeeld te volgen, **ObjectId** Hallo *SomeUser* gebruiker 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 is.

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

Zodra u Hallo hebt **ObjectId** voor Hallo gebruiker en de naam van een aangepaste rol, kunt u die rol toohello gebruiker Hello toewijzen **New AzureRmRoleAssignment** cmdlet:

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

In het vorige voorbeeld Hallo Hallo **AllowedVmSizesInLab** beleid wordt gebruikt. U kunt een van de volgende beleidsregels hello gebruiken:

* MaxVmsAllowedPerUser
* MaxVmsAllowedPerLab
* AllowedVmSizesInLab
* LabVmsShutdown

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Volgende stappen
U hebt verleende machtigingen toospecific labbeleidsregels, hier zijn enkele volgende stappen tooconsider:

* [Veilige toegang tooa lab](devtest-lab-add-devtest-user.md).
* [Labbeleidsregels instellen](devtest-lab-set-lab-policy.md).
* [Een labsjabloon maken](devtest-lab-create-template.md).
* [Aangepaste artefacten maken voor uw virtuele machines](devtest-lab-artifact-author.md).
* [Toevoegen van een VM met artefacten tooa lab](devtest-lab-add-vm-with-artifacts.md).

