---
title: aaaAzure container register opslagplaatsen | Microsoft Docs
description: "Hoe toouse Azure Container register opslagplaatsen voor Docker-installatiekopieën"
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
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a>Maken van een persoonlijke Docker-container register hello Azure PowerShell gebruiken
Gebruik de opdrachten in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate een register container en beheren van de instellingen van uw Windows-computer. U kunt ook maken en beheren van container registers met Hallo [Azure-portal](container-registry-get-started-portal.md), Hallo [Azure CLI](container-registry-get-started-azure-cli.md), of programmatisch met Hallo Container register [REST-API](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Zie voor de achtergrond en concepten [Hallo overzicht](container-registry-intro.md)
* Zie voor een volledige lijst van ondersteunde cmdlets [register-Cmdlets voor Azure Container](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).


## <a name="prerequisites"></a>Vereisten
* **Azure PowerShell**: tooinstall en aan de slag met Azure PowerShell, Zie Hallo [installatie-instructies](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). Meld u bij de Azure-abonnement tooyour door te voeren `Login-AzureRMAccount`. Zie voor meer informatie [aan de slag met Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).
* **Resourcegroep**: maak eerst een [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) voordat u een containerregister maakt of gebruik een bestaande resourcegroep. Zorg ervoor dat Hallo resourcegroep bevindt zich in een locatie waar Hallo Container Registry-service is [beschikbaar](https://azure.microsoft.com/regions/services/). een resourcegroep met Azure PowerShell toocreate Zie [Hallo PowerShell-referentie](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).
* **Storage-account** (optioneel): Maak een standaard Azure [opslagaccount](../storage/common/storage-introduction.md) tooback Hallo container register in Hallo dezelfde locatie. Als u een opslagaccount niet opgeven bij het maken van een register met `New-AzureRMContainerRegistry`, Hallo opdracht maakt u een voor u. toocreate een opslag-account met behulp van PowerShell, raadpleegt u [Hallo PowerShell-referentie](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount). Premium-opslag wordt momenteel niet ondersteund.
* **Service-principal** (optioneel): wanneer u een register met PowerShell maakt, standaard het is niet ingesteld voor toegang. Afhankelijk van uw behoeften kunt u een bestaande Azure Active Directory service principal tooa register toewijzen of maken en toewijzen van een nieuwe. U kunt ook van het register Hallo beheerder gebruikersaccount inschakelen. Zie Hallo secties verderop in dit artikel. Zie voor meer informatie over toegang tot het register, [verifiëren met Hallo container register](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Een containerregister maken
Voer Hallo `New-AzureRMContainerRegistry` opdracht toocreate een container-register.

> [!TIP]
> Geef bij het maken van een register een unieke domeinnaam op het hoogste niveau op, bestaande uit alleen letters en cijfers. naam van de Hallo register in Hallo voorbeelden is `MyRegistry`, maar vervangen door een unieke naam van uw eigen.
>
>

Hallo van de volgende opdracht maakt gebruik van Hallo minimale parameters toocreate container register `MyRegistry` in de resourcegroep Hallo `MyResourceGroup` in Hallo Zuid-centraal VS locatie:

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* `-StorageAccountName` is optioneel. Als dat niet is opgegeven, een opslagaccount is gemaakt met een naam die bestaan uit Hallo registernaam en een tijdstempel in Hallo opgegeven resourcegroep.

## <a name="assign-a-service-principal"></a>Een service-principal toewijzen
Gebruik PowerShell-opdrachten tooassign een Azure Active Directory [service-principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa register. Hallo service-principal in deze voorbeelden is toegewezen rol van eigenaar hello, maar u kunt toewijzen [andere rollen](../active-directory/role-based-access-control-configure.md) als u wilt.

### <a name="create-a-service-principal"></a>Een service-principal maken
In Hallo volgende opdracht, wordt een nieuwe service-principal gemaakt. Geef een sterk wachtwoord Hello `-Password` parameter.

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a>Een nieuwe of bestaande service-principal toewijzen
U kunt een nieuwe of een bestaande service-principal tooa register toewijzen. tooassign deze eigenaar rol toegang toohello register, uitvoeren van een opdracht vergelijkbare toohello voorbeeld te volgen:

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a>Meld u aan toohello register met Hallo service-principal
Na het toewijzen van Hallo service principal toohello register, kunt u zich aanmeldt met Hallo volgende opdracht:

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a>Beheerreferenties beheren
Er wordt automatisch een beheeraccount gemaakt voor elk containerregister. Dit account is standaard uitgeschakeld. Hallo volgende voorbeelden tonen PowerShell-opdrachten toomanage Hallo beheerdersreferenties voor de container-register.

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
* [Uw eerste installatiekopie met behulp van Docker CLI Hallo push](container-registry-get-started-docker-cli.md)
