---
title: aaaHow toocreate API's in Azure API Management
description: Meer informatie over hoe toocreate en API's configureren in Azure API Management.
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
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a><span data-ttu-id="2ec18-103">Hoe toocreate API's in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="2ec18-103">How toocreate APIs in Azure API Management</span></span>
<span data-ttu-id="2ec18-104">Een API Management-API vertegenwoordigt een reeks bewerkingen die kunnen worden aangeroepen door clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="2ec18-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="2ec18-105">Nieuwe API's worden gemaakt in de publicatieportal hello en vervolgens Hallo gewenst bewerkingen zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="2ec18-105">New APIs are created in hello publisher portal, and then hello desired operations are added.</span></span> <span data-ttu-id="2ec18-106">Zodra het Hallo-bewerkingen worden toegevoegd, wordt Hallo API tooa product is toegevoegd en kan worden gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="2ec18-106">Once hello operations are added, hello API is added tooa product and can be published.</span></span> <span data-ttu-id="2ec18-107">Als een API is gepubliceerd, kan het geabonneerde tooand gebruikt door ontwikkelaars zijn.</span><span class="sxs-lookup"><span data-stu-id="2ec18-107">Once an API is published, it can be subscribed tooand used by developers.</span></span>

<span data-ttu-id="2ec18-108">Deze handleiding wordt getoond Hallo eerste stap in Hallo proces: hoe toocreate en configureert u een nieuwe API in API Management.</span><span class="sxs-lookup"><span data-stu-id="2ec18-108">This guide shows hello first step in hello process: how toocreate and configure a new API in API Management.</span></span> <span data-ttu-id="2ec18-109">Zie voor meer informatie over het toevoegen van bewerkingen en een product publiceren [hoe tooadd operations tooan API] [ How tooadd operations tooan API] en [hoe toocreate en een product publiceren] [ How toocreate and publish a product].</span><span class="sxs-lookup"><span data-stu-id="2ec18-109">For more information on adding operations and publishing a product, see [How tooadd operations tooan API][How tooadd operations tooan API] and [How toocreate and publish a product][How toocreate and publish a product].</span></span>

## <span data-ttu-id="2ec18-110"><a name="create-new-api"></a>Maken van een nieuwe API</span><span class="sxs-lookup"><span data-stu-id="2ec18-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="2ec18-111">API's zijn gemaakt en geconfigureerd in de publicatieportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ec18-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="2ec18-112">tooaccess publisher en klik op Hallo **publicatieportal** in hello Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="2ec18-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Publicatieportal][api-management-management-console]

> <span data-ttu-id="2ec18-114">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="2ec18-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="2ec18-115">Klik op **API's** van Hallo **API Management** menu op Hallo links en klik vervolgens op **API toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2ec18-115">Click **APIs** from hello **API Management** menu on hello left, and then click **add API**.</span></span>

![API maken][api-management-create-api]

<span data-ttu-id="2ec18-117">Gebruik Hallo **nieuwe API toevoegen** venster tooconfigure Hallo nieuwe API.</span><span class="sxs-lookup"><span data-stu-id="2ec18-117">Use hello **Add new API** window tooconfigure hello new API.</span></span>

![Nieuwe API toevoegen][api-management-add-new-api]

<span data-ttu-id="2ec18-119">Hallo volgende velden zijn gebruikte tooconfigure Hallo nieuwe API.</span><span class="sxs-lookup"><span data-stu-id="2ec18-119">hello following fields are used tooconfigure hello new API.</span></span>

* <span data-ttu-id="2ec18-120">**De naam van de web-API** biedt een unieke en beschrijvende naam voor Hallo API.</span><span class="sxs-lookup"><span data-stu-id="2ec18-120">**Web API name** provides a unique and descriptive name for hello API.</span></span> <span data-ttu-id="2ec18-121">Deze wordt weergegeven in het Hallo-ontwikkelaars en uitgever portals.</span><span class="sxs-lookup"><span data-stu-id="2ec18-121">It is displayed in hello developer and publisher portals.</span></span>
* <span data-ttu-id="2ec18-122">**Webservice-URL** verwijzingen Hallo Hallo API implementeren HTTP-service.</span><span class="sxs-lookup"><span data-stu-id="2ec18-122">**Web service URL** references hello HTTP service implementing hello API.</span></span> <span data-ttu-id="2ec18-123">API management verzendt aanvragen toothis adres.</span><span class="sxs-lookup"><span data-stu-id="2ec18-123">API management forwards requests toothis address.</span></span>
* <span data-ttu-id="2ec18-124">**Achtervoegsel voor web-API-URL** toegevoegde toohello basis-URL voor Hallo API management-service is.</span><span class="sxs-lookup"><span data-stu-id="2ec18-124">**Web API URL suffix** is appended toohello base URL for hello API management service.</span></span> <span data-ttu-id="2ec18-125">Hallo basis-URL is gebruikelijk voor alle API's die worden gehost door een exemplaar van API Management-service.</span><span class="sxs-lookup"><span data-stu-id="2ec18-125">hello base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="2ec18-126">API Management API's onderscheidt door hun achtervoegsel en daarom Hallo achtervoegsel moet uniek zijn voor elke API voor een opgegeven uitgever.</span><span class="sxs-lookup"><span data-stu-id="2ec18-126">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="2ec18-127">**Web-API-URL-schema** bepaalt welke protocollen gebruikte tooaccess Hallo API kunnen zijn.</span><span class="sxs-lookup"><span data-stu-id="2ec18-127">**Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span> <span data-ttu-id="2ec18-128">Standaard HTTPs is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2ec18-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="2ec18-129">toooptionally deze nieuwe API tooa product toevoegen, klikt u op Hallo **producten (optioneel)** vervolgkeuzelijst en kies een product.</span><span class="sxs-lookup"><span data-stu-id="2ec18-129">toooptionally add this new API tooa product, click hello **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="2ec18-130">Deze stap kan herhaalde verschillende keren tooadd Hallo API toomultiple producten zijn.</span><span class="sxs-lookup"><span data-stu-id="2ec18-130">This step can be repeated multiple times tooadd hello API toomultiple products.</span></span>

<span data-ttu-id="2ec18-131">Zodra het Hallo gewenst waarden zijn geconfigureerd, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2ec18-131">Once hello desired values are configured, click **Save**.</span></span> <span data-ttu-id="2ec18-132">Zodra de nieuwe API Hallo is gemaakt, wordt hello overzichtspagina voor Hallo API weergegeven in de publicatieportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ec18-132">Once hello new API is created, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![API-overzicht][api-management-api-summary]

## <span data-ttu-id="2ec18-134"><a name="configure-api-settings"></a>Instellingen voor de API configureren</span><span class="sxs-lookup"><span data-stu-id="2ec18-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="2ec18-135">U kunt Hallo **instellingen** tooverify tabblad en Hallo-configuratie voor een API te bewerken.</span><span class="sxs-lookup"><span data-stu-id="2ec18-135">You can use hello **Settings** tab tooverify and edit hello configuration for an API.</span></span> <span data-ttu-id="2ec18-136">**De naam van de web-API**, **webservice-URL**, en **achtervoegsel URL Web-API** zijn in eerste instantie ingesteld als Hallo API wordt gemaakt en kan worden gewijzigd hier.</span><span class="sxs-lookup"><span data-stu-id="2ec18-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when hello API is created and can be modified here.</span></span> <span data-ttu-id="2ec18-137">**Beschrijving** biedt een optionele beschrijving en **Web API-URL-schema** bepaalt welke protocollen gebruikte tooaccess Hallo API kunnen zijn.</span><span class="sxs-lookup"><span data-stu-id="2ec18-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span>

![Instellingen voor de API][api-management-api-settings]

<span data-ttu-id="2ec18-139">tooconfigure gatewayverificatie hello back-end-service geïmplementeerd Hallo-API, selecteert u Hallo **beveiliging** tabblad Hallo **met referenties** vervolgkeuzelijst mag gebruikte tooconfigure **HTTP Basic** of **clientcertificaten** verificatie.</span><span class="sxs-lookup"><span data-stu-id="2ec18-139">tooconfigure gateway authentication for hello backend service implementing hello API, select hello **Security** tab. hello **With credentials** drop-down can be used tooconfigure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="2ec18-140">Basisverificatie toouse HTTP gewoon Hallo desired-referenties invoeren.</span><span class="sxs-lookup"><span data-stu-id="2ec18-140">toouse HTTP basic authentication, simply enter hello desired credentials.</span></span> <span data-ttu-id="2ec18-141">Zie voor meer informatie over het gebruik van verificatie van clientcertificaten [hoe toosecure back-end-services met behulp van client-certificaat gebaseerde verificatie in Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2ec18-141">For information on using client certificate authentication, see [How toosecure back-end services using client certificate authentication in Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="2ec18-142">Hallo **beveiliging** tabblad kan ook worden gebruikt tooconfigure **gebruikersautorisatie** met behulp van OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="2ec18-142">hello **Security** tab can also be used tooconfigure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="2ec18-143">Zie voor meer informatie [hoe tooauthorize developer gebruikersaccounts via OAuth 2.0 in Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2ec18-143">For more information, see [How tooauthorize developer accounts using OAuth 2.0 in Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Instellingen voor basisverificatie][api-management-api-settings-credentials]

<span data-ttu-id="2ec18-145">Klik op **opslaan** toosave wijzigingen die u aanbrengt toohello instellingen voor de API.</span><span class="sxs-lookup"><span data-stu-id="2ec18-145">Click **Save** toosave any changes you make toohello API settings.</span></span>

## <span data-ttu-id="2ec18-146"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2ec18-146"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="2ec18-147">Nadat een API is gemaakt en het Hallo-instellingen die zijn geconfigureerd, de volgende stappen Hallo zijn tooadd Hallo operations toohello API, Hallo API tooa product toevoegen en publiceren zodat deze beschikbaar voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="2ec18-147">Once an API is created and hello settings configured, hello next steps are tooadd hello operations toohello API, add hello API tooa product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="2ec18-148">Zie Hallo volgende artikelen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2ec18-148">For more information, see hello following articles.</span></span>

* <span data-ttu-id="2ec18-149">[Hoe tooadd operations tooan API][How tooadd operations tooan API]</span><span class="sxs-lookup"><span data-stu-id="2ec18-149">[How tooadd operations tooan API][How tooadd operations tooan API]</span></span>
* <span data-ttu-id="2ec18-150">[Hoe toocreate en een product publiceren][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="2ec18-150">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
