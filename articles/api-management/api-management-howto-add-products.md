---
title: aaaHow toocreate en een product publiceren in Azure API Management
description: Meer informatie over hoe toocreate en producten publiceren in Azure API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a>Hoe toocreate en een product publiceren in Azure API Management
In Azure API Management zijn een product bevat een of meer API's, evenals een usage-quota's en Hallo gebruiksvoorwaarden. Zodra een product is gepubliceerd, kunnen ontwikkelaars toohello product abonneren en begint toouse Hallo product API's. Hallo onderwerp bevat een handleiding toocreating een product, een API toevoegen en publiceren voor ontwikkelaars.

## <a name="create-product"></a>Een product maken
Bewerkingen worden toegevoegd en tooan API in de publicatieportal Hallo geconfigureerd. tooaccess publisher en klik op Hallo **publicatieportal** in hello Azure-Portal voor uw API Management-service.

![Publicatieportal][api-management-management-console]

> Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.
> 
> 

Klik op **producten** in Hallo-menu op Hallo links toodisplay hello **producten** pagina en klik op **Product toevoegen**.

![Producten][api-management-products]

![Nieuw product][api-management-add-new-product]

Voer een beschrijvende naam voor Hallo product in Hallo **naam** veld en een beschrijving van het product in Hallo Hallo **beschrijving** veld.

Producten in API Management kunnen worden **Open** of **beveiligde**. Beveiligde producten moet geabonneerde toobefore ze kunnen worden gebruikt, terwijl open producten zonder abonnement kunnen worden gebruikt. Controleer **abonnement vereisen** toocreate een beveiligd product waarvoor een abonnement. Dit is de standaardinstelling Hallo.

Controleer **goedkeuring abonnement vereisen** als u wilt dat een beheerder tooreview en accepteren of weigeren abonnement toothis product probeert. Als Hallo selectievakje uitgeschakeld is, worden abonnementspogingen automatisch goedgekeurd. Zie voor meer informatie over abonnementen [weergave abonnees tooa product][View subscribers tooa product].

tooallow developer accounts toosubscribe meerdere keren toohello product, Controleer Hallo **meerdere abonnementen toestaan** selectievakje. Als dit selectievakje niet is ingeschakeld, kunt alleen een product voor één keer toohello zich abonneren elke developer-account.

![Onbeperkte meerdere abonnementen][api-management-unlimited-multiple-subscriptions]

toolimit hello telling van meerdere gelijktijdige abonnementen controleren Hallo **beperken het aantal gelijktijdige abonnementen op** selectievakje en Voer Hallo limiet voor het abonnement. Gelijktijdige abonnementen zijn in de Hallo voorbeeld te volgen, beperkt toofour per developer-account.

![Vier meerdere abonnementen][api-management-four-multiple-subscriptions]

Nadat alle productopties voor nieuw zijn geconfigureerd, klikt u op **opslaan** toocreate Hallo nieuw product.

![Producten][api-management-products-page]

> Standaard worden nieuwe producten zijn niet gepubliceerd en zijn zichtbaar alleen toohello **beheerders** groep.
> 
> 

tooconfigure een product, klikt u op Hallo productnaam in Hallo **producten** tabblad.

## <a name="add-apis"></a>Toevoegen-API's tooa product
Hallo **producten** pagina bevat vier koppelingen voor de configuratie: **samenvatting**, **instellingen**, **zichtbaarheid**, en  **Abonnees**. Hallo **samenvatting** tabblad kunt u API's toevoegen en publiceren of ongedaan maken van een product is.

![Samenvatting][api-management-new-product-summary]

Voordat het product publiceren moet u tooadd een of meer API's. toodo, klikt u op **API toevoegen tooproduct**.

![API's toevoegen][api-management-add-apis-to-product]

Selecteer Hallo gewenst API's en klik op **opslaan**.

## <a name="add-description"></a>Beschrijvende informatie tooa-product toevoegen
Hallo **instellingen** tabblad kunt u tooprovide gedetailleerde informatie over Hallo product zoals het doel ervan, Hallo toegang tot biedt API's en andere nuttige informatie. Hallo-inhoud is gericht op Hallo-ontwikkelaars die aanroepen van Hallo API en kunnen worden geschreven in tekst zonder opmaak of HTML-opmaak.

![Productinstellingen][api-management-product-settings]

Controleer **abonnement vereisen** toocreate een beveiligd product waarvoor een abonnement toobe gebruikte, of schakel Hallo selectievakje toocreate een open product dat kan worden aangeroepen zonder een abonnement.

Selecteer **goedkeuring abonnement vereisen** als u wilt dat toomanually alle product abonnement aanvragen goedkeuren. Standaard worden alle product abonnementen automatisch verleend.

tooallow developer accounts toosubscribe meerdere keren toohello product, Controleer Hallo **meerdere abonnementen toestaan** selectievakje en geef optioneel een limiet. Als dit selectievakje niet is ingeschakeld, kunt alleen een product voor één keer toohello zich abonneren elke developer-account.

Vul eventueel Hallo **gebruiksvoorwaarden** veld Hallo gebruiksvoorwaarden voor Hallo product die abonnees in volgorde toouse Hallo product moeten accepteren.

## <a name="publish-product"></a>Een product publiceren
Voordat Hallo API's in een product kan worden aangeroepen, moet Hallo product worden gepubliceerd. Op Hallo **samenvatting** voor Hallo product en klik op **publiceren**, en klik vervolgens op **Ja, publiceren** tooconfirm. toomake een persoonlijk eerder gepubliceerde product, klikt u op **publicatie ongedaan maken**.

![Product publiceren][api-management-publish-product]

## <a name="make-visible"></a>Maken van een product zichtbaar toodevelopers
Hallo **zichtbaarheid** tabblad kunt u toochoose welke functies kunnen toosee Hallo product op Hallo-portal voor ontwikkelaars en toohello product abonneren.

![Zichtbaarheid van het product][api-management-product-visiblity]

controleren of schakel het selectievakje Hallo naast Hallo groep en klik vervolgens op tooenable of schakelt u de zichtbaarheid van een product voor ontwikkelaars Hallo in een groep **opslaan**.

> Zie voor meer informatie [hoe toocreate en gebruik groepen toomanage developer accounts in Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].
> 
> 

## <a name="view-subscribers"></a>Abonnees tooa-product weergeven
Hallo **abonnees** tabblad Hallo-ontwikkelaars die zijn geabonneerd toohello product bevat. Hallo kunnen-gegevens en instellingen voor elke ontwikkelaar worden bekeken door te klikken op Hallo ontwikkelaarshandleiding naam. In dit voorbeeld hebben geen ontwikkelaars nog toohello product geabonneerd.

![Ontwikkelaars][api-management-developer-list]

## <a name="next-steps"> </a>Volgende stappen
Hallo gewenste eenmaal API's toegevoegd en Hallo product is gepubliceerd, ontwikkelaars kunnen toohello product abonneren en beginnen met toocall Hallo API's. Zie voor een zelfstudie leert u hoe wordt deze items, evenals een geavanceerde productconfiguratie [maken en configureren van geavanceerde productinstellingen in Azure API Management][How create and configure advanced product settings in Azure API Management].

Zie voor meer informatie over het werken met producten Hallo video te volgen.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
