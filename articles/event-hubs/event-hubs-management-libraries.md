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
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="ad5e0-103">Event Hubs management-bibliotheken</span><span class="sxs-lookup"><span data-stu-id="ad5e0-103">Event Hubs management libraries</span></span>

<span data-ttu-id="ad5e0-104">Hallo Event Hubs managementbibliotheken kunnen richten op dynamische wijze Event Hubs-naamruimten en entiteiten.</span><span class="sxs-lookup"><span data-stu-id="ad5e0-104">hello Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="ad5e0-105">Hiermee kunnen complexe implementaties en berichtverzending, zodat u via een programma welke tooprovision entiteiten bepalen kunt.</span><span class="sxs-lookup"><span data-stu-id="ad5e0-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities tooprovision.</span></span> <span data-ttu-id="ad5e0-106">Deze bibliotheken zijn momenteel beschikbaar voor .NET.</span><span class="sxs-lookup"><span data-stu-id="ad5e0-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="ad5e0-107">Ondersteunde functionaliteit</span><span class="sxs-lookup"><span data-stu-id="ad5e0-107">Supported functionality</span></span>

* <span data-ttu-id="ad5e0-108">Namespace maken, bijwerken, verwijderen</span><span class="sxs-lookup"><span data-stu-id="ad5e0-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="ad5e0-109">Event Hubs maken, bijwerken, verwijderen</span><span class="sxs-lookup"><span data-stu-id="ad5e0-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="ad5e0-110">Consumergroep maken, bijwerken, verwijderen</span><span class="sxs-lookup"><span data-stu-id="ad5e0-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad5e0-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ad5e0-111">Prerequisites</span></span>

<span data-ttu-id="ad5e0-112">tooget gestart met behulp van Hallo Event Hubs management-bibliotheken, moet u verifiëren met Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="ad5e0-112">tooget started using hello Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="ad5e0-113">AAD vereist dat u verificatie uitvoeren als een service-principal die toegang tooyour Azure-resources biedt.</span><span class="sxs-lookup"><span data-stu-id="ad5e0-113">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="ad5e0-114">Zie voor informatie over het maken van een service principal, een van deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="ad5e0-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="ad5e0-115">Gebruik hello Azure portal toocreate Active Directory-toepassing en service-principal die toegang bronnen tot</span><span class="sxs-lookup"><span data-stu-id="ad5e0-115">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="ad5e0-116">Een service principal tooaccess-resources voor Azure PowerShell toocreate gebruiken</span><span class="sxs-lookup"><span data-stu-id="ad5e0-116">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="ad5e0-117">Een service principal tooaccess-resources voor Azure CLI toocreate gebruiken</span><span class="sxs-lookup"><span data-stu-id="ad5e0-117">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="ad5e0-118">Deze zelfstudies beschikt u over een `AppId` (Client-ID), `TenantId`, en `ClientSecret` (verificatiesleutel), die allemaal worden gebruikt voor verificatie door Hallo management-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="ad5e0-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="ad5e0-119">U moet hebben **eigenaar** machtigingen voor resourcegroep Hallo waarop toorun.</span><span class="sxs-lookup"><span data-stu-id="ad5e0-119">You must have **Owner** permissions for hello resource group on which you want toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="ad5e0-120">Patroon programmering</span><span class="sxs-lookup"><span data-stu-id="ad5e0-120">Programming pattern</span></span>

<span data-ttu-id="ad5e0-121">Hallo patroon toomanipulate alle Event Hubs-bronnen, volgt een gemeenschappelijke protocol:</span><span class="sxs-lookup"><span data-stu-id="ad5e0-121">hello pattern toomanipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="ad5e0-122">Verkrijgen van een token van AAD Hallo met `Microsoft.IdentityModel.Clients.ActiveDirectory` bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="ad5e0-122">Obtain a token from AAD using hello `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="ad5e0-123">Hallo maken `EventHubManagementClient` object.</span><span class="sxs-lookup"><span data-stu-id="ad5e0-123">Create hello `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="ad5e0-124">Set Hallo `CreateOrUpdate` parameters tooyour opgegeven waarden.</span><span class="sxs-lookup"><span data-stu-id="ad5e0-124">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="ad5e0-125">Hallo-aanroep uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ad5e0-125">Execute hello call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="ad5e0-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ad5e0-126">Next steps</span></span>
* [<span data-ttu-id="ad5e0-127">Voorbeeld van de .NET-management</span><span class="sxs-lookup"><span data-stu-id="ad5e0-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="ad5e0-128">Microsoft.Azure.Management.EventHub verwijzing</span><span class="sxs-lookup"><span data-stu-id="ad5e0-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
