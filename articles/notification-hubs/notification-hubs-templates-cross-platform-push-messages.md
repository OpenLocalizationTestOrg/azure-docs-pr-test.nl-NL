---
title: aaaTemplates
description: Dit onderwerp worden de sjablonen voor Azure notification hubs.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a>Sjablonen
## <a name="overview"></a>Overzicht
Sjablonen inschakelen een client toepassing toospecify Hallo precieze indeling van Hallo meldingen dat deze tooreceive wil. Met behulp van sjablonen, kan een app diverse verschillende voordelen, waaronder Hallo volgende voordelen:

* Een back-end platform networkdirect
* Aangepaste meldingen
* Onafhankelijkheid van de client-versie
* Eenvoudig lokalisatie

Deze sectie bevat twee gedetailleerde voorbeelden van hoe toouse sjablonen toosend platform networkdirect meldingen die gericht is op al uw apparaten op platforms en toopersonalize tooeach meldingsapparaten broadcast.

## <a name="using-templates-cross-platform"></a>Met behulp van sjablonen cross-platform
Hallo standaardmanier toosend pushmeldingen is toosend voor elk bericht dat is verzonden, toobe een specifieke nettolading tooplatform notification services (WNS, APNS). Hallo nettolading is bijvoorbeeld een waarschuwing tooAPNS toosend een Json-object Hallo formulier te volgen:

    {"aps": {"alert" : "Hello!" }}

toosend een vergelijkbare pop-up bericht op een Windows Store-toepassing, Hallo XML-nettolading is als volgt:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

U kunt vergelijkbare nettoladingen maken voor MPNS (Windows Phone) en (Android) GCM-platforms.

Deze vereiste forceert Hallo app back-end tooproduce verschillende nettoladingen voor elk platform, waardoor het effectief Hallo back-end die verantwoordelijk is voor een deel van Hallo presentation beschermingslaag Hallo-app. Sommige problemen bevatten te lokaliseren en grafische indelingen (vooral voor Windows Store-apps die meldingen voor verschillende soorten tegels bevatten).

Hallo Notification Hubs sjabloon functie kunt een client-app toocreate speciale registraties, aangeroepen sjabloon registraties, waaronder, Daarnaast toohello reeks labels, een sjabloon. Hallo Notification Hubs sjabloon functie kunt een client-app tooassociate apparaten met behulp van sjablonen of u met werkt (voorkeur)-installaties of -registraties. Hallo voorafgaand aan de nettolading van voorbeelden gegeven, is hello alleen platformonafhankelijk informatie Hallo werkelijke-waarschuwingsbericht (Hallo!). Een sjabloon is een verzameling instructies voor het Hallo Notification Hub op hoe tooformat een platformonafhankelijk bericht voor de registratie van Hallo van die specifieke client-app. Hallo voorgaande voorbeeld, onafhankelijke welkomstbericht platform is één eigenschap: **bericht = Hallo!**.

Hallo volgende afbeelding ziet u Hallo hierboven proces:

![](./media/notification-hubs-templates/notification-hubs-hello.png)

Hallo-sjabloon voor Hallo iOS-app clientregistratie is als volgt:

    {"aps": {"alert": "$(message)"}}

Hallo bijbehorende sjabloon voor Windows Store-clientapp Hallo is:

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

U ziet dat werkelijke Hallo-bericht is vervangen door Hallo expressie $(bericht). Deze expressie geïnstrueerd Hallo Notification Hub wanneer het verzendt een bericht toothis bepaalde registratie, toobuild een bericht dat volgt op deze en switches in Hallo algemene waarde.

Als u met installatie-model werkt, bevat Hallo installatie 'sjablonen' sleutel een JSON met meerdere sjablonen. Als u met registratie model werkt, kunt Hallo clienttoepassing maken meerdere registraties volgorde toouse meerdere sjablonen. bijvoorbeeld, een sjabloon voor waarschuwingsberichten en een sjabloon voor updates van de tegel. Client-toepassingen kunnen u ook systeemeigen registraties (registraties zonder sjabloon) en sjabloon registraties elkaar.

Hallo Notification Hub verzendt een melding voor elke sjabloon zonder rekening te houden of ze toohello horen dezelfde client-app. Dit gedrag kan worden gebruikt tootranslate platformonafhankelijk meldingen naar meer meldingen. Bijvoorbeeld, Hallo hetzelfde platform onafhankelijke bericht toohello die Notification Hub naadloos kan worden omgezet in een toast-melding en een update tegel Hallo zonder back-end toobe hiervan bewust zijn. Opmerking dat sommige platformen (bijvoorbeeld iOS) meerdere meldingen toohello mogelijk samenvouwen hetzelfde apparaat als ze worden verzonden in een korte periode.

## <a name="using-templates-for-personalization"></a>Met behulp van sjablonen voor persoonlijke instellingen
Een ander voordeel toousing sjablonen is Hallo mogelijkheid toouse Notification Hubs tooperform per registratie personalisatie van meldingen. Neem bijvoorbeeld een app weer waarin een tegel met de voorwaarden van Hallo weer op een specifieke locatie. Een gebruiker kan kiezen tussen c of Fahrenheit graden en een prognose enkele of vijf dagen. Met behulp van sjablonen, de installatie van elke client-app kunt registreren voor vereiste Hallo-indeling (1 dag Celsius, 1 dag Fahrenheit, 5 dagen c 5 dagen Fahrenheit), en Hallo back-end voor één bericht met alle Hallo informatie vereiste toofill die sturen sjablonen (bijvoorbeeld vijf maal prognose met c en Fahrenheit graden).

Hallo-sjabloon voor Hallo één dag prognose met c temperaturen is als volgt:

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

Hallo-bericht verzonden toohello Notification Hub bevat alle Hallo volgende eigenschappen:

<table border="1">

<tr><td>day1_image</td><td>day2_image</td><td>day3_image</td><td>day4_image</td><td>day5_image</td></tr>

<tr><td>day1_tempC</td><td>day2_tempC</td><td>day3_tempC</td><td>day4_tempC</td><td>day5_tempC</td></tr>

<tr><td>day1_tempF</td><td>day2_tempF</td><td>day3_tempF</td><td>day4_tempF</td><td>day5_tempF</td></tr>
</table><br/>

Met behulp van dit patroon verzendt Hallo back-end slechts één bericht zonder toostore specifieke personalisatie opties voor het Hallo-app-gebruikers. Hallo volgende afbeelding ziet u dit scenario:

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a>Hoe tooregister sjablonen
Zie tooregister met sjablonen met Hallo installatiemodel (aanbevolen) of Hallo registratie model [registratie Management](notification-hubs-push-notification-registration-management.md).

## <a name="template-expression-language"></a>Expressie sjabloontaal
Sjablonen zijn beperkt tooXML of de opmaak van de JSON-documenten. Bovendien kunt u alleen plaatsen expressies in bepaalde plaatsen; bijvoorbeeld, de kenmerken van knooppunt of de waarden voor XML tekenreeks eigenschapswaarden voor JSON.

Hallo ziet volgende tabel u Hallo taal toegestaan in sjablonen:

| expressie | Beschrijving |
| --- | --- |
| $(prop) |Tooan gebeurtenis verwijzingseigenschap met Hallo opgegeven naam. De namen van eigenschappen zijn niet hoofdlettergevoelig. Deze expressie wordt omgezet in de tekstwaarde van de eigenschap hello of een lege tekenreeks als Hallo-eigenschap niet aanwezig is. |
| $(prop, n) |Zoals hierboven, maar hello tekst expliciet is afgekapt op n tekens, bijvoorbeeld $(titel, 20) knipt Hallo inhoud van de eigenschap title Hallo op 20 tekens bestaan. |
| . (prop, n) |Als hierboven, maar hello tekst met de drie puntjes voorafgegaan, zoals deze is afgekapt. totale grootte van de Hallo Hallo afgekapt tekenreeks en Hallo achtervoegsel niet meer dan n tekens. . (titel, 20) met een invoer-eigenschap van de resultaten in 'Is Hallo titelregel' **dit is de titel Hallo...** |
| %(Prop) |Vergelijkbare too$(name) behalve die Hallo-uitvoer is de URI-codering. |
| #(prop) |In JSON-sjablonen gebruikt (bijvoorbeeld voor iOS en Android-sjablonen).<br><br>Deze functie werkt Hallo precies hetzelfde als $(prop) eerder hebt opgegeven, behalve wanneer in JSON-sjablonen (bijvoorbeeld een Apple-sjablonen). In dit geval, als deze functie wordt niet omgeven door '{','}' (bijvoorbeeld myJsonProperty: '#(naam)'), en het nummer in Javascript-indeling, bijvoorbeeld regexp tooa evalueert: (0 &#124; (&#91; 1-9, #93; &#91; 0-9 & #93 ;*))(\. &#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, en vervolgens Hallo uitvoer JSON is een getal.<br><br>Bijvoorbeeld ' badge: '#(naam)', wordt de badge': 40 (en niet 40). |
| 'text' of 'text' |Een letterlijke waarde. Letterlijke waarden bevatten willekeurige tekst tussen enkele of dubbele aanhalingstekens. |
| Expr1 + expr2 |Hallo samenvoegingsoperator lid te worden twee expressies in één tekenreeks. |

Hallo-expressies zijn Hallo voorafgaand aan formulieren.

Wanneer u samenvoeging gebruikt, moet u Hallo gehele expressie tussen met {}. Bijvoorbeeld, {$(prop) + '-' + $(prop2)}. |

Hallo volgende is bijvoorbeeld niet een geldig XML-sjabloon:

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


Uitgelegd hierboven, wanneer u samenvoeging moeten expressies worden verpakt tussen accolades. Bijvoorbeeld:

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

