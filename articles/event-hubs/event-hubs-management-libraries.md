---
title: aaaAzure Event Hubs managementbibliotheken | Microsoft Docs
description: Event Hubs-naamruimten en entiteiten beheren vanaf .NET
services: event-hubs
cloud: na
documentationcenter: na
author: sethmanheim
manager: timlt
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: b7db0077f6f31397ae46e926c3c28630a157824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-management-libraries"></a>Event Hubs management-bibliotheken

Hallo Event Hubs managementbibliotheken kunnen richten op dynamische wijze Event Hubs-naamruimten en entiteiten. Hiermee kunnen complexe implementaties en berichtverzending, zodat u via een programma welke tooprovision entiteiten bepalen kunt. Deze bibliotheken zijn momenteel beschikbaar voor .NET.

## <a name="supported-functionality"></a>Ondersteunde functionaliteit

* Namespace maken, bijwerken, verwijderen
* Event Hubs maken, bijwerken, verwijderen
* Consumergroep maken, bijwerken, verwijderen

## <a name="prerequisites"></a>Vereisten

tooget gestart met behulp van Hallo Event Hubs management-bibliotheken, moet u verifiëren met Azure Active Directory (AAD). AAD vereist dat u verificatie uitvoeren als een service-principal die toegang tooyour Azure-resources biedt. Zie voor informatie over het maken van een service principal, een van deze artikelen:  

* [Gebruik hello Azure portal toocreate Active Directory-toepassing en service-principal die toegang bronnen tot](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Een service principal tooaccess-resources voor Azure PowerShell toocreate gebruiken](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Een service principal tooaccess-resources voor Azure CLI toocreate gebruiken](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

Deze zelfstudies beschikt u over een `AppId` (Client-ID), `TenantId`, en `ClientSecret` (verificatiesleutel), die allemaal worden gebruikt voor verificatie door Hallo management-bibliotheken. U moet hebben **eigenaar** machtigingen voor resourcegroep Hallo waarop toorun.

## <a name="programming-pattern"></a>Patroon programmering

Hallo patroon toomanipulate alle Event Hubs-bronnen, volgt een gemeenschappelijke protocol:

1. Verkrijgen van een token van AAD Hallo met `Microsoft.IdentityModel.Clients.ActiveDirectory` bibliotheek.
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. Hallo maken `EventHubManagementClient` object.
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. Set Hallo `CreateOrUpdate` parameters tooyour opgegeven waarden.
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. Hallo-aanroep uitvoeren.
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a>Volgende stappen
* [Voorbeeld van de .NET-management](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [Microsoft.Azure.Management.EventHub verwijzing](/dotnet/api/Microsoft.Azure.Management.EventHub) 
