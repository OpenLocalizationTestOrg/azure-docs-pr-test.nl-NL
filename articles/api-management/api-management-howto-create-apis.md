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
# <a name="how-toocreate-apis-in-azure-api-management"></a>Hoe toocreate API's in Azure API Management
Een API Management-API vertegenwoordigt een reeks bewerkingen die kunnen worden aangeroepen door clienttoepassingen. Nieuwe API's worden gemaakt in de publicatieportal hello en vervolgens Hallo gewenst bewerkingen zijn toegevoegd. Zodra het Hallo-bewerkingen worden toegevoegd, wordt Hallo API tooa product is toegevoegd en kan worden gepubliceerd. Als een API is gepubliceerd, kan het geabonneerde tooand gebruikt door ontwikkelaars zijn.

Deze handleiding wordt getoond Hallo eerste stap in Hallo proces: hoe toocreate en configureert u een nieuwe API in API Management. Zie voor meer informatie over het toevoegen van bewerkingen en een product publiceren [hoe tooadd operations tooan API] [ How tooadd operations tooan API] en [hoe toocreate en een product publiceren] [ How toocreate and publish a product].

## <a name="create-new-api"></a>Maken van een nieuwe API
API's zijn gemaakt en geconfigureerd in de publicatieportal Hallo. tooaccess publisher en klik op Hallo **publicatieportal** in hello Azure-Portal voor uw API Management-service.

![Publicatieportal][api-management-management-console]

> Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.
> 
> 

Klik op **API's** van Hallo **API Management** menu op Hallo links en klik vervolgens op **API toevoegen**.

![API maken][api-management-create-api]

Gebruik Hallo **nieuwe API toevoegen** venster tooconfigure Hallo nieuwe API.

![Nieuwe API toevoegen][api-management-add-new-api]

Hallo volgende velden zijn gebruikte tooconfigure Hallo nieuwe API.

* **De naam van de web-API** biedt een unieke en beschrijvende naam voor Hallo API. Deze wordt weergegeven in het Hallo-ontwikkelaars en uitgever portals.
* **Webservice-URL** verwijzingen Hallo Hallo API implementeren HTTP-service. API management verzendt aanvragen toothis adres.
* **Achtervoegsel voor web-API-URL** toegevoegde toohello basis-URL voor Hallo API management-service is. Hallo basis-URL is gebruikelijk voor alle API's die worden gehost door een exemplaar van API Management-service. API Management API's onderscheidt door hun achtervoegsel en daarom Hallo achtervoegsel moet uniek zijn voor elke API voor een opgegeven uitgever.
* **Web-API-URL-schema** bepaalt welke protocollen gebruikte tooaccess Hallo API kunnen zijn. Standaard HTTPs is opgegeven.
* toooptionally deze nieuwe API tooa product toevoegen, klikt u op Hallo **producten (optioneel)** vervolgkeuzelijst en kies een product. Deze stap kan herhaalde verschillende keren tooadd Hallo API toomultiple producten zijn.

Zodra het Hallo gewenst waarden zijn geconfigureerd, klikt u op **opslaan**. Zodra de nieuwe API Hallo is gemaakt, wordt hello overzichtspagina voor Hallo API weergegeven in de publicatieportal Hallo.

![API-overzicht][api-management-api-summary]

## <a name="configure-api-settings"></a>Instellingen voor de API configureren
U kunt Hallo **instellingen** tooverify tabblad en Hallo-configuratie voor een API te bewerken. **De naam van de web-API**, **webservice-URL**, en **achtervoegsel URL Web-API** zijn in eerste instantie ingesteld als Hallo API wordt gemaakt en kan worden gewijzigd hier. **Beschrijving** biedt een optionele beschrijving en **Web API-URL-schema** bepaalt welke protocollen gebruikte tooaccess Hallo API kunnen zijn.

![Instellingen voor de API][api-management-api-settings]

tooconfigure gatewayverificatie hello back-end-service geïmplementeerd Hallo-API, selecteert u Hallo **beveiliging** tabblad Hallo **met referenties** vervolgkeuzelijst mag gebruikte tooconfigure **HTTP Basic** of **clientcertificaten** verificatie. Basisverificatie toouse HTTP gewoon Hallo desired-referenties invoeren. Zie voor meer informatie over het gebruik van verificatie van clientcertificaten [hoe toosecure back-end-services met behulp van client-certificaat gebaseerde verificatie in Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].

Hallo **beveiliging** tabblad kan ook worden gebruikt tooconfigure **gebruikersautorisatie** met behulp van OAuth 2.0. Zie voor meer informatie [hoe tooauthorize developer gebruikersaccounts via OAuth 2.0 in Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].

![Instellingen voor basisverificatie][api-management-api-settings-credentials]

Klik op **opslaan** toosave wijzigingen die u aanbrengt toohello instellingen voor de API.

## <a name="next-steps"> </a>Volgende stappen
Nadat een API is gemaakt en het Hallo-instellingen die zijn geconfigureerd, de volgende stappen Hallo zijn tooadd Hallo operations toohello API, Hallo API tooa product toevoegen en publiceren zodat deze beschikbaar voor ontwikkelaars. Zie Hallo volgende artikelen voor meer informatie.

* [Hoe tooadd operations tooan API][How tooadd operations tooan API]
* [Hoe toocreate en een product publiceren][How toocreate and publish a product]

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
