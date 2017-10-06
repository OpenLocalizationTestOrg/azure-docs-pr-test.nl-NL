---
title: aaaCustomize hello API Management-portal voor ontwikkelaars met behulp van sjablonen-Azure | Microsoft Docs
description: Meer informatie over hoe toocustomize hello Azure API Management-portal voor ontwikkelaars met behulp van sjablonen.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: a195675b-f7d0-4fc9-90bf-860e6f17ccf7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: b00d5f1534e9466f30ff3920e7aae048feb8b8c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-hello-azure-api-management-developer-portal-using-templates"></a>Hoe toocustomize hello Azure API Management-portal voor ontwikkelaars met behulp van sjablonen

Er zijn drie manieren Hallo toocustomize ontwikkelaarsportal in Azure API Management:

* [Hallo-inhoud van statische pagina's en pagina-elementen voor lay-out bewerken][modify-content-layout]
* [Update Hallo stijlen worden gebruikt voor pagina-elementen over Hallo-portal voor ontwikkelaars][customize-styles]
* [Hallo-sjablonen die worden gebruikt voor pagina's die worden gegenereerd door Hallo portal wijzigen] [ portal-templates] (uitgelegd in deze handleiding)

Sjablonen zijn gebruikte toocustomize Hallo inhoud van het systeem gegenereerde developer portal-pagina's (bijvoorbeeld API docs, producten, gebruikersverificatie, enz.). Met behulp van [DotLiquid](http://dotliquidmarkup.org/) syntaxis en een opgegeven set bronnen met gelokaliseerde tekenreeksen, pictogrammen en paginabesturingselementen, hebt u aanzienlijke flexibiliteit tooconfigure Hallo inhoud van het Hallo-pagina's wens naar.

## <a name="developer-portal-templates-overview"></a>Overzicht van Developer portal-sjablonen
Het bewerken van sjablonen wordt uitgevoerd van Hallo **ontwikkelaarsportal** tijdens wordt aangemeld als beheerder. tooget er eerst hello Azure Portal openen en op **publicatieportal** van Hallo service werkbalk van uw exemplaar van API Management.

![Publicatieportal][api-management-management-console]

Klik vervolgens op **ontwikkelaarsportal** op Hallo rechtsboven. 

![Menu Developer-portal][api-management-developer-portal-menu]

tooaccess Hallo developer portal-sjablonen, klikt u op Hallo-pictogram op Hallo links toodisplay Hallo aanpassing menu aanpassen en klik op **sjablonen**.

![Developer portal-sjablonen][api-management-customize-menu]

Hallo-Sjabloonlijst weergegeven verschillende categorieën van sjablonen die betrekking hebben op Hallo verschillende pagina's in de ontwikkelaarsportal Hallo. Elke sjabloon verschilt, maar Hallo stappen tooedit ze en Hallo wijzigingen publiceren zijn dezelfde Hallo. tooedit een sjabloon, klikt u op Hallo-naam van Hallo-sjabloon.

![Developer portal-sjablonen][api-management-templates-menu]

Een sjabloon te klikken, gaat u toohello developer portal-pagina die kan worden aangepast door dat de sjabloon. In dit voorbeeld Hallo **productlijst** sjabloon wordt weergegeven. Hallo **productlijst** sjabloon besturingselementen Hallo van Hallo scherm, aangegeven door Hallo rode rechthoek. 

![De sjabloon lijst met producten][api-management-developer-portal-templates-overview]

Sommige sjablonen, zoals Hallo **gebruikersprofiel** sjablonen aanpassen verschillende onderdelen van Hallo dezelfde pagina. 

![Gebruiker-profielsjablonen][api-management-user-profile-templates]

Hallo-editor voor elke developer portal-sjabloon bevat twee secties onderaan Hallo Hallo pagina weergegeven. Hallo linkerkant Hallo deelvenster voor Hallo-sjabloon bewerken wordt weergegeven en rechterkant Hallo Hallo-gegevensmodel voor Hallo sjabloon weergegeven. 

Hallo-sjabloon bewerken deelvenster bevat Hallo aantekeningen die Hallo uiterlijk en gedrag van de betreffende pagina Hallo van Hallo-portal voor ontwikkelaars bepaalt. Hallo-opmaak in Hallo-sjabloon gebruikt Hallo [DotLiquid](http://dotliquidmarkup.org/) syntaxis. Is een populair editor voor DotLiquid [DotLiquid voor ontwerpers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers). Tijdens het bewerken van sjablonen toohello wijzigingen worden weergegeven in realtime in Hallo browser, maar zijn niet zichtbaar tooyour klanten totdat u [opslaan](#to-save-a-template) en [publiceren](#to-publish-a-template) Hallo-sjabloon.

![Sjabloon aantekeningen][api-management-template]

Hallo **sjabloongegevens** deelvenster biedt een handleiding toohello gegevens model voor Hallo entiteiten die beschikbaar voor gebruik in een bepaalde sjabloon zijn. Deze handleiding biedt door Hallo dynamische gegevens die momenteel worden weergegeven in de ontwikkelaarsportal Hallo weer te geven. U kunt Hallo sjabloon deelvensters uitbreiden door te klikken op Hallo rechthoek op Hallo rechterbovenhoek Hallo **sjabloongegevens** deelvenster.

![Sjabloon-gegevensmodel][api-management-template-data]

In het vorige voorbeeld Hallo zijn er twee producten weergegeven in het Hallo-portal voor ontwikkelaars die zijn opgehaald van de gegevens in Hallo Hallo **sjabloongegevens** deelvenster, zoals wordt weergegeven in Hallo voorbeeld te volgen.

```json
{
    "Paging": {
        "Page": 1,
        "PageSize": 10,
        "TotalItemCount": 2,
        "ShowAll": false,
        "PageCount": 1
    },
    "Filtering": {
        "Pattern": null,
        "Placeholder": "Search products"
    },
    "Products": [
        {
            "Id": "56ec64c380ed850042060001",
            "Title": "Starter",
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",
            "Terms": "",
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        },
        {
            "Id": "56ec64c380ed850042060002",
            "Title": "Unlimited",
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",
            "Terms": null,
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        }
    ]
}
```

Hallo-opmaak in Hallo **productlijst** Sjabloonprocessen Hallo gegevensuitvoer tooprovide Hallo gewenst door het Hallo-verzameling van informatie over producten toodisplay en een koppeling tooeach afzonderlijke producten doorlopen. Opmerking Hallo `<search-control>` en `<page-control>` elementen in het Hallo-opmaak. Deze Hallo-weergave van Hallo zoeken en besturingselementen op de pagina Hallo paging bepalen. `ProductsStrings|PageTitleProducts`een gelokaliseerde tekenreeks verwijzing met Hallo `h2` koptekst voor Hallo pagina. Zie voor een lijst met tekenreeksbronnen, paginabesturingselementen en pictogrammen beschikbaar voor gebruik in developer portal-sjablonen, [API Management-referentie voor ontwikkelaars portal sjablonen](api-management-developer-portal-templates-reference.md).

```html
<search-control></search-control>
<div class="row">
    <div class="col-md-9">
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>
    </div>
</div>
<div class="row">
    <div class="col-md-12">
    {% if products.size > 0 %}
    <ul class="list-unstyled">
    {% for product in products %}
        <li>
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>
            {{product.description}}
        </li>    
    {% endfor %}
    </ul>
    <paging-control></paging-control>
    {% else %}
    {% localized "CommonResources|NoItemsToDisplay" %}
    {% endif %}
    </div>
</div>
```

## <a name="toosave-a-template"></a>een sjabloon toosave
toosave een sjabloon, klik op opslaan in de editor voor Hallo-sjabloon.

![Sjabloon opslaan][api-management-save-template]

Opgeslagen wijzigingen zijn niet in de ontwikkelaarsportal Hallo live totdat ze worden gepubliceerd.

## <a name="toopublish-a-template"></a>een sjabloon toopublish
Opgeslagen sjablonen kunnen worden gepubliceerd, afzonderlijk of Alles samenvoegen. een afzonderlijke template toopublish, klikken op publish in Hallo sjablooneditor.

![Sjabloon publiceren][api-management-publish-template]

Klik op **Ja** tooconfirm en Hallo sjabloon live op Hallo-portal voor ontwikkelaars.

![Bevestig publiceren][api-management-publish-template-confirm]

toopublish alle sjabloonversies niet gepubliceerd, klikt u op **publiceren** in de lijst met sjablonen Hallo. Niet-gepubliceerde sjablonen worden aangewezen door een sterretje Hallo sjabloonnaam te volgen. In dit voorbeeld Hallo **productlijst** en **Product** sjablonen worden gepubliceerd.

![Sjablonen publiceren][api-management-publish-templates]

Klik op **aanpassingen publiceert** tooconfirm.

![Bevestig publiceren][api-management-publish-customizations]

Nieuw gepubliceerde sjablonen zijn effectief in het Hallo-portal voor ontwikkelaars.

## <a name="toorevert-a-template-toohello-previous-version"></a>een eerdere versie van sjabloon toohello toorevert
toorevert sjabloon toohello vorige gepubliceerde versie, klik op herstellen in de editor voor Hallo-sjabloon.

![Sjabloon herstellen][api-management-revert-template]

Klik op **Ja** tooconfirm.

![Bevestigen][api-management-revert-template-confirm]

Hallo eerder gepubliceerde versie van een sjabloon is live in Hallo-portal voor ontwikkelaars zodra Hallo bewerking herstellen is voltooid.

## <a name="toorestore-a-template-toohello-default-version"></a>de standaardversie van een sjabloon toohello toorestore
Herstellen sjablonen tootheir standaardversie is een proces in twee stappen. Eerste Hallo sjablonen moeten worden hersteld en vervolgens Hallo hersteld moet worden gepubliceerd.

een standaardversie van één sjabloon toohello toorestore Klik op herstellen in de editor voor Hallo-sjabloon.

![Sjabloon herstellen][api-management-reset-template]

Klik op **Ja** tooconfirm.

![Bevestigen][api-management-reset-template-confirm]

toorestore alle sjablonen tootheir standaardversies, klikt u op **herstellen standaardsjablonen** op Hallo Sjabloonlijst.

![Sjablonen herstellen][api-management-restore-templates]

Hallo herstelde sjablonen moeten vervolgens worden gepubliceerd afzonderlijk of in één keer door stappen te volgen Hallo in [toopublish een sjabloon](#to-publish-a-template).

## <a name="next-steps"></a>Volgende stappen
Zie voor informatie over developer portal-sjablonen, tekenreeksbronnen pictogrammen en paginabesturingselementen, [API Management-referentie voor ontwikkelaars portal sjablonen](api-management-developer-portal-templates-reference.md).

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customize-menu]: ./media/api-management-developer-portal-templates/api-management-customize-menu.png
[api-management-templates-menu]: ./media/api-management-developer-portal-templates/api-management-templates-menu.png
[api-management-developer-portal-templates-overview]: ./media/api-management-developer-portal-templates/api-management-developer-portal-templates-overview.png
[api-management-template]: ./media/api-management-developer-portal-templates/api-management-template.png
[api-management-template-data]: ./media/api-management-developer-portal-templates/api-management-template-data.png
[api-management-developer-portal-menu]: ./media/api-management-developer-portal-templates/api-management-developer-portal-menu.png
[api-management-management-console]: ./media/api-management-developer-portal-templates/api-management-management-console.png
[api-management-browse]: ./media/api-management-developer-portal-templates/api-management-browse.png
[api-management-user-profile-templates]: ./media/api-management-developer-portal-templates/api-management-user-profile-templates.png
[api-management-save-template]: ./media/api-management-developer-portal-templates/api-management-save-template.png
[api-management-publish-template]: ./media/api-management-developer-portal-templates/api-management-publish-template.png
[api-management-publish-template-confirm]: ./media/api-management-developer-portal-templates/api-management-publish-template-confirm.png
[api-management-publish-templates]: ./media/api-management-developer-portal-templates/api-management-publish-templates.png
[api-management-publish-customizations]: ./media/api-management-developer-portal-templates/api-management-publish-customizations.png
[api-management-revert-template]: ./media/api-management-developer-portal-templates/api-management-revert-template.png
[api-management-revert-template-confirm]: ./media/api-management-developer-portal-templates/api-management-revert-template-confirm.png
[api-management-reset-template]: ./media/api-management-developer-portal-templates/api-management-reset-template.png
[api-management-reset-template-confirm]: ./media/api-management-developer-portal-templates/api-management-reset-template-confirm.png
[api-management-restore-templates]: ./media/api-management-developer-portal-templates/api-management-restore-templates.png







