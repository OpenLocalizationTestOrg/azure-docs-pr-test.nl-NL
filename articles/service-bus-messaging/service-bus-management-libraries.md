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
# <a name="service-bus-management-libraries"></a><span data-ttu-id="5104d-103">Management-Service Bus-bibliotheken</span><span class="sxs-lookup"><span data-stu-id="5104d-103">Service Bus management libraries</span></span>

<span data-ttu-id="5104d-104">Hello Azure Service Bus-management-bibliotheken kunnen richten op dynamische wijze Service Bus-naamruimten en entiteiten.</span><span class="sxs-lookup"><span data-stu-id="5104d-104">hello Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="5104d-105">Hiermee kunt u complexe implementaties en berichtverzending en maakt het mogelijk tooprogrammatically bepalen welke tooprovision entiteiten.</span><span class="sxs-lookup"><span data-stu-id="5104d-105">This enables complex deployments and messaging scenarios, and makes it possible tooprogrammatically determine what entities tooprovision.</span></span> <span data-ttu-id="5104d-106">Deze bibliotheken zijn momenteel beschikbaar voor .NET.</span><span class="sxs-lookup"><span data-stu-id="5104d-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="5104d-107">Ondersteunde functionaliteit</span><span class="sxs-lookup"><span data-stu-id="5104d-107">Supported functionality</span></span>

* <span data-ttu-id="5104d-108">Namespace maken, bijwerken, verwijderen</span><span class="sxs-lookup"><span data-stu-id="5104d-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="5104d-109">Wachtrijen maken, bijwerken, verwijderen</span><span class="sxs-lookup"><span data-stu-id="5104d-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="5104d-110">Onderwerp maken, bijwerken, verwijderen</span><span class="sxs-lookup"><span data-stu-id="5104d-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="5104d-111">Abonnement maken, bijwerken, verwijderen</span><span class="sxs-lookup"><span data-stu-id="5104d-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5104d-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5104d-112">Prerequisites</span></span>

<span data-ttu-id="5104d-113">tooget gestart met behulp van Hallo Service Bus-bibliotheken voor beheer, moet u zicht aanmeldt met hello Azure Active Directory (AAD)-service.</span><span class="sxs-lookup"><span data-stu-id="5104d-113">tooget started using hello Service Bus management libraries, you must authenticate with hello Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="5104d-114">AAD vereist dat u verificatie uitvoeren als een service-principal die toegang tooyour Azure-resources biedt.</span><span class="sxs-lookup"><span data-stu-id="5104d-114">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="5104d-115">Zie voor informatie over het maken van een service principal, een van deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="5104d-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="5104d-116">Gebruik hello Azure portal toocreate Active Directory-toepassing en service-principal die toegang bronnen tot</span><span class="sxs-lookup"><span data-stu-id="5104d-116">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="5104d-117">Een service principal tooaccess-resources voor Azure PowerShell toocreate gebruiken</span><span class="sxs-lookup"><span data-stu-id="5104d-117">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="5104d-118">Een service principal tooaccess-resources voor Azure CLI toocreate gebruiken</span><span class="sxs-lookup"><span data-stu-id="5104d-118">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="5104d-119">Deze zelfstudies beschikt u over een `AppId` (Client-ID), `TenantId`, en `ClientSecret` (verificatiesleutel), die allemaal worden gebruikt voor verificatie door Hallo management-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="5104d-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="5104d-120">U moet hebben **eigenaar** machtigingen voor resourcegroep Hallo waarvoor u wenst dat toorun.</span><span class="sxs-lookup"><span data-stu-id="5104d-120">You must have **Owner** permissions for hello resource group on which you wish toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="5104d-121">Patroon programmering</span><span class="sxs-lookup"><span data-stu-id="5104d-121">Programming pattern</span></span>

<span data-ttu-id="5104d-122">Hallo patroon toomanipulate een Service Bus-resource een gemeenschappelijke protocol volgt:</span><span class="sxs-lookup"><span data-stu-id="5104d-122">hello pattern toomanipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="5104d-123">Een token verkrijgen van Azure Active Directory met Hallo **Microsoft.IdentityModel.Clients.ActiveDirectory** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="5104d-123">Obtain a token from Azure Active Directory using hello **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="5104d-124">Hallo maken `ServiceBusManagementClient` object.</span><span class="sxs-lookup"><span data-stu-id="5104d-124">Create hello `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="5104d-125">Set Hallo `CreateOrUpdate` parameters tooyour opgegeven waarden.</span><span class="sxs-lookup"><span data-stu-id="5104d-125">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="5104d-126">Hallo-aanroep uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5104d-126">Execute hello call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="5104d-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5104d-127">Next steps</span></span>
* [<span data-ttu-id="5104d-128">Voorbeeld van .NET-management</span><span class="sxs-lookup"><span data-stu-id="5104d-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="5104d-129">Microsoft.Azure.Management.ServiceBus API-verwijzing</span><span class="sxs-lookup"><span data-stu-id="5104d-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
