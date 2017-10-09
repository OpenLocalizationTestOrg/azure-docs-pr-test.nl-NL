---
title: De gebruikersstatistieken aaaAnalyze met Azure CDN geavanceerde HTTP-rapporten | Microsoft Docs
description: Meer informatie over hoe toocreate geavanceerde HTTP-rapporten in Microsoft Azure CDN. Deze rapporten bevatten gedetailleerde informatie over CDN-activiteit.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ef90adc1-580e-4955-8ff1-bde3f3cafc5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 3184ec00d089613e25c62762f93043cb4ba68394
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-usage-statistics-with-azure-cdn-advanced-http-reports"></a>Gebruiksstatistieken analyseren met Azure CDN geavanceerde HTTP-rapporten
## <a name="overview"></a>Overzicht
Dit document wordt uitgelegd geavanceerde HTTP-rapportage in Microsoft Azure CDN. Deze rapporten bevatten gedetailleerde informatie over CDN-activiteit.

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="accessing-advanced-http-reports"></a>Toegang tot geavanceerde HTTP-rapporten
1. Blade voor Hallo CDN-profiel, klik op Hallo **beheren** knop.
   
    ![Knop blade CDN-profiel beheren](./media/cdn-advanced-http-reports/cdn-manage-btn.png)
   
    Hallo CDN-beheerportal geopend.
2. Houd de muis boven Hallo **Analytics** tabblad en houd de muis boven Hallo **geavanceerde HTTP-rapporten** doel.  Klik op **HTTP grote Platform**.
   
    ![CDN-beheerportal - menu Geavanceerde rapporten](./media/cdn-advanced-http-reports/cdn-advanced-reports.png)
   
    Rapportopties worden weergegeven.

## <a name="geography-reports-map-based"></a>Geografie-rapporten (kaart gebaseerd)
Er zijn vijf rapporten die gebruikmaken van een kaart tooindicate Hallo regio's waar uw inhoud wordt aangevraagd. Deze rapporten zijn wereld-kaart, Verenigde Staten-kaart, Canada-kaart, Europa kaart en Azië en Stille Oceaan kaart.

Elk rapport op basis van een kaart worden gerangschikt op geografische entiteiten (dat wil zeggen, landen, provincies en provincies) volgens toohello percentage treffers die afkomstig van die regio zijn. Bovendien is een kaart opgegeven toohelp u visualiseren Hallo locaties waarvan de inhoud wordt aangevraagd. Kan toodo is het dus door elke regio kleurcodering volgens toohello bedrag van de aanvraag in deze regio opgetreden. Lichter gearceerde gebieden aangeven lagere vraag naar de inhoud, terwijl donkere regio's hogere niveaus van de vraag naar uw inhoud geven.

Rechtstreeks hieronder Hallo kaart vindt u gedetailleerde informatie voor de verkeer en bandbreedte voor elke regio. Hiermee kunt u tooview Hallo totaal aantal treffers, Hallo percentage treffers, Hallo totale hoeveelheid gegevens overgedragen (in gigabytes) en Hallo percentage van de gegevens die zijn overgedragen voor elke regio. Een beschrijving op voor elk van deze metrische gegevens weergeven. Ten slotte wanneer u de muisaanwijzer op een regio (dat wil zeggen, land, staat of provincie), Hallo naam en het Hallo percentage treffers dat is opgetreden in de regio Hallo weergegeven als knopinfo.

Hieronder vindt u een korte beschrijving voor elk type op basis van kaart Geografie-rapport.

| Rapportnaam | Beschrijving |
| --- | --- |
| Wereldkaart |Dit rapport kunt u tooview Hallo wereldwijde vraag naar uw CDN-inhoud. Elk land is gekleurde op Hallo wereld kaart tooindicate Hallo percentage treffers die afkomstig van die regio zijn. |
| Verenigde Staten-kaart |Dit rapport kunt u tooview Hallo vraag naar uw CDN-inhoud in Hallo Verenigde Staten. Elke status is voorzien van een kleurcode op deze kaart tooindicate Hallo percentage treffers die afkomstig van die regio zijn. |
| Canada-kaart |Dit rapport kunt u tooview Hallo vraag naar uw CDN-inhoud in Canada. Elke provincie is voorzien van een kleurcode op deze kaart tooindicate Hallo percentage treffers die afkomstig van die regio zijn. |
| Europa-kaart |Dit rapport kunt u tooview Hallo vraag naar uw CDN-inhoud in Europa. Elk land wordt voorzien van een kleurcode op deze kaart tooindicate Hallo percentage treffers die afkomstig van die regio zijn. |
| Azië Pacific-kaart |Dit rapport kunt u tooview Hallo vraag naar uw CDN-inhoud in Azië. Elk land wordt voorzien van een kleurcode op deze kaart tooindicate Hallo percentage treffers die afkomstig van die regio zijn. |

## <a name="geography-reports-bar-charts"></a>Geografie rapporten (staafdiagrammen)
Er zijn twee aanvullende rapporten die statistische informatie geven op basis van toogeography, Top steden en Top landen. Deze rapporten rangschikken steden en landen, respectievelijk volgens toohello aantal treffers die afkomstig van die regio's zijn. Bij het genereren van dit type rapport geeft een staafdiagram Hallo bovenste 10 steden of landen aangevraagde inhoud via een specifiek platform. U kunt deze staafdiagram tooquickly beoordelen Hallo-regio's die genereren Hallo hoogste aantal aanvragen voor uw inhoud.

de linkerkant Hallo van Hallo grafiek (y-as) geeft aan hoe vaak opgetreden in Hallo opgegeven regio. Direct onder Hallo grafiek (x-as) vindt u een label voor elke Hallo bovenste 10 regio's.

### <a name="using-hello-bar-charts"></a>Met behulp van Hallo staafdiagrammen
* Als u de muisaanwijzer op een balk, Hallo naam en het totaal aantal treffers dat is opgetreden in de regio Hallo Hallo weergegeven als knopinfo.
* Hallo knopinfo voor Hallo boven steden rapport identificeert een plaats door de naam, staat/provincie en Landafkorting.
* Als Hallo of regio (dat wil zeggen, staat/provincie) die een aanvraag afkomstig is kan niet worden bepaald, wordt deze vervolgens aangegeven dat onbekende zijn. Als Hallo land onbekend en klik vervolgens twee vraagtekens (dat wil zeggen veldnamenrij), wordt weergegeven.
* Een rapport kan metrische gegevens voor 'Europa' of ' Azië/regio.' hello bevatten Deze items zijn niet bedoeld voor tooprovide statistische informatie over alle IP-adressen in die gebieden. In plaats daarvan ze alleen van toepassing toorequests die afkomstig zijn van IP-adressen die zijn verdeeld over Europa of Azië/in plaats van tooa Haarlem of land.

Hallo-gegevens die gebruikt toogenerate Hallo staafdiagram zijn kunnen worden bekeken eronder. Hier vindt u Hallo kunt u het totaal aantal treffers, Hallo percentage treffers, Hallo en de hoeveelheid gegevens overgedragen (in gigabytes) en Hallo percentage van de gegevens die overgedragen voor Hallo bovenste 250 regio's. Een beschrijving op voor elk van deze metrische gegevens weergeven.

Een korte beschrijving is opgegeven voor beide rapporttypen hieronder.

| Rapportnaam | Beschrijving |
| --- | --- |
| Top plaatsen |Dit rapport worden gerangschikt op basis van het aantal treffers die afkomstig van die regio zijn toohello plaatsen. |
| Bovenste landen |Dit rapport worden gerangschikt op basis van het aantal treffers die afkomstig van die regio zijn toohello landen. |

## <a name="daily-summary"></a>Dagelijkse samenvatting
Hallo samenvattingsrapport voor dagelijkse kunt u tooview Hallo totaal aantal treffers en gegevens die overgedragen via een bepaald platform dagelijks. Deze informatie kan worden gebruikt tooquickly onderscheiden CDN activiteit patronen. Bijvoorbeeld: in dit rapport kunt u detecteren welke dagen ervaren hoger of lager is dan het verwachte verkeer.

Bij het genereren van dit type rapport wordt wordt een staafdiagram bieden een visuele indicatie als toohello bedrag van de platform-specifieke vraag ervaren dagelijks via Hallo periode waarvoor Hallo lijst. Het wordt dit doen door een balk voor elke dag in Hallo rapport weer te geven. Bijvoorbeeld 'Afgelopen Week' hello periode selecteren aangeroepen een staafdiagram met zeven balken wordt gegenereerd. Elke balk geeft Hallo kunt u het totaal aantal treffers op die dag opgetreden.

Hallo linkerkant van de grafiek hello (y-as) geeft aan hoe vaak opgetreden op Hallo opgegeven datum. Direct onder Hallo grafiek (x-as), vindt u een label dat Hallo datum geeft (indeling: jjjj-MM-DD) voor elke dag in Hallo rapport opgenomen.

> [!TIP]
> Als u de muisaanwijzer op een balk, Hallo kunt u het totaal aantal treffers die is opgetreden op die datum weergegeven als knopinfo.
> 
> 

Hallo-gegevens die gebruikt toogenerate Hallo staafdiagram zijn kunnen worden bekeken eronder. Er vindt u Hallo totaal aantal treffers en Hallo en de hoeveelheid gegevens overgedragen (in gigabytes) voor elke dag wordt gedekt door Hallo-rapport.

## <a name="by-hour"></a>Per uur
Hallo door uur rapport kunt u tooview Hallo totaal aantal treffers en gegevens die overgedragen via een bepaald platform op uurbasis. Deze informatie kan worden gebruikt tooquickly onderscheiden CDN activiteit patronen. Bijvoorbeeld: in dit rapport kunt u detecteren Hallo tijdsperioden tijdens Hallo dag die zich hoger of lager is dan het verwachte verkeer.

Bij het genereren van dit type rapport bieden een staafdiagram een visuele indicatie als toohello hoeveelheid platform-specifieke aanvraag opgetreden op uurbasis via Hallo periode waarvoor Hallo-lijst. Het wordt dit doen door een balk voor elk uur wordt gedekt door Hallo rapport weer te geven. Bijvoorbeeld, een 24-uurs selecteren periode genereert een staafdiagram met 24 balken. Elke balk geeft Hallo kunt u het totaal aantal treffers ondervonden tijdens dat uur.

de linkerkant Hallo van Hallo grafiek (y-as) geeft aan hoe vaak opgetreden op Hallo opgegeven uur. Direct onder Hallo grafiek (x-as), vindt u een label dat Hallo datum/tijd wordt aangegeven (indeling: jjjj-MM-DD uu: mm) voor elk uur in Hallo rapport opgenomen. Tijd wordt aangegeven met 24-uurs indeling en deze is opgegeven met behulp van Hallo UTC/GMT-tijdzone.

> [!TIP]
> Als u de muisaanwijzer op een balk, Hallo kunt u het totaal aantal treffers die is opgetreden tijdens dat uur weergegeven als knopinfo.
> 
> 

Hallo-gegevens die gebruikt toogenerate Hallo staafdiagram zijn kunnen worden bekeken eronder. Er vindt u Hallo totaal aantal treffers en Hallo en de hoeveelheid gegevens overgedragen (in gigabytes) voor elk uur wordt gedekt door Hallo-rapport.

## <a name="by-file"></a>Door het bestand
Hallo door bestand rapport kunt u tooview Hallo hoeveelheid vraag en Hallo verkeer dat gedurende een bepaald platform voor Hallo meest aangevraagde activa. Bij het genereren van dit type rapport wordt een staafdiagram worden gegenereerd op Hallo bovenste 10 meest aangevraagde activa over Hallo opgegeven periode.

> [!NOTE]
> Rand CNAME-URL's zijn voor Hallo toepassing van dit rapport wordt geconverteerde tootheir gelijkwaardige CDN URL's. Hierdoor kan dat een nauwkeurige tally voor Hallo totaal aantal treffers gekoppeld aan een asset ongeacht Hallo CDN of toorequest van rand CNAME-URL die wordt gebruikt.
> 
> 

de linkerkant Hallo van Hallo grafiek (y-as) geeft Hallo aantal aanvragen voor elk actief via Hallo opgegeven periode. Direct onder Hallo grafiek (x-as) vindt u een label dat de bestandsnaam Hallo voor elk Hallo bovenste 10 aangevraagde activa geeft.

Hallo-gegevens die gebruikt toogenerate Hallo staafdiagram zijn kunnen worden bekeken eronder. Hier vindt u Hallo volgende informatie voor elke Hallo bovenste 250 aangevraagde activa: relatief pad, Hallo totaal aantal treffers, Hallo percentage treffers, Hallo en de hoeveelheid gegevens overgedragen (in gigabytes) en het Hallo-percentage overgedragen gegevens.

## <a name="by-file-detail"></a>Door het bestand details
Hallo door bestand gedetailleerd rapport kunt u tooview Hallo hoeveelheid vraag en Hallo verkeer dat gedurende een bepaald platform voor een bepaalde asset. Hallo is helemaal boven aan dit rapport Hallo bestand Details voor optie. Deze optie biedt een lijst met de meest aangevraagde activa op Hallo geselecteerde platform. In de volgorde toogenerate een rapport met details moet u tooselect Hallo gewenste asset van Hallo optie voor meer informatie in het bestand. Waarna een staafdiagram Hallo hoeveelheid dagelijkse vraag die wordt gegenereerd via Hallo opgegeven tijdsperiode wordt aangegeven.

de linkerkant Hallo van Hallo grafiek (y-as) geeft aan Hallo kunt u het totale aantal aanvragen dat een actief op een bepaalde dag is. Direct onder Hallo grafiek (x-as), vindt u een label dat Hallo datum geeft (indeling: jjjj-MM-DD) voor welke vraag CDN voor Hallo asset is gerapporteerd.

Hallo-gegevens die gebruikt toogenerate Hallo staafdiagram zijn kunnen worden bekeken eronder. Er vindt u Hallo totaal aantal treffers en Hallo en de hoeveelheid gegevens overgedragen (in gigabytes) voor elke dag wordt gedekt door Hallo-rapport.

## <a name="by-file-type"></a>Door het bestandstype
Hallo door het bestandstype rapport kunt u tooview Hallo hoeveelheid vraag en Hallo verkeer die door het bestandstype. Bij het genereren van dit type rapport geeft een grafiek ring Hallo percentage treffers die worden gegenereerd door Hallo bovenste 10-bestandstypen.

> [!TIP]
> Als u de muisaanwijzer op een segment in Hallo ring grafiek, mediatype Hallo Internet van dat bestandstype wordt weergegeven als knopinfo.
> 
> 

Hallo-gegevens die gebruikt toogenerate Hallo ring grafiek zijn kunnen worden bekeken eronder. Er wordt u Hallo naam extensie/Internet media bestandstype, Hallo totaal aantal treffers, Hallo percentage treffers, Hallo en de hoeveelheid gegevens overgedragen (in gigabytes) vinden en hello percentage van de gegevens die overgedragen voor elk Hallo top 250 bestandstypen.

## <a name="by-directory"></a>Door Directory
Hallo door Directory rapport kunt u tooview Hallo hoeveelheid vraag en Hallo verkeer dat gedurende een bepaald platform naar inhoud vanaf een specifieke map. Bij dit type rapport worden gegenereerd, wordt een staafdiagram Hallo kunt u het totaal aantal treffers die worden gegenereerd door de inhoud in de bovenste 10 mappen Hallo aangegeven.

### <a name="using-hello-bar-chart"></a>Met behulp van Hallo staafdiagram
* Beweeg de muisaanwijzer over een balk tooview Hallo relatief pad toohello bijbehorende map.
* Inhoud die is opgeslagen in een submap van een map telt niet mee bij het berekenen van de aanvraag door de directory. Deze berekening uitsluitend gebruikmaakt van het aantal aanvragen voor inhoud die is opgeslagen in de huidige map Hallo gegenereerd Hallo.
* Rand CNAME-URL's zijn voor Hallo toepassing van dit rapport wordt geconverteerde tootheir gelijkwaardige CDN URL's. Hierdoor kan een nauwkeurige tally voor alle statistische gegevens die zijn gekoppeld aan een asset ongeacht Hallo CDN of edge CNAME-URL die wordt gebruikt toorequest deze.

Hallo geeft linkerkant van de grafiek hello (y-as) Hallo kunt u het totale aantal aanvragen voor Hallo inhoud opgeslagen in de bovenste 10 mappen. Elke staaf op Hallo grafiek vertegenwoordigt een map. Gebruik Hallo toomatch schema van een balk kleurcodering tooa directory vermeld in Hallo boven 250 volledige mappen sectie.

Hallo-gegevens die gebruikt toogenerate Hallo staafdiagram zijn kunnen worden bekeken eronder. Hier vindt u Hallo volgende informatie voor elke Hallo boven 250 mappen: relatief pad, Hallo totaal aantal treffers, Hallo percentage treffers, Hallo en de hoeveelheid gegevens overgedragen (in gigabytes) en het Hallo-percentage overgedragen gegevens.

## <a name="by-browser"></a>Door de Browser
Hallo door Browser rapport kunt u tooview welke browsers gebruikte toorequest inhoud zijn. Bij het genereren van dit type rapport geeft een cirkeldiagram Hallo percentage aanvragen dat is verwerkt door Hallo top 10 van browsers.

### <a name="using-hello-pie-chart"></a>Met behulp van het cirkeldiagram Hallo
* Beweeg de muisaanwijzer over een segment in Hallo cirkeldiagram tooview een browser naam en versie.
* Voor Hallo toepassing van dit rapport wordt elke combinatie unieke browserversie wordt beschouwd als een andere browser.
* Hallo-segment aangeroepen 'Overig' geeft Hallo percentage aanvragen dat is verwerkt door andere browsers en versies.

Hallo-gegevens die gebruikt toogenerate Hallo cirkeldiagram zijn kunnen worden bekeken eronder. U vindt er Hallo browser type/versienummer, Hallo totaal aantal treffers en het Hallo percentage treffers voor elk van de bovenste 250 browsers Hallo.

## <a name="by-referrer"></a>Door de verwijzende site
Hallo door verwijzende rapport kunt u tooview Hallo bovenste verwijzingen toocontent op Hallo geselecteerde platform. Een verwijzende site geeft Hallo-hostnaam op basis waarvan een aanvraag is gegenereerd. Bij het genereren van dit type rapport geeft een staafdiagram Hallo hoeveelheid aanvraag (dat wil zeggen, hits) die worden gegenereerd door Hallo bovenste 10 verwijzingen.

de linkerkant Hallo van Hallo grafiek (y-as) geeft aan Hallo kunt u het totale aantal aanvragen dat een asset voor elke verwijzende site opgetreden. Elke staaf op Hallo grafiek vertegenwoordigt een verwijzende site. Gebruik Hallo toomatch schema van een balk kleurcodering tooa verwijzende vermeld in Hallo boven 250 verwijzende sectie.

Hallo-gegevens die gebruikt toogenerate Hallo staafdiagram zijn kunnen worden bekeken eronder. U vindt er Hallo-URL, Hallo totaal aantal treffers en het Hallo percentage treffers gegenereerd op basis van elk van de bovenste 250 verwijzingen Hallo.

## <a name="by-download"></a>Door downloaden
Hallo downloaden door rapport kunt u tooanalyze downloaden patronen voor uw meest aangevraagde inhoud. Hallo bovenaan Hallo rapport bevat een staafdiagram dat vergelijkt geprobeerd downloads met voltooide downloads voor Hallo top 10 aangevraagde activa. Elke staaf is voorzien van een kleurcode volgens toowhether is een poging tot gedownload (blauw) of een voltooide downloaden (groen).

> [!NOTE]
> Rand CNAME-URL's zijn voor Hallo toepassing van dit rapport wordt geconverteerde tootheir gelijkwaardige CDN URL's. Hierdoor kan een nauwkeurige tally voor alle statistische gegevens die zijn gekoppeld aan een asset ongeacht Hallo CDN of edge CNAME-URL die wordt gebruikt toorequest deze.
> 
> 

de linkerkant Hallo van Hallo grafiek (y-as) geeft de bestandsnaam Hallo voor elk Hallo bovenste 10 aangevraagde activa. Direct onder Hallo grafiek (x-as) vindt u de labels die wijzen op Hallo kunt u het totale aantal downloads geprobeerd kan niet worden voltooid.

Rechtstreeks onder staafdiagram Hallo Hallo volgende informatie wordt weergegeven voor Hallo bovenste 250 aangevraagde activa: relatief pad (inclusief bestandsnaam), Hallo aantal keren dat het gedownloade toocompletion Hallo aantal keren dat deze is gevraagd en Hallo was het percentage aanvragen dat heeft geresulteerd in een volledige download.

> [!TIP]
> Onze CDN is niet op de hoogte door een HTTP-client (dat wil zeggen browser) wanneer een asset volledig zijn gedownload. Als gevolg hiervan hebben we toocalculate of een asset volledig is gedownload en byte-bereikaanvragen volgens toostatus-foutcodes. Hallo zoekt eerst te beginnen we wanneer deze berekening of Hallo-aanvraag resulteert in een statuscode van 200 OK. Als dit het geval is, klikt u vervolgens kijken we bereik aan bytes aanvragen tooensure dat ze hebben betrekking op Hallo gehele activa. Ten slotte vergelijken we Hallo hoeveelheid overgedragen gegevens toohello grootte van de aangevraagde asset Hallo. Als Hallo gegevens overgebracht gelijk tooor groter is dan de bestandsgrootte Hallo en Hallo-byte-bereikaanvragen geschikt zijn voor die asset vervolgens Hallo hit worden geteld als een volledige download.
> 
> Vanwege de aard van toohello interpretatie van dit rapport, dient u rekening Hallo punten die Hallo consistentie en juistheid van dit rapport kunnen wijzigen na houden.
> 
> * Verkeerspatronen kunnen niet nauwkeurig worden voorspeld wanneer gebruikersagenten zich anders gedragen. Dit kan leiden tot downloadresultaten voltooide die groter dan 100 zijn %.
> * Activa die van HTTP-progressief downloaden gebruikmaken mogelijk niet nauwkeurig worden vertegenwoordigd door dit rapport. Dit is vanwege toousers om toodifferent posities in een video.
> 
> 

## <a name="by-404-errors"></a>Door 404-fouten
Hallo rapport door 404-fouten kunt u tooidentify Hallo type inhoud dat Hallo meest aantal 404 statuscodes niet gevonden genereert. Hallo bovenaan Hallo rapport bevat een staafdiagram voor Hallo top 10 activa waarvoor een statuscode 404 niet gevonden geretourneerd. Deze staafdiagram vergelijkt Hallo kunt u het totale aantal aanvragen met aanvragen dat heeft geresulteerd in een 404 niet gevonden statuscode voor deze activa. Elke balk is gekleurde. Een gele balk wordt gebruikt tooindicate die aanvraag Hallo resulteerde in een statuscode 404 niet gevonden. Wordt gebruikt met een rode balk tooindicate Hallo totaal aantal aanvragen voor Hallo asset.

> [!NOTE]
> Let op Hallo volgende oog op Hallo van dit rapport wordt:
> 
> * Een treffer vertegenwoordigt een aanvraag voor een asset ongeacht de statuscode.
> * Rand CNAME-URL's zijn geconverteerde tootheir gelijkwaardige CDN URL's. Hierdoor kan een nauwkeurige tally voor alle statistische gegevens die zijn gekoppeld aan een asset ongeacht Hallo CDN of edge CNAME-URL die wordt gebruikt toorequest deze.
> 
> 

de linkerkant Hallo van Hallo grafiek (y-as) geeft de bestandsnaam Hallo voor elk Hallo bovenste 10 aangevraagde activa dat heeft geresulteerd in een statuscode 404 niet gevonden. Direct onder Hallo grafiek (x-as) vindt u de labels die wijzen op Hallo kunt u het totale aantal aanvragen en Hallo aantal aanvragen dat heeft geresulteerd in een statuscode 404 niet gevonden.

Rechtstreeks onder staafdiagram Hallo Hallo volgende informatie wordt weergegeven voor Hallo bovenste 250 aangevraagde activa: relatief pad (inclusief bestandsnaam), het aantal aanvragen dat heeft geresulteerd in een 404 niet gevonden statuscode totaal aantal keren dat asset Hallo HALLO hallo is aangevraagd en Hallo percentage aanvragen dat heeft geresulteerd in een statuscode 404 niet gevonden.

## <a name="see-also"></a>Zie ook
* [Overzicht van Azure CDN](cdn-overview.md)
* [Realtime statistieken in Microsoft Azure CDN](cdn-real-time-stats.md)
* [Standaardgedrag HTTP met Hallo regelengine](cdn-rules-engine.md)
* [Edge-prestaties analyseren](cdn-edge-performance.md)

