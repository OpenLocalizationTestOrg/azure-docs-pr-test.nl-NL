---
title: App Service API Apps-metagegevens voor het genereren van code voor het opsporen en | Microsoft Docs
description: Meer informatie over hoe API-Apps in Azure App Service Swagger-metagegevens gebruiken ter bevordering van de API-detectie en genereren van code.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: c7f8e33a-61cc-486f-89df-4a97dc3c71d4
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: alkarche
ms.openlocfilehash: 800bb9df9b957bec2c80abb3edefbaf354b549ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a>App Service API Apps-metagegevens voor de API-detectie en genereren van code
Ondersteuning voor [Swagger 2.0](http://swagger.io/) API-metagegevens is ingebouwd in App Service API-Apps. U hoeft niet te gebruiken van Swagger, maar als u deze gebruikt, kunt u profiteren van API Apps-functies die detectie en het verbruik van vereenvoudigen.   

## <a name="swagger-endpoint"></a>Swagger-eindpunt
U kunt een eindpunt met Swagger 2.0 JSON-metagegevens voor een API-app in een eigenschap van de API-app opgeven. Het eindpunt mag ten opzichte van de basis-URL van de API-app of een absolute URL zijn. Absolute URL's kunnen verwijzen buiten de API-app. 

Veel downstream-clients (voor bijvoorbeeld codegeneratie voor Visual Studio en PowerApps 'API toevoegen' stroom), de URL moet openbaar toegankelijk (niet beveiligd door een gebruiker of service-verificatie). Dit betekent dat als u App Service-verificatie gebruikt en beschikbaar wilt maken van de API-definitie van uw app zelf, u verificatieoptie waarmee anoniem verkeer moet naar uw API bereiken gebruiken. Zie voor meer informatie [verificatie en autorisatie voor API-Apps van App Service](app-service-api-authentication.md).

### <a name="portal-blade"></a>Portalblade
In de [Azure-portal](https://portal.azure.com/) de eindpunt-URL kan worden weergegeven en gewijzigd op de **API-definitie** blade.

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a>Azure Resource Manager-eigenschap
U kunt ook de URL van de API-definitie voor een API-app configureren met behulp van [Resource Explorer](https://resources.azure.com/) of [Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-authoring-templates.md) in opdrachtregelhulpprogramma's zoals [Azure PowerShell](/powershell/azureps-cmdlets-docs)en de [Azure CLI](../cli-install-nodejs.md). 

In **Resource Explorer**, gaat u naar **abonnementen > {uw abonnement} > resourceGroups > {uw resourcegroep} > providers > Microsoft.Web > sites > {uw site} > config > web** , en u ziet de `apiDefinition` eigenschap:

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

Voor een voorbeeld van een Azure Resource Manager-sjabloon die u stelt de `apiDefinition` eigenschap, open de [bestand azuredeploy.json in de voorbeeldtoepassing takenlijst](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Zoek de sectie met de sjabloon die op de bovenstaande JSON-voorbeeld lijkt.

### <a name="default-value"></a>Standaardwaarde
Wanneer u Visual Studio gebruikt voor het maken van een API-app, het eindpunt van de API-definitie automatisch ingesteld op de basis-URL van de API-app plus `/swagger/docs/v1`. Dit is de standaard-URL die de [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet-pakket gebruikt om te dienen als dynamisch gegenereerde Swagger-metagegevens voor een ASP.NET Web API-project. 

## <a name="code-generation"></a>Codegeneratie
Een van de voordelen van de integratie van Swagger in Azure API-apps is het automatisch genereren van code. Gegenereerde clientklassen maken het gemakkelijker code te schrijven die een API-app aanroepen.

U kunt genereren van clientcode voor een API-app met behulp van Visual Studio of vanaf de opdrachtregel. Zie voor meer informatie over het genereren van clientklassen in Visual Studio voor een ASP.NET Web API-project [aan de slag met API-Apps en ASP.NET](app-service-api-dotnet-get-started.md#codegen). Voor informatie over hoe u kunt dit doen vanaf de opdrachtregel voor alle ondersteunde talen, Zie het Leesmij-bestand van de [Azure/autorest](https://github.com/azure/autorest) opslagplaats op GitHub.com.

## <a name="next-steps"></a>Volgende stappen
Zie voor een stapsgewijze zelfstudie die u bij het maken begeleidt, implementeren en gebruiken van een API-app [aan de slag met API-Apps in Azure App Service](app-service-api-dotnet-get-started.md).

Als u Azure API Management met API-Apps gebruikt, kunt u Swagger-metagegevens importeren van uw API in API Management. Zie voor meer informatie [het importeren van de definitie van een API met bewerkingen in Azure API Management](../api-management/api-management-howto-import-api.md). 

