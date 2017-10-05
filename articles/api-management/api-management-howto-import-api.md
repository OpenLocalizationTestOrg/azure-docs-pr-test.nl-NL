---
title: Een API importeren in Azure API Management | Microsoft Docs
description: Informatie over het importeren van een API en bewerkingen in Azure API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c851b88fc1067e65044266d07775717c028e75d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-the-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="40421-103">Het importeren van de definitie van een API met bewerkingen in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="40421-103">How to import the definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="40421-104">Nieuwe API's kunnen worden gemaakt in API Management en de bewerkingen zijn handmatig toegevoegd of de API kan samen met de bewerkingen in één stap worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="40421-104">In API Management, new APIs can be created and the operations added manually, or the API can be imported along with the operations in one step.</span></span>

<span data-ttu-id="40421-105">API's en hun bewerkingen kunnen worden geïmporteerd met de volgende indelingen.</span><span class="sxs-lookup"><span data-stu-id="40421-105">APIs and their operations can be imported using the following formats.</span></span>

* <span data-ttu-id="40421-106">WADL</span><span class="sxs-lookup"><span data-stu-id="40421-106">WADL</span></span>
* <span data-ttu-id="40421-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="40421-107">Swagger</span></span>

<span data-ttu-id="40421-108">Deze handleiding bevat een nieuwe API maken en importeren van bewerkingen in één stap.</span><span class="sxs-lookup"><span data-stu-id="40421-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="40421-109">Zie voor informatie over het handmatig maken van een API en het toevoegen van bewerkingen, [API's maken] [ How to create APIs] en [bewerkingen toevoegen aan een API][How to add operations to an API].</span><span class="sxs-lookup"><span data-stu-id="40421-109">For information on manually creating an API and adding operations, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span></span>

## <span data-ttu-id="40421-110"><a name="import-api"> </a>Een API importeren</span><span class="sxs-lookup"><span data-stu-id="40421-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="40421-111">API's zijn gemaakt en geconfigureerd in de publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="40421-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="40421-112">Voor toegang tot de publicatieportal bevindt, klikt u op **publicatieportal** in de Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="40421-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="40421-113">Als u nog geen service-exemplaar van API Management hebt gemaakt, raadpleegt u [Service-exemplaar van API Management maken][Create an API Management service instance] in de zelfstudie [Aan de slag met Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="40421-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Publicatieportal][api-management-management-console]

<span data-ttu-id="40421-115">Klik op **API's** van de **API Management** menu aan de linkerkant en klik vervolgens op **importeren API**.</span><span class="sxs-lookup"><span data-stu-id="40421-115">Click **APIs** from the **API Management** menu on the left, and then click **import API**.</span></span>

![API importeren][api-management-import-apis]

<span data-ttu-id="40421-117">De **Import API** venster bestaat uit drie tabbladen die met de drie manieren overeenkomen om de API-specificatie.</span><span class="sxs-lookup"><span data-stu-id="40421-117">The **Import API** window has three tabs that correspond to the three ways to provide the API specification.</span></span>

* <span data-ttu-id="40421-118">**Van Klembord** kunt u de API-specificatie plak in het tekstvak aangewezen.</span><span class="sxs-lookup"><span data-stu-id="40421-118">**From clipboard** allows you to paste the API specification into the designated text box.</span></span>
* <span data-ttu-id="40421-119">**Uit bestand** kunt u bladeren naar en selecteer het bestand waarin de API-specificatie.</span><span class="sxs-lookup"><span data-stu-id="40421-119">**From file** allows you to browse to and select the file that contains the API specification.</span></span>
* <span data-ttu-id="40421-120">**Van URL** kunt u de URL de specificatie voor de API.</span><span class="sxs-lookup"><span data-stu-id="40421-120">**From URL** allows you to supply the URL to the specification for the API.</span></span>

![Indeling van de API importeren][api-management-import-api-clipboard]

<span data-ttu-id="40421-122">Gebruik de keuzerondjes aan de rechterkant om aan te geven van de indeling specificatie na het opgeven van de API-specificatie.</span><span class="sxs-lookup"><span data-stu-id="40421-122">After providing the API specification, use the radio buttons on the right to indicate the specification format.</span></span> <span data-ttu-id="40421-123">De volgende indelingen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="40421-123">The following formats are supported.</span></span>

* <span data-ttu-id="40421-124">WADL</span><span class="sxs-lookup"><span data-stu-id="40421-124">WADL</span></span>
* <span data-ttu-id="40421-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="40421-125">Swagger</span></span>

<span data-ttu-id="40421-126">Geef vervolgens een **achtervoegsel URL Web-API**.</span><span class="sxs-lookup"><span data-stu-id="40421-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="40421-127">Dit wordt toegevoegd aan de basis-URL voor uw API management-service.</span><span class="sxs-lookup"><span data-stu-id="40421-127">This is appended to the base URL for your API management service.</span></span> <span data-ttu-id="40421-128">De basis-URL is gemeenschappelijk voor alle API's die worden gehost op elk exemplaar van API Management-service.</span><span class="sxs-lookup"><span data-stu-id="40421-128">The base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="40421-129">API Management API's onderscheidt door hun achtervoegsel en daarom het achtervoegsel moet uniek zijn voor elke API in een specifiek exemplaar van API management-service.</span><span class="sxs-lookup"><span data-stu-id="40421-129">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="40421-130">Nadat alle waarden zijn ingevoerd, klikt u op **opslaan** voor het maken van de API en de gekoppelde bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="40421-130">Once all values are entered, click **Save** to create the API and the associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="40421-131">Zie voor een zelfstudie over het importeren van de basisrekenmachine API in Swagger-indeling, [uw eerste API beheren in Azure API Management](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="40421-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="40421-132"><a name="export-api"></a> Exporteren van een API</span><span class="sxs-lookup"><span data-stu-id="40421-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="40421-133">Naast de nieuwe API's importeert, kunt u de definities van uw API's exporteren in de publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="40421-133">In addition to importing new APIs, you can export the definitions of your APIs from the publisher portal.</span></span> <span data-ttu-id="40421-134">Om dit te doen, klikt u op **exporteren API** van de **tabblad Samenvatting** van uw **API**.</span><span class="sxs-lookup"><span data-stu-id="40421-134">To do so, click **Export API** from the **Summary tab** of your **API**.</span></span>

![API exporteren][api-management-export-api]

<span data-ttu-id="40421-136">API's kunnen worden geëxporteerd met WADL of Swagger.</span><span class="sxs-lookup"><span data-stu-id="40421-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="40421-137">Selecteer de gewenste indeling, klikt u op **opslaan**, en kies de locatie op waar het bestand wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="40421-137">Select the desired format, click **Save**, and choose the location in which to save the file.</span></span>

![API-indeling voor exporteren][api-management-export-api-format]

## <span data-ttu-id="40421-139"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="40421-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="40421-140">Nadat een API is gemaakt en de bewerkingen die zijn geïmporteerd, die u kunt bekijken en configureren van eventuele aanvullende instellingen de API toevoegen aan een Product en publiceren zodat deze beschikbaar voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="40421-140">Once an API is created and the operations imported, you can review and configure any additional settings, add the API to a Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="40421-141">Zie de volgende handleidingen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="40421-141">For more information, see the following guides.</span></span>

* <span data-ttu-id="40421-142">[Het configureren van instellingen voor de API][How to configure API settings]</span><span class="sxs-lookup"><span data-stu-id="40421-142">[How to configure API settings][How to configure API settings]</span></span>
* <span data-ttu-id="40421-143">[Het maken en een product publiceren][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="40421-143">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create APIs]: api-management-howto-create-apis.md
[How to configure API settings]: api-management-howto-create-apis.md#configure-api-settings
