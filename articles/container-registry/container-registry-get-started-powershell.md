---
title: Azure-container register opslagplaatsen | Microsoft Docs
description: "Het gebruik van Azure Container register-opslagplaatsen voor Docker-installatiekopieën"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 1e5d5ea5b1ec121fe008abc48178b1d58f540ce1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-powershell"></a>Maken van een persoonlijke Docker-container register met de Azure PowerShell
Gebruik de opdrachten in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) een register container maken en beheren van de instellingen van uw Windows-computer. U kunt ook maken en beheren van container registers met behulp van de [Azure-portal](container-registry-get-started-portal.md), wordt de [Azure CLI](container-registry-get-started-azure-cli.md), of programmatisch met het register van de Container [REST-API](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Zie [het overzicht](container-registry-intro.md) voor meer achtergrondinformatie en concepten
* Zie voor een volledige lijst van ondersteunde cmdlets [register-Cmdlets voor Azure Container](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).


## <a name="prerequisites"></a>Vereisten
* **Azure PowerShell**: wilt installeren en aan de slag met Azure PowerShell, Zie de [installatie-instructies](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). Meld u aan bij uw Azure-abonnement door `Login-AzureRMAccount` uit te voeren. Zie voor meer informatie [aan de slag met Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).
* **Resourcegroep**: maak eerst een [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) voordat u een containerregister maakt of gebruik een bestaande resourcegroep. De resourcegroep moet op een locatie staan waar de Container Registry-service [beschikbaar](https://azure.microsoft.com/regions/services/) is. Zie het maken van een resourcegroep met Azure PowerShell [de PowerShell-referentie](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).
* **Opslagaccount** (optioneel): maak een standaard-Azure-[opslagaccount](../storage/common/storage-introduction.md) om een back-up van het containerregister te maken op dezelfde locatie. Als u geen opslagaccount opgeeft bij het maken van een register met `New-AzureRMContainerRegistry`, maakt de opdracht er een. Zie het maken van een opslagaccount met behulp van PowerShell [de PowerShell-referentie](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount). Premium-opslag wordt momenteel niet ondersteund.
* **Service-principal** (optioneel): wanneer u een register met PowerShell maakt, standaard het is niet ingesteld voor toegang. Afhankelijk van uw behoeften kunt u een bestaand Azure Active Directory-service-principal toewijzen aan een register of maken en toewijzen van een nieuwe. U kunt ook kunt u een gebruikersaccount in het register beheerder inschakelen. Zie de gedeelten verderop in dit artikel. Bekijk voor meer informatie over registertoegang [Verifiëren met het containerregister](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Een containerregister maken
Voer de opdracht `New-AzureRMContainerRegistry` uit om een containerregister te maken.

> [!TIP]
> Geef bij het maken van een register een unieke domeinnaam op het hoogste niveau op, bestaande uit alleen letters en cijfers. De registernaam in de voorbeelden is `MyRegistry`, maar u hoort deze door uw eigen unieke naam te vervangen.
>
>

De volgende opdracht maakt gebruik van de minimale parameters om containerregister `MyRegistry` te maken in de resourcegroep `MyResourceGroup` in de locatie Zuid-centraal VS:

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* `-StorageAccountName` is optioneel. Als deze optie niet wordt opgegeven, wordt er een opslagaccount gemaakt in de opgegeven resourcegroep met een naam die bestaat uit de registernaam en een tijdstempel.

## <a name="assign-a-service-principal"></a>Een service-principal toewijzen
PowerShell-opdrachten gebruiken voor het toewijzen van een Azure Active Directory [service-principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) met een register. Aan de service-principal in deze voorbeelden is de rol Eigenaar toegewezen, maar u kunt ook [andere rollen](../active-directory/role-based-access-control-configure.md) toewijzen.

### <a name="create-a-service-principal"></a>Een service-principal maken
In de volgende opdracht, wordt een nieuwe service-principal gemaakt. Geef een sterk wachtwoord op voor de parameter `-Password`.

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a>Een nieuwe of bestaande service-principal toewijzen
U kunt een nieuwe of een bestaande service-principal toewijzen aan een register. Toe te wijzen eigenaar roltoegang aan het register, een opdracht die vergelijkbaar is met het volgende voorbeeld wordt uitgevoerd:

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-to-the-registry-with-the-service-principal"></a>Meld u aan met het register met de service-principal
Na het toewijzen van de service-principal in het register, kunt u aanmelden met de volgende opdracht:

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a>Beheerreferenties beheren
Er wordt automatisch een beheeraccount gemaakt voor elk containerregister. Dit account is standaard uitgeschakeld. De volgende voorbeelden tonen PowerShell-opdrachten voor het beheren van de beheerdersreferenties voor de container-register.

### <a name="obtain-admin-user-credentials"></a>Beheerreferenties ophalen
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Beheerder inschakelen voor een bestaand register
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Beheerder uitschakelen voor een bestaand register
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a>Volgende stappen
* [Uw eerste installatiekopie pushen met de Docker-CLI](container-registry-get-started-docker-cli.md)
