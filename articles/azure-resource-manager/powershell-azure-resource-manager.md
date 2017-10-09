---
title: aaaManage Azure oplossingen met PowerShell | Microsoft Docs
description: Gebruik Azure PowerShell en Resource Manager toomanage uw resources.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a>Resources beheren met Azure PowerShell en Resource Manager
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md)
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [REST API](resource-manager-rest-api.md)
>
>

In dit artikel leert u hoe toomanage uw oplossingen met Azure PowerShell en Azure Resource Manager. Als u niet bekend met Resource Manager, Zie [overzicht van Resource Manager](resource-group-overview.md). Dit onderwerp richt zich op beheertaken. U gaat het volgende doen:

1. Een resourcegroep maken
2. Een resourcegroep voor resource toohello toevoegen
3. Een label toohello resource toevoegen
4. Een query uitvoeren op basis van namen of labelwaarden resources
5. Toepassen en verwijderen van een vergrendeling op Hallo resource
6. Verwijderen van een resourcegroep

In dit artikel wordt niet weergegeven hoe toodeploy een Resource Manager sjabloon tooyour abonnement. Zie voor die informatie [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy.md).

## <a name="get-started-with-azure-powershell"></a>Aan de slag met Azure PowerShell

Als u Azure PowerShell nog niet hebt geïnstalleerd, raadpleegt u [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

Als u Azure PowerShell hebt geïnstalleerd in de afgelopen hello, maar hebben niet het onlangs bijgewerkt, Overweeg de installatie van de meest recente versie Hallo. U kunt bijwerken Hallo-versie via Hallo dezelfde manier waarop u tooinstall deze. Als u Hallo Web Platform Installer gebruikt, bijvoorbeeld opnieuw te starten en zoekt u een update.

uw versie van hello Azure-Resources-module, gebruikt u toocheck Hallo volgende cmdlet:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

In dit onderwerp is bijgewerkt voor versie 3.3.0. Als u een eerdere versie hebt, uw ervaring mogelijk niet overeen met Hallo stappen in dit onderwerp. Zie voor documentatie over cmdlets in deze versie Hallo [AzureRM.Resources Module](/powershell/module/azurerm.resources).

## <a name="log-in-tooyour-azure-account"></a>Meld u bij tooyour Azure-account
Voordat u aan uw oplossing werkt, moet u tooyour account aanmelden.

toolog in tooyour Azure-account gebruiken Hallo **Login-AzureRmAccount** cmdlet.

```powershell
Login-AzureRmAccount
```

Hallo-cmdlet wordt u gevraagd om de aanmeldingsreferenties Hallo voor uw Azure-account. Na het aanmelden, downloadt het instellingen van uw account, zodat ze beschikbaar tooAzure PowerShell.

Hallo cmdlet retourneert informatie over uw account en Hallo abonnement toouse voor Hallo taken.

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

Als u meer dan één abonnement hebt, kunt u een ander abonnement tooa overschakelen. Eerst gaan we kijken alle Hallo abonnementen voor uw account.

```powershell
Get-AzureRmSubscription
```

Het resultaat van ingeschakelde en uitgeschakelde abonnementen.

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

tooswitch tooa ander abonnement, de naam van een abonnement Hallo voorzien van Hallo **Set-AzureRmContext** cmdlet.

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a>Een resourcegroep maken
Voordat u een abonnement van resources tooyour implementeert, moet u een resourcegroep die Hallo resources bevat.

een resourcegroep toocreate gebruiken Hallo **New-AzureRmResourceGroup** cmdlet. Hallo-opdracht gebruikt Hallo **naam** parameter toospecify een naam voor de resourcegroep Hallo en Hallo **locatie** parameter toospecify de locatie.

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

Hallo-uitvoer is in de volgende indeling Hallo:

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

Als u later nodig tooretrieve Hallo resourcegroep hebt, gebruikt u Hallo volgende cmdlet:

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

tooget alle resourcegroepen in uw abonnement Hallo, geen naam opgeeft:

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a>Toevoegen van bronnen tooa resourcegroep
een resourcegroep voor resource toohello tooadd, kunt u Hallo **nieuw AzureRmResource** cmdlet of een cmdlet die specifieke toohello type resource dat u wilt maken (zoals **nieuw AzureRmStorageAccount**). U vindt het misschien gemakkelijker toouse een cmdlet die specifieke tooa brontype is omdat deze parameters op voor het Hallo-eigenschappen die nodig zijn voor de nieuwe resource Hallo bevat. toouse **nieuw AzureRmResource**, moet u alle Hallo eigenschappen tooset zonder te worden gevraagd ze weten.

Echter, het toevoegen van een resource via cmdlets kan veroorzaken toekomstige verwarring omdat Hallo nieuwe resource niet in een Resource Manager-sjabloon bestaat. Microsoft raadt het Hallo-infrastructuur voor uw Azure oplossing definiëren in een Resource Manager-sjabloon. Sjablonen kunnen u tooreliably en uw oplossing herhaaldelijk implementeren. Voor dit onderwerp, hebt u een opslagaccount met een PowerShell-cmdlet, maar later het genereren van een sjabloon uit de resourcegroep.

Hallo volgende cmdlet maakt een opslagaccount. In plaats van Hallo-naam wordt weergegeven in voorbeeld hello, Geef een unieke naam voor het Hallo-opslagaccount. Hallo naam moet tussen 3 en 24 tekens lang zijn en alleen cijfers en kleine letters gebruiken. Als u Hallo-naam wordt weergegeven in Hallo-voorbeeld gebruikt, ontvangt u een fout opgetreden omdat deze naam al gebruikt wordt.

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

Als u later nodig tooretrieve deze bron hebt, gebruikt u Hallo volgende cmdlet:

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a>Een label toevoegen

Labels kunnen u tooorganize uw resources op basis van toodifferent eigenschappen. Bijvoorbeeld wellicht hebt u verschillende resources in verschillende resourcegroepen die deel uitmaken van toohello dezelfde afdeling. U kunt een afdeling tag en waarde toothose resources toomark toepassen als toohello uitmaken van dezelfde categorie. Of u kunt markeren of een resource wordt gebruikt in een productie- of testomgeving. In dit onderwerp leert u labels tooonly één resource toepassen, maar in uw omgeving is het meest waarschijnlijke zinvol tooapply tags tooall uw resources.

Hallo cmdlet na geldt twee labels tooyour storage-account:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

Labels zijn als een enkel object bijgewerkt. tooadd een tag tooa bron die reeds labels bevat, worden eerst Hallo bestaande labels opgehaald. Hallo nieuwe tag toohello-object met bestaande Hallo-tags toevoegen en alle Hallo labels toohello resource pas.

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a>Zoeken naar resources

Gebruik Hallo **zoeken AzureRmResource** cmdlet tooretrieve bronnen voor verschillende zoekcriteria.

* een resource met de naam, tooget bieden Hallo **ResourceNameContains** parameter:

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* tooget alle Hallo resources in een resourcegroep bieden Hallo **ResourceGroupNameContains** parameter:

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* tooget alle Hallo resources met een naam en waarde, bieden Hallo **TagName** en **TagValue** parameters:

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* tooall hello resources met een bepaald brontype bieden Hallo **ResourceType** parameter:

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a>Vergrendelen van een resource

Wanneer u ervoor dat een essentiële resource niet per ongeluk is verwijderd of gewijzigd toomake moet, van toepassing een vergrendeling toohello resource. U kunt opgeven dat ofwel een **CanNotDelete** of **ReadOnly**.

management-vergrendelingen toocreate of verwijderen, moet u beschikken te`Microsoft.Authorization/*` of `Microsoft.Authorization/locks/*` acties. Van de ingebouwde rollen hello, worden alleen de eigenaar en de beheerder voor gebruikerstoegang die acties verleend.

een vergrendeling tooapply gebruik Hallo volgende cmdlet:

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

worden Hallo vergrendelde bron in het voorgaande voorbeeld Hallo kan niet verwijderd totdat Hallo vergrendeling wordt verwijderd. een vergrendeling tooremove gebruiken:

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Zie voor meer informatie over de instelling vergrendelingen [resources met Azure Resource Manager vergrendelen](resource-group-lock-resources.md).

## <a name="remove-resources-or-resource-group"></a>Verwijder resources of resourcegroep
U kunt een resource of resourcegroep verwijderen. Wanneer u een resourcegroep verwijdert, verwijdert u ook alle Hallo resources in die resourcegroep.

* een bron van de resourcegroep hello, gebruik Hallo toodelete **verwijderen AzureRmResource** cmdlet. Deze cmdlet Hallo resource wordt verwijderd, maar biedt niet Hallo resourcegroep verwijderen.

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* toodelete een resourcegroep en alle bijbehorende resources gebruiken Hallo **Remove-AzureRmResourceGroup** cmdlet.

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

Voor beide cmdlets, wordt u gevraagd tooconfirm dat u tooremove Hallo resource of resourcegroep wenst. Als wordt Hallo bewerking Hallo resource of resourcegroep is verwijderd, retourneert **True**.

## <a name="run-resource-manager-scripts-with-azure-automation"></a>Resource Manager-scripts uitvoeren met Azure Automation

Dit onderwerp leest u hoe tooperform basisbewerkingen op uw resources met Azure PowerShell. Voor meer geavanceerde scenario's voor beheer, u doorgaans wilt toocreate een script en script opnieuw naar behoefte of volgens een schema. [Azure Automation](../automation/automation-intro.md) biedt een manier voor u tooautomate veelgebruikte scripts waarmee uw Azure-oplossingen kunt beheren.

Hallo volgende onderwerpen bevatten informatie over hoe toouse Azure Automation, Resource Manager en PowerShell tooeffectively beheertaken uitvoeren:

- Zie voor meer informatie over het maken van een runbook [Mijn eerste PowerShell-runbook](../automation/automation-first-runbook-textual-powershell.md).
- Zie voor meer informatie over het werken met galerieën scripts [galerieën Runbook en de module voor Azure Automation](../automation/automation-runbook-gallery.md).
- Zie voor runbooks die starten en stoppen van virtuele machines, [Azure Automation-scenario: labels met behulp van JSON-indeling toocreate een planning voor de virtuele machine van Azure opstarten en afsluiten](../automation/automation-scenario-start-stop-vm-wjson-tags.md).
- Zie voor runbooks die starten en stoppen van virtuele machines rustige uren, [starten/stoppen virtuele machines tijdens rustige uren oplossing in Automation](../automation/automation-solution-vm-management.md).

## <a name="next-steps"></a>Volgende stappen
* toolearn over het maken van Resource Manager-sjablonen, Zie [Azure Resource Manager-sjablonen ontwerpen](resource-group-authoring-templates.md).
* toolearn over het implementeren van sjablonen, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).
* U kunt bestaande resources tooa nieuwe resourcegroep verplaatsen. Zie voor voorbeelden [verplaatsen van Resources tooNew resourcegroep of abonnement](resource-group-move-resources.md).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).

