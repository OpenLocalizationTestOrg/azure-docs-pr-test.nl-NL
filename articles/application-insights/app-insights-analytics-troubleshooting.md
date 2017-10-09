---
title: aaaTroubleshoot analyses in Azure Application Insights | Microsoft Docs
description: 'Problemen met Application Insights analytics? Begin hier. '
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a>Problemen met analyses in Application Insights oplossen
Problemen met [Application Insights Analytics](app-insights-analytics.md)? Begin hier. Analytics is een krachtige zoekfunctie Hallo van Azure Application Insights.

## <a name="limits"></a>Limieten
* Momenteel zijn queryresultaten beperkt toojust over een week van afgelopen gegevens.
* We testen op browsers: meest recente edities van Chrome, rand en Internet Explorer.

## <a name="known-incompatible-browser-extensions"></a>Bekende incompatibele browser-extensies
* Ghostery

Hallo uitbreiding uitschakelen of een andere browser gebruikt.

## <a name="e-a"></a>'Fout'
![Onverwachte foutscherm](./media/app-insights-analytics-troubleshooting/010.png)

Er is een interne fout opgetreden tijdens de runtime portal: niet-verwerkte uitzondering.

* Hallo browsercache reinigen. 

## <a name="e-b"></a>403... Probeer tooreload
![403... Probeer tooreload](./media/app-insights-analytics-troubleshooting/020.png)

Een verificatie gerelateerde fout (tijdens de verificatie of access token genereren). Hallo portal heeft misschien geen enkele manier te herstellen zonder browserinstellingen te wijzigen.

* Controleer of [cookies van derden zijn ingeschakeld](#cookies) in Hallo browser. 

## <a name="authentication"></a>403... beveiligingszone controleren
![403.. .verify beveiligingszone](./media/app-insights-analytics-troubleshooting/030.png)

Een verificatie gerelateerde fout (tijdens de verificatie of access token genereren). Hallo portal heeft misschien geen enkele manier te herstellen zonder browserinstellingen te wijzigen.

1. Controleer of [cookies van derden zijn ingeschakeld](#cookies) in Hallo browser. 
2. Hebt u een favoriet, bladwijzer of opgeslagen koppeling tooopen Hallo Analytics-portal gebruikt? Weet u bent aangemeld met andere referenties dan u hebt gebruikt toen u Hallo koppeling opgeslagen?
3. Probeer het met een in-persoonlijke/incognito-browservenster (na het sluiten van alle dergelijke vensters). Hebt u tooprovide uw referenties. 
4. Open een andere (gewone) browservenster en gaat u te[Azure](https://portal.azure.com). Meld u af. Open de koppeling vervolgens en meld u aan met de juiste referenties Hallo.
5. Rand en Internet Explorer krijgen gebruikers kunnen ook te deze fout als vertrouwde zone-instellingen worden niet ondersteund.
   
    Controleer of beide [Analytics-portal](https://analytics.applicationinsights.io) en [Azure Active Directory-portal](https://portal.azure.com) zijn in Hallo dezelfde beveiligingszone:
   
   * Open in Internet Explorer, **Internetopties**, **beveiliging**, **vertrouwde websites**, **Sites**:
     
     ![Dialoogvenster Internet-opties, een site toe te voegen tooTrusted Sites](./media/app-insights-analytics-troubleshooting/033.png)
     
     In de lijst met Websites van hello, als een van de volgende URL's Hallo opgenomen zijn, controleert u of die Hallo anderen ook zijn opgenomen:
     
     https://Analytics.applicationinsights.IO<br/>
     https://login.microsoftonline.com<br/>
     https://login.windows.net

## <a name="e-d"></a>404 ... Kan de resource niet vinden
![404... bron is niet gevonden](./media/app-insights-analytics-troubleshooting/040.png)

Bron van toepassing is verwijderd uit de Application Insights en is niet langer beschikbaar. Dit kan gebeuren als u Hallo URL toohello Analytics pagina opgeslagen.

## <a name="e-e"></a>403 ... Geen autorisatie
![403... niet geautoriseerd](./media/app-insights-analytics-troubleshooting/050.png)

U hebt geen machtiging tooopen deze toepassing in Analytics.

* Krijgt u de koppeling Hallo van iemand anders? Vraagt u ze ervoor dat u in Hallo toomake [lezers of inzenders voor deze resourcegroep](app-insights-resources-roles-access-control.md).
* U Hallo koppeling met andere referenties opslaan? Open Hallo [Azure-portal](https://portal.azure.com), meldt u zich af en probeer deze koppeling opnieuw opgeven van de juiste referenties Hallo.

## <a name="html-storage"></a>403 ... HTML5-opslag
Onze portal maakt gebruik van HTML5 localStorage en sessionStorage.

* Chrome: Instellingen, privacy, instellingen van de inhoud.
* Internet Explorer: Internet-opties, tabblad Geavanceerd, beveiliging, de DOM-opslag inschakelen

![403... Probeer tooenable HTML5-opslag](./media/app-insights-analytics-troubleshooting/060.png)

## <a name="e-g"></a>404 ... Abonnement is niet gevonden
![404 ... Abonnement is niet gevonden](./media/app-insights-analytics-troubleshooting/070.png)

Hallo-URL is ongeldig. 

* Hallo app resource in openen [Application Insights-portal](https://portal.azure.com). Gebruik vervolgens Hallo Analytics-knop.

## <a name="e-h"></a>404... pagina bestaat niet
![404 ... Pagina bestaat niet](./media/app-insights-analytics-troubleshooting/080.png)

Hallo-URL is ongeldig.

* Hallo app resource in openen [Application Insights-portal](https://portal.azure.com). Gebruik vervolgens Hallo Analytics-knop.

## <a name="cookies"></a>Cookies van derden inschakelen
  Zie [hoe toodisable derden cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), maar zoals u ziet, moeten we te**inschakelen** ze.


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

