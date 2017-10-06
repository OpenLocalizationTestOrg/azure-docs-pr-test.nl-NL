---
title: Toegangsbeheer op basis van aaaRole met REST - Azure AD | Microsoft Docs
description: Toegangsbeheer op basis van rollen met Hallo REST-API beheren
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a>Toegangsbeheer op basis van rollen met Hallo REST-API beheren
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Azure-CLI](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)

Op rollen gebaseerde toegangsbeheer (RBAC) in hello Azure-portal en Azure Resource Manager-API kunt u access tooyour abonnement en bronnen op een heel nauwkeurig beheren. Met deze functie kunt u toegang tot Active Directory-gebruikers, groepen of service-principals verlenen door toe te wijzen van sommige rollen toothem bij een bepaald bereik.

## <a name="list-all-role-assignments"></a>Lijst van alle roltoewijzingen
Een lijst met alle Hallo roltoewijzingen op Hallo opgegeven bereik en subscopes.

roltoewijzingen toolist, u moet de toegang te hebben`Microsoft.Authorization/roleAssignments/read` bewerking bij Hallo bereik. Alle Hallo ingebouwde rollen krijgen toegang toothis bewerking. Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).

### <a name="request"></a>Aanvraag
Gebruik Hallo **ophalen** methode Hello URI te volgen:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:

1. Vervang *{bereik}* met Hallo bereik waarvoor toolist Hallo roltoewijzingen. Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:

   * Abonnement: /subscriptions/ {abonnement-id}  
   * Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1  
   * Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Vervang *{api-versie}* met 2015-07-01.
3. Vervang *{filter}* met Hallo voorwaarde dat u wenst dat tooapply toofilter Hallo rol toewijzingslijst:

   * Lijst roltoewijzingen voor alleen Hallo opgegeven bereik, inclusief niet Hallo roltoewijzingen op subscopes:`atScope()`    
   * Roltoewijzingen lijst voor een specifieke gebruiker, groep of toepassing:`principalId%20eq%20'{objectId of user, group, or service principal}'`  
   * Lijst van roltoewijzingen voor een specifieke gebruiker, inclusief overgenomen van groepen |`assignedTo('{objectId of user}')`

### <a name="response"></a>Antwoord
Statuscode: 200

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a>Informatie ophalen over een roltoewijzing
Hiermee haalt u informatie over één roltoewijzing opgegeven Hallo rol toewijzing-id.

tooget informatie over een roltoewijzing, u moet de toegang te hebben`Microsoft.Authorization/roleAssignments/read` bewerking. Alle Hallo ingebouwde rollen krijgen toegang toothis bewerking. Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).

### <a name="request"></a>Aanvraag
Gebruik Hallo **ophalen** methode Hello URI te volgen:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:

1. Vervang *{bereik}* met Hallo bereik waarvoor toolist Hallo roltoewijzingen. Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:

   * Abonnement: /subscriptions/ {abonnement-id}  
   * Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1  
   * Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Vervang *{toewijzing-rol-id}* met Hallo GUID-id van de roltoewijzing Hallo.
3. Vervang *{api-versie}* met 2015-07-01.

### <a name="response"></a>Antwoord
Statuscode: 200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a>Een roltoewijzing maken
Een gebruikersrol maakt toewijzing op Hallo opgegeven bereik voor Hallo principal verlenen Hallo opgegeven rol opgegeven.

een roltoewijzing toocreate, u moet de toegang te hebben`Microsoft.Authorization/roleAssignments/write` bewerking. Hallo ingebouwde rollen, alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang toothis bewerking. Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).

### <a name="request"></a>Aanvraag
Gebruik Hallo **plaatsen** methode Hello URI te volgen:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:

1. Vervang *{bereik}* met Hallo bereik op die u toocreate Hallo roltoewijzingen wenst. Als u een roltoewijzing op een bovenliggend bereik maakt, alle onderliggende bereiken Hallo overgenomen dezelfde roltoewijzing. Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:

   * Abonnement: /subscriptions/ {abonnement-id}  
   * Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1   
   * Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Vervang *{toewijzing-rol-id}* met een nieuwe GUID die Hallo GUID-id van nieuwe roltoewijzing hello wordt.
3. Vervang *{api-versie}* met 2015-07-01.

Voor de aanvraagtekst hello, bieden Hallo waarden in de volgende indeling Hallo:

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| Elementnaam | Vereist | Type | Beschrijving |
| --- | --- | --- | --- |
| roleDefinitionId |Ja |Tekenreeks |Hallo-id van Hallo-rol. Hallo-indeling van het Hallo-id is:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}` |
| principalId |Ja |Tekenreeks |objectId hello Azure AD-principal (gebruiker, groep of service-principal) toowhich Hallo rol wordt toegewezen. |

### <a name="response"></a>Antwoord
Statuscode: 201

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a>Een roltoewijzing verwijderen
Een roltoewijzing bij Hallo verwijderen opgegeven bereik.

een roltoewijzing toodelete, hebt u toegang toohello `Microsoft.Authorization/roleAssignments/delete` bewerking. Hallo ingebouwde rollen, alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang toothis bewerking. Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).

### <a name="request"></a>Aanvraag
Gebruik Hallo **verwijderen** methode Hello URI te volgen:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:

1. Vervang *{bereik}* met Hallo bereik op die u toocreate Hallo roltoewijzingen wenst. Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:

   * Abonnement: /subscriptions/ {abonnement-id}  
   * Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1  
   * Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Vervang *{toewijzing-rol-id}* met Hallo roltoewijzings-id GUID.
3. Vervang *{api-versie}* met 2015-07-01.

### <a name="response"></a>Antwoord
Statuscode: 200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a>Lijst van alle rollen
Geeft een lijst van alle Hallo-functies die beschikbaar voor toewijzing op Hallo opgegeven zijn bereik.

toolist rollen, u moet de toegang te hebben`Microsoft.Authorization/roleDefinitions/read` bewerking bij Hallo bereik. Alle Hallo ingebouwde rollen krijgen toegang toothis bewerking. Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).

### <a name="request"></a>Aanvraag
Gebruik Hallo **ophalen** methode Hello URI te volgen:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:

1. Vervang *{bereik}* met Hallo bereik waarvoor toolist Hallo rollen. Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:

   * Abonnement: /subscriptions/ {abonnement-id}  
   * Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1  
   * Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Vervang *{api-versie}* met 2015-07-01.
3. Vervang *{filter}* met Hallo voorwaarde dat u wenst dat tooapply toofilter Hallo lijst met rollen:

   * Lijst met beschikbare rollen voor toewijzing op Hallo opgegeven bereik en een van de onderliggende bereiken:`atScopeAndBelow()`
   * Zoeken naar een rol met de exacte weergavenaam: `roleName%20eq%20'{role-display-name}'`. Hallo URL gecodeerde vorm van Hallo exacte weergavenaam van de rol hello gebruiken. Bijvoorbeeld:`$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |

### <a name="response"></a>Antwoord
Statuscode: 200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a>Informatie ophalen over een rol
Hiermee haalt u informatie over een enkele rol door Hallo rol definitie-id opgegeven. Zie informatie over één rol met de weergavenaam tooget [lijst van alle rollen](role-based-access-control-manage-access-rest.md#list-all-roles).

tooget informatie over een rol, u moet de toegang te hebben`Microsoft.Authorization/roleDefinitions/read` bewerking. Alle Hallo ingebouwde rollen krijgen toegang toothis bewerking. Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).

### <a name="request"></a>Aanvraag
Gebruik Hallo **ophalen** methode Hello URI te volgen:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:

1. Vervang *{bereik}* met Hallo bereik waarvoor toolist Hallo roltoewijzingen. Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:

   * Abonnement: /subscriptions/ {abonnement-id}  
   * Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1  
   * Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Vervang *{rol-definitie-id}* met Hallo GUID-id van de roldefinitie Hallo.
3. Vervang *{api-versie}* met 2015-07-01.

### <a name="response"></a>Antwoord
Statuscode: 200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a>Een aangepaste beveiligingsrol maken
Maak een aangepaste beveiligingsrol.

een aangepaste beveiligingsrol toocreate, u moet de toegang te hebben`Microsoft.Authorization/roleDefinitions/write` bewerking op alle Hallo `AssignableScopes`. Hallo ingebouwde rollen, alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang toothis bewerking. Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).

### <a name="request"></a>Aanvraag
Gebruik Hallo **plaatsen** methode Hello URI te volgen:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:

1. Vervang *{bereik}* Hello eerste *AssignableScope* van Hallo aangepaste rol. Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus.

   * Abonnement: /subscriptions/ {abonnement-id}  
   * Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1  
   * Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Vervang *{rol-definitie-id}* met een nieuwe GUID die Hallo GUID-id van nieuwe aangepaste rol hello wordt.
3. Vervang *{api-versie}* met 2015-07-01.

Voor de aanvraagtekst hello, bieden Hallo waarden in de volgende indeling Hallo:

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| Elementnaam | Vereist | Type | Beschrijving |
| --- | --- | --- | --- |
| naam |Ja |Tekenreeks |GUID-id van de aangepaste rol Hallo. |
| properties.roleName |Ja |Tekenreeks |Weergavenaam van de aangepaste rol Hallo. Maximale grootte 128 tekens. |
| Properties.Description |Nee |Tekenreeks |Beschrijving van aangepaste Hallo-rol. Maximale grootte 1024 tekens. |
| Properties.type |Ja |Tekenreeks |Stel te 'CustomRole'. |
| Properties.permissions.Actions |Ja |String] |Een matrix van actie tekenreeksen geven Hallo operations verleend door Hallo aangepaste rol. |
| properties.permissions.notActions |Nee |String] |Een matrix met actie tekenreeksen Hallo operations tooexclude van Hallo-bewerkingen die zijn verleend door de aangepaste rol Hallo opgeven. |
| properties.assignableScopes |Ja |String] |Een matrix van bereiken in welke Hallo aangepaste rol kan worden gebruikt. |

### <a name="response"></a>Antwoord
Statuscode: 201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a>Bijwerken van een aangepaste rol
Een aangepaste rol wijzigen.

een aangepaste beveiligingsrol toomodify, u moet de toegang te hebben`Microsoft.Authorization/roleDefinitions/write` bewerking op alle Hallo `AssignableScopes`. Hallo ingebouwde rollen, alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang toothis bewerking. Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).

### <a name="request"></a>Aanvraag
Gebruik Hallo **plaatsen** methode Hello URI te volgen:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:

1. Vervang *{bereik}* Hello eerste *AssignableScope* van Hallo aangepaste rol. Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:

   * Abonnement: /subscriptions/ {abonnement-id}  
   * Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1  
   * Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Vervang *{rol-definitie-id}* met Hallo GUID-id van de aangepaste rol Hallo.
3. Vervang *{api-versie}* met 2015-07-01.

Voor de aanvraagtekst hello, bieden Hallo waarden in de volgende indeling Hallo:

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| Elementnaam | Vereist | Type | Beschrijving |
| --- | --- | --- | --- |
| naam |Ja |Tekenreeks |GUID-id van de aangepaste rol Hallo. |
| properties.roleName |Ja |Tekenreeks |Weergavenaam van Hallo bijgewerkt aangepaste rol. |
| Properties.Description |Nee |Tekenreeks |Beschrijving van Hallo bijgewerkt aangepaste rol. |
| Properties.type |Ja |Tekenreeks |Stel te 'CustomRole'. |
| Properties.permissions.Actions |Ja |String] |Een matrix met actie tekenreeksen geven Hallo operations toowhich Hallo bijgewerkt aangepaste rol verleent toegang. |
| properties.permissions.notActions |Nee |String] |Een matrix van actie tekenreeksen geven Hallo operations tooexclude van welke Hallo aangepaste rol verleent bijgewerkt Hallo-bewerkingen. |
| properties.assignableScopes |Ja |String] |Een matrix van bereiken in welke Hallo bijgewerkte aangepaste rol kan worden gebruikt. |

### <a name="response"></a>Antwoord
Statuscode: 201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a>Een aangepaste rol verwijderen
Een aangepaste rol verwijderen.

een aangepaste beveiligingsrol toodelete, u moet de toegang te hebben`Microsoft.Authorization/roleDefinitions/delete` bewerking op alle Hallo `AssignableScopes`. Hallo ingebouwde rollen, alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang toothis bewerking. Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).

### <a name="request"></a>Aanvraag
Gebruik Hallo **verwijderen** methode Hello URI te volgen:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:

1. Vervang *{bereik}* met Hallo-bereik dat u wenst dat toodelete Hallo roldefinitie. Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:

   * Abonnement: /subscriptions/ {abonnement-id}  
   * Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1  
   * Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Vervang *{rol-definitie-id}* met Hallo GUID roldefinitie-id van de aangepaste rol Hallo.
3. Vervang *{api-versie}* met 2015-07-01.

### <a name="response"></a>Antwoord
Statuscode: 200

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
