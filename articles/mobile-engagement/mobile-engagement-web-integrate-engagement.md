---
title: aaaAzure Mobile Engagement Web SDK-integratie | Microsoft Docs
description: meest recente updates en procedures voor het Azure Mobile Engagement Web SDK Hallo Hallo
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a>Azure Mobile Engagement integreren in een webtoepassing
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Hallo procedures in dit artikel wordt beschreven Hallo eenvoudigste manier tooactivate Hallo analytics en bewaking van functies in Azure Mobile Engagement in uw webtoepassing.

Ga als volgt Hallo stappen tooactivate Hallo logboek rapporten die vereist toocompute zijn alle statistische gegevens over gebruikers, sessies, activiteiten, crashes en technicals. Voor statistieken van afhankelijk zijn van toepassing, zoals gebeurtenissen, fouten en taken, moet u handmatig log-rapporten activeren met behulp van hello Azure Mobile Engagement-API. Informatie voor meer informatie over [hoe toouse Hallo Mobile Engagement API tags in een webtoepassing geavanceerde](mobile-engagement-web-use-engagement-api.md).

## <a name="introduction"></a>Inleiding
[Hello Azure Mobile Engagement Web SDK downloaden](http://aka.ms/P7b453).
Hallo Mobile Engagement Web SDK wordt geleverd als een enkel JavaScript-bestand, azure-engagement.js, die u hebt tooinclude op elke pagina van de toepassing van uw site of webtoepassing.

> [!IMPORTANT]
> Voordat u dit script uitvoert, moet u een script uitvoeren of code codefragment tooconfigure Mobile Engagement te schrijven voor uw toepassing.
> 
> 

## <a name="browser-compatibility"></a>Browsercompatibiliteit
Hallo Mobile Engagement Web SDK maakt gebruik van systeemeigen JSON coderen en decoderen bovendien toocross domein AJAX-aanvragen (relying op Hallo W3C CORS-specificatie). Is compatibel met de volgende browsers Hallo:

* Microsoft Edge 12 +
* Internet Explorer 10 +
* Firefox 3.5 +
* Chrome 4 +
* Safari 6 +
* Opera 12 +

## <a name="configure-mobile-engagement"></a>Configureren van Mobile Engagement
Een script schrijven dat wordt gemaakt van een globale `azureEngagement` JavaScript-object, zoals in het volgende voorbeeld Hallo. Omdat de site meerdere pagina's hebben mogelijk, in dit voorbeeld wordt ervan uitgegaan dat dit script wordt opgenomen in elke pagina. In dit voorbeeld Hallo JavaScript-object met de naam `azure-engagement-conf.js`.

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

Hallo `connectionString` waarde wordt weergegeven in uw toepassing hello Azure-portal.

> [!NOTE]
> `appVersionName`en `appVersionCode` zijn optioneel. We raden echter aan dat u ze configureren zodat analytics versie-informatie kan verwerken.
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a>Mobile Engagement scripts opnemen in uw pagina 's
Mobile Engagement scripts tooyour pagina's op een van de volgende manieren Hallo toevoegen:

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

Of dit:

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a>Alias
Nadat Hallo Mobile Engagement Web SDK-script is geladen, het maken van Hallo **engagement** alias tooaccess Hallo SDK-API's. U kunt deze alias toodefine Hallo SDK-configuratie niet gebruiken. Deze alias wordt gebruikt als een verwijzing in deze documentatie.

Houd er rekening mee dat als Hallo standaardalias met een andere globale variabele van uw pagina conflicteert, u het in Hallo configuratie als volgt desgewenst kunt voordat u Hallo Mobile Engagement Web SDK laden:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a>Basic-rapportage
Basic rapportage in Mobile Engagement bevat informatie over de statistieken van de sessie-niveau, zoals statistieken over gebruikers, sessies, activiteiten en crashes.

### <a name="session-tracking"></a>Sessie bijhouden
Een sessie Mobile Engagement is onderverdeeld in een volgorde van activiteiten, elk aangeduid met een naam.

In een klassieke website raden wij u aan een andere activiteit te declareren op elke pagina van uw site. Voor een website of webtoepassing toepassing in welke Hallo huidige pagina nooit verandert, kunt u tootrack Hallo activiteiten op kleinere schaal, zoals binnen Hallo pagina.

Ofwel manier, toostart of wijzig Hallo huidige gebruikersactiviteit aanroep Hallo `engagement.agent.startActivity` functie. Bijvoorbeeld:

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

Hallo Mobile Engagement-server beëindigd automatisch een geopende sessie binnen drie minuten nadat de pagina van de toepassing hello is gesloten.

U kunt ook u kunt een sessie beëindigen handmatig door het aanroepen van `engagement.agent.endActivity`. Hiermee stelt u Hallo huidige gebruiker activiteit too'Idle.'  Hallo-sessie 10 seconden later worden beëindigd tenzij een nieuwe aanroep te`engagement.agent.startActivity` Hallo sessie hervatten.

U kunt Hallo 10 seconden vertraging in Hallo globale engagement-object als volgt configureren:

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> U kunt geen gebruiken `engagement.agent.endActivity` in Hallo `onunload` retouraanroep omdat u niet AJAX-aanroepen in deze fase.
> 
> 

## <a name="advanced-reporting"></a>Geavanceerde rapportage
Als u wilt dat tooreport toepassingsspecifieke gebeurtenissen, fouten en taken, moet u eventueel toouse Hallo Mobile Engagement-API. U toegang tot Mobile Engagement API Hallo via Hallo `engagement.agent` object.

U kunt toegang tot alle Hallo geavanceerde mogelijkheden in Mobile Engagement in Hallo Mobile Engagement-API. Hallo API wordt beschreven in artikel Hallo [hoe toouse Hallo Mobile Engagement API tags in een webtoepassing geavanceerde](mobile-engagement-web-use-engagement-api.md).

## <a name="customize-hello-urls-used-for-ajax-calls"></a>Hallo-URL's gebruikt voor AJAX-aanroepen aanpassen
U kunt URL's aanpassen die gebruikmaakt van Mobile Engagement Web SDK Hallo. Bijvoorbeeld: tooredefine Hallo logboek URL (Hallo SDK eindpunt voor logboekregistratie), kunt u Hallo configuratie overschrijven als volgt uit:

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

Als de functies van uw URL als een tekenreeks die begint resultaat met `/`, `//`, `http://`, of `https://`, Hallo standaardschema wordt niet gebruikt. Standaard Hallo `https://` schema wordt gebruikt voor deze URL's. Als u toocustomize Hallo standaardschema wilt, overschrijven Hallo-configuratie, als volgt:

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
