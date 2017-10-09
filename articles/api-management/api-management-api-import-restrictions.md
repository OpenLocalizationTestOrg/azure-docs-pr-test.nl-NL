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
# <a name="api-import-restrictions-and-known-issues"></a>API importeren beperkingen en bekende problemen
## <a name="about-this-list"></a>Over deze lijst
Terwijl alles in het werk wordt tooensure die uw API te importeren in Azure API Management als naadloze is en foutloos mogelijk, we zo nu en dan beperkingen opleggen of problemen die toobe verholpen moet voordat u met succes kunt importeren. In dit artikel wordt deze georganiseerd door indeling voor het importeren van Hallo Hallo API.

## <a name="open-api"></a>API/Swagger openen
In het algemeen als u uw document Open API importeren fouten ontvangt, zorg ervoor dat u hebt deze - gevalideerd met de designer Hallo Hallo in de nieuwe Azure Portal (ontwerp - Front-End - API specificatie Editor openen), of met een 3rd partij hulpprogramma zoals <a href="http://www.swagger.io"> Swagger Editor</a>.

* **Hostnaam** moet een name-hostnaamkenmerk.
* **Pad baseren** moet een kenmerk basispad.
* **Schema's** moet een matrix van het schema. 

## <a name="wsdl"></a>WSDL
WSDL-bestanden zijn gebruikte toogenerate SOAP Pass Through-API's of fungeren als Hallo back-end van een SOAP-REST-API.

* **WSDL: import** wordt momenteel niet ondersteund met behulp van dit kenmerk API's. Klanten moeten Hallo geïmporteerd elementen samenvoegen in één document.
* **Berichten met meerdere onderdelen** worden momenteel niet ondersteund.
* **WCF-wsHttpBinding** SOAP-services die zijn gemaakt met Windows Communication Foundation basicHttpBinding moeten gebruiken - wsHttpBinding wordt niet ondersteund.
* **MTOM** MTOM-Services <em>kan</em> werken. Op dit moment is geen officiële ondersteuning geboden.
* **Recursie** typen die zijn gedefinieerd recursief (bv. Raadpleeg tooan matrix van zichzelf) worden niet ondersteund.

## <a name="wadl"></a>WADL
Er zijn momenteel geen bekende problemen van WADL importeren.


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
