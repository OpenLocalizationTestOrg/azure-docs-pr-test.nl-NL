---
title: overzicht en belangrijkste concepten van aaaAzure API Management | Microsoft Docs
description: Meer informatie over API's, producten, rollen, groepen en andere belangrijke concepten van API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: e71da405-835a-48f3-956f-45c1a85698d7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a77b24b4632d868afa15bd6cf88060982046cb38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-api-management"></a>Wat is API Management?
API Management helpt organisaties bij het publiceren van API's tooexternal, partner en interne ontwikkelaars toounlock Hallo potentieel van hun gegevens en services. Bedrijven zijn overal tooextend hun activiteiten zoeken als een digitaal platform, waarbij nieuwe kanalen, nieuwe klanten worden gevonden en grotere betrokkenheid met bestaande. API Management biedt Hallo core vaardigheden tooensure een geslaagd API-programma via ontwikkelaarsbetrokkenheid, zakelijke inzichten, analytics, beveiliging en bescherming.

Bekijkt hello volgende video voor een overzicht van Azure API Management en leer hoe toouse API Management tooadd veel functies tooyour API, met inbegrip van toegangsbeheer, beoordelen beperken, bewaking, logboekregistratie en antwoord in cache plaatsen, met minimale inspanning.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-API-Management-Overview/player]
> 
> 

toouse API Management, beheerders maken API's. Elke API bestaat uit een of meer bewerkingen en elke API tooone of meer producten kan worden toegevoegd. een API toouse, ontwikkelaars abonneren tooa product dat die API bevat en vervolgens zij Hallo van API-bewerking, onderwerp tooany gebruiksbeleid die mogelijk van kracht kunnen aanroepen.

In dit onderwerp wordt een overzicht gegeven van de belangrijkste concepten van API Management.

> [!NOTE]
> Zie voor meer informatie, Hallo [Cloud-gebaseerde API Management: Harnessing Hallo kracht van API's](http://j.mp/ms-apim-whitepaper) PDF-document. In dit inleidende technische document over API Management door CITO Research wordt het volgende besproken: 
> 
> * Algemene API-vereisten en -uitdagingen
> * API's loskoppelen en façades presenteren
> * Ontwikkelaars snel aan de slag helpen
> * Toegang beveiligen
> * Analytische en metrische gegevens
> * Controle en inzicht verkrijgen met een API Management-platform
> * Cloud- versus on-premises oplossingen gebruiken
> * Azure API Management
> 
> 

## <a name="apis"> </a>API's en bewerkingen
Hallo basis van een service-exemplaar van API Management-API's zijn. Elke API vertegenwoordigt een reeks bewerkingen beschikbaar toodevelopers. Elke API bevat een verwijzing toohello back-end-service die Hallo API implementeert en bewerkingen toohello bewerkingen die zijn geïmplementeerd door het back-endservice Hallo toewijzen. Bewerkingen in API Management zijn zeer goed te configureren, met controle over URL-toewijzing, query- en padparameters, aanvraag- en antwoordinhoud en het in de cache opslaan van bewerkingsantwoorden. Frequentielimiet, quota en IP-beperking beleidsregels kunnen ook worden geïmplementeerd op Hallo API of afzonderlijke bewerking niveau.

Zie voor meer informatie [hoe toocreate API's] [ How toocreate APIs] en [hoe tooadd operations tooan API][How tooadd operations tooan API].

## <a name="products"> </a> Producten
Producten zijn hoe API's opgehaald toodevelopers zijn. Producten in API Management hebben een of meer API's en worden geconfigureerd met een titel, beschrijving en gebruiksvoorwaarden. Producten kunnen **open** of **beveiligd** zijn. Beveiligde producten moet geabonneerde toobefore ze kunnen worden gebruikt, terwijl open producten zonder abonnement kunnen worden gebruikt. Wanneer een product gereed is voor gebruik door ontwikkelaars, kan het worden gepubliceerd. Zodra deze wordt gepubliceerd, kunnen worden bekeken (en in Hallo geval van beveiligde producten geabonneerd op) door ontwikkelaars. Goedkeuring abonnement kunt wordt geconfigureerd op productniveau Hallo en goedkeuring door beheerder vereisen of worden automatisch goedgekeurd.

Groepen zijn gebruikte toomanage Hallo zichtbaarheid van producten toodevelopers. Voor producten wordt zichtbaarheid toogroups verleend en ontwikkelaars kunnen bekijken en zich abonneren toohello producten die zichtbaar toohello groepen waartoe ze behoren. 

Zie voor meer informatie [hoe toocreate en een product publiceren] [ How toocreate and publish a product] en Hallo volgende video.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

## <a name="groups"> </a> Groepen
Groepen zijn gebruikte toomanage Hallo zichtbaarheid van producten toodevelopers. API Management heeft Hallo volgende onveranderbare systeemgroepen.

* **Beheerders** - Azure-abonnementbeheerders zijn lid van deze groep. Beheerders beheren service-exemplaren van API Management, maken Hallo-API's, bewerkingen en producten die worden gebruikt door ontwikkelaars.
* **Ontwikkelaars** - Geverifieerde gebruikers van de ontwikkelaarsportal vallen in deze groep. Ontwikkelaars zijn Hallo-klanten die toepassingen bouwen met uw API's. Ontwikkelaars krijgen toegang toohello ontwikkelaarsportal en bouwen toepassingen waarmee Hallo bewerkingen van een API aanroepen.
* **Gasten** -niet-geverifieerde gebruikers van de ontwikkelaarsportal, zoals potentiële klanten bezoeken Hallo-portal voor ontwikkelaars een API Management-exemplaar vallen in deze groep. Ze kunnen bepaalde alleen-lezen toegang zoals Hallo mogelijkheid tooview API's worden verleend, maar deze niet aanroepen.

In aanvulling toothese systeemgroepen kunnen beheerders aangepaste groepen maken of [gebruikmaken van externe groepen in gekoppelde Azure Active Directory-tenants](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group). Aangepaste en externe groepen kunnen worden gebruikt naast systeemgroepen waardoor ontwikkelaars zichtbaarheid en toegang tot tooAPI producten. U kunt bijvoorbeeld één aangepaste groep maken voor ontwikkelaars die zijn gekoppeld aan een specifieke bronpartnerorganisatie en toegang toestaan toohello API's van een product dat alleen relevante API's bevat. Een gebruiker kan lid zijn van meerdere groepen.

Zie voor meer informatie [hoe toocreate en gebruik groepen][How toocreate and use groups].

## <a name="developers"> </a> Ontwikkelaars
Ontwikkelaars vertegenwoordigen Hallo gebruikersaccounts in een API Management-service-exemplaar. Ontwikkelaars kunnen worden gemaakt of uitgenodigd toojoin door beheerders, of ze kunnen zich registreren vanuit Hallo [ontwikkelaarsportal][Developer portal]. Elke ontwikkelaar is lid van een of meer groepen en mag zich abonneren toohello producten die zichtbaarheid toothose groepen verlenen.

Als ontwikkelaars zich tooa product abonneert krijgen ze Hallo primaire en secundaire sleutel voor het Hallo-product. Deze sleutel wordt gebruikt bij het aanroepen van het product Hallo-API's.

Zie voor meer informatie [hoe toocreate of uitnodiging ontwikkelaars] [ How toocreate or invite developers] en [hoe tooassociate groepen met ontwikkelaars][How tooassociate groups with developers].

## <a name="policies"> </a> Beleidsregels
Beleidsregels zijn een krachtige mogelijkheid van API Management waarmee Hallo publisher toochange Hallo gedrag van Hallo API via configuratie. Beleidsregels zijn een verzameling instructies die sequentieel worden uitgevoerd op Hallo aanvraag of antwoord van een API. Populaire instructies omvatten Indelingsconversie van XML-tooJSON en aanroep snelheidsbeperking toorestrict Hallo hoeveelheid inkomende aanroepen van een ontwikkelaar en vele andere beleidsregels zijn beschikbaar.

Beleidsexpressies kunnen worden gebruikt als kenmerkwaarden of tekstwaarden in API Management-beleidsregels hello, tenzij Hallo beleid iets anders aangeeft. Sommige beleidsregels zoals Hallo [transportbesturing](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose) en [variabele instellen](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable) beleid is gebaseerd op beleidsexpressies. Zie voor meer informatie [Geavanceerde beleidsregels](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies), [beleidsexpressies](https://msdn.microsoft.com/library/azure/dn910913.aspx), en bekijk Hallo de volgende video.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

Zie [Naslaginformatie over beleid][Policy reference] voor een volledige lijst met API Management-beleidsregels. Zie [API Management-beleidsregels][API Management policies] voor meer informatie over het gebruiken en configureren van beleidsregels. Zie [Geavanceerde productinstellingen maken en configureren][How create and configure advanced product settings] voor een zelfstudie over het maken van een product met beleidsregels voor frequentielimiet en quotum. Zie voor een demo Hallo video te volgen.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <a name="developer-portal"> </a> Ontwikkelaarsportal
Hallo-portal voor ontwikkelaars is waar ontwikkelaars kunnen meer informatie over de bewerkingen van uw API's, bekijken en aanroepen en zich abonneren tooproducts. Potentiële klanten kunnen bezoeken Hallo-portal voor ontwikkelaars, API's en bewerkingen bekijken en zich aanmeldt. Hallo-URL voor uw ontwikkelaarsportal bevindt zich op Hallo dashboard in Hallo klassieke Azure-Portal voor uw API Management-service-exemplaar.

U kunt Hallo uiterlijk van uw ontwikkelaarsportal aanpassen door aangepaste inhoud toe te voegen, stijlen aan te passen en uw huisstijl toe te voegen.

## <a name="api-management-and-hello-api-economy"></a>API Management en Hallo API-economie
meer informatie over API Management, bekijk Hallo volgende presentatie uit conferentie Microsoft Ignite 2015 Hallo toolearn.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3708/player]
> 
> 

[APIs and operations]: #apis
[Products]: #products
[Groups]: #groups
[Developers]: #developers
[Policies]: #policies
[Developer portal]: #developer-portal

[How toocreate APIs]: api-management-howto-create-apis.md
[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer
[How create and configure advanced product settings]: api-management-howto-product-with-rules.md
[How toocreate or invite developers]: api-management-howto-create-or-invite-developers.md
[Policy reference]: api-management-policy-reference.md
[API Management policies]: api-management-howto-policies.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance




