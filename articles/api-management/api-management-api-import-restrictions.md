---
title: aaaRestrictions en bekende problemen in Azure API Management-API importeren | Microsoft Docs
description: Details van de bekende problemen en beperkingen voor het importeren in Azure API Management Hallo Open API, WSDL of WADL indelingen.
services: api-management
documentationcenter: 
author: mattfarm
manager: vlvinogr
editor: 
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: apipm
ms.openlocfilehash: 0bed5ace47de6ccbfbecba25ea6b69c5329de089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="41c2b-103">API importeren beperkingen en bekende problemen</span><span class="sxs-lookup"><span data-stu-id="41c2b-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="41c2b-104">Over deze lijst</span><span class="sxs-lookup"><span data-stu-id="41c2b-104">About this list</span></span>
<span data-ttu-id="41c2b-105">Terwijl alles in het werk wordt tooensure die uw API te importeren in Azure API Management als naadloze is en foutloos mogelijk, we zo nu en dan beperkingen opleggen of problemen die toobe verholpen moet voordat u met succes kunt importeren.</span><span class="sxs-lookup"><span data-stu-id="41c2b-105">While every effort is made tooensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need toobe rectified before you can successfully import.</span></span> <span data-ttu-id="41c2b-106">In dit artikel wordt deze georganiseerd door indeling voor het importeren van Hallo Hallo API.</span><span class="sxs-lookup"><span data-stu-id="41c2b-106">This article documents these, organised by hello import format of hello API.</span></span>

## <span data-ttu-id="41c2b-107"><a name="open-api"></a>API/Swagger openen</span><span class="sxs-lookup"><span data-stu-id="41c2b-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="41c2b-108">In het algemeen als u uw document Open API importeren fouten ontvangt, zorg ervoor dat u hebt deze - gevalideerd met de designer Hallo Hallo in de nieuwe Azure Portal (ontwerp - Front-End - API specificatie Editor openen), of met een 3rd partij hulpprogramma zoals <a href="http://www.swagger.io"> Swagger Editor</a>.</span><span class="sxs-lookup"><span data-stu-id="41c2b-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using hello designer in hello new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="41c2b-109">**Hostnaam** moet een name-hostnaamkenmerk.</span><span class="sxs-lookup"><span data-stu-id="41c2b-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="41c2b-110">**Pad baseren** moet een kenmerk basispad.</span><span class="sxs-lookup"><span data-stu-id="41c2b-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="41c2b-111">**Schema's** moet een matrix van het schema.</span><span class="sxs-lookup"><span data-stu-id="41c2b-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="41c2b-112"><a name="wsdl"></a>WSDL</span><span class="sxs-lookup"><span data-stu-id="41c2b-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="41c2b-113">WSDL-bestanden zijn gebruikte toogenerate SOAP Pass Through-API's of fungeren als Hallo back-end van een SOAP-REST-API.</span><span class="sxs-lookup"><span data-stu-id="41c2b-113">WSDL files are used toogenerate SOAP Pass-through APIs, or serve as hello backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="41c2b-114">**WSDL: import** wordt momenteel niet ondersteund met behulp van dit kenmerk API's.</span><span class="sxs-lookup"><span data-stu-id="41c2b-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="41c2b-115">Klanten moeten Hallo geïmporteerd elementen samenvoegen in één document.</span><span class="sxs-lookup"><span data-stu-id="41c2b-115">Customers should merge hello imported elements into one document.</span></span>
* <span data-ttu-id="41c2b-116">**Berichten met meerdere onderdelen** worden momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="41c2b-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="41c2b-117">**WCF-wsHttpBinding** SOAP-services die zijn gemaakt met Windows Communication Foundation basicHttpBinding moeten gebruiken - wsHttpBinding wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="41c2b-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="41c2b-118">**MTOM** MTOM-Services <em>kan</em> werken.</span><span class="sxs-lookup"><span data-stu-id="41c2b-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="41c2b-119">Op dit moment is geen officiële ondersteuning geboden.</span><span class="sxs-lookup"><span data-stu-id="41c2b-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="41c2b-120">**Recursie** typen die zijn gedefinieerd recursief (bv. Raadpleeg tooan matrix van zichzelf) worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="41c2b-120">**Recursion** types that are defined recursively (e.g. refer tooan array of themselves) are not supported.</span></span>

## <span data-ttu-id="41c2b-121"><a name="wadl"></a>WADL</span><span class="sxs-lookup"><span data-stu-id="41c2b-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="41c2b-122">Er zijn momenteel geen bekende problemen van WADL importeren.</span><span class="sxs-lookup"><span data-stu-id="41c2b-122">There are no known WADL import issues currently.</span></span>


[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
