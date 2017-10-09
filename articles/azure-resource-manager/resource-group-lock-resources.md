---
title: aaaLock Azure-resources tooprevent wijzigingen | Microsoft Docs
description: "Voorkomen dat gebruikers bijwerken of verwijderen van essentiële Azure-resources door het toepassen van een vergrendeling voor alle gebruikers en rollen."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a>Vergrendelen van resources tooprevent onverwachte wijzigingen 
Als beheerder moet u mogelijk toolock een abonnement, resourcegroep of resource tooprevent andere gebruikers in uw organisatie per ongeluk worden kritieke bronnen wijzigen of verwijderen. U kunt instellen Hallo vergrendeling te**CanNotDelete** of **ReadOnly**. 

* **CanNotDelete** betekent geautoriseerde gebruikers kunnen nog steeds lezen en wijzigen van een resource, maar ze Hallo resource niet verwijderen. 
* **Alleen-lezen** betekent geautoriseerde gebruikers kunnen een resource lezen, maar ze niet verwijderen of bijwerken van de bron Hallo. Vergelijkbare toorestricting alle gebruikers toohello machtigingen verleend door Hallo geautoriseerd voor het toepassen van deze vergrendeling is **lezer** rol. 

## <a name="how-locks-are-applied"></a>Hoe vergrendelingen worden toegepast

Wanneer u een vergrendeling op een bovenliggend bereik toepast, alle resources binnen dat bereik Hallo overnemen dezelfde vergrendelen. Hallo vergrendeling overnemen zelfs resources die u later toevoegen van bovenliggende Hallo. de meest beperkende vergrendeling Hallo in Hallo overname voorrang.

In tegenstelling tot rollen gebaseerd toegangsbeheer kunt u management vergrendelingen tooapply een beperking voor alle gebruikers en -functies gebruiken. toolearn over het instellen van machtigingen voor gebruikers en rollen, Zie [toegangsbeheer op basis van rollen in Azure](../active-directory/role-based-access-control-configure.md).

Vergrendelingen van Resource Manager alleen toooperations die ontstaan in vlak voor Hallo die uit operations verzonden bestaat toepassen`https://management.azure.com`. Hallo vergrendelingen beperken niet hoe resources hun eigen functies uitvoeren. Wijzigingen in de resourcedefinitie zijn beperkt, maar de bewerkingen van resources zijn niet beperkt. Bijvoorbeeld, een vergrendeling van het kenmerk alleen-lezen voor een SQL-Database, voorkomt u dat verwijderen of wijzigen Hallo-database, maar het verhindert niet dat u maken, bijwerken of verwijderen van gegevens in het Hallo-database. Gegevenstransacties worden toegestaan, omdat deze bewerkingen niet te worden verzonden`https://management.azure.com`.

Toepassen van **ReadOnly** toounexpected resultaten kan leiden, omdat bepaalde bewerkingen die lijkt lezen bewerkingen daadwerkelijk extra acties vereist. Bijvoorbeeld, brengen een **ReadOnly** vergrendeling van een opslagaccount wordt voorkomen dat alle gebruikers aanbieding Hallo sleutels. Hallo lijst sleutels opnieuw wordt verwerkt door een POST-aanvraag omdat Hallo geretourneerd sleutels zijn beschikbaar voor schrijfbewerkingen. Voor een ander voorbeeld plaatsen van een **ReadOnly** vergrendelen op een App Service-bron wordt voorkomen dat Visual Studio Server Explorer weergeven van bestanden voor de resource Hallo omdat die interactie voor toegang voor schrijven vereist.

## <a name="who-can-create-or-delete-locks-in-your-organization"></a>Wie kunt maken of verwijderen van vergrendelingen in uw organisatie
management-vergrendelingen toocreate of verwijderen, moet u beschikken te`Microsoft.Authorization/*` of `Microsoft.Authorization/locks/*` acties. Hallo ingebouwde rollen, alleen **eigenaar** en **beheerder voor gebruikerstoegang** deze acties worden verleend.

## <a name="portal"></a>Portal
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a>Template
Hallo volgende voorbeeld ziet u een sjabloon die wordt gemaakt van een vergrendeling op een opslagaccount. Hallo storage-account op welke tooapply Hallo vergrendeling is opgegeven als parameter. Hello naam Hallo vergrendeling wordt gemaakt door Hallo resourcenaam met cookievalidatie **/Microsoft.Authorization/** en de naam van de vergrendeling hello, in dit geval Hallo **myLock**.

Hallo type dat is opgegeven is specifiek toohello resourcetype. Voor opslag, stelt u Hallo type too"Microsoft.Storage/storageaccounts/providers/locks'.

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a>PowerShell
U vergrendeling resources met Azure PowerShell geïmplementeerd met behulp van Hallo [nieuw AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) opdracht.

een resource toolock bieden Hallo-naam van Hallo resource, het resourcetype en de naam van de resourcegroep.

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

een resourcegroep toolock bieden Hallo-naam van de resourcegroep Hallo.

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

informatie over een vergrendeling, gebruik tooget [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock). tooget alle Hallo vergrendelingen in uw abonnement gebruiken:

```powershell
Get-AzureRmResourceLock
```

tooget alle vergrendelingen voor een bron gebruiken:

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

tooget gebruiken voor alle vergrendelingen voor een resourcegroep:

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

Azure PowerShell biedt andere opdrachten voor vergrendelingen werken, zoals [Set AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate een vergrendeling en [verwijderen AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete een vergrendeling.

## <a name="azure-cli"></a>Azure CLI

U vergrendeling resources met Azure CLI geïmplementeerd met behulp van Hallo [az vergrendeling maken](/cli/azure/lock#create) opdracht.

een resource toolock bieden Hallo-naam van Hallo resource, het resourcetype en de naam van de resourcegroep.

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

een resourcegroep toolock bieden Hallo-naam van de resourcegroep Hallo.

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

informatie over een vergrendeling, gebruik tooget [az vergrendeling lijst](/cli/azure/lock#list). tooget alle Hallo vergrendelingen in uw abonnement gebruiken:

```azurecli
az lock list
```

tooget alle vergrendelingen voor een bron gebruiken:

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

tooget gebruiken voor alle vergrendelingen voor een resourcegroep:

```azurecli
az lock list --resource-group exampleresourcegroup
```

Azure CLI biedt andere opdrachten voor vergrendelingen werken, zoals [az vergrendeling update](/cli/azure/lock#update) tooupdate een vergrendeling en [az vergrendeling verwijderen](/cli/azure/lock#delete) toodelete een vergrendeling.

## <a name="rest-api"></a>REST API
U kunt vergrendelen geïmplementeerde resources Hello [REST-API voor beheer van vergrendelingen](https://docs.microsoft.com/rest/api/resources/managementlocks). Hallo REST-API kunt u toocreate vergrendelingen worden verwijderd en informatie ophalen over bestaande vergrendelingen.

toocreate een vergrendeling uitvoeren:

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

Hallo-scope wordt mogelijk een abonnement, resourcegroep of resource. Hallo-vergrendelingsnaam is elke gewenste toocall Hallo vergrendelen. Gebruik voor de api-versie **01-01-2015**.

Hallo-aanvraag bevatten een JSON-object waarmee Hallo-eigenschappen voor Hallo vergrendelen.

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het werken met resource vergrendelingen [vergrendeling omlaag Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)
* Zie toolearn over logisch indelen van uw resources [Using tags tooorganize uw resources](resource-group-using-tags.md)
* toochange welke resourcegroep een bron zich bevindt, Zie [verplaatsen resources toonew resourcegroep](resource-group-move-resources.md)
* U kunt beperkingen en conventies toepassen voor uw abonnement met aangepast beleid. Zie voor meer informatie [beleid toomanage resources en toegang beheren](resource-manager-policy.md).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).

