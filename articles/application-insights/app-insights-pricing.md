---
title: de prijzen en -gegevens volume aaaManage voor Azure Application Insights | Microsoft Docs
description: Telemetrie volumes beheren en bewaken van kosten in Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: ebd0d843-4780-4ff3-bc68-932aa44185f6
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: bwren
ms.openlocfilehash: 4621c989cd467735aefc48ec9547fcbe1b1ae41b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-pricing-and-data-volume-in-application-insights"></a>Volume-prijzen en -gegevens in Application Insights beheren


Prijzen voor [Azure Application Insights] [ start] is gebaseerd op een gegevensvolume per toepassing. Lage gebruik tijdens de ontwikkeling of voor een kleine app is waarschijnlijk toobe vrij, omdat er een 1 GB maandelijkse tegoed van telemetriegegevens.

Elke Application Insights-resource wordt in rekening gebracht als een afzonderlijke service en toohello factuur voor uw abonnement tooAzure bijdraagt.

Er zijn twee prijscategorie plannen. Hallo standaardplan heet Basic. U kunt kiezen voor Hallo enterpriseplan heeft, dagelijkse kosten met zich mee, maar schakelt bepaalde aanvullende functies zoals [continue export](app-insights-export-telemetry.md).

Als u vragen hebt over hoe u prijzen voor Application Insights werkt, kunt u gratis toopost een vraag in onze [forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=ApplicationInsights). 

## <a name="hello-price-plans"></a>Hallo prijs plannen

Zie Hallo [Application Insights pagina met prijzen] [ pricing] voor huidige prijzen in de valuta.

### <a name="basic-plan"></a>Basic-abonnement

Hallo basisniveau is standaard Hallo wanneer een nieuwe Application Insights-resource is gemaakt en er is voldoende voor de meeste klanten.

* In de basisniveau hello, u in rekening worden gebracht door gegevensvolume: aantal bytes van telemetrie ontvangen door de Application Insights. Gegevensvolume wordt gemeten als Hallo grootte van Hallo ongecomprimeerde JSON-gegevenspakket is ontvangen door de Application Insights van uw toepassing.
Voor [tabelgegevens geïmporteerd in Analytics](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-import), Hallo gegevensvolume als niet-gecomprimeerde grootte van bestanden die worden verzonden tooApplication Insights Hallo wordt gemeten.  
* Uw eerste 1 GB voor elke app is gratis, dus als u alleen experimenteren of ontwikkelen, u waarschijnlijk niet toohave toopay bent.
* [Metrische gegevens livestream](app-insights-live-stream.md) gegevens wordt niet meegeteld voor de doeleinden prijzen.
* [Continue Export](app-insights-export-telemetry.md) is beschikbaar voor de kosten van een extra GB in Hallo basisniveau.

### <a name="enterprise-plan"></a>Enterpriseplan

* Uw app kunt Hallo-enterpriseplan alle Hallo functies van Application Insights gebruiken. [Continue Export](app-insights-export-telemetry.md) en 

[Meld u Analytics connector](https://go.microsoft.com/fwlink/?LinkId=833039&amp;clcid=0x409) beschikbaar zijn zonder eventuele extra kosten zijn in Hallo-enterpriseplan.
* U betaalt per knooppunt dat telemetrie voor alle apps in Hallo-enterpriseplan verzendt. 
 * Een *knooppunt* is een fysieke of virtuele server-computer of op een exemplaar van de rol Platform as a Service, die als host fungeert voor uw app.
 * Machines voor ontwikkeling, clientbrowsers en mobiele apparaten worden niet meegeteld als knooppunten.
 * Als uw app heeft verschillende onderdelen die verzenden van telemetrie, zoals een webservice en een back-end-worker, worden ze afzonderlijk meegeteld.
 * [Metrische gegevens livestream](app-insights-live-stream.md) gegevens wordt niet meegeteld voor de prijzen purposes.* over een abonnement, zijn uw kosten per knooppunt niet per app. Als u vijf knooppunten verzenden van telemetrie hebt voor 12 apps en vervolgens Hallo kosten in rekening gebracht voor vijf knooppunten is.
* Hoewel kosten worden genoteerd per maand, bent u in rekening gebracht voor elk uur waarin een knooppunt telemetrie vanuit een app verzendt alleen. Hallo kosten per uur is Hallo aanhalingstekens maandelijkse kosten / 744 (Hallo aantal uren in een maand 31 dagen).
* De toewijzing van een data volume van 200 MB per dag wordt gegeven voor elk knooppunt (met de Uurlijkse samenvattingen) zijn gedetecteerd. Ongebruikte gegevens toewijzing wordt niet overgenomen van één dag toohello naast.
 * Als u Hallo prijscategorie Enterprise-optie kiest, worden in elk abonnement een dagelijkse vergoeding van gegevens op basis van het aantal knooppunten verzenden van telemetrie toohello Application Insights-resources in het desbetreffende abonnement Hallo krijgt. Dus als er 5 verzenden van gegevens alle dag-knooppunten, u een gegroepeerde correctie van 1 GB toegepast tooall Hallo Application Insights-resources in het desbetreffende abonnement hebt. Het maakt niet uit als bepaalde knooppunten dat meer gegevens dan andere knooppunten verzendt omdat Hallo gegevens opgenomen wordt gedeeld door alle knooppunten. Als op een bepaalde dag Hallo Application Insights-resources meer gegevens ontvangt dan is opgenomen in het dagelijkse gegevens toewijzing Hallo voor dit abonnement, Hallo per GB overschrijding gegevens gelden. 
 * Hallo dagelijkse gegevens vergoeding wordt berekend als het aantal uren in Hallo dag (met behulp van UTC) Hallo dat elk knooppunt gedeeld door 24 keer 200 MB telemetrie verzendt. Dus als er 4 knooppunten verzenden van telemetrie tijdens 15 Hallo 24 uur Hallo dag, Hallo gegevens opgenomen voor die dag zou worden ((4 x 15) / 24) x 200 MB = 500 MB. Hallo de prijs van 2.30 USD per GB voor data overschrijding, zou Hallo kosten voor 1.15 USD zijn als Hallo knooppunten 1 GB aan gegevens die dag verzonden.
 * Houd er rekening mee dat dagelijkse vergoeding Hallo enterpriseplan niet wordt gedeeld met toepassingen die u ervoor optie Hallo gekozen hebt en ongebruikte toegestane wordt niet overgenomen van dagelijkse. 
* Hier volgen enkele voorbeelden van het aantal afzonderlijke knooppunten te bepalen:
| Scenario                               | Totaal aantal per dag knooppunt |
|:---------------------------------------|:----------------:|
| 1 toepassing gebruik maakt van 3-Azure App Service-exemplaren en 1 virtuele server | 4 |
| 3-toepassingen met 2 virtuele machines en Hallo Application Insights-resources voor deze toepassingen zijn hetzelfde abonnement hello en in Hallo Enterprise plannen | 2 | 
| 4 toepassingen waarvan toepassingen Insights-bronnen bevinden zich in hetzelfde abonnement Hallo. Elke toepassing wordt uitgevoerd 2 exemplaren 16 piekuren en 4 exemplaren tijdens de piekuren die 8. | 13.33 | 
| Cloudservices met Werkrol 1 en 1 Webrol met elk 2 exemplaren | 4 | 
| 5-knooppunt Service Fabric-Cluster met 50 micro-services, elke micro-service met 3 exemplaren | 5|

* Hallo nauwkeurig knooppunt tellen gedrag is afhankelijk van waarop Application Insights-SDK uw toepassing wordt gebruikt. 
  * In de SDK-versies 2.2 en en hoger, beide Application Insights Hallo [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) of [Web SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) wordt elke toepassingshost als een knooppunt rapporteren, bijvoorbeeld Hallo computernaam voor de fysieke server en VM-hosts of Hallo in geval van Hallo van cloudservices-exemplaarnaam.  Hallo alleen uitzondering toepassingen is alleen [.NET Core](https://dotnet.github.io/) en Hallo Application Insights-Core SDK, waarin u slechts één case-knooppunt wordt gerapporteerd voor alle hosts omdat Hallo hostnaam niet beschikbaar is. 
  * Voor eerdere versies van Hallo SDK Hallo [Web SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) werken net zoals hello nieuwere versies van de SDK, echter Hallo wordt [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) slechts één knooppunt, ongeacht het aantal huidige toepassingshosts Hallo rapporteert. 
  * Houd er rekening mee dat als uw toepassing hello SDK tooset roleInstance tooa aangepaste waarde gebruikt, standaard die dezelfde waarde wordt gebruikt toodetermine Hallo aantal knooppunten. 
  * Als u een nieuwe versie van de SDK gebruikt met een app die wordt uitgevoerd vanaf clientcomputers of mobiele apparaten, is het mogelijk dat het aantal knooppunten Hallo mogelijk een getal retourneren dat erg groot is (van Hallo groot aantal clientcomputers of mobiele apparaten). 

### <a name="multi-step-web-tests"></a>Webtests met meerdere stappen

Er is een extra kosten voor [webtests met meerdere stappen](app-insights-monitor-web-app-availability.md#multi-step-web-tests). Dit verwijst tooweb tests die een reeks acties uitvoeren. 

Er zijn geen afzonderlijke kosten voor pingtests van één pagina. Telemetrie uit meerdere stappen tests en ping-tests is in rekening gebracht samen met andere telemetrie van uw app.
 
## <a name="operations-management-suite-subscription-entitlement"></a>Operations Management Suite-abonnement recht

Als [onlangs aangekondigd](https://blogs.technet.microsoft.com/msoms/2017/05/19/azure-application-insights-enterprise-as-part-of-operations-management-suite-subscription/), klanten die kopen van Microsoft Operations Management Suite E1 en E2 kunnen tooget Application Insights Enterprise als een extra onderdeel zonder extra kosten zijn. Elke eenheid van Operations Management Suite E1 en E2 bevat met name een knooppunt van de too1 recht van het Hallo-enterpriseplan van Application Insights. Zoals eerder vermeld, bevat elk knooppunt van de Application Insights too200 MB aan gegevens per dag (gescheiden van logboekanalyse gegevensopname), met behoud van 90 dagen voor gegevens zonder extra kosten ingenomen. 

> [!NOTE]
> tooensure dat u dit recht krijgt, hebt u uw Application Insights-resources in de onderneming Hallo plan prijzen. Dit recht geldt alleen als knooppunten, zodat het geen voordeel Application Insights-resources in Hallo basisniveau niet realiseren. Houd er rekening mee dat dit recht is niet meer zichtbaar op Hallo geschatte kosten weergegeven op Hallo functies en prijzen blade. 
>
 
## <a name="review-pricing-plans-and-estimate-costs"></a>Bekijk prijscategorie plannen en kosten schatten

Applicaition Insights maakt het eenvoudig toounderstand Hallo prijsstelling beschikbaar is en welke Hallo kosten zijn waarschijnlijk worden gebaseerd op recente gebruikspatronen. Begin door Hallo openen **functies + prijzen** blade in Hallo Application Insights-resource in hello Azure-portal:

![Kies de prijzen.](./media/app-insights-pricing/01-pricing.png)

**a.** Bekijk uw gegevensvolume Hallo maand. Dit omvat alle Hallo gegevens ontvangen en bewaard (na een [steekproeven](app-insights-sampling.md) van uw server en client-apps en van de beschikbaarheidstests.

**b.** Afzonderlijke kosten met zich mee worden gesteld voor [webtests met meerdere stappen](app-insights-monitor-web-app-availability.md#multi-step-web-tests). (De van eenvoudige beschikbaarheidstests die zijn opgenomen in Hallo gegevens volume kosten worden niet opgenomen.)

**c.** Hallo-enterpriseplan inschakelen.

**d.** Klik door toodata management opties tooview gegevensvolume voor Hallo afgelopen maand, een dagelijkse limiet ingesteld of opname steekproeven instellen.

Application Insights kosten worden tooyour Azure-factuur toegevoegd. U kunt details van uw Azure factureren op Hallo facturering sectie van hello Azure-portal of in Hallo bekijken [Azure Billing Portal](https://account.windowsazure.com/Subscriptions). 

![Kies Hallo side menu facturering.](./media/app-insights-pricing/02-billing.png)

## <a name="data-rate"></a>Verwerkingssnelheid van gegevens
Er zijn drie manieren in welke Hallo volume verzenden van gegevens beperkt is:

* **Steekproeven:** dit mechanisme kan worden gebruikt beperken Hallo telemetrie van uw server en client-apps met minimale vervalsing van de metrische gegevens worden verzonden. Dit is de primaire hulpprogramma Hallo u tootune Hallo hoeveelheid gegevens hebt. Meer informatie over [steekproef nemen functies](app-insights-sampling.md). 
* **Dagelijkse cap:** wanneer een Application Insights-resource maken van hello Azure-portal dit too500 GB per dag is ingesteld. Hallo standaard bij het maken van een Application Insights-resource vanuit Visual Studio, is klein (alleen 32,3 MB/dag) is bedoeld alleen toofaciliate testen. In dit geval wordt het bedoeld dat die gebruiker Hallo Hallo dagelijkse cap verhoogt voordat het Hallo-app implementeren in productie. de maximumcapaciteit Hallo is 500 GB per dag, tenzij u hebt aangevraagd, een hogere maximum voor een toepassing intensief verkeer. Wees voorzichtig bij het instellen van de dagelijkse cap hello, zoals het uw bedoeling moet **nooit toohit Hallo dagelijkse cap**, omdat u vervolgens gegevens voor de rest van de dag Hallo Hallo verliezen en toomonitor kan niet worden uw toepassing. toochange ervan gebruik Hallo dagelijkse volume cap blade gekoppeld Hallo Volume gegevensbeheer blade (Zie hieronder). Houd er rekening mee dat sommige typen abonnement tegoed dat kan worden gebruikt voor Application Insights. Als het Hallo-abonnement heeft een bestedingslimiet beperken, dagelijks Hallo cap blade instructies hoe hebt tooremove deze en schakel Hallo dagelijkse cap toobe buiten 32,3 MB per dag wordt gegenereerd.  
* **Beperking:** deze limieten Hallo gegevens snelheid too32 k gebeurtenissen per seconde, gemiddelde waarde van meer dan 1 minuut. 


*Wat gebeurt er als mijn app groter is dan de bandbreedteregeling snelheid Hallo?*

* Hallo hoeveelheid gegevens die uw app verzendt, wordt elke minuut beoordeeld. Als het Hallo per seconde, gemiddeld in Hallo minuut overschrijdt, weigert Hallo server bepaalde aanvragen. Hallo SDK buffert Hallo gegevens en probeert vervolgens tooresend, een piek uit spreiden over enkele minuten. Als uw app consistent data-at-hierboven Hallo bandbreedteregeling snelheid verzendt, is enkele gegevens wordt verwijderd. (Hallo ASP.NET, Java en JavaScript SDK's probeer tooresend op deze manier en andere SDK gewoon neerzetten beperkt gegevens mogelijk.) Als beperking optreedt, ziet u een melding waarschuwing dit is gebeurd.

*Hoe weet ik hoeveel gegevens van mijn app verzenden?*

* Open Hallo **volume gegevensbeheer** blade toosee Hallo dagelijkse gegevens volume grafiek. 
* Of in Metrics Explorer, Voeg een nieuwe grafiek toe en selecteer **gegevenspuntvolume** als de metriek. Ga voor de groepering en groeperen op **gegevenstype**.

## <a name="tooreduce-your-data-rate"></a>tooreduce de snelheid waarmee u gegevens
Hier volgen enkele dingen die u tooreduce uw gegevensvolume kunt doen:

* Gebruik [steekproeven](app-insights-sampling.md). Deze technologie verkleint gegevenssnelheid zonder metrische gegevens over uw scheeftrekken en zonder Hallo mogelijkheid toonavigate tussen verwante items in de zoekopdracht te verstoren. In server apps werkt automatisch.
* [Beperk het aantal Ajax-aanroepen die kan worden gerapporteerd Hallo](app-insights-javascript.md#detailed-configuration) in elke pagina of de switch uit Ajax-rapportage.
* Verzameling-modules die u niet nodig hebt met uitschakelen [ApplicationInsights.config bewerken](app-insights-configuration-with-applicationinsights-config.md). U kunt bijvoorbeeld besluiten dat prestatiemeteritems of afhankelijkheidsgegevens inessential zijn.
* Uw telemetrie tooseparate instrumentatiesleutels splitsen. 
* Vooraf cumulatieve metrische gegevens. Als in uw app aanroepen tooTrackMetric hebt geplaatst, kunt u verkeer beperken met behulp van Hallo overbelasting waarvoor de berekening van gemiddelde Hallo en de standaarddeviatie van een batch van metingen accepteert. Of u kunt een [vooraf verzamelen pakket](https://www.myget.org/gallery/applicationinsights-sdk-labs).

## <a name="managing-hello-maximum-daily-data-volume"></a>Hallo die dagelijks maximum gegevensvolume beheren

Kunt u Hallo dagelijkse volume cap toolimit Hallo gegevens die zijn verzameld, maar als Hallo kapje wordt voldaan, het zal leiden tot verlies van alle telemetery verzonden vanuit uw toepassing hello rest van de dag Hallo. Het is **niet aangeraden** toohave uw toepassing toohit Hallo dagelijkse cap sinds u zijn niet kan tootrack Hallo status en prestaties van uw toepassing nadat deze is bereikt. 

Gebruik in plaats daarvan [steekproeven](app-insights-sampling.md) tootune Hallo volume toohello gegevensniveau u wilt, en dagelijkse cap Hallo alleen gebruiken zoals 'laatste toevlucht' als uw toepassing wordt gestart met het verzenden van veel grotere volumes van telemetery onverwacht. 

toochange hello dagelijkse cap in Hallo sectie configureren van uw toepassing Insihgts resource, klikt u op **volume gegevensbeheer** vervolgens **dagelijkse Cap**.

![Hallo dagelijkse telemetrie volume cap aanpassen](./media/app-insights-pricing/daily-cap.png) 

## <a name="sampling"></a>Steekproeven
[Steekproef nemen](app-insights-sampling.md) is een methode te verlagen Hallo snelheid waarmee telemetrie tooyour app, is verzonden terwijl blijven behouden Hallo mogelijkheid toofind gebeurtenissen tijdens diagnostische zoekopdrachten gerelateerde en nog steeds behoudende juist gebeurtenis telt. 

Steekproeven is een effectieve manier tooreduce brengt en binnen uw maandelijkse quotum blijven. Hallo steekproeven algoritme behoudt verwante items van telemetrie, zodat bijvoorbeeld, wanneer u de zoekfunctie gebruiken, kunt u vinden Hallo aanvraag gerelateerde tooa bepaalde uitzondering. Hallo-algoritme behoudt ook juiste aantallen, zodat u de juiste waarden Hallo in Verkenner metrische gegevens voor aanvraag tarieven uitzondering tarieven en andere aantallen zien.

Er zijn verschillende vormen van steekproeven.

* [Adaptieve steekproeven](app-insights-sampling.md) is de standaardoptie Hallo voor Hallo ASP.NET-SDK, die automatisch wordt aangepast volume toohello telemetrie die uw app verzendt. Dit werkt automatisch in Hallo SDK in uw web-app zodat Hallo telemetrie verkeer op Hallo netwerk wordt verminderd. 
* *Opname steekproeven* vormt een alternatief dat werkt op Hallo punt waar de telemetrie van uw app Hallo Application Insights-service krijgt. Dit heeft geen invloed op Hallo volume telemetrie van uw app verzonden, maar dit verlaagt Hallo volume behouden door Hallo-service. U kunt deze gebruiken tooreduce Hallo quotum gebruikt door de telemetrie van browsers en andere SDK.

tooset opname steekproef nemen, Hallo besturingselement in Hallo prijzen blade ingesteld:

![Hallo quotum en prijzen blade, klikt u op Hallo voorbeelden tegel en selecteer een fractie van steekproeven.](./media/app-insights-pricing/04.png)

> [!WARNING]
> Hallo gegevens steekproeven blade alleen besturingselementen Hallo-waarde van opname steekproeven. Hallo samplefrequentie die wordt toegepast door Hallo Application Insights-SDK in uw app weer niet. Als al steekproefgewijs Hallo binnenkomende telemetrie op Hallo SDK verkregen, opname steekproeven niet toegepast.
> 

toodiscover hello werkelijke snelheid ongeacht waar deze zijn toegepast, wordt gebruikt een [Analytics query](app-insights-analytics.md) zoals deze:

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

In elk bewaard record, `itemCount` geeft het aantal oorspronkelijke records die deze vertegenwoordigt, gelijk too1 + aantal eerdere verwijderde records Hallo Hallo. 


## <a name="automation"></a>Automatisering

U kunt een script tooset Hallo prijs plan schrijven met Azure Resource Management. [Meer informatie over hoe](app-insights-powershell.md#price).

## <a name="limits-summary"></a>Limieten samenvatting
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

## <a name="next-steps"></a>Volgende stappen

* [Steekproeven](app-insights-sampling.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[start]: app-insights-overview.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/

