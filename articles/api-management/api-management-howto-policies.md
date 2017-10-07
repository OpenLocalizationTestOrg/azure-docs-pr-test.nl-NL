---
title: aaaPolicies in Azure API Management | Microsoft Docs
description: Ontdek hoe toocreate, bewerken en configureren van beleid in API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a>Beleid in Azure API Management
In Azure API Management zijn-beleidsregels een krachtige functie Hallo-systeem dat Hallo publisher toochange Hallo gedrag Hallo API via configuratie toestaan. Beleidsregels zijn een verzameling instructies die sequentieel worden uitgevoerd op Hallo aanvraag of antwoord van een API. Populaire instructies omvatten Indelingsconversie van XML-tooJSON en snelheidsbeperking toorestrict Hallo hoeveelheid inkomende aanroepen van een ontwikkelaar aanroepen. Veel meer beleidsregels zijn out of box Hallo beschikbaar.

Zie Hallo [beleidsverwijzing] [ Policy Reference] voor een volledige lijst met beleidsverklaringen en de bijbehorende instellingen.

Beleidsregels worden toegepast binnen bevindt zich tussen Hallo API consumer en Hallo managed API Hallo-gateway. Hallo gateway ontvangt alle aanvragen en stuurt ze ongewijzigd meestal door toohello onderliggende API. Een beleid kunt echter wijzigingen tooboth Hallo binnenkomende aanvraag en het uitgaande antwoord toepassen.

Beleidsexpressies kunnen worden gebruikt als kenmerkwaarden of tekstwaarden in API Management-beleidsregels hello, tenzij Hallo beleid iets anders aangeeft. Sommige beleidsregels zoals Hallo [transportbesturing] [ Control flow] en [variabele instellen] [ Set variable] beleid is gebaseerd op beleidsexpressies. Zie voor meer informatie [Geavanceerde beleidsregels] [ Advanced policies] en [beleidsexpressies][Policy expressions].

## <a name="scopes"></a>Hoe tooconfigure beleid
Beleid kan worden geconfigureerd globaal of Hallo bereik van een [Product][Product], [API] [ API] of [bewerking] [Operation]. tooconfigure een beleid, gaat u toohello beleid editor in de publicatieportal Hallo.

![Menu beleid][policies-menu]

Hallo beleidsregels editor bestaat uit drie gedeelten: Hallo bereik (boven), Hallo beleid beleidsdefinitie waarbij beleid (links) worden bewerkt en Hallo instructies lijst (rechts):

![Beleid-editor][policies-editor]

toobegin een beleid die moet u eerst Hallo bereik welke Hallo beleid moet toepassen selecteren te configureren. In de schermafbeelding hieronder Hallo Hallo **Starter** product is geselecteerd. Houd er rekening mee dat Hallo vierkante symbool volgende toohello beleidsnaam geeft aan dat een beleid al op dit niveau toegepast is.

![Bereik][policies-scope]

Omdat er al een beleid is toegepast, wordt in Hallo definitie weergave Hallo configuratie weergegeven.

![Configureren][policies-configure]

Hallo-beleid wordt weergegeven in de alleen-lezen in eerste instantie. Klik in volgorde tooedit Hallo definitie op Hallo **beleid configureren** in te grijpen.

![Bewerken][policies-edit]

Hallo beleidsdefinitie is een eenvoudige XML-document dat wordt een reeks binnenkomend en uitgaand instructies beschreven. Hallo XML kan rechtstreeks in Hallo definitievenster worden bewerkt. Een lijst van de instructies wordt verstrekt toohello rechts en instructies van toepassing toohello huidige bereik zijn ingeschakeld en geselecteerd. zoals blijkt uit Hallo **limiet aanroepen snelheid** instructie in de bovenstaande Hallo.

Te klikken op een ingeschakelde instructie toevoegt juiste XML op Hallo-locatie van de cursor in de weergave typedefinitie Hallo HALLO hallo. 

> [!NOTE]
> Als het Hallo-beleid dat u wilt dat tooadd niet is ingeschakeld, zorg ervoor dat u in de juiste bereik Hallo voor dat beleid. Elke instructie beleid is ontworpen voor gebruik in bepaalde scopes en beleid-secties. tooreview hello beleid secties en bereiken voor een beleid controleren Hallo **gebruik** sectie voor dat beleid in Hallo [beleidsverwijzing][Policy Reference].
> 
> 

Een volledige lijst met beleidsverklaringen en hun instellingen zijn beschikbaar in Hallo [beleidsverwijzing][Policy Reference].

Bijvoorbeeld, tooadd een nieuwe instructie toorestrict binnenkomende aanvragen toospecified IP-adressen, plaatst u Hallo cursor net binnen Hallo inhoud Hallo `inbound` XML-element en klik op Hallo **beperken aanroeper IP-adressen** instructie.

![Beleid voor softwarebeperking][policies-restrict]

Hiermee voegt u toe een XML-fragment toohello `inbound` element dat richtlijnen biedt voor hoe tooconfigure Hallo instructie.

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

toolimit binnenkomende aanvragen en accepteert alleen die uit een IP-adres van 1.2.3.4 Hallo XML als volgt wijzigen:

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Opslaan][policies-save]

Als u klaar Hallo-instructies voor het Hallo-beleid configureren, klikt u op **opslaan** en Hallo wijzigingen wordt onmiddellijk doorgegeven toohello API Management gateway.

## <a name="sections"></a>Understanding beleidsconfiguratie
Een beleid is een reeks instructies die worden uitgevoerd om een antwoord en aanvragen. Hallo-configuratie op de juiste wijze is onderverdeeld in `inbound`, `backend`, `outbound`, en `on-error` gedeelten in Hallo na configuratie wordt weergegeven.

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

Als er een fout opgetreden tijdens het verwerken van een aanvraag hello, alle overige stappen in Hallo `inbound`, `backend`, of `outbound` secties worden overgeslagen en uitvoering aan de slag gaat toohello instructies in Hallo `on-error` sectie. Door het plaatsen van beleidsverklaringen in Hallo `on-error` sectie kunt u Hallo fout bekijken met behulp van Hallo `context.LastError` eigenschap, controleren en aanpassen van Hallo fout antwoord aan de hand van Hallo `set-body` beleid, en configureren van wat er gebeurt als een fout optreedt. Er zijn foutcodes voor ingebouwde stappen en voor fouten die tijdens het Hallo-verwerking van beleid voor instructies optreden. Zie voor meer informatie [foutafhandeling in API Management-beleidsregels](https://msdn.microsoft.com/library/azure/mt629506.aspx).

Omdat het beleid kunnen worden opgegeven op verschillende niveaus (globale, product, api en bewerking) biedt Hallo-configuratie een manier voor u toospecify Hallo volgorde waarin instructies Hallo beleid definition met het beleid ten opzichte van toohello bovenliggende uitvoeren. 

Beleid scopes worden in Hallo volgorde geëvalueerd.

1. Globaal bereik
2. Product-bereik
3. API-bereik
4. Bewerkingsbereik

Hallo instructies in deze worden beoordeeld volgens toohello plaatsing van Hallo `base` element, indien aanwezig. Globaal beleid heeft geen bovenliggende beleid en het gebruik van Hallo `<base>` -element in het heeft geen effect.

Bijvoorbeeld, als u een beleid op Hallo globale niveau en een beleid dat is geconfigureerd voor een API hebt, klikt u vervolgens wanneer die bepaalde API wordt gebruikt beide beleidsregels gelden. API Management kunt u deterministische ordening van gecombineerde beleidsverklaringen via Hallo base-element. 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

Hallo in Hallo voorbeeld beleidsdefinitie hierboven, `cross-domain` instructie zou worden uitgevoerd voordat een hogere beleid die op zijn beurt worden gevolgd door Hallo `find-and-replace` beleid. 

toosee Hallo-beleid in het huidige bereik Hallo in de beleidseditor hello, klikt u op **herberekenen effectief beleid voor de geselecteerde scope**.

## <a name="next-steps"></a>Volgende stappen
Bekijk na video op beleidsexpressies.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
