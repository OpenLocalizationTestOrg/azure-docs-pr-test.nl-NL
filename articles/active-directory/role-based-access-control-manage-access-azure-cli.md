---
title: aaaManage op rollen gebaseerde toegangsbeheer (RBAC) met Azure CLI | Microsoft Docs
description: Meer informatie over hoe toomanage op rollen gebaseerde toegangsbeheer (RBAC) Hello Azure opdrachtregelprogramma interface door functies van de aanbieding en rol acties en door het toewijzen van rollen toohello abonnement en de toepassing bereiken.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 3483ee01-8177-49e7-b337-4d5cb14f5e32
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 438418e5f6ee9b98908c9c264d516eb722a4e26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a>Toegangsbeheer op basis van rollen met hello Azure-opdrachtregelinterface beheren
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Azure-CLI](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)


In hello Azure-portal en Azure Resource Manager-API toomanage toegang tooyour abonnement en bronnen op een heel nauwkeurig kunt u rollen gebaseerd toegangsbeheer (RBAC). Met deze functie kunt u toegang tot Active Directory-gebruikers, groepen of service-principals verlenen door toe te wijzen van sommige rollen toothem bij een bepaald bereik.

Voordat u hello Azure-opdrachtregelinterface (CLI) toomanage RBAC gebruiken kunt, hebt u Hallo volgende vereisten:

* Azure CLI versie 0.8.8 of hoger. meest recente versie van tooinstall hello en koppel deze met uw Azure-abonnement Zie [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md).
* Azure Resource Manager in Azure CLI. Ga te[Using hello Azure CLI Hello Resource Manager](../xplat-cli-azure-resource-manager.md) voor meer informatie.

## <a name="list-roles"></a>Lijst met rollen
### <a name="list-all-available-roles"></a>Lijst van alle beschikbare rollen
toolist gebruiken voor alle beschikbare rollen:

        azure role list

Hallo volgende voorbeeld ziet u Hallo lijst met *alle beschikbare rollen*.

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Azure RBAC opdrachtregel - lijst van de functie van de azure - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a>Van Lijstacties van een rol
toolist hello acties van een functie, gebruiken:

    azure role show "<role name>"

Hallo volgende voorbeeld ziet u acties Hallo Hallo *Inzender* en *Virtual Machine Contributor* rollen.

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Azure RBAC opdrachtregel - functie van azure weergeven - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a>Lijst met toegang
### <a name="list-role-assignments-effective-on-a-resource-group"></a>Roltoewijzingen lijst effectieve op een resourcegroep
toolist hello roltoewijzingen die aanwezig zijn in een resourcegroep of gebruik:

    azure role assignment list --resource-group <resource group name>

Hallo in volgende voorbeeld ziet roltoewijzingen Hallo Hallo *pharma-verkoop-projecforcast* groep.

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Azure RBAC opdrachtregel - toewijzing-lijst per groep functie van azure - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a>Lijst roltoewijzingen voor een gebruiker
toolist hello roltoewijzingen voor een specifieke gebruiker en het Hallo-toewijzingen die zijn toegewezen tooa gebruikersgroepen, gebruiken:

    azure role assignment list --signInName <user email>

U ziet ook roltoewijzingen die zijn overgenomen van groepen doordat Hallo-opdracht:

    azure role assignment list --expandPrincipalGroups --signInName <user email>

Hallo volgende voorbeeld ziet u Hallo roltoewijzingen die worden verleend toohello  *sameert@aaddemo.com*  gebruiker. Dit omvat functies die rechtstreeks toohello gebruiker zijn toegewezen en functies die zijn overgenomen van groepen.

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Azure RBAC opdrachtregel - toewijzingslijst azure rol door gebruiker - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a>Toegang verlenen
toogrant toegang nadat u hebt aangegeven dat u wilt dat tooassign Hallo-rol, gebruiken:

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a>Een rol toogroup op Hallo abonnementsbereik toewijzen
een groep rol tooa bij Hallo abonnementsbereik, gebruik tooassign:

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

Hallo volgende voorbeeld wordt toegewezen Hallo *lezer* rol te*van Christine Koch Team* op Hallo *abonnement* bereik.

![RBAC Azure vanaf de opdrachtregel - azure roltoewijzing maken door de groep - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Een rol tooan toepassing in het bereik van Hallo abonnement toewijzen
een rol tooan toepassing bij Hallo abonnementsbereik, gebruik tooassign:

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

Hallo volgende voorbeeld verleent Hallo *Inzender* rol tooan *Azure AD* toepassing op Hallo abonnement selecteren.

 ![RBAC Azure vanaf de opdrachtregel - azure roltoewijzing maken door toepassing](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Een gebruiker van de rol tooa op Hallo resource groepsbereik toewijzen
een gebruiker van de rol tooa op Hallo resource groepsbereik gebruik tooassign:

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

Hallo volgende voorbeeld verleent Hallo *Virtual Machine Contributor* rol te *samert@aaddemo.com*  gebruiker op Hallo *Pharma-verkoop-ProjectForcast* resource groepsbereik.

![RBAC Azure vanaf de opdrachtregel - azure roltoewijzing maken door gebruiker - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Een groep rol tooa bij Hallo resource bereik worden toegewezen
een groep rol tooa bij Hallo resource bereik, gebruik tooassign:

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

Hallo volgende voorbeeld verleent Hallo *Virtual Machine Contributor* rol tooan *Azure AD* groep op een *subnet*.

![RBAC Azure vanaf de opdrachtregel - azure roltoewijzing maken door de groep - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a>Toegang verwijderen
een roltoewijzing tooremove gebruiken:

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

Hallo volgende voorbeeld wordt verwijderd Hallo *Virtual Machine Contributor* functietoewijzing uit Hallo  *sammert@aaddemo.com*  gebruiker op Hallo *Pharma-verkoop-ProjectForcast* resourcegroep.
de roltoewijzing Hallo verwijdert Hallo voorbeeld uit een groep op Hallo-abonnement.

![Azure RBAC opdrachtregel - azure-functie toewijzing delete - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a>Een aangepaste beveiligingsrol maken
een aangepaste beveiligingsrol toocreate gebruiken:

    azure role create --inputfile <file path>

Hallo volgende voorbeeld maakt u een aangepaste beveiligingsrol aangeroepen *virtuele Machine Operator*. Deze aangepaste rol verleent toegang tooall leesbewerkingen van *Microsoft.Compute*, *Microsoft.Storage*, en *Microsoft.Network* providers en verleent toegang tot bedrijfsbronnen toostart, opnieuw opstarten en virtuele machines bewaken. Deze aangepaste rol kan worden gebruikt in twee abonnementen. Dit voorbeeld wordt een JSON-bestand als invoer.

![JSON - aangepaste roldefinitie - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![RBAC Azure vanaf de opdrachtregel - azure-functie maken - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a>Een aangepaste rol wijzigen
een aangepaste beveiligingsrol toomodify Hallo voor het eerst gebruiken `azure role show` opdracht tooretrieve roldefinitie. Controleer vervolgens Hallo gewenste wijzigingen aan toohello rol-definitiebestand. Gebruik tot slot `azure role set` toosave Hallo roldefinitie gewijzigd.

    azure role set --inputfile <file path>

Hallo volgende voorbeeld wordt toegevoegd Hallo *Microsoft.Insights/diagnosticSettings/* bewerking toohello **acties**, en een Azure-abonnement toohello **AssignableScopes**van aangepaste rol van Hallo Operator van de virtuele Machine.

![JSON - wijzigen aangepaste roldefinitie - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Azure RBAC opdrachtregel - azure-functie set - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a>Een aangepaste rol verwijderen
een aangepaste beveiligingsrol toodelete Hallo voor het eerst gebruiken `azure role show` opdracht toodetermine hello **ID** van Hallo-rol. Gebruik vervolgens Hallo `azure role delete` opdracht toodelete Hallo rol door op te geven Hallo **ID**.

Hallo volgende voorbeeld wordt verwijderd Hallo *virtuele Machine Operator* aangepaste rol.

![Azure RBAC opdrachtregel - azure-functie delete - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a>Lijst met aangepaste rollen
toolist hello functies die beschikbaar zijn voor toewijzing op een scope gebruiken Hallo `azure role list` opdracht.

Hallo volgende opdracht geeft een lijst van alle functies die beschikbaar voor toewijzing in Hallo geselecteerde abonnement zijn.

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Azure RBAC opdrachtregel - lijst van de functie van de azure - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

Hallo in Hallo voorbeeld te volgen, *virtuele Machine Operator* aangepaste rol is niet beschikbaar in Hallo *Production4* abonnement omdat dat abonnement niet Hallo  **AssignableScopes** van Hallo-rol.

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Azure RBAC opdrachtregel - lijst met azure-functie voor aangepaste rollen - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

