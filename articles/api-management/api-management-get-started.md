---
title: aaaManage uw eerste API in Azure API Management | Microsoft Docs
description: Ontdek hoe toocreate API's, bewerkingen toevoegen en aan de slag met API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a>Uw eerste API beheren in Azure API Management
## <a name="overview"> </a>Overzicht
Deze handleiding wordt beschreven hoe tooquickly aan de slag met Azure API Management en uw eerste API-aanroep.

## <a name="concepts"> </a>Wat is Azure API Management?
U kunt elke back-end voor Azure API Management tootake gebruiken en start een volwaardig API-programma op basis van deze.

Algemene scenario's omvatten de volgende:

* **Mobiele infrastructuur beveiligen** door het beperken van toegang met API-sleutels, het voorkomen van DOS-aanvallen door middel van beperking, of het gebruiken van geavanceerd beveiligingsbeleid zoals validatie van JWT-tokens.
* **ISV-partner-partnerecosystemen inschakelen** door het aanbieden van snelle onboarding via Hallo developer-portal en het bouwen van een API-façade toodecouple van interne implementaties die zijn niet gereed zijn voor partner.
* **Een intern API-programma uitvoeren** door het aanbieden van een centrale locatie voor Hallo organisatie toocommunicate over Hallo beschikbaarheid en de meest recente tooAPIs wijzigt, beperken van toegang op basis van organisatieaccounts, alle gebaseerd op een veilig kanaal tussen Hallo API-gateway en het Hallo-back-end.

Hallo-systeem bestaat uit Hallo volgende onderdelen:

* Hallo **API-gateway** Hallo eindpunt waarmee:
  
  * API-aanroepen ontvangen en doorgestuurd tooyour back-ends accepteert.
  * API-sleutels, JWT-tokens, certificaten en andere referenties worden geverifieerd.
  * Quota voor gebruik en frequentielimieten worden afgedwongen.
  * Hiermee transformeert u uw API snel Hallo zonder codewijzigingen.
  * Antwoorden van de back-end in de cache worden opgeslagen indien ingesteld.
  * Aanroepmetagegevens worden voor analysedoeleinden aan het logboek toegevoegd.
* Hallo **publicatieportal** is Hallo beheerinterface waar u uw API-programma instelt. Gebruik deze voor het volgende:
  
  * API-schema definiëren of importeren.
  * API's verpakken in producten.
  * Beleidsregels instellen zoals quota of transformaties voor Hallo API's.
  * Inzicht krijgen van analytische gegevens.
  * Gebruikers beheren.
* Hallo **ontwikkelaarsportal** fungeert als Hallo hoofdweb aanwezigheid voor ontwikkelaars, ze kunnen hier:
  
  * API-documentatie lezen.
  * Een API via de interactieve console Hallo uitproberen.
  * Een account maken en zich abonneren tooget API-sleutels.
  * Analytische gegevens openen over hun eigen gebruik.

## <a name="create-service-instance"> </a>Een API Management-exemplaar maken
> [!NOTE]
> toocomplete in deze zelfstudie, moet u een Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een gratis account maken. Zie [Gratis proefversie van Azure][Azure Free Trial] voor meer informatie.
> 
> 

Hallo eerste stap bij het werken met API Management is toocreate een service-exemplaar. Meld u aan toohello [Azure Portal] [ Azure Portal] en klik op **nieuw**, **Web en mobiel**, **API Management**.

![Nieuw API Management-exemplaar][api-management-create-instance-menu]

Voor **naam**, Geef een unieke subdomeinnaam naam toouse voor Hallo service-URL.

Kies Hallo gewenst **abonnement**, **resourcegroep** en **locatie** voor uw service-exemplaar.

Voer **Contoso Ltd.** voor Hallo **organisatienaam**, en voer uw e-mailadres in Hallo **E-Mail beheerder** veld.

> [!NOTE]
> Dit e-mailadres wordt gebruikt voor meldingen van Hallo API Management-systeem. Zie voor meer informatie [hoe tooconfigure meldingen en e-mailsjablonen in Azure API Management][How tooconfigure notifications and email templates in Azure API Management].
> 
> 

![Nieuwe API Management-service][api-management-create-instance-step1]

Service-exemplaren van API Management zijn beschikbaar in drie categorieën: Developer, Standard en Premium.

> [!NOTE]
> Hallo categorie Developer is voor ontwikkeling, testen en test API-programma's waar maximale beschikbaarheid niet van belang is. In Hallo Standard en Premium-categorieën, kunt u uw aantal gereserveerde eenheid toohandle meer verkeer schalen. Hallo-categorieën Standard en Premium bieden uw API Management-service met Hallo meeste verwerkingskracht en prestaties. U kunt elke categorie gebruiken om deze zelfstudie te voltooien. Zie voor meer informatie over API Management-categorieën [API Management-prijzen][API Management pricing].
> 
> 

Klik op **maken** toostart inrichting van uw service-exemplaar.

![Nieuwe API Management-service][api-management-instance-created]

Zodra Hallo service-exemplaar is gemaakt, wordt de volgende stap Hallo toocreate is of een API importeren.

## <a name="create-api"> </a>Een API importeren
Een API bestaat uit een reeks bewerkingen die vanuit een clienttoepassing kunnen worden aangeroepen. API-bewerkingen worden via proxy tooexisting webservices.

API's kunnen handmatig worden gemaakt (en bewerkingen kunnen handmatig worden toegevoegd) of ze kunnen worden geïmporteerd. In deze zelfstudie importeren we Hallo API voor een voorbeeldrekenmachinewebservice door Microsoft geleverd en gehost in Azure.

> [!NOTE]
> Zie voor instructies over het maken van een API en handmatig toevoegen van bewerkingen [hoe toocreate API's](api-management-howto-create-apis.md) en [hoe tooadd operations tooan API](api-management-howto-add-operations.md).
> 
> 

API's worden geconfigureerd in de publicatieportal Hallo. tooreach, klikt u op **publicatieportal** Hallo service werkbalk van.

![Publicatieportal][api-management-management-console]

tooimport hello Rekenmachine-API, klikt u op **API's** van Hallo **API Management** menu op Hallo links en klik vervolgens op **Import API**.

![Knop API importeren][api-management-import-api]

Voer Hallo tooconfigure hello basisrekenmachine-API stappen te volgen:

1. Klik op **van URL**, voer **http://calcapi.cloudapp.net/calcapi.json** in Hallo **URL specificatiedocument** tekst vak en klikt u op Hallo **Swagger**  keuzerondje.
2. Type **calc** in Hallo **achtervoegsel URL Web-API** in het tekstvak.
3. Klik in het Hallo **producten (optioneel)** vak en kies **Starter**.
4. Klik op **opslaan** tooimport Hallo API.

![Nieuwe API toevoegen][api-management-import-new-api]

> [!NOTE]
> In **API Management** wordt momenteel zowel versie 1.2 als versie 2.0 van het Swagger-document voor import ondersteund. Hoewel in de [Swagger 2.0-specificatie](http://swagger.io/specification) wordt aangegeven dat eigenschappen `host`, `basePath` en `schemes` optioneel zijn, **MOET** uw Swagger 2.0-document deze eigenschappen bevatten, anders wordt het niet geïmporteerd. 
> 
> 

Zodra het Hallo-API is geïmporteerd, wordt hello overzichtspagina voor Hallo API weergegeven in de publicatieportal Hallo.

![API-overzicht][api-management-imported-api-summary]

Hallo API-sectie bevat meerdere tabbladen. Hallo **samenvatting** tabblad worden basismetrieken en informatie over Hallo API. Hallo [instellingen](api-management-howto-create-apis.md#configure-api-settings) tabblad gebruikte tooview en bewerk Hallo configuratie voor een API is. Hallo [Operations](api-management-howto-add-operations.md) tabblad is gebruikte toomanage Hallo van API-bewerkingen. Hallo **beveiliging** tabblad gebruikte tooconfigure gatewayverificatie voor de back-endserver Hallo kan worden met behulp van basisverificatie of [wederzijdse certificaatverificatie](api-management-howto-mutual-certificates.md), en tooconfigure [ gebruikersautorisatie met behulp van OAuth 2.0](api-management-howto-oauth2.md).  Hallo **problemen** tabblad is gebruikte tooview problemen die worden gerapporteerd door Hallo-ontwikkelaars die uw API's gebruiken. Hallo **producten** tabblad is gebruikte tooconfigure Hallo producten die deze API bevatten.

Standaard wordt elk API Management-exemplaar geleverd met twee voorbeeldproducten:

* **Starter**
* **Onbeperkt**

In deze zelfstudie is Hallo basisrekenmachine-API toohello Starter-product toegevoegd wanneer Hallo API is geïmporteerd.

In de volgorde toomake aanroepen tooan API ontwikkelaars moeten zich eerst abonneren tooa product waarmee ze toegang tooit. Ontwikkelaars kunnen zich abonneren tooproducts in Hallo developer-portal of beheerders kunnen ontwikkelaars tooproducts in de publicatieportal Hallo abonneren. U bent een beheerder omdat u Hallo API Management-exemplaar in Hallo vorige stappen in de zelfstudie hello, gemaakt zodat u al geabonneerd tooevery product standaard bent.

## <a name="call-operation"></a>Een bewerking aanroepen vanuit de ontwikkelaarsportal Hallo
Bewerkingen rechtstreeks vanuit de ontwikkelaarsportal hello, waardoor een handige manier tooview kunnen worden aangeroepen en Hallo bewerkingen van een API testen. In deze zelfstudiestap roept u Hallo basisrekenmachine-API van **twee gehele getallen toevoegen** bewerking. Klik op **-portal voor ontwikkelaars** in Hallo Hallo menu rechts van de publicatieportal Hallo top.

![ontwikkelaarsportal][api-management-developer-portal-menu]

Klik op **API's** van Hallo bovenste menu en klik vervolgens op **basisrekenmachine** toosee Hallo beschikbare bewerkingen.

![ontwikkelaarsportal][api-management-developer-portal-calc-api]

Houd er rekening mee Hallo voorbeeldbeschrijvingen en parameters die zijn geïmporteerd samen met de Hallo API en bewerkingen, om documentatie voor ontwikkelaars Hallo die wordt gebruikt voor deze bewerking te bieden. Deze beschrijvingen kunnen ook worden toegevoegd wanneer bewerkingen handmatig worden toegevoegd.

Hallo toocall **twee gehele getallen toevoegen** bewerking, klikt u op **Try it**.

![Probeer het nu][api-management-developer-portal-calc-api-console]

Sommige waarden opgeven voor Hallo parameters of houden Hallo standaardwaarden en klik op **verzenden**.

![HTTP Get][api-management-invoke-get]

Nadat een bewerking is aangeroepen, Hallo ontwikkelaarsportal hello **antwoordstatus**, Hallo **antwoordheaders**, en er is een **antwoordinhoud**.

![Antwoord][api-management-invoke-get-response]

## <a name="view-analytics"> </a>Analytische gegevens bekijken
tooview analytics voor de basisrekenmachine switch back toohello publicatieportal door te selecteren **beheren** in Hallo Hallo menu rechts van de ontwikkelaarsportal Hallo top.

![Beheren][api-management-manage-menu]

Hallo standaardweergave voor de publicatieportal Hallo is Hallo **Dashboard**, waarmee u een overzicht van uw exemplaar van API Management.

![Dashboard][api-management-dashboard]

Aanwijzen Hallo muis over Hallo-grafiek voor **basisrekenmachine** toosee Hallo specifieke metrische gegevens voor het gebruik van Hallo Hallo API voor een bepaalde periode.

> [!NOTE]
> Als u niet alle regels in uw grafiek ziet, switch back toohello developer-portal en voert u enkele aanroepen in Hallo API, wacht even en vervolgens terugkeren toohello dashboard.
> 
> 

Klik op **Details weergeven** tooview Hallo overzichtspagina voor Hallo API, met inbegrip van een grotere versie van Hallo weergegeven metrische gegevens.

![Analytische gegevens][api-management-mouse-over]

![Samenvatting][api-management-api-summary-metrics]

Klik voor gedetailleerde metrische gegevens en rapporten **Analytics** van Hallo **API Management** menu aan de linkerkant Hallo.

![Overzicht][api-management-analytics-overview]

Hallo **Analytics** sectie heeft Hallo volgende vier tabbladen:

* **In een oogopslag** bevat algemene informatie over het gebruik en status metrische gegevens, evenals Hallo belangrijkste ontwikkelaars, producten, API's en bewerkingen.
* **Gebruik** biedt een diepgaande blik op API-aanroepen en bandbreedte, met inbegrip van een geografische weergave.
* **Status** richt zich op statuscodes, succespercentages van de cache, reactietijden, en reactietijden van de API en de service.
* **Activiteit** biedt rapporten die Inzoomen op Hallo specifieke activiteit per ontwikkelaar, product, API en bewerking.

## <a name="next-steps"> </a>Volgende stappen
* Meer informatie over hoe te[uw API beveiligen met frequentielimieten](api-management-howto-product-with-rules.md).

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
