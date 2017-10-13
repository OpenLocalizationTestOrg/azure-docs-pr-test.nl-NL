---
title: Uw API beveiligen met Azure API Management | Microsoft Docs
description: Informatie over het beveiligen van uw API met beleidsregels voor quota en (frequentie)beperking.
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 300b1d762a61c810dbffde5aaacd8a85f12c9fca
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/11/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a>Uw API beveiligen met frequentielimieten met behulp van Azure API Management
In deze handleiding wordt getoond hoe eenvoudig het is om beveiliging toe te voegen voor uw back-end-API door frequentielimiet- en quotumbeleidsregels te configureren met Azure API Management.

In deze zelfstudie maakt u een API-product Gratis proefversie waarmee ontwikkelaars maximaal 10 aanroepen per minuut en maximaal 200 oproepen per week naar uw API kunnen doen met de beleidsregels [Aanroepfrequentie per abonnement beperken](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) en [Gebruiksquotum per abonnement instellen](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota). Vervolgens publiceert u de API en test u het frequentielimietbeleid.

Voor meer geavanceerde beperkingsscenario's met behulp van de beleidsregels [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) en [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) raadpleegt u [Geavanceerde aanvraagbeperking met Azure API Management](api-management-sample-flexible-throttling.md).

## <a name="create-product"> </a>Een product maken
In deze stap maakt u een product Gratis proefversie waarvoor geen abonnementsgoedkeuring is vereist.

> [!NOTE]
> Als u al een product hebt geconfigureerd en u dit wilt gebruiken voor deze zelfstudie, kunt u verder gaan naar [Aanroepfrequentielimiet- en quotumbeleidsregels configureren][Configure call rate limit and quota policies] en de zelfstudie vanaf daar volgen met uw product in plaats van het product Gratis proefversie.
> 
> 

Als u aan de slag wilt gaan, klikt u op **Publicatieportal** in Azure Portal voor uw API Management-service.

![Publicatieportal][api-management-management-console]

> Als u nog geen service-exemplaar van API Management hebt gemaakt, raadpleegt u [Service-exemplaar van API Management maken][Create an API Management service instance] in de zelfstudie [Uw eerste API beheren][Manage your first API in Azure API Management] in Azure API Management.
> 
> 

Klik op **Producten** in het menu **API Management** aan de linkerkant om de pagina **Producten** weer te geven.

![Product toevoegen][api-management-add-product]

Klik op **Product toevoegen** om het dialoogvenster **Nieuw product toevoegen** weer te geven.

![Nieuw product toevoegen][api-management-new-product-window]

Typ **Gratis proefversie** in het vak **Titel**.

Typ in het vak **Beschrijving** de volgende tekst: **Abonnees kunnen 10 aanroepen/minuut uitvoeren met maximaal 200 aanroepen/week, waarna toegang wordt geweigerd.**

Producten in API Management kunnen worden beveiligd of open zijn. Voor beveiligde producten is een abonnement vereist voordat ze kunnen worden gebruikt. Open producten kunnen zonder abonnement worden gebruikt. Zorg ervoor dat **Abonnement vereisen** is ingeschakeld voor het maken van een beveiligd product waarvoor een abonnement is vereist. Dit is de standaardinstelling.

Als u wilt dat een beheerder abonnementspogingen voor dit product beoordeelt en accepteert of weigert, schakelt u **Goedkeuring abonnement vereisen** in. Als het selectievakje niet is ingeschakeld, worden abonnementspogingen automatisch goedgekeurd. In dit voorbeeld worden abonnementen automatisch goedgekeurd, dus schakel het selectievakje niet in.

Als u wilt toestaan dat ontwikkelaarsaccounts meerdere abonnementen op het nieuwe product hebben, schakelt u het selectievakje **Meerdere gelijktijdige abonnementen toestaan** in. In deze zelfstudie worden meerdere gelijktijdige abonnementen niet gebruikt, dus laat het vakje uitgeschakeld.

Nadat alle waarden zijn ingevoerd, klikt u op **Opslaan** om het product te maken.

![Product toegevoegd][api-management-product-added]

Nieuwe producten zijn standaard zichtbaar voor gebruikers in de groep **Beheerders**. We gaan de groep **Ontwikkelaars** toevoegen. Klik op **Gratis proefversie** en klik vervolgens op het tabblad **Zichtbaarheid**.

> In API Management worden groepen gebruikt voor het beheren van de zichtbaarheid van producten voor ontwikkelaars. Voor producten wordt zichtbaarheid aan groepen verleend en ontwikkelaars kunnen de producten bekijken en zich abonneren op de producten die zichtbaar zijn voor de groepen waartoe de ontwikkelaars behoren. Zie voor meer informatie [Groepen maken en gebruiken in Azure API Management][How to create and use groups in Azure API Management].
> 
> 

![Ontwikkelaarsgroep toevoegen][api-management-add-developers-group]

Schakel het selectievakje **Ontwikkelaars** in en klik vervolgens op **Opslaan**.

## <a name="add-api"> </a>Een API toevoegen aan het product
In deze stap van de zelfstudie voegen we de Echo-API toe aan het nieuwe product Gratis proefversie.

> Elk service-exemplaar van API Management wordt al geconfigureerd geleverd met een Echo-API die kan worden gebruikt om te experimenteren met API Management en hier meer over te leren. Zie voor meer informatie [Uw eerste API beheren in Azure API Management][Manage your first API in Azure API Management].
> 
> 

Klik op **Producten** in het menu **API Management** aan de linkerkant en klik vervolgens op **Gratis proefversie** om het product te configureren.

![Product configureren][api-management-configure-product]

Klik op **API toevoegen aan product**.

![API toevoegen aan product][api-management-add-api]

Selecteer **Echo-API** en klik vervolgens op **Opslaan**.

![Echo-API toevoegen][api-management-add-echo-api]

## <a name="policies"> </a>Aanroepfrequentielimiet- en quotumbeleidsregels configureren
Frequentielimieten en quota worden geconfigureerd in de beleidseditor. De twee beleidsregels die we in deze zelfstudie toevoegen, zijn [Aanroepfrequentie per abonnement beperken](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) en [Gebruiksquotum per abonnement instellen](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota). Dit beleid moeten worden toegepast op het productbereik.

Klik op **Beleidsregels** in het menu **API Management** aan de linkerkant. Klik in de lijst **Product** op **Gratis proefversie**.

![Productbeleid][api-management-product-policy]

Klik op **Beleid toevoegen** om de beleidssjabloon te importeren en begin met het maken van de frequentielimiet- en quotumbeleidsregels.

![Beleid toevoegen][api-management-add-policy]

Frequentielimiet- en quotumbeleidsregels zijn inkomende beleidsregels, dus plaats de cursor in het inkomende element.

![Beleidseditor][api-management-policy-editor-inbound]

Blader door de lijst met beleidsregels en zoek de beleidsvermelding **Aanroepfrequentie per abonnement beperken**.

![Beleidsinstructies][api-management-limit-policies]

Nadat de cursor in het **inkomende** beleidselement is geplaatst, klikt u op de pijl naast **Aanroepfrequentie per abonnement beperken** om de bijbehorende beleidssjabloon in te voegen.

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

Zoals u in het codefragment kunt zien, kunt u met het beleid limieten instellen voor de API's en bewerkingen van het product. In deze zelfstudie maken we geen gebruik van die mogelijkheid, dus verwijder de elementen **api** en **operation** uit het element **rate-limit**, zodat alleen het buitenste element **rate-limit** overblijft, zoals in het volgende voorbeeld wordt getoond.

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

In het product Gratis proefversie is de maximaal toegestane aanroepfrequentie 10 aanroepen per minuut, dus typ **10** als de waarde voor het kenmerk **calls** en **60** voor het kenmerk **renewal-period**.

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

Als u het beleid **Gebruiksquotum per abonnement instellen** wilt configureren, plaatst u de cursor direct onder het zojuist toegevoegde element **rate-limit** binnen het element **inbound** en klikt u vervolgens op de pijl links van **Gebruiksquotum per abonnement instellen**.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

Net als het beleid **Aanroepfrequentie per abonnement beperken** kunt u met het beleid **Gebruiksquotum per abonnement instellen** limieten instellen voor de API's en bewerkingen van het product. In deze zelfstudie maken we geen gebruik van die mogelijkheid, dus verwijder de elementen **api** en **operation** uit het element **quota**, zoals in het volgende voorbeeld wordt getoond.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

Quota kunnen zijn gebaseerd op het aantal aanroepen per interval, de bandbreedte of beide. In deze zelfstudie beperken we niet op basis van bandbreedte, dus verwijder het kenmerk **bandwidth**.

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

In het product Gratis proefversie is het quotum 200 aanroepen per week. Geef **200** op als de waarde voor het kenmerk **calls** en geef vervolgens **604800** op als de waarde voor het kenmerk **renewal-period**.

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> Beleidsintervallen worden in seconden opgegeven. Als u het interval voor een week wilt berekenen, kunt u het aantal dagen (7) vermenigvuldigen met het aantal uren in een dag (24) maal het aantal minuten in een uur (60) maal het aantal seconden in een minuut (60): 7 * 24 * 60 * 60 = 604800.
> 
> 

Wanneer u klaar bent met het configureren van het beleid, moet het overeenkomen met het volgende voorbeeld.

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

Nadat de gewenste beleidsregels zijn geconfigureerd, klikt u op **Opslaan**.

![Beleid opslaan][api-management-policy-save]

## <a name="publish-product"> </a>Het product publiceren
Nu de API's zijn toegevoegd en de beleidsregels zijn geconfigureerd, moet het product worden gepubliceerd zodat het door ontwikkelaars kan worden gebruikt. Klik op **Producten** in het menu **API Management** aan de linkerkant en klik vervolgens op **Gratis proefversie** om het product te configureren.

![Product configureren][api-management-configure-product]

Klik op **Publiceren** en klik vervolgens op **Ja, publiceren** om te bevestigen.

![Product publiceren][api-management-publish-product]

## <a name="subscribe-account"> </a>Een ontwikkelaarsaccount abonneren op het product
Nu het product is gepubliceerd, is het beschikbaar voor ontwikkelaars om zich op te abonneren en om te worden gebruikt.

> Beheerders van een API Management-exemplaar worden automatisch op elk product geabonneerd. In deze zelfstudiestap abonneren we een van de ontwikkelaarsaccounts dat geen beheerdersaccount is op het product Gratis proefversie. Als uw ontwikkelaarsaccount deel uitmaakt van de rol Beheerder, kunt u doorgaan met deze stap, ook al bent u al geabonneerd.
> 
> 

Klik op **Gebruikers** in het menu **API Management** aan de linkerkant en klik vervolgens op de naam van uw ontwikkelaarsaccount. In dit voorbeeld gebruiken we het ontwikkelaarsaccount **Floris Kregel**.

![Ontwikkelaar configureren][api-management-configure-developer]

Klik op **Abonnement toevoegen**.

![Abonnement toevoegen][api-management-add-subscription-menu]

Selecteer **Gratis proefversie** en klik vervolgens op **Abonneren**.

![Abonnement toevoegen][api-management-add-subscription]

> [!NOTE]
> In deze zelfstudie zijn meerdere gelijktijdige abonnementen niet ingeschakeld voor het product Gratis proefversie. Als dat wel het geval zou zijn, zou u om de naam van het abonnement worden gevraagd, zoals in het volgende voorbeeld wordt getoond.
> 
> 

![Abonnement toevoegen][api-management-add-subscription-multiple]

Nadat u op **Abonneren** hebt geklikt, wordt het product weergegeven in de lijst **Abonnement** voor de gebruiker.

![Abonnement toegevoegd][api-management-subscription-added]

## <a name="test-rate-limit"> </a>Een bewerking aanroepen en de frequentielimiet testen
Nu het product Gratis proefversie is geconfigureerd en gepubliceerd, kunnen we enkele bewerkingen aanroepen en het beleid voor frequentielimiet testen.
Schakel over naar de ontwikkelaarsportal door te klikken op **Ontwikkelaarsportal** in het menu rechtsboven.

![ontwikkelaarsportal][api-management-developer-portal-menu]

Klik op **API's** in het bovenste menu en klik op **Echo-API**.

![ontwikkelaarsportal][api-management-developer-portal-api-menu]

Klik op **GET Resource** en klik vervolgens op **Probeer het nu**.

![Console openen][api-management-open-console]

Behoud de standaardparameterwaarden en selecteer uw abonnementssleutel voor het product Gratis proefversie.

![Abonnementssleutel][api-management-select-key]

> [!NOTE]
> Als u meerdere abonnementen hebt, moet u ervoor zorgen dat u de sleutel voor **Gratis proefversie** selecteert, anders zijn de beleidsregels die in de vorige stappen zijn geconfigureerd niet van kracht.
> 
> 

Klik op **Verzenden** en bekijk vervolgens het antwoord. Noteer de **Antwoordstatus** van **200 OK**.

![Bewerkingsresultaten][api-management-http-get-results]

Klik op **Verzenden** met een hogere frequentie dan het beleid voor een frequentielimiet van 10 aanroepen per minuut. Nadat het beleid voor de frequentielimiet is overschreden, wordt een antwoordstatus van **429 te veel aanvragen** geretourneerd.

![Bewerkingsresultaten][api-management-http-get-429]

Met de **Antwoordinhoud** wordt het resterende interval aangegeven voordat nieuwe pogingen lukken.

Wanneer het beleid voor een frequentielimiet van 10 aanroepen per minuut van kracht is, mislukken volgende aanroepen tot 60 seconden na de eerste van de 10 geslaagde aanroepen naar het product zijn verstreken voordat de frequentielimiet werd overschreden. In dit voorbeeld is het resterende interval 54 seconden.

## <a name="next-steps"> </a>Volgende stappen
* Bekijk een demo voor het instellen van frequentielimieten en quota in de volgende video.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How to create and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers to a product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API to the product]: #add-api
[Publish the product]: #publish-product
[Subscribe a developer account to the product]: #subscribe-account
[Call an operation and test the rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
