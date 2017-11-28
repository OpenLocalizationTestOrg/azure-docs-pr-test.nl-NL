---
title: een API aaaImport in Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooimport een API en bewerkingen in Azure API Management.
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
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="bd419-103">Hoe tooimport Hallo definitie van een API met bewerkingen in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="bd419-103">How tooimport hello definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="bd419-104">Nieuwe API's kunnen worden gemaakt in API Management en Hallo bewerkingen handmatig toegevoegd of Hallo API kan samen met de Hallo-bewerkingen in één stap worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="bd419-104">In API Management, new APIs can be created and hello operations added manually, or hello API can be imported along with hello operations in one step.</span></span>

<span data-ttu-id="bd419-105">API's en hun bewerkingen kunnen worden geïmporteerd met behulp van de volgende indelingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="bd419-105">APIs and their operations can be imported using hello following formats.</span></span>

* <span data-ttu-id="bd419-106">WADL</span><span class="sxs-lookup"><span data-stu-id="bd419-106">WADL</span></span>
* <span data-ttu-id="bd419-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="bd419-107">Swagger</span></span>

<span data-ttu-id="bd419-108">Deze handleiding bevat een nieuwe API maken en importeren van bewerkingen in één stap.</span><span class="sxs-lookup"><span data-stu-id="bd419-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="bd419-109">Zie voor informatie over het handmatig maken van een API en het toevoegen van bewerkingen, [hoe toocreate API's] [ How toocreate APIs] en [hoe tooadd operations tooan API] [ How tooadd operations tooan API].</span><span class="sxs-lookup"><span data-stu-id="bd419-109">For information on manually creating an API and adding operations, see [How toocreate APIs][How toocreate APIs] and [How tooadd operations tooan API][How tooadd operations tooan API].</span></span>

## <span data-ttu-id="bd419-110"><a name="import-api"> </a>Een API importeren</span><span class="sxs-lookup"><span data-stu-id="bd419-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="bd419-111">API's zijn gemaakt en geconfigureerd in de publicatieportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="bd419-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="bd419-112">tooaccess publisher en klik op Hallo **publicatieportal** in hello Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="bd419-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="bd419-113">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="bd419-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Publicatieportal][api-management-management-console]

<span data-ttu-id="bd419-115">Klik op **API's** van Hallo **API Management** menu op Hallo links en klik vervolgens op **importeren API**.</span><span class="sxs-lookup"><span data-stu-id="bd419-115">Click **APIs** from hello **API Management** menu on hello left, and then click **import API**.</span></span>

![API importeren][api-management-import-apis]

<span data-ttu-id="bd419-117">Hallo **Import API** venster bestaat uit drie tabbladen die overeenkomen met toohello drie manieren tooprovide Hallo API-specificatie.</span><span class="sxs-lookup"><span data-stu-id="bd419-117">hello **Import API** window has three tabs that correspond toohello three ways tooprovide hello API specification.</span></span>

* <span data-ttu-id="bd419-118">**Van Klembord** kunt u toopaste Hallo API-specificatie in aangewezen Hallo-tekstvak.</span><span class="sxs-lookup"><span data-stu-id="bd419-118">**From clipboard** allows you toopaste hello API specification into hello designated text box.</span></span>
* <span data-ttu-id="bd419-119">**Uit bestand** kunt u toobrowse tooand Selecteer Hallo-bestand met de Hallo API-specificatie.</span><span class="sxs-lookup"><span data-stu-id="bd419-119">**From file** allows you toobrowse tooand select hello file that contains hello API specification.</span></span>
* <span data-ttu-id="bd419-120">**Van URL** kunt u toosupply Hallo URL toohello-specificatie voor Hallo API.</span><span class="sxs-lookup"><span data-stu-id="bd419-120">**From URL** allows you toosupply hello URL toohello specification for hello API.</span></span>

![Indeling van de API importeren][api-management-import-api-clipboard]

<span data-ttu-id="bd419-122">Gebruik na het opgeven van Hallo API-specificatie Hallo keuzerondjes op Hallo rechts tooindicate Hallo specificatie indeling.</span><span class="sxs-lookup"><span data-stu-id="bd419-122">After providing hello API specification, use hello radio buttons on hello right tooindicate hello specification format.</span></span> <span data-ttu-id="bd419-123">Hallo volgende indelingen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="bd419-123">hello following formats are supported.</span></span>

* <span data-ttu-id="bd419-124">WADL</span><span class="sxs-lookup"><span data-stu-id="bd419-124">WADL</span></span>
* <span data-ttu-id="bd419-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="bd419-125">Swagger</span></span>

<span data-ttu-id="bd419-126">Geef vervolgens een **achtervoegsel URL Web-API**.</span><span class="sxs-lookup"><span data-stu-id="bd419-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="bd419-127">Dit is de toegevoegde toohello basis-URL voor uw API management-service.</span><span class="sxs-lookup"><span data-stu-id="bd419-127">This is appended toohello base URL for your API management service.</span></span> <span data-ttu-id="bd419-128">Hallo basis-URL is gebruikelijk voor alle API's die worden gehost op elk exemplaar van API Management-service.</span><span class="sxs-lookup"><span data-stu-id="bd419-128">hello base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="bd419-129">API Management API's onderscheidt door hun achtervoegsel en daarom Hallo achtervoegsel moet uniek zijn voor elke API in een specifiek exemplaar van API management-service.</span><span class="sxs-lookup"><span data-stu-id="bd419-129">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="bd419-130">Nadat alle waarden zijn ingevoerd, klikt u op **opslaan** toocreate Hallo API en Hallo operations gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="bd419-130">Once all values are entered, click **Save** toocreate hello API and hello associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="bd419-131">Zie voor een zelfstudie over het importeren van de basisrekenmachine API in Swagger-indeling, [uw eerste API beheren in Azure API Management](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bd419-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="bd419-132"><a name="export-api"></a> Exporteren van een API</span><span class="sxs-lookup"><span data-stu-id="bd419-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="bd419-133">In aanvulling tooimporting nieuwe API's, kunt u Hallo definities van uw API's van de publicatieportal Hallo exporteren.</span><span class="sxs-lookup"><span data-stu-id="bd419-133">In addition tooimporting new APIs, you can export hello definitions of your APIs from hello publisher portal.</span></span> <span data-ttu-id="bd419-134">toodo hiervoor, klikt u op **exporteren API** van Hallo **tabblad Samenvatting** van uw **API**.</span><span class="sxs-lookup"><span data-stu-id="bd419-134">toodo so, click **Export API** from hello **Summary tab** of your **API**.</span></span>

![API exporteren][api-management-export-api]

<span data-ttu-id="bd419-136">API's kunnen worden geëxporteerd met WADL of Swagger.</span><span class="sxs-lookup"><span data-stu-id="bd419-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="bd419-137">Selecteer de gewenste indeling hello, klikt u op **opslaan**, en Hallo locatie kiezen in welke toosave Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="bd419-137">Select hello desired format, click **Save**, and choose hello location in which toosave hello file.</span></span>

![API-indeling voor exporteren][api-management-export-api-format]

## <span data-ttu-id="bd419-139"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bd419-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="bd419-140">Nadat een API is gemaakt en Hallo-bewerkingen die zijn geïmporteerd, die u kunt bekijken en configureren van eventuele aanvullende instellingen Hallo API tooa Product toevoegen en publiceren zodat deze beschikbaar voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="bd419-140">Once an API is created and hello operations imported, you can review and configure any additional settings, add hello API tooa Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="bd419-141">Zie voor meer informatie Hallo handleidingen te volgen.</span><span class="sxs-lookup"><span data-stu-id="bd419-141">For more information, see hello following guides.</span></span>

* <span data-ttu-id="bd419-142">[Hoe tooconfigure API-instellingen][How tooconfigure API settings]</span><span class="sxs-lookup"><span data-stu-id="bd419-142">[How tooconfigure API settings][How tooconfigure API settings]</span></span>
* <span data-ttu-id="bd419-143">[Hoe toocreate en een product publiceren][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="bd419-143">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
