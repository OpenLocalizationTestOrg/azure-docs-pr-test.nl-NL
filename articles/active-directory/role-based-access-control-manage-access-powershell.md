---
title: aaaManage op rollen gebaseerde toegangsbeheer (RBAC) met Azure PowerShell | Microsoft Docs
description: Hoe toomanage RBAC met Azure PowerShell, met inbegrip van de aanbieding rollen, rollen toewijzen en het verwijderen van roltoewijzingen.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 9e225dba-9044-4b13-b573-2f30d77925a9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: fa44991113e75b345177867b0bede38de4373e04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a>Toegangsbeheer op basis van rollen beheren met Azure PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Azure-CLI](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)

In hello Azure-portal en Azure Resource Management-API toomanage toegang tooyour abonnement heel nauwkeurig kunt u rollen gebaseerd toegangsbeheer (RBAC). Met deze functie kunt u toegang tot Active Directory-gebruikers, groepen of service-principals verlenen door toe te wijzen van sommige rollen toothem bij een bepaald bereik.

Voordat u PowerShell toomanage RBAC gebruiken kunt, moet u Hallo volgende vereisten:

* Azure PowerShell versie 0.8.8 of hoger. meest recente versie van tooinstall hello en koppel deze met uw Azure-abonnement Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).
* Azure Resource Manager-cmdlets. Hallo installeren [Azure Resource Manager-cmdlets](/powershell/azure/overview) in PowerShell.

## <a name="list-roles"></a>Lijst met rollen
### <a name="list-all-available-roles"></a>Lijst van alle beschikbare rollen
toolist RBAC functies die beschikbaar zijn voor toewijzing en tooinspect Hallo operations toowhich ze toegang, gebruik `Get-AzureRmRoleDefinition`.

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell-Get AzureRmRoleDefinition - schermafbeelding](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a>Van Lijstacties van een rol
Gebruik toolist Hallo acties voor een specifieke rol `Get-AzureRmRoleDefinition <role name>`.

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell-Get AzureRmRoleDefinition voor een specifieke rol - schermafbeelding](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a>Zien wie toegang heeft
toolist RBAC toegangstoewijzingen gebruiken `Get-AzureRmRoleAssignment`.

### <a name="list-role-assignments-at-a-specific-scope"></a>Roltoewijzingen lijst op een specifiek bereik
Hier ziet u alle toewijzingen van Hallo toegang voor een opgegeven abonnement, resourcegroep of resource. Bijvoorbeeld, toosee alle actieve Hallo-toewijzingen voor een resourcegroep of gebruik Hallo `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment voor een resourcegroep - schermafbeelding](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a>Lijst met rollen toegewezen tooa gebruiker
alle Hallo rollen die zijn toegewezen tooa opgegeven gebruikers- en Hallo-rollen die zijn toegewezen toohello groepen toowhich Hallo gebruiker behoort, toolist gebruik `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment voor een gebruiker - schermafbeelding](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a>Lijst met klassieke servicebeheerder en coadmin roltoewijzingen
toolist toegangstoewijzingen voor de klassieke abonnementsbeheerder Hallo en coadministrators, gebruiken:

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a>Toegang verlenen
### <a name="search-for-object-ids"></a>Zoeken naar object-id 's
tooassign een rol, moet u tooidentify zowel Hallo-object (gebruiker, groep of toepassing) en Hallo bereik.

Als u Hallo abonnements-ID niet weet, kunt u deze vinden in Hallo **abonnementen** blade in hello Azure-portal. hoe tooquery voor Hallo abonnements-ID, Zie toolearn [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) op MSDN.

tooget Hallo-object-ID voor een Azure AD-groep gebruiken:

    Get-AzureRmADGroup -SearchString <group name in quotes>

tooget Hallo-object-ID voor een Azure AD-service-principal of toepassing, gebruiken:

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Een rol tooan toepassing in het bereik van Hallo abonnement toewijzen
toogrant toegang tooan-toepassing op Hallo abonnementsbereik gebruiken:

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - nieuwe AzureRmRoleAssignment - schermafbeelding](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Een gebruiker van de rol tooa op Hallo resource groepsbereik toewijzen
toogrant toegang tooa gebruiker op Hallo resource groepsbereik gebruiken:

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - nieuwe AzureRmRoleAssignment - schermafbeelding](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Een groep rol tooa bij Hallo resource bereik worden toegewezen
toogrant tooa toegangsgroep op Hallo resource bereik gebruiken:

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - nieuwe AzureRmRoleAssignment - schermafbeelding](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a>Toegang verwijderen
tooremove toegang voor gebruikers, groepen en toepassingen, gebruik:

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell-Remove AzureRmRoleAssignment - schermafbeelding](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a>Een aangepaste beveiligingsrol maken
een aangepaste beveiligingsrol toocreate gebruiken Hallo ```New-AzureRmRoleDefinition``` opdracht. Er zijn twee methoden voor het structureren Hallo-rol, met behulp van PSRoleDefinitionObject of een JSON-sjabloon. 

## <a name="get-actions-for-a-resource-provider"></a>Acties voor een Resourceprovider ophalen
Tijdens het maken van aangepaste rollen maken, het is belangrijk tooknow alle mogelijke bewerkingen van de resourceproviders Hallo Hallo.
Gebruik Hallo ```Get-AzureRMProviderOperation``` opdracht tooget deze informatie.
Als u wilt dat toocheck gebruiken alle beschikbare Hallo-bewerkingen voor de virtuele Machine met deze opdracht:

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a>Rol maken met PSRoleDefinitionObject
Wanneer u PowerShell toocreate een aangepaste beveiligingsrol gebruikt, kunt u helemaal opnieuw begint of gebruik een van de Hallo [ingebouwde rollen](role-based-access-built-in-roles.md) als uitgangspunt. Hallo-voorbeeld in deze sectie begint met een ingebouwde rol en past deze met meer bevoegdheden. Hallo kenmerken tooadd Hallo bewerken *acties*, *notActions*, of *scopes* die u wilt gebruiken en dan Hallo wijzigingen opslaan als een nieuwe rol.

Hallo volgende voorbeeld wordt gestart met de Hallo *Virtual Machine Contributor* rol en gebruikt die toocreate een aangepaste beveiligingsrol aangeroepen *virtuele Machine Operator*. de nieuwe rol Hallo verleent toegang tooall leesbewerkingen van *Microsoft.Compute*, *Microsoft.Storage*, en *Microsoft.Network* providers en verleent toegang tot bedrijfsbronnen toostart, opnieuw opstarten en virtuele machines bewaken. Hallo aangepaste rol kan worden gebruikt in twee abonnementen.

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Contributor"
$role.Id = $null
$role.Name = "Virtual Machine Operator"
$role.Description = "Can monitor and restart virtual machines."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/*/read")
$role.Actions.Add("Microsoft.Network/*/read")
$role.Actions.Add("Microsoft.Compute/*/read")
$role.Actions.Add("Microsoft.Compute/virtualMachines/start/action")
$role.Actions.Add("Microsoft.Compute/virtualMachines/restart/action")
$role.Actions.Add("Microsoft.Authorization/*/read")
$role.Actions.Add("Microsoft.Resources/subscriptions/resourceGroups/read")
$role.Actions.Add("Microsoft.Insights/alertRules/*")
$role.Actions.Add("Microsoft.Support/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e")
$role.AssignableScopes.Add("/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624")
New-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell-Get AzureRmRoleDefinition - schermafbeelding](./media/role-based-access-control-manage-access-powershell/2-new-azurermroledefinition.png)

### <a name="create-role-with-json-template"></a>Rol met JSON-sjabloon maken
Een JSON-sjabloon kan worden gebruikt als de brondefinitie Hallo voor Hallo aangepaste rol. Hallo volgende voorbeeld maakt u een aangepaste rol die leestoegang toostorage kunt rekenresources, toegang tot toosupport en voegt die rol tootwo abonnementen. Maak een nieuw bestand `C:\CustomRoles\customrole1.json` Hello voorbeeld te volgen. Hallo-Id moet worden ingesteld te`null` op het eerste rol maken als een nieuwe ID automatisch wordt gegenereerd. 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```
tooadd hello rol toohello abonnementen Hallo volgende PowerShell-opdracht uitvoeren:
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a>Een aangepaste rol wijzigen
Vergelijkbare toocreating een aangepaste beveiligingsrol, kunt u een bestaande aangepaste rol met behulp van Hallo PSRoleDefinitionObject of een JSON-sjabloon wijzigen.

### <a name="modify-role-with-psroledefinitionobject"></a>Rol met PSRoleDefinitionObject wijzigen
Hallo eerst met behulp van een aangepaste beveiligingsrol toomodify `Get-AzureRmRoleDefinition` tooretrieve Hallo roldefinitie opdracht. Ten tweede aanbrengen Hallo gewenst toohello roldefinitie. Gebruik tot slot Hallo `Set-AzureRmRoleDefinition` opdracht toosave Hallo roldefinitie gewijzigd.

Hallo volgende voorbeeld wordt toegevoegd Hallo `Microsoft.Insights/diagnosticSettings/*` bewerking toohello *virtuele Machine Operator* aangepaste rol.

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - schermafbeelding](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

Hallo volgende voorbeeld wordt een Azure-abonnement toohello toewijsbare bereiken Hallo *virtuele Machine Operator* aangepaste rol.

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - schermafbeelding](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a>Rol met JSON-sjabloon wijzigen
Hallo vorige JSON-sjabloon gebruikt, kunt u eenvoudig een bestaande aangepaste rol tooadd wijzigen of verwijderen van acties. Hallo JSON-sjabloon bijwerken en toevoegen van Hallo lezen actie die netwerken, zoals wordt weergegeven in het volgende voorbeeld Hallo. Hallo-definities op Hallo sjabloon zijn niet cumulatief toegepaste tooan bestaande definitie, wat betekent dat die rol Hallo verschijnt precies zoals u in de sjabloon Hallo opgeven. U moet ook tooupdate Hallo-Id-veld met Hallo Hallo rol-ID. Als u niet zeker weet wat deze waarde is, kunt u Hallo `Get-AzureRmRoleDefinition` cmdlet tooget deze informatie.

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```

tooupdate hello bestaande rol, Hallo volgende PowerShell-opdracht uitvoeren:
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a>Een aangepaste rol verwijderen
een aangepaste beveiligingsrol toodelete gebruiken Hallo `Remove-AzureRmRoleDefinition` opdracht.

Hallo volgende voorbeeld wordt verwijderd Hallo *virtuele Machine Operator* aangepaste rol.

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - schermafbeelding](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a>Lijst met aangepaste rollen
toolist hello functies die beschikbaar zijn voor toewijzing op een scope gebruiken Hallo `Get-AzureRmRoleDefinition` opdracht.

Hallo volgende voorbeeld worden alle functies die beschikbaar voor toewijzing in Hallo geselecteerde abonnement zijn.

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell-Get AzureRmRoleDefinition - schermafbeelding](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

Hallo in Hallo voorbeeld te volgen, *virtuele Machine Operator* aangepaste rol is niet beschikbaar in Hallo *Production4* abonnement omdat dat abonnement niet Hallo  **AssignableScopes** van Hallo-rol.

![RBAC PowerShell-Get AzureRmRoleDefinition - schermafbeelding](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a>Zie ook
* [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

