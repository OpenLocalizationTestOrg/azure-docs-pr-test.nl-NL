---
title: API's maken in Azure API Management
description: Informatie over het maken en configureren van API's in Azure API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ab08256fbc3caca05bf23a12016ad2acf4fc7412
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-apis-in-azure-api-management"></a><span data-ttu-id="4afb9-103">API's maken in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="4afb9-103">How to create APIs in Azure API Management</span></span>
<span data-ttu-id="4afb9-104">Een API Management-API vertegenwoordigt een reeks bewerkingen die kunnen worden aangeroepen door clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="4afb9-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="4afb9-105">Nieuwe API's worden gemaakt in de publicatieportal en klikt u vervolgens de gewenste bewerkingen worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="4afb9-105">New APIs are created in the publisher portal, and then the desired operations are added.</span></span> <span data-ttu-id="4afb9-106">Nadat de bewerkingen zijn toegevoegd, wordt de API is toegevoegd aan een product en kan worden gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="4afb9-106">Once the operations are added, the API is added to a product and can be published.</span></span> <span data-ttu-id="4afb9-107">Als een API is gepubliceerd, kunt u het abonnement op en gebruikt door ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="4afb9-107">Once an API is published, it can be subscribed to and used by developers.</span></span>

<span data-ttu-id="4afb9-108">Deze handleiding bevat de eerste stap in het proces: het maken en configureren van een nieuwe API in API Management.</span><span class="sxs-lookup"><span data-stu-id="4afb9-108">This guide shows the first step in the process: how to create and configure a new API in API Management.</span></span> <span data-ttu-id="4afb9-109">Zie voor meer informatie over het toevoegen van bewerkingen en een product publiceren [bewerkingen toevoegen aan een API] [ How to add operations to an API] en [maken en publiceren van een product] [ How to create and publish a product].</span><span class="sxs-lookup"><span data-stu-id="4afb9-109">For more information on adding operations and publishing a product, see [How to add operations to an API][How to add operations to an API] and [How to create and publish a product][How to create and publish a product].</span></span>

## <span data-ttu-id="4afb9-110"><a name="create-new-api"></a>Maken van een nieuwe API</span><span class="sxs-lookup"><span data-stu-id="4afb9-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="4afb9-111">API's zijn gemaakt en geconfigureerd in de publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="4afb9-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="4afb9-112">Voor toegang tot de publicatieportal bevindt, klikt u op **publicatieportal** in de Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="4afb9-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Publicatieportal][api-management-management-console]

> <span data-ttu-id="4afb9-114">Als u nog geen service-exemplaar van API Management hebt gemaakt, raadpleegt u [Service-exemplaar van API Management maken][Create an API Management service instance] in de zelfstudie [Aan de slag met Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="4afb9-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="4afb9-115">Klik op **API's** van de **API Management** menu aan de linkerkant en klik vervolgens op **API toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4afb9-115">Click **APIs** from the **API Management** menu on the left, and then click **add API**.</span></span>

![API maken][api-management-create-api]

<span data-ttu-id="4afb9-117">Gebruik de **nieuwe API toevoegen** venster voor het configureren van de nieuwe API.</span><span class="sxs-lookup"><span data-stu-id="4afb9-117">Use the **Add new API** window to configure the new API.</span></span>

![Nieuwe API toevoegen][api-management-add-new-api]

<span data-ttu-id="4afb9-119">De volgende velden worden gebruikt voor het configureren van de nieuwe API.</span><span class="sxs-lookup"><span data-stu-id="4afb9-119">The following fields are used to configure the new API.</span></span>

* <span data-ttu-id="4afb9-120">**De naam van de web-API** biedt een unieke en beschrijvende naam voor de API.</span><span class="sxs-lookup"><span data-stu-id="4afb9-120">**Web API name** provides a unique and descriptive name for the API.</span></span> <span data-ttu-id="4afb9-121">Deze wordt weergegeven in de portals ontwikkelaars en uitgever.</span><span class="sxs-lookup"><span data-stu-id="4afb9-121">It is displayed in the developer and publisher portals.</span></span>
* <span data-ttu-id="4afb9-122">**Webservice-URL** verwijst naar de HTTP-service voor het implementeren van de API.</span><span class="sxs-lookup"><span data-stu-id="4afb9-122">**Web service URL** references the HTTP service implementing the API.</span></span> <span data-ttu-id="4afb9-123">API management verzendt aanvragen naar dit adres.</span><span class="sxs-lookup"><span data-stu-id="4afb9-123">API management forwards requests to this address.</span></span>
* <span data-ttu-id="4afb9-124">**Achtervoegsel voor web-API-URL** wordt toegevoegd aan de basis-URL voor de API management-service.</span><span class="sxs-lookup"><span data-stu-id="4afb9-124">**Web API URL suffix** is appended to the base URL for the API management service.</span></span> <span data-ttu-id="4afb9-125">De basis-URL is gemeenschappelijk voor alle API's die worden gehost door een exemplaar van API Management-service.</span><span class="sxs-lookup"><span data-stu-id="4afb9-125">The base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="4afb9-126">API Management API's onderscheidt door hun achtervoegsel en daarom het achtervoegsel moet uniek zijn voor elke API voor een opgegeven uitgever.</span><span class="sxs-lookup"><span data-stu-id="4afb9-126">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="4afb9-127">**Web-API-URL-schema** bepaalt welke protocollen kunnen worden gebruikt voor toegang tot de API.</span><span class="sxs-lookup"><span data-stu-id="4afb9-127">**Web API URL scheme** determines which protocols can be used to access the API.</span></span> <span data-ttu-id="4afb9-128">Standaard HTTPs is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="4afb9-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="4afb9-129">Als u wilt eventueel deze nieuwe API toevoegen aan een product, klikt u op de **producten (optioneel)** vervolgkeuzelijst en kies een product.</span><span class="sxs-lookup"><span data-stu-id="4afb9-129">To optionally add this new API to a product, click the **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="4afb9-130">Deze stap kan meerdere keren toevoegen van de API aan meerdere producten worden herhaald.</span><span class="sxs-lookup"><span data-stu-id="4afb9-130">This step can be repeated multiple times to add the API to multiple products.</span></span>

<span data-ttu-id="4afb9-131">Nadat de gewenste waarden zijn geconfigureerd, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4afb9-131">Once the desired values are configured, click **Save**.</span></span> <span data-ttu-id="4afb9-132">Zodra de nieuwe API is gemaakt, wordt de overzichtspagina voor de API weergegeven in de publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="4afb9-132">Once the new API is created, the summary page for the API is displayed in the publisher portal.</span></span>

![API-overzicht][api-management-api-summary]

## <span data-ttu-id="4afb9-134"><a name="configure-api-settings"></a>Instellingen voor de API configureren</span><span class="sxs-lookup"><span data-stu-id="4afb9-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="4afb9-135">U kunt de **instellingen** tab om te controleren en bewerken van de configuratie voor een API.</span><span class="sxs-lookup"><span data-stu-id="4afb9-135">You can use the **Settings** tab to verify and edit the configuration for an API.</span></span> <span data-ttu-id="4afb9-136">**De naam van de web-API**, **webservice-URL**, en **achtervoegsel URL Web-API** zijn in eerste instantie ingesteld als de API wordt gemaakt en kan worden gewijzigd hier.</span><span class="sxs-lookup"><span data-stu-id="4afb9-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when the API is created and can be modified here.</span></span> <span data-ttu-id="4afb9-137">**Beschrijving** biedt een optionele beschrijving en **Web API-URL-schema** bepaalt welke protocollen kunnen worden gebruikt voor toegang tot de API.</span><span class="sxs-lookup"><span data-stu-id="4afb9-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used to access the API.</span></span>

![Instellingen voor de API][api-management-api-settings]

<span data-ttu-id="4afb9-139">Als gatewayverificatie wilt configureren voor het implementeren van de API van de back-endservice, selecteer de **beveiliging** tabblad.</span><span class="sxs-lookup"><span data-stu-id="4afb9-139">To configure gateway authentication for the backend service implementing the API, select the **Security** tab.</span></span> <span data-ttu-id="4afb9-140">De **met referenties** vervolgkeuzelijst kan worden gebruikt voor het configureren van **HTTP basic** of **clientcertificaten** verificatie.</span><span class="sxs-lookup"><span data-stu-id="4afb9-140">The **With credentials** drop-down can be used to configure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="4afb9-141">Voer de gewenste referenties voor het gebruik van HTTP-basisverificatie.</span><span class="sxs-lookup"><span data-stu-id="4afb9-141">To use HTTP basic authentication, simply enter the desired credentials.</span></span> <span data-ttu-id="4afb9-142">Zie voor meer informatie over het gebruik van verificatie van clientcertificaten [het beveiligen van back-end-services met behulp van client certificaatverificatie in Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="4afb9-142">For information on using client certificate authentication, see [How to secure back-end services using client certificate authentication in Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="4afb9-143">De **beveiliging** tabblad kan ook worden gebruikt voor het configureren van **gebruikersautorisatie** met behulp van OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="4afb9-143">The **Security** tab can also be used to configure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="4afb9-144">Zie voor meer informatie [hoe autoriseren met behulp van OAuth 2.0 in Azure API Management ontwikkelaarsaccounts][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="4afb9-144">For more information, see [How to authorize developer accounts using OAuth 2.0 in Azure API Management][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Instellingen voor basisverificatie][api-management-api-settings-credentials]

<span data-ttu-id="4afb9-146">Klik op **opslaan** wijzigingen in de API-instellingen wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="4afb9-146">Click **Save** to save any changes you make to the API settings.</span></span>

## <span data-ttu-id="4afb9-147"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4afb9-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="4afb9-148">Zodra een API is gemaakt en de instellingen die zijn geconfigureerd, de volgende stappen zijn de bewerkingen toevoegen aan de API, de API toevoegen aan een product en publiceren zodat deze beschikbaar voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="4afb9-148">Once an API is created and the settings configured, the next steps are to add the operations to the API, add the API to a product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="4afb9-149">Zie de volgende artikelen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4afb9-149">For more information, see the following articles.</span></span>

* <span data-ttu-id="4afb9-150">[Bewerkingen toevoegen aan een API][How to add operations to an API]</span><span class="sxs-lookup"><span data-stu-id="4afb9-150">[How to add operations to an API][How to add operations to an API]</span></span>
* <span data-ttu-id="4afb9-151">[Het maken en een product publiceren][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="4afb9-151">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How to secure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How to authorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
