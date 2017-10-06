---
title: aaaHow tooadd operations tooan API in Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooadd operations tooan API in Azure API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a>Hoe tooadd operations tooan API in Azure API Management
Voordat een API in API Management kan worden gebruikt, kunnen bewerkingen moeten worden toegevoegd. Dit toont hoe begeleiden tooadd en configureren van verschillende soorten bewerkingen tooan API in API Management.

## <a name="add-operation"></a>Een bewerking toevoegen
Bewerkingen worden toegevoegd en tooan API in de publicatieportal Hallo geconfigureerd. tooaccess publisher en klik op Hallo **publicatieportal** in hello Azure-Portal voor uw API Management-service.

![Publicatieportal][api-management-management-console]

> Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.
> 
> 

Selecteer Hallo gewenste API in de publicatieportal hello en selecteer vervolgens Hallo **Operations** tabblad. 

![Bewerkingen][api-management-operations]

Klik op **bewerking toevoegen** tooadd een nieuwe bewerking. Hallo **nieuwe bewerking** wordt weergegeven en Hallo **handtekening** tabblad wordt standaard geselecteerd.

![Bewerking toevoegen][api-management-add-operation]

Geef Hallo **HTTP-term** door in de vervolgkeuzelijst hello te kiezen.

![HTTP-methode][api-management-http-method]

<a name="url-template"></a>

Hallo URL sjabloon door te typen in een URL-fragment die bestaan uit een of meer URL-padsegmenten en nul of meer queryreeksparameters definiëren. Hallo URL sjabloon, toegevoegde toohello basis-URL van Hallo API, identificeert één HTTP-bewerking. Bevat een of meer benoemde variabele onderdelen die zijn geïdentificeerd door accolades. Deze variabele delen Sjabloonparameters worden genoemd en worden de waarden die worden opgehaald uit het Hallo-aanvraag-URL wanneer het Hallo-aanvraag wordt verwerkt door Hallo API Management-platform dynamisch toegewezen.

> Hallo URL sjabloon kan jokertekenpatronen bevatten. Bijvoorbeeld, geven `/*` sturen alle aanvragen voor deze HTTP-methode toohello terug eindigt service.

![URL-sjabloon][api-management-url-template]

<a name="rewrite-url-template"></a>

Geef desgewenst Hallo **herschrijven van URL sjabloon**. Hiermee kunt u toouse Hallo standaard URL-sjabloon voor het verwerken van inkomende aanvragen op de front-hello, tijdens het aanroepen van Hallo back-end via een geconverteerde URL volgens toohello Herschrijf de sjabloon. Sjabloonparameters van Hallo URL sjabloon moeten worden gebruikt in Hallo herschrijven sjabloon. Hallo volgende voorbeeld ziet u hoe inhoudstype gecodeerd zoals padsegment in de webservice Hallo uit het vorige voorbeeld Hallo kan worden opgegeven als een queryparameter in Hallo dat API gepubliceerd via Hallo Hallo URL sjablonen met behulp van API Management-platform.

![Herschrijven van URL-sjabloon][api-management-url-template-rewrite]

Gebruikmaken van aanroepfuncties toohello bewerking Hallo indeling `/customers?customerid=ALFKI` en dit te worden toegewezen`/Customers('ALFKI')` wanneer Hallo back-end-service wordt aangeroepen.

**Weergave** naam en **beschrijving** Geef een beschrijving van de bewerking Hallo en gebruikte tooprovide documentatie zijn toohello ontwikkelaars met behulp van deze API in Hallo developer portal.

![Beschrijving][api-management-description]

Hallo bewerking beschrijving kan worden opgegeven als tekst zonder opmaak of HTML in Hallo **beschrijving** in het tekstvak.

## <a name="operation-caching"></a>Bewerking opslaan in cache
Antwoord in cache opslaan vermindert de latentie waargenomen door de consument Hallo API, verlaagt bandbreedteverbruik en afname Hallo belasting op het Hallo HTTP web service implementeren Hallo API. 

tooeasily en snel geschikt maken voor Hallo bewerking, selecteer Hallo caching **opslaan in cache** tabblad en controleer Hallo **inschakelen** selectievakje.

![Caching][api-management-caching-tab]

**Duur** Hallo periode gedurende welke Hallo bewerkingsantwoord in cache Hallo blijft bevat. Hallo-standaardwaarde is 3600 seconden oftewel 1 uur.

Cache-sleutels zijn gebruikte toodifferentiate tussen antwoorden zodat Hallo-antwoord overeenkomt tooeach verschillende Cachesleutel een eigen afzonderlijke waarde in de cache krijgt. Voer desgewenst specifieke queryreeksparameters en/of HTTP-headers toobe gebruikt in de cache-sleutelwaarden in Hallo computing **variëren op queryreeksparameters** en **variëren op headers** tekstvakken respectievelijk. Wanneer er geen is opgegeven, volledige aanvraag-URL en Hallo volgende HTTP-headerwaarden worden gebruikt in de cache genereren van sleutels: **accepteren** en **Accept-Charset**.

> Zie voor meer informatie over opslaan in cache en cachebeleidsregels [hoe toocache bewerking resulteert in Azure API Management][How toocache operation results in Azure API Management].
> 
> 

## <a name="request-parameters"></a>Aanvraagparameters
Bewerkingsparameters worden beheerd op het tabblad Hallo-Parameters. Parameters die zijn opgegeven in Hallo **URL sjabloon** op Hallo **handtekening** tabblad worden automatisch toegevoegd en kan worden gewijzigd alleen Hallo URL door sjabloon te bewerken. Extra parameters kunnen handmatig worden ingevoerd.

een nieuwe queryparameter tooadd klikt u op **queryparameter toevoegen** en voer de volgende informatie Hallo:

* **Naam** -parameternaam.
* **Beschrijving** -een korte beschrijving van het Hallo-parameter (optioneel).
* **Type** -type voor parameter in de vervolgkeuzelijst Hallo geselecteerd.
* **Waarden** -waarden die kunnen worden toegewezen toothis-parameter. Hallo-waarden kan worden als standaardwaarde gemarkeerd (optioneel).
* **Vereist** -Hallo parameter verplicht te stellen door Hallo selectievakje. 

![Parameters van de aanvraag][api-management-request-parameters]

## <a name="request-body"></a>Aanvraagtekst
Als het Hallo-bewerking staat (bijvoorbeeld PUT, POST) en kunt u desgewenst een voorbeeld van dit voor alle Hallo hoofdtekst ondersteunde weergave-indelingen (bijvoorbeeld json, XML) vereist. 

> Hallo aanvraagtekst alleen voor documentatie wordt gebruikt en niet wordt gevalideerd.
> 
> 

een aanvraagtekst tooenter overschakelen toohello **hoofdtekst** tabblad.

Klik op **weergave toevoegen**begint te typen gewenste inhoudstype-naam (bijvoorbeeld application/json), selecteert u deze in de vervolgkeuzelijst Hallo en plakken Hallo voorbeeld van de aanvraag hoofdtekst in geselecteerde Hallo-indeling in het tekstvak Hallo gewenst. 

![Aanvraagtekst][api-management-request-body]

In de aanvullende toorepresentations, kunt u ook een optionele beschrijving in Hallo opgeven **beschrijving** in het tekstvak.

## <a name="responses"></a>Antwoorden
Het is een goede gewoonte tooprovide voorbeelden van reacties voor alle statuscodes die Hallo-bewerking kan opleveren. Elke statuscode mogelijk meer dan één antwoord hoofdtekst voorbeeld, één voor elk Hallo inhoudstypen ondersteund. 

een antwoord tooadd klikt u op **toevoegen** en typ de gewenste Hallo-statuscode. In dit voorbeeld Hallo status code is **200 OK**. Zodra het Hallo-code wordt weergegeven in de vervolgkeuzelijst hello, selecteren en Hallo antwoordcode is gemaakt en toegevoegd tooyour bewerking.

![Reactiecode][api-management-response-code]

Klik op **weergave toevoegen**, typ de naam van de gewenste inhoudstype hello (bijvoorbeeld application/json) en selecteer vervolgens in Hallo vervolgkeuzelijst.

![Inhoudstype voor hoofdtekst][api-management-response-body-content-type]

Hallo antwoord hoofdtekst voorbeeld in de geselecteerde indeling Hallo in Hallo tekstvak plakken. 

![Antwoordtekst][api-management-response-body]

Indien gewenst, voer een optionele beschrijving in Hallo **beschrijving** in het tekstvak.

Zodra het Hallo-bewerking is geconfigureerd, klikt u op **opslaan**.

## <a name="next-steps"> </a>Volgende stappen
Nadat Hallo bewerkingen zijn tooan API toegevoegd, wordt de volgende stap Hallo tooassociate Hallo API met een product is en deze publiceren zodat ontwikkelaars kunnen aanroepen op de operations.

* [Hoe toocreate en een product publiceren][How toocreate and publish a product]

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
