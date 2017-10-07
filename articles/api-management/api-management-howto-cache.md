---
title: aaaAdd opslaan in cache tooimprove prestaties in Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooimprove Hallo latentie, bandbreedtegebruik en webservice voor API Management-serviceaanroepen geladen.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a>Toevoegen van cachebewerkingen tooimprove prestaties in Azure API Management
Bewerkingen in API Management kunnen worden geconfigureerd voor het opslaan van antwoorden in de cache. Door het opslaan van antwoorden in de cache kan de API-latentie, het bandbreedteverbruik en de webservicewerklast aanzienlijk worden verminderd voor gegevens die niet vaak wijzigen.

Deze handleiding ontdekt u hoe tooadd antwoord in cache opslaan voor uw API en beleidsregels voor Hallo voorbeeld-Echo-API-bewerkingen te configureren. U kunt vervolgens Hallo bewerking aanroepen vanuit het Hallo developer portal tooverify cache in te grijpen.

> [!NOTE]
> Zie [Aangepast opslaan in cache in Azure API Management](api-management-sample-cache-by-key.md) voor informatie over het opslaan van items in de cache per sleutel met behulp van beleidsexpressies.
> 
> 

## <a name="prerequisites"></a>Vereisten
Voordat de volgende Hallo stappen in deze handleiding, hebt u een API Management-service-exemplaar met een API en een product dat is geconfigureerd. Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.

## <a name="configure-caching"> </a>Een bewerking voor opslaan in cache configureren
In deze stap controleert u opslaan in cache-instellingen van Hallo Hallo **GET Resource (in cache)** bewerking van Hallo voorbeeld-Echo-API.

> [!NOTE]
> Elk exemplaar van API Management-service is vooraf geconfigureerd met een Echo-API die kan worden gebruikt tooexperiment met en meer informatie over API Management. Zie [Aan de slag met Azure API Management][Get started with Azure API Management] voor meer informatie.
> 
> 

tooget gestart, klikt u op **publicatieportal** in hello Azure-Portal voor uw API Management-service. Hiermee gaat u toohello API Management-publicatieportal.

![Publicatieportal][api-management-management-console]

Klik op **API's** van Hallo **API Management** menu op Hallo links en klik vervolgens op **Echo-API**.

![Echo-API][api-management-echo-api]

Klik op Hallo **Operations** tabblad en klik vervolgens op Hallo **GET Resource (in cache)** bewerking Hallo **Operations** lijst.

![Bewerkingen Echo-API][api-management-echo-api-operations]

Klik op Hallo **opslaan in cache** tabblad tooview Hallo opslaan in cache-instellingen voor deze bewerking.

![Tabblad Opslaan in cache][api-management-caching-tab]

tooenable cache voor een bewerking, selecteer Hallo **inschakelen** selectievakje. In dit voorbeeld is opslaan in cache ingeschakeld.

Het bewerkingsantwoord van elke sleutelhash op basis van waarden in Hallo Hallo **variëren op queryreeksparameters** en **variëren op headers** velden. Als u meerdere antwoorden op basis van queryreeksparameters of headers toocache wilt, kunt u ze configureren in deze twee velden.

**Duur** wordt Hallo Vervalinterval opgegeven van Hallo in de cache opgeslagen reacties. In dit voorbeeld hello-interval is **3600** seconden, dat gelijkwaardige tooone uur.

Eerste aanvraag toohello Hallo opslaan in cache configureren in dit voorbeeld gebruikt, Hallo **GET Resource (in cache)** bewerking een antwoord geretourneerd van Hallo back-endservice. Dit antwoord wordt in de cache opgeslagen, ingevoerd met Hallo opgegeven headers en query tekenreeksparameters. Volgende aanroepen toohello bewerking, met overeenkomende parameters, Hallo hebben in de cache opgeslagen antwoord geretourneerd totdat Hallo cacheduurinterval is verlopen.

## <a name="caching-policies"></a>Revisie Hallo cachebeleidsregels
In deze stap controleert u opslaan in cache-instellingen voor Hallo Hallo **GET Resource (in cache)** bewerking van Hallo voorbeeld-Echo-API.

Wanneer er cache-instellingen zijn geconfigureerd voor een bewerking op Hallo **opslaan in cache** tabblad opslaan in cache toegevoegd voor Hallo-bewerking. Deze beleidsregels kunnen worden bekeken en bewerkt in de beleidseditor Hallo.

Klik op **beleid** van Hallo **API Management** menu op Hallo linker- en selecteer vervolgens **Echo-API / GET Resource (in cache)** van Hallo **bewerking**vervolgkeuzelijst.

![Bewerking beleidsbereik][api-management-operation-dropdown]

Hallo-beleid voor deze bewerking weergegeven in de beleidseditor Hallo.

![Beleidseditor API Management][api-management-policy-editor]

Hallo beleidsdefinitie voor deze bewerking bevat Hallo beleidsregels waarmee Hallo caching configuratie gedefinieerd, die is gecontroleerd met Hallo **opslaan in cache** tabblad in de vorige stap Hallo.

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> Wijzigingen toohello cachebeleidsregels in de beleidseditor hello, worden weergegeven op Hallo **opslaan in cache** tabblad van een bewerking en vice versa.
> 
> 

## <a name="test-operation"></a>Een bewerking aanroepen en Hallo opslaan in cache testen
toosee hello caching in actie, kunnen we Hallo bewerking aanroepen vanuit Hallo-portal voor ontwikkelaars. Klik op **ontwikkelaarsportal** in Hallo menu rechtsboven.

![ontwikkelaarsportal][api-management-developer-portal-menu]

Klik op **API's** in Hallo bovenste menu en selecteer vervolgens **Echo-API**.

![Echo-API][api-management-apis-echo-api]

> Als er slechts één API is geconfigureerd of zichtbaar tooyour-account op de API's te klikken u rechtstreeks toohello bewerkingen voor die API gaat.
> 
> 

Selecteer Hallo **GET Resource (in cache)** bewerking en klik vervolgens op **Console openen**.

![Console openen][api-management-open-console]

Hallo-console kunt u bewerkingen rechtstreeks vanuit de ontwikkelaarsportal hello tooinvoke.

![Console][api-management-console]

Behoud de standaardwaarden Hallo voor **param1** en **param2**.

Selecteer de gewenste sleutel in Hallo Hallo **abonnementssleutel** vervolgkeuzelijst. Als uw account slechts één abonnement heeft, is de sleutel al geselecteerd.

Voer **sampleheader: Value1** in Hallo **aanvraagheaders** in het tekstvak.

Klik op **HTTP Get** en maak een notitie van Hallo antwoordheaders.

Voer **sampleheader: Value2** in Hallo **aanvraagheaders** in het tekstvak en klik vervolgens op **HTTP Get**.

Houd er rekening mee dat Hallo de waarde van **sampleheader** nog steeds **value1** Hallo reactie. Probeer een aantal verschillende waarden en merk op dat in de cache opgeslagen reactie van de eerste aanroep Hallo Hallo wordt geretourneerd.

Voer **25** in Hallo **param2** veld en klik vervolgens op **HTTP Get**.

Houd er rekening mee dat Hallo de waarde van **sampleheader** in Hallo antwoord is nu **value2**. Omdat Hallo per querytekenreeks Bewerkingsresultaten, Hallo vorige cacheantwoord niet geretourneerd.

## <a name="next-steps"> </a>Volgende stappen
* Zie voor meer informatie over cachebeleidsregels [cachebeleidsregels] [ Caching policies] in Hallo [documentatie voor API Management-beleid][API Management policy reference].
* Zie [Aangepast opslaan in cache in Azure API Management](api-management-sample-cache-by-key.md) voor informatie over het opslaan van items in de cache per sleutel met behulp van beleidsexpressies.

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
