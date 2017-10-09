---
title: aaaHow toouse eigenschappen in Azure API Management-beleidsregels
description: Meer informatie over hoe toouse eigenschappen in Azure API Management-beleidsregels.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a>Hoe toouse eigenschappen in Azure API Management-beleidsregels
API Management-beleidsregels zijn een krachtige mogelijkheid Hallo-systeem dat Hallo publisher toochange Hallo gedrag Hallo API via configuratie toestaan. Beleidsregels zijn een verzameling instructies die sequentieel worden uitgevoerd op Hallo aanvraag of antwoord van een API. Beleidsverklaringen kunnen worden samengesteld met behulp van letterlijke tekstwaarden, beleidsexpressies en eigenschappen. 

Elk exemplaar van API Management-service heeft een verzameling eigenschappen van sleutel/waarde-paren die globale toohello service-exemplaar zijn. Deze eigenschappen kunnen gebruikte toomanage constante string-waarden worden voor alle configuratie-API en beleidsregels. Elke eigenschap heeft Hallo kenmerken te volgen.

| Kenmerk | Type | Beschrijving |
| --- | --- | --- |
| Naam |Tekenreeks |Hallo-naam van Hallo-eigenschap. Mogelijk bevatten alleen letters, cijfers, periode, streepjes en onderstrepingstekens bevatten. |
| Waarde |Tekenreeks |Hallo-waarde van Hallo-eigenschap. Het is niet leeg zijn of alleen witruimte bevatten. |
| Geheim |Booleaanse waarde |Bepaalt of Hallo-waarde een geheim is en moet worden versleuteld of niet. |
| Tags |Matrix van tekenreeks |Optioneel tags die de gebruikte toofilter Hallo eigenschappenlijst kan worden opgegeven. |

Eigenschappen zijn geconfigureerd in de publicatieportal Hallo op Hallo **eigenschappen** tabblad. In de Hallo voorbeeld te volgen, zijn drie eigenschappen geconfigureerd.

![Eigenschappen][api-management-properties]

Eigenschapswaarden letterlijke tekenreeksen kunnen bevatten en [beleidsexpressies](https://msdn.microsoft.com/library/azure/dn910913.aspx). Hallo volgende tabel toont Hallo vorige drie Voorbeeld eigenschappen en hun kenmerken. waarde van Hallo `ExpressionProperty` is een beleidsexpressie die resulteert in een tekenreeks met Hallo de huidige datum en tijd. Hallo eigenschap `ContosoHeaderValue` is gemarkeerd als een geheim, zodat de waarde wordt niet weergegeven.

| Naam | Waarde | Geheim | Tags |
| --- | --- | --- | --- |
| ContosoHeader |trackingId |False |Contoso |
| ContosoHeaderValue |•••••••••••••••••••••• |True |Contoso |
| ExpressionProperty |@(DateTime.Now.ToString()) |False | |

## <a name="toouse-a-property"></a>een eigenschap toouse
een eigenschap in een beleid toouse, plaats Hallo eigenschapsnaam in een dubbele paar accolades, zoals `{{ContosoHeader}}`, zoals weergegeven in het volgende voorbeeld Hallo.

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

In dit voorbeeld `ContosoHeader` wordt gebruikt als Hallo-naam van een kop in een `set-header` beleid, en `ContosoHeaderValue` wordt gebruikt als Hallo-waarde van deze header. Wanneer dit beleid wordt beoordeeld tijdens een aanvraag of antwoord toohello API Management-gateway, `{{ContosoHeader}}` en `{{ContosoHeaderValue}}` worden vervangen door hun respectieve eigenschapswaarden.

Eigenschappen kunnen worden gebruikt als volledige kenmerk of elementwaarden zoals weergegeven in het vorige voorbeeld hello, maar ze kunnen ook worden ingevoegd in of in combinatie met een deel van een expressie letterlijke tekst zoals weergegeven in het volgende voorbeeld Hallo:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`

Eigenschappen bevatten ook beleidsexpressies. Hallo in Hallo voorbeeld te volgen, `ExpressionProperty` wordt gebruikt.

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

Wanneer dit beleid wordt beoordeeld `{{ExpressionProperty}}` is vervangen door de waarde ervan: `@(DateTime.Now.ToString())`. Aangezien Hallo-waarde een beleidsexpressie is, Hallo expressie wordt geëvalueerd en Hallo beleid doorgegaan met de uitvoering ervan.

U kunt dit uit in de ontwikkelaarsportal Hallo testen door het aanroepen van een bewerking die een beleid met eigenschappen in het bereik heeft. In Hallo voorbeeld te volgen, een bewerking is aangeroepen met de twee vorige voorbeeld Hallo `set-header` beleid met eigenschappen. Houd er rekening mee dat antwoord Hallo bevat twee aangepaste headers die zijn geconfigureerd met beleid van eigenschappen.

![ontwikkelaarsportal][api-management-send-results]

Als u hello bekijkt [API Inspector trace](api-management-howto-api-inspector.md) voor een aanroep die Hallo twee vorige voorbeeld beleidsregels met eigenschappen bevat, ziet u twee Hallo `set-header` beleid met Hallo eigenschapswaarden ingevoegd en de beleidsexpressie Hallo evaluatie voor Hallo-eigenschap die Hallo beleidsexpressie opgenomen.

![API-Inspector tracering][api-management-api-inspector-trace]

Houd er rekening mee dat terwijl eigenschapswaarden beleidsexpressies bevatten kunnen, eigenschapswaarden kunnen geen andere eigenschappen bevatten. Als tekst met een eigenschapverwijzing wordt gebruikt voor de waarde van een eigenschap, zoals `Property value text {{MyProperty}}`, dat eigenschapverwijzing won't worden vervangen en opgenomen als onderdeel van de eigenschapswaarde Hallo worden.

## <a name="toocreate-a-property"></a>een eigenschap toocreate
toocreate een eigenschap, klikt u op **eigenschap toevoegen** op Hallo **eigenschappen** tabblad.

![Eigenschap toevoegen][api-management-properties-add-property-menu]

**Naam** en **waarde** vereiste waarden zijn. Als de waarde van deze eigenschap een geheim is, controleert u Hallo **dit is een geheim** selectievakje. Geef een of meer optionele labels toohelp met eigenschappen voor het ordenen en op **opslaan**.

![Eigenschap toevoegen][api-management-properties-add-property]

Wanneer een nieuwe eigenschap wordt opgeslagen, Hallo **eigenschap zoeken** textbox is gevuld met de naam van de nieuwe eigenschap Hallo Hallo en de nieuwe eigenschap hello wordt weergegeven. alle eigenschappen, schakelt u toodisplay hello **eigenschap zoeken** textbox en druk op enter.

![Eigenschappen][api-management-properties-property-saved]

Zie voor meer informatie over het maken van een eigenschap Hallo REST-API met [maakt u een eigenschap Hallo REST-API met](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).

## <a name="tooedit-a-property"></a>een eigenschap tooedit
tooedit een eigenschap, klikt u op **bewerken** naast Hallo eigenschap tooedit.

![De eigenschap bewerken][api-management-properties-edit]

Breng de gewenste wijzigingen klik vervolgens op **opslaan**. Als u de naam van de eigenschap Hallo wijzigt, worden alle beleidsregels die verwijzen naar die eigenschap automatisch bijgewerkt toouse Hallo nieuwe naam.

![De eigenschap bewerken][api-management-properties-edit-property]

Zie voor meer informatie over het bewerken van een eigenschap Hallo REST-API met [bewerken van een eigenschap Hallo REST-API met](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).

## <a name="toodelete-a-property"></a>een eigenschap toodelete
toodelete een eigenschap, klikt u op **verwijderen** naast Hallo eigenschap toodelete.

![Eigenschap verwijderen][api-management-properties-delete]

Klik op **Ja, deze verwijderen** tooconfirm.

![De verwijdering bevestigen][api-management-delete-confirm]

> [!IMPORTANT]
> Als de eigenschap Hallo wordt verwezen door andere beleidsregels, kunt u zich niet toosuccessfully verwijderen als u de eigenschap Hallo verwijdert uit alle beleidsregels die worden gebruikt.
> 
> 

Zie voor meer informatie over het verwijderen van een eigenschap Hallo REST-API met [verwijderen van een eigenschap Hallo REST-API met](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).

## <a name="toosearch-and-filter-properties"></a>Eigenschappen toosearch en filter
Hallo **eigenschappen** tabblad Zoeken en filteren mogelijkheden toohelp beheren van uw eigenschappen bevat. toofilter Hallo-eigenschappenlijst met de eigenschapsnaam, voert u een zoekterm in Hallo **eigenschap zoeken** textbox. alle eigenschappen, schakelt u toodisplay hello **eigenschap zoeken** textbox en druk op enter.

![Search][api-management-properties-search]

toofilter hello eigenschappenlijst door code-waarden, een of meer labels invoeren in Hallo **filteren op labels** textbox. alle eigenschappen, schakelt u toodisplay hello **filteren op labels** textbox en druk op enter.

![Filteren][api-management-properties-filter]

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over het werken met beleid
  * [Beleidsregels in API Management](api-management-howto-policies.md)
  * [Naslaginformatie over beleidsregels](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [Beleidsexpressies](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a>Bekijk een video-overzicht
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

