---
title: aaaProtect uw API met Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooprotect uw API met quota's en beleidsregels (snelheidsbeperking) beperking.
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
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a>Uw API beveiligen met frequentielimieten met behulp van Azure API Management
Deze handleiding wordt getoond hoe eenvoudig het is tooadd beveiliging voor uw back-end API door aanroepfrequentielimiet-en quota configureren met Azure API Management.

In deze zelfstudie maakt u een ' API-product gratis proefversie waarmee ontwikkelaars toomake too10 aanroepen per minuut en up tooa maximaal 200 oproepen per week tooyour API met behulp van Hallo [aanroepfrequentie per abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) en [ Gebruiksquotum per abonnement instellen](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) beleid. U wordt vervolgens Hallo API publiceren en Hallo het beleid voor frequentielimiet testen.

Voor meer geavanceerde beperkingsscenario's met behulp van Hallo [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) en [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) beleid, Zie [geavanceerde aanvraagbeperking met Azure API Management](api-management-sample-flexible-throttling.md).

## <a name="create-product"></a>toocreate een product
In deze stap maakt u een product Gratis proefversie waarvoor geen abonnementsgoedkeuring is vereist.

> [!NOTE]
> Als u al een product geconfigureerd hebt en toouse wilt deze voor deze zelfstudie kunt u verdergaan te[configureren aanroepen snelheid en quotumbeleidsregels] [ Configure call rate limit and quota policies] en Hallo zelfstudie vanaf daar volgen met uw product in plaats van Hallo-product gratis proefversie.
> 
> 

tooget gestart, klikt u op **publicatieportal** in hello Azure-Portal voor uw API Management-service.

![Publicatieportal][api-management-management-console]

> Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [uw eerste API beheren in Azure API Management] [ Manage your first API in Azure API Management] zelfstudie.
> 
> 

Klik op **producten** in Hallo **API Management** menu op Hallo links toodisplay hello **producten** pagina.

![Product toevoegen][api-management-add-product]

Klik op **product toevoegen** toodisplay hello **nieuw product toevoegen** in het dialoogvenster.

![Nieuw product toevoegen][api-management-new-product-window]

In Hallo **titel** in het vak **gratis proefversie**.

In Hallo **beschrijving** vak, type Hallo volgende tekst: **zijn abonnees kunnen toorun 10 aanroepen per minuut up tooa maximaal 200 aanroepen/week, waarna toegang wordt geweigerd.**

Producten in API Management kunnen worden beveiligd of open zijn. Beveiligde producten moeten geabonneerde toobefore ze kunnen worden gebruikt. Open producten kunnen zonder abonnement worden gebruikt. Zorg ervoor dat **abonnement vereisen** geselecteerde toocreate is een beveiligd product waarvoor een abonnement. Dit is de standaardinstelling Hallo.

Als u wilt dat een beheerder tooreview en accepteren of weigeren abonnement toothis product probeert, selecteert u **goedkeuring abonnement vereisen**. Als het selectievakje Hallo niet is ingeschakeld, worden abonnementspogingen automatisch goedgekeurd. In dit voorbeeld worden abonnementen automatisch goedgekeurd, dus niet aanvinkt Hallo.

tooallow developer accounts toosubscribe meerdere keren toohello nieuw product, selecteer Hallo **meerdere gelijktijdige abonnementen toestaan** selectievakje. In deze zelfstudie worden meerdere gelijktijdige abonnementen niet gebruikt, dus laat het vakje uitgeschakeld.

Nadat alle waarden zijn ingevoerd, klikt u op **opslaan** toocreate Hallo product.

![Product toegevoegd][api-management-product-added]

Nieuwe producten zijn standaard zichtbaar toousers in Hallo **beheerders** groep. We gaan tooadd hello **ontwikkelaars** groep. Klik op **gratis proefversie**, en klik vervolgens op Hallo **zichtbaarheid** tabblad.

> Groepen zijn in API Management gebruikte toomanage Hallo zichtbaarheid van producten toodevelopers. Voor producten wordt zichtbaarheid toogroups verleend en ontwikkelaars kunnen bekijken en zich abonneren toohello producten die zichtbaar toohello groepen waartoe ze behoren. Zie voor meer informatie [hoe toocreate en gebruik groepen in Azure API Management][How toocreate and use groups in Azure API Management].
> 
> 

![Ontwikkelaarsgroep toevoegen][api-management-add-developers-group]

Selecteer Hallo **ontwikkelaars** selectievakje en klik vervolgens op **opslaan**.

## <a name="add-api"></a>tooadd een API toohello product
In deze stap van de zelfstudie Hallo voegt Hallo Echo-API toohello nieuwe product gratis proefversie toe.

> Elk exemplaar van API Management-service wordt geleverd met een Echo-API die kan worden gebruikt tooexperiment met en meer informatie over API Management vooraf geconfigureerd. Zie voor meer informatie [Uw eerste API beheren in Azure API Management][Manage your first API in Azure API Management].
> 
> 

Klik op **producten** van Hallo **API Management** menu op Hallo links en klik vervolgens op **gratis proefversie** tooconfigure Hallo product.

![Product configureren][api-management-configure-product]

Klik op **API toevoegen tooproduct**.

![API-tooproduct toevoegen][api-management-add-api]

Selecteer **Echo-API** en klik vervolgens op **Opslaan**.

![Echo-API toevoegen][api-management-add-echo-api]

## <a name="policies"></a>tooconfigure aanroepen snelheid en quotumbeleidsregels
Frequentielimieten en quota worden geconfigureerd in de beleidseditor Hallo. Hallo twee beleidsregels die we in deze zelfstudie gaat toevoegen zijn Hallo [aanroepfrequentie per abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) en [gebruiksquotum per abonnement instellen](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) beleid. Dit beleid moeten worden toegepast op Hallo product bereik.

Klik op **beleid** onder Hallo **API Management** menu aan de linkerkant Hallo. In Hallo **Product** lijst, klikt u op **gratis proefversie**.

![Productbeleid][api-management-product-policy]

Klik op **beleid toevoegen** tooimport Hallo beleidssjabloon en begin met het maken van Hallo aanroepfrequentielimiet-en quotum.

![Beleid toevoegen][api-management-add-policy]

Frequentie zijn en quotumbeleidsregels inkomende beleidsregels, geval positie Hallo cursor inkomende hello-element.

![Beleidseditor][api-management-policy-editor-inbound]

Schuif door Hallo lijst met beleidsregels en zoek Hallo **aanroepfrequentie per abonnement** beleidsvermelding.

![Beleidsinstructies][api-management-limit-policies]

Na het Hallo cursor wordt geplaatst in Hallo **inkomende** beleidselement, klikt u op de pijl naast Hallo **aanroepfrequentie per abonnement** tooinsert bijbehorende beleidssjabloon.

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

Als u in het codefragment Hallo zien kunt, kunt Hallo beleid limieten instellen voor de API's en bewerkingen van het product Hallo. In deze zelfstudie wordt er niet gebruiken die mogelijkheid, dus verwijder Hallo **api** en **bewerking** elementen uit Hallo **rate-limit** element, zodat alleen Hallo buitenste **rate-limit** overblijft, zoals weergegeven in het volgende voorbeeld Hallo.

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

In het product gratis proefversie hello, Hallo maximaal toegestane aanroepfrequentie 10 aanroepen per minuut, dus typ **10** als waarde voor Hallo Hallo **aanroepen** kenmerk, en **60** voor Hallo **vernieuwingsperiode** kenmerk.

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

Hallo tooconfigure **gebruiksquotum per abonnement instellen** beleid, plaats de cursor direct onder Hallo toegevoegde **rate-limit** element in Hallo **binnenkomende** element en zoek vervolgens en klikt u op Hallo pijl toohello links van **gebruiksquotum per abonnement instellen**.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

Op dezelfde manier toohello **gebruiksquotum per abonnement instellen** beleid, **gebruiksquotum per abonnement instellen** beleid kunt u de caps voor instelling op van het product Hallo API's en bewerkingen. In deze zelfstudie wordt er niet gebruiken die mogelijkheid, dus verwijder Hallo **api** en **bewerking** elementen uit Hallo **quotum** element, zoals wordt weergegeven in Hallo voorbeeld te volgen.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

Quota's kunnen worden gebaseerd op Hallo aantal aanroepen per interval, de bandbreedte of beide. In deze zelfstudie beperken we niet op basis van bandbreedte, dus verwijder Hallo **bandbreedte** kenmerk.

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

Hallo-product gratis proefversie is Hallo quotum 200 oproepen per week. Geef **200** als waarde voor Hallo Hallo **aanroepen** kenmerk en geef vervolgens **604800** als waarde voor Hallo Hallo **vernieuwingsperiode** kenmerk.

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> Beleidsintervallen worden in seconden opgegeven. toocalculate hello-interval voor een week, kunt u het aantal dagen (7) door het aantal uren in een dag (24) door het aantal minuten in een uur (60) maal het aantal seconden in een minuut (60) Hallo Hallo HALLO hallo vermenigvuldigen: 7 * 24 * 60 * 60 = 604800.
> 
> 

Wanneer u klaar bent met het Hallo-beleid configureren, moet het overeenkomen met Hallo voorbeeld te volgen.

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

Nadat het Hallo gewenste beleidsregels zijn geconfigureerd, klikt u op **opslaan**.

![Beleid opslaan][api-management-policy-save]

## <a name="publish-product"></a> toopublish Hallo product
Nu dat hello hello API's toegevoegd en Hallo beleidsregels zijn geconfigureerd, moet Hallo product worden gepubliceerd zodat deze kan worden gebruikt door ontwikkelaars. Klik op **producten** van Hallo **API Management** menu op Hallo links en klik vervolgens op **gratis proefversie** tooconfigure Hallo product.

![Product configureren][api-management-configure-product]

Klik op **publiceren**, en klik vervolgens op **Ja, publiceren** tooconfirm.

![Product publiceren][api-management-publish-product]

## <a name="subscribe-account"></a>toosubscribe een developer-account toohello product
Nu dat Hallo-product is gepubliceerd, is beschikbaar toobe geabonneerd tooand gebruikt door ontwikkelaars.

> Beheerders van een exemplaar van API Management zijn automatisch geabonneerde tooevery product. In deze zelfstudiestap abonneren we een Hallo beheerder developer accounts toohello-product gratis proefversie. Als uw ontwikkelaarsaccount deel van de rol Administrator hello uitmaakt, kunt klikt u vervolgens u met deze stap, zelfs als u bent al geabonneerd.
> 
> 

Klik op **gebruikers** op Hallo **API Management** menu op Hallo links en klik vervolgens op Hallo-naam van uw ontwikkelaarsaccount. In dit voorbeeld gebruiken we Hallo **Clayton Gragg** developer-account.

![Ontwikkelaar configureren][api-management-configure-developer]

Klik op **Abonnement toevoegen**.

![Abonnement toevoegen][api-management-add-subscription-menu]

Selecteer **Gratis proefversie** en klik vervolgens op **Abonneren**.

![Abonnement toevoegen][api-management-add-subscription]

> [!NOTE]
> In deze zelfstudie worden meerdere gelijktijdige abonnementen niet ingeschakeld voor Hallo-product gratis proefversie. Als dat zo is, zou u na vragen aan gebruiker tooname Hallo abonnement, zoals weergegeven in het volgende voorbeeld Hallo.
> 
> 

![Abonnement toevoegen][api-management-add-subscription-multiple]

Wanneer u op **abonneren**, Hallo product weergegeven in Hallo **abonnement** lijst voor Hallo-gebruiker.

![Abonnement toegevoegd][api-management-subscription-added]

## <a name="test-rate-limit"></a>toocall een bewerking en test Hallo frequentielimiet
Nu dat hello product gratis proefversie is geconfigureerd en gepubliceerd, kunnen we enkele bewerkingen aanroepen en Hallo het beleid voor frequentielimiet testen.
Switch toohello developer-portal door te klikken op **ontwikkelaarsportal** in het menu van Hallo rechtsboven.

![ontwikkelaarsportal][api-management-developer-portal-menu]

Klik op **API's** in Hallo bovenste menu en klik vervolgens op **Echo-API**.

![ontwikkelaarsportal][api-management-developer-portal-api-menu]

Klik op **GET Resource** en klik vervolgens op **Probeer het nu**.

![Console openen][api-management-open-console]

Gebruik Hallo standaardwaarde parameterwaarden en selecteer uw abonnementssleutel voor Hallo-product gratis proefversie.

![Abonnementssleutel][api-management-select-key]

> [!NOTE]
> Als u meerdere abonnementen hebt, worden ervoor tooselect Hallo-sleutel voor **gratis proefversie**, of anders Hallo-beleidsregels die zijn geconfigureerd in de vorige stappen Hallo niet meer van kracht.
> 
> 

Klik op **verzenden**, en bekijk vervolgens Hallo antwoord. Opmerking Hallo **antwoordstatus** van **200 OK**.

![Bewerkingsresultaten][api-management-http-get-results]

Klik op **verzenden** met een hogere frequentie dan Hallo beleid voor frequentielimiet van 10 aanroepen per minuut. Nadat het beleid voor frequentielimiet Hallo is overschreden, een antwoordstatus van **429 te veel aanvragen** wordt geretourneerd.

![Bewerkingsresultaten][api-management-http-get-429]

Hallo **antwoordinhoud** geeft Hallo resterende interval voordat nieuwe pogingen lukken.

Wanneer beleid voor Hallo frequentielimiet van 10 aanroepen per minuut van kracht is, mislukken volgende aanroepen tot 60 seconden na Hallo eerste Hallo 10 geslaagde aanroepen toohello product voordat Hallo frequentielimiet werd overschreden. In dit voorbeeld is Hallo resterende interval 54 seconden.

## <a name="next-steps"> </a>Volgende stappen
* Bekijk een demo voor het instellen van frequentielimieten en quota in Hallo video te volgen.

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
