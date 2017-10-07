---
title: aaaApp Service API Apps-metagegevens voor het genereren van code voor het opsporen en | Microsoft Docs
description: Informatie over hoe de Swagger-metagegevens toofacilitate API-detectie en genereren van code voor het gebruik van API-Apps in Azure App Service.
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
ms.openlocfilehash: b27e70b7dd6bd97f5b0b490b496320befe7442c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a>App Service API Apps-metagegevens voor de API-detectie en genereren van code
Ondersteuning voor [Swagger 2.0](http://swagger.io/) API-metagegevens is ingebouwd in App Service API-Apps. U hebt geen toouse Swagger, maar als u deze gebruikt, kunt u profiteren van API Apps-functies die detectie en het verbruik van vereenvoudigen.   

## <a name="swagger-endpoint"></a>Swagger-eindpunt
U kunt een eindpunt met Swagger 2.0 JSON-metagegevens voor een API-app in een eigenschap van het Hallo-API-app opgeven. Hallo-eindpunt kan relatief toohello basis-URL van de API-app hello of een absolute URL zijn. Absolute URL's kunnen verwijzen buiten Hallo API-app. 

Veel downstream-clients (voor bijvoorbeeld codegeneratie voor Visual Studio en PowerApps 'API toevoegen' stroom), Hallo URL moet openbaar toegankelijk (niet beveiligd door een gebruiker of service-verificatie). Dit betekent dat als u App Service-verificatie gebruikt en tooexpose Hallo API-definitie van binnen uw app zelf, moet u toouse verificatieoptie waarmee anoniem verkeer tooreach uw API. Zie voor meer informatie [verificatie en autorisatie voor API-Apps van App Service](app-service-api-authentication.md).

### <a name="portal-blade"></a>Portalblade
In Hallo [Azure-portal](https://portal.azure.com/) eindpunt-URL kan worden weergegeven en gewijzigd op Hallo Hallo **API-definitie** blade.

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a>Azure Resource Manager-eigenschap
U kunt ook Hallo API-definitie-URL voor een API-app configureren met behulp van [Resource Explorer](https://resources.azure.com/) of [Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-authoring-templates.md) in opdrachtregelhulpprogramma's zoals [Azure PowerShell](/powershell/azureps-cmdlets-docs)en Hallo [Azure CLI](../cli-install-nodejs.md). 

In **Resource Explorer**, gaat u te**abonnementen > {uw abonnement} > resourceGroups > {uw resourcegroep} > providers > Microsoft.Web > sites > {uw site} > config > web**, en u ziet Hallo `apiDefinition` eigenschap:

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

Voor een voorbeeld van een Azure Resource Manager-sjabloon die wordt ingesteld Hallo `apiDefinition` eigenschap, open Hallo [bestand azuredeploy.json in Hallo takenlijst voorbeeldtoepassing](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Hallo-sectie van het Hallo-sjabloon die op Hallo JSON-voorbeeld lijkt hierboven weergegeven vinden.

### <a name="default-value"></a>Standaardwaarde
Wanneer u Visual Studio toocreate een API-app gebruikt, Hallo API-definitie eindpunt toohello basis-URL van Hallo API-app plus automatisch ingesteld `/swagger/docs/v1`. Dit is standaard-URL voor Hallo die Hallo [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet-pakket gebruikt tooserve dynamisch gegenereerd Swagger-metagegevens voor een ASP.NET Web API-project. 

## <a name="code-generation"></a>Codegeneratie
Een van de voordelen van de integratie van Swagger in Azure API-apps Hallo is automatisch genereren van code. Gegenereerde clientklassen maken het gemakkelijker toowrite-code die een API-app aanroept.

U kunt genereren van clientcode voor een API-app met behulp van Visual Studio of vanuit de opdrachtregel Hallo. Zie voor meer informatie over hoe toogenerate client in Visual Studio voor een ASP.NET Web API-project klassen [aan de slag met API-Apps en ASP.NET](app-service-api-dotnet-get-started.md#codegen). Zie voor informatie over hoe toodo op Hallo opdracht regel voor alle ondersteunde talen Hallo Leesmij-bestand Hallo [Azure/autorest](https://github.com/azure/autorest) opslagplaats op GitHub.com.

## <a name="next-steps"></a>Volgende stappen
Zie voor een stapsgewijze zelfstudie die u bij het maken begeleidt, implementeren en gebruiken van een API-app [aan de slag met API-Apps in Azure App Service](app-service-api-dotnet-get-started.md).

Als u Azure API Management met API-Apps gebruikt, kunt u Swagger-metagegevens tooimport uw API in API Management. Zie voor meer informatie [hoe tooimport definitie van een API met bewerkingen in Azure API Management Hallo](../api-management/api-management-howto-import-api.md). 

