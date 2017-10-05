---
title: Azure Service Bus-bibliotheken voor management | Microsoft Docs
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
ms.openlocfilehash: 1db00dc1f91e8976b622030450445babbe547ad8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="service-bus-management-libraries"></a><span data-ttu-id="c35fa-103">Management-Service Bus-bibliotheken</span><span class="sxs-lookup"><span data-stu-id="c35fa-103">Service Bus management libraries</span></span>

<span data-ttu-id="c35fa-104">De Azure Service Bus-managementbibliotheken kunnen richten op dynamische wijze Service Bus-naamruimten en entiteiten.</span><span class="sxs-lookup"><span data-stu-id="c35fa-104">The Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="c35fa-105">Dit kunt u complexe implementaties en berichtverzending en maakt het mogelijk via een programma bepalen welke entiteiten te richten.</span><span class="sxs-lookup"><span data-stu-id="c35fa-105">This enables complex deployments and messaging scenarios, and makes it possible to programmatically determine what entities to provision.</span></span> <span data-ttu-id="c35fa-106">Deze bibliotheken zijn momenteel beschikbaar voor .NET.</span><span class="sxs-lookup"><span data-stu-id="c35fa-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="c35fa-107">Ondersteunde functionaliteit</span><span class="sxs-lookup"><span data-stu-id="c35fa-107">Supported functionality</span></span>

* <span data-ttu-id="c35fa-108">Namespace maken, bijwerken, verwijderen</span><span class="sxs-lookup"><span data-stu-id="c35fa-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="c35fa-109">Wachtrijen maken, bijwerken, verwijderen</span><span class="sxs-lookup"><span data-stu-id="c35fa-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="c35fa-110">Onderwerp maken, bijwerken, verwijderen</span><span class="sxs-lookup"><span data-stu-id="c35fa-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="c35fa-111">Abonnement maken, bijwerken, verwijderen</span><span class="sxs-lookup"><span data-stu-id="c35fa-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c35fa-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c35fa-112">Prerequisites</span></span>

<span data-ttu-id="c35fa-113">Om te beginnen met behulp van de Service Bus-bibliotheken voor beheer, moet u verifiëren met de service Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="c35fa-113">To get started using the Service Bus management libraries, you must authenticate with the Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="c35fa-114">AAD vereist dat u verificatie uitvoeren als een service-principal die toegang tot uw Azure-resources biedt.</span><span class="sxs-lookup"><span data-stu-id="c35fa-114">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="c35fa-115">Zie voor informatie over het maken van een service principal, een van deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="c35fa-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="c35fa-116">De Azure portal gebruiken om Active Directory-toepassing en service-principal die toegang bronnen tot te maken</span><span class="sxs-lookup"><span data-stu-id="c35fa-116">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="c35fa-117">Azure PowerShell gebruiken om een service-principal te maken voor toegang tot resources</span><span class="sxs-lookup"><span data-stu-id="c35fa-117">Use Azure PowerShell to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="c35fa-118">Azure CLI gebruiken om een service-principal te maken voor toegang tot resources</span><span class="sxs-lookup"><span data-stu-id="c35fa-118">Use Azure CLI to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="c35fa-119">Deze zelfstudies beschikt u over een `AppId` (Client-ID), `TenantId`, en `ClientSecret` (verificatiesleutel), die allemaal worden gebruikt voor verificatie door de management-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="c35fa-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="c35fa-120">U moet hebben **eigenaar** machtigingen voor de resourcegroep waarin u wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c35fa-120">You must have **Owner** permissions for the resource group on which you wish to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="c35fa-121">Patroon programmering</span><span class="sxs-lookup"><span data-stu-id="c35fa-121">Programming pattern</span></span>

<span data-ttu-id="c35fa-122">Hier volgt een gemeenschappelijke protocol het patroon voor het bewerken van een Service Bus-resource:</span><span class="sxs-lookup"><span data-stu-id="c35fa-122">The pattern to manipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="c35fa-123">Een token verkrijgen van het gebruik van Azure Active Directory de **Microsoft.IdentityModel.Clients.ActiveDirectory** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="c35fa-123">Obtain a token from Azure Active Directory using the **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="c35fa-124">Maak de `ServiceBusManagementClient` object.</span><span class="sxs-lookup"><span data-stu-id="c35fa-124">Create the `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="c35fa-125">Stel de `CreateOrUpdate` parameters met de opgegeven waarden.</span><span class="sxs-lookup"><span data-stu-id="c35fa-125">Set the `CreateOrUpdate` parameters to your specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="c35fa-126">De aanroep worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c35fa-126">Execute the call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="c35fa-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c35fa-127">Next steps</span></span>
* [<span data-ttu-id="c35fa-128">Voorbeeld van .NET-management</span><span class="sxs-lookup"><span data-stu-id="c35fa-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="c35fa-129">Microsoft.Azure.Management.ServiceBus API-verwijzing</span><span class="sxs-lookup"><span data-stu-id="c35fa-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
