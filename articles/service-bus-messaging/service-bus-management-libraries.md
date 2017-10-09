---
title: Service Bus-managementbibliotheken aaaAzure | Microsoft Docs
description: Service Bus-naamruimten en berichtentiteiten in .NET beheren.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 9e4ad91f22815ca0838e6e4647a3606109b2b441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-management-libraries"></a>Management-Service Bus-bibliotheken

Hello Azure Service Bus-management-bibliotheken kunnen richten op dynamische wijze Service Bus-naamruimten en entiteiten. Hiermee kunt u complexe implementaties en berichtverzending en maakt het mogelijk tooprogrammatically bepalen welke tooprovision entiteiten. Deze bibliotheken zijn momenteel beschikbaar voor .NET.

## <a name="supported-functionality"></a>Ondersteunde functionaliteit

* Namespace maken, bijwerken, verwijderen
* Wachtrijen maken, bijwerken, verwijderen
* Onderwerp maken, bijwerken, verwijderen
* Abonnement maken, bijwerken, verwijderen

## <a name="prerequisites"></a>Vereisten

tooget gestart met behulp van Hallo Service Bus-bibliotheken voor beheer, moet u zicht aanmeldt met hello Azure Active Directory (AAD)-service. AAD vereist dat u verificatie uitvoeren als een service-principal die toegang tooyour Azure-resources biedt. Zie voor informatie over het maken van een service principal, een van deze artikelen:  

* [Gebruik hello Azure portal toocreate Active Directory-toepassing en service-principal die toegang bronnen tot](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [Een service principal tooaccess-resources voor Azure PowerShell toocreate gebruiken](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Een service principal tooaccess-resources voor Azure CLI toocreate gebruiken](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

Deze zelfstudies beschikt u over een `AppId` (Client-ID), `TenantId`, en `ClientSecret` (verificatiesleutel), die allemaal worden gebruikt voor verificatie door Hallo management-bibliotheken. U moet hebben **eigenaar** machtigingen voor resourcegroep Hallo waarvoor u wenst dat toorun.

## <a name="programming-pattern"></a>Patroon programmering

Hallo patroon toomanipulate een Service Bus-resource een gemeenschappelijke protocol volgt:

1. Een token verkrijgen van Azure Active Directory met Hallo **Microsoft.IdentityModel.Clients.ActiveDirectory** bibliotheek.
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. Hallo maken `ServiceBusManagementClient` object.

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. Set Hallo `CreateOrUpdate` parameters tooyour opgegeven waarden.

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. Hallo-aanroep uitvoeren.

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a>Volgende stappen
* [Voorbeeld van .NET-management](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [Microsoft.Azure.Management.ServiceBus API-verwijzing](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
