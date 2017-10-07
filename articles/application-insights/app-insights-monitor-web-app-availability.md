---
title: aaaMonitor beschikbaarheid en reactiesnelheid van een website | Microsoft Docs
description: Stel webtests in Application Insights in. Ontvang een waarschuwing wanneer een website niet meer beschikbaar is of traag reageert.
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 46dc13b4-eb2e-4142-a21c-94a156f760ee
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: bwren
ms.openlocfilehash: 4c5425c948770cc57a648ca50e217c75ac75fbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a>De beschikbaarheid en reactiesnelheid van een website bewaken
Nadat u uw web-app of website tooany server hebt geïmplementeerd, kunt u tests toomonitor instellen beschikbaarheid en reactiesnelheid ervan. [Azure Application Insights](app-insights-overview.md) verzendt webaanvragen tooyour toepassing met regelmatige tussenpozen vanaf punten overal Hallo wereld. U wordt gewaarschuwd als uw toepassing niet of langzaam reageert.

U kunt beschikbaarheidstests instellen voor alle HTTP of HTTPS-eindpunt dat toegankelijk is vanaf Hallo openbare internet. U hebt geen tooadd alles toohello-website die u test. Zelfs heeft geen toobe uw site: kan het testen van een REST-API-service waarvan u afhankelijk zijn.

Er zijn twee soorten beschikbaarheidstests:

* [URL-Pingtest](#create): een eenvoudige test die u in hello Azure-portal kunt maken.
* [WebTest met meerdere stappen](#multi-step-web-tests): die u maakt in Visual Studio Enterprise en uploaden toohello portal.

U kunt maken van de beschikbaarheidstests too25 per toepassingsresource.

## <a name="create"></a>1. Een resource openen voor uw beschikbaarheidstestrapporten

**Als u al hebt geconfigureerd Application Insights** voor uw web-app, opent u de Application Insights-resource in Hallo [Azure-portal](https://portal.azure.com).

**Of, als u wilt dat toosee uw rapporten in een nieuwe resource** te registreren[Microsoft Azure](http://azure.com), gaat u toohello [Azure-portal](https://portal.azure.com), en maak een Application Insights-resource.

![Nieuw > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

Klik op **alle resources** tooopen hello overzichtsblade voor Hallo nieuwe resource.

## <a name="setup"></a>2. Een URL-pingtest aanmaken
Hallo beschikbaarheid blade geopend en een test toevoegen.

![Opvulling Hallo ten minste URL van uw website](./media/app-insights-monitor-web-app-availability/13-availability.png)

* **Hallo URL** een webpagina kunnen worden gewenste tootest, maar deze moet zichtbaar zijn op Hallo van openbare internet. Hallo-URL kan een queryreeks bevatten. Zo kunt u bijvoorbeeld oefenen met uw database. Als Hallo-URL wordt omgezet tooa omleiding, volgen we het too10 omleidingen.
* **Afhankelijke aanvragen parseren**: als deze optie is ingeschakeld, Hallo test installatiekopieën, scripts, Stijlbestanden en andere bestanden die deel van de webpagina Hallo onder test uitmaken aanvragen. Hallo omvat vastgelegde reactietijd Hallo tijd tooget deze bestanden. Hallo-test mislukt als al deze resources is binnen de time-out voor de hele test Hallo Hallo kunnen niet worden gedownload. 

    Als het Hallo-optie niet is ingeschakeld, vraagt Hallo test alleen Hallo-bestand op Hallo-URL die u hebt opgegeven.
* **Nieuwe pogingen inschakelen**: als deze optie is ingeschakeld, Hallo test mislukt, wordt opnieuw geprobeerd na een korte periode. Fouten worden pas gerapporteerd als er drie opeenvolgende pogingen mislukken. Daaropvolgende tests worden dan uitgevoerd op de gebruikelijke Testfrequentie Hallo. Nieuwe pogingen worden tijdelijk uitgesteld tot Hallo volgende geslaagd. Deze regel wordt onafhankelijk toegepast op elke testlocatie. Deze optie wordt aangeraden. Gemiddeld verdwijnt ongeveer 80% van de fouten na het opnieuw proberen.
* **Testfrequentie**: Hiermee stelt u hoe vaak hello test wordt uitgevoerd vanaf elke testlocatie. Met een frequentie van vijf minuten en vijf testlocaties wordt uw site gemiddeld per minuut getest.
* **Testlocaties** zijn Hallo plaatst van waar onze servers tooyour-URL voor webinhoud aanvragen verzenden. Kies meer dan één testlocatie, zodat u problemen met uw website kunt onderscheiden van netwerkproblemen. U kunt selecteren too16 vestigingen.
* **Criteria voor succes**:

    **Time-out van de test**: deze waarde toobe gewaarschuwd over trage reacties afnemen. Hallo-test wordt als mislukt beschouwd als Hallo-antwoorden van uw site niet binnen deze periode zijn ontvangen. Als u hebt geselecteerd **afhankelijke aanvragen parseren**vervolgens alle Hallo afbeeldingen, Stijlbestanden, scripts en andere afhankelijke resources moeten worden ontvangen binnen deze periode.

    **HTTP-antwoord**: Hallo geretourneerde statuscode die voor een geslaagde test staat. 200 is Hallo-code waarmee wordt aangegeven dat een normale webpagina is geretourneerd.

    **Inhoudsovereenkomst**: een tekenreeks, zoals 'Welkom!' Er wordt getest of er in elke respons een exacte (hoofdlettergevoelige) overeenkomst wordt gevonden. Het moet een eenvoudige tekenreeks zijn, zonder jokertekens. Vergeet niet dat als de pagina inhoud wijzigingen die u wellicht tooupdate deze.
* **Waarschuwingen** zijn, worden standaard verzonden tooyou als er fouten op drie locaties gedurende vijf minuten. Een fout op één locatie is waarschijnlijk toobe een probleem met het netwerk en niet per se aan uw site. Maar kunt u Hallo drempelwaarde toobe meer of minder gevoelig, en u kunt ook wijzigen die Hallo e-mailberichten naar moeten worden verzonden.

    U kunt een [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) instellen die wordt aangeroepen wanneer er een waarschuwing wordt gegenereerd. (Merk op dat, momenteel, queryparameters niet worden doorgegeven als Eigenschappen.)

### <a name="test-more-urls"></a>Meer URL’s testen
Voeg meer tests toe. Bijvoorbeeld In toevoeging tootesting uw startpagina, kunt u ervoor dat de database door te testen Hallo-URL voor een zoekopdracht wordt uitgevoerd.


## <a name="monitor"></a>3. De resultaten van de beschikbaarheidstest bekijken

Na een paar minuten, klikt u op **vernieuwen** toosee testresultaten. 

![Samenvatting van de resultaten op de startblade Hallo](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

Hallo scatterplot ziet u voorbeelden van Hallo testresultaten met details van de diagnostische test-stap. Hallo test engine slaat diagnostische gegevens voor tests met fouten. Voor geslaagde tests worden diagnostische gegevens worden opgeslagen voor een subset van Hallo uitvoeringen. Beweeg de muisaanwijzer over een van de Hallo groen/rood punten toosee Hallo test timestamp, testduur, locatie en naam van test. Klik in elk punt in Hallo spreidingsgrafiek tekent toosee Hallo details van Hallo testresultaat.  

Selecteer een afzonderlijke test locatie, of Hallo verkorten periode toosee meer rond Hallo periode van belang resultaten. Search Explorer toosee resultaten van alle uitvoeringen gebruiken of aangepaste rapporten voor toorun Analytics-query's op deze gegevens gebruiken.

In aanvulling toohello onbewerkte resultaten, moet u er twee beschikbaarheid metrische gegevens zijn in Metrics Explorer: 

1. Beschikbaarheid: Percentage Hallo tests die uitgevoerd op alle test uitvoeringen zijn. 
2. Testduur: gemiddelde testduur van alle testuitvoeringen.

U kunt filters toepassen op de naam van de test hello, locatie tooanalyze trends van een afzonderlijke test en/of de locatie.

## <a name="edit"></a> Tests bekijken en bewerken

Selecteer een specifieke test Hallo overzichtspagina. Hier kunt u de specifieke resultaten bekijken en de test bewerken of tijdelijk uitschakelen.

![Een webtest bewerken of uitschakelen](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

Wilt u misschien toodisable beschikbaarheidstests of Hallo waarschuwing regels die zijn gekoppeld aan deze tijdens het uitvoeren van onderhoud op uw service. 

## <a name="failures"></a>Als u mislukte tests ziet
Klik op een rode punt.

![Op een rode punt klikken](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


Vanuit het resultaat van een beschikbaarheidstest kunt u:

* Hallo-antwoord ontvangen van uw server te controleren.
* Open Hallo telemetrie verzonden door uw app server tijdens het verwerken van Hallo-exemplaar voor mislukte aanvragen.
* Meld een probleem of een werkitem in Git of VSTS tootrack Hallo probleem. Hallo bug bevat een koppeling toothis-gebeurtenis.
* Testresultaat van Hallo web openen in Visual Studio.


*Zien de resultaten er goed uit, maar wordt de test toch als mislukt aangeduid?* Controleer alle Hallo-installatiekopieën, scripts, opmaakmodellen en andere bestanden door Hallo pagina wordt geladen. Als een van deze mislukt, is Hallo test gerapporteerd, mislukt, zelfs als Hallo hoofd-html-pagina correct wordt geladen.

*Zijn er geen verwante items?* Als u Application Insights hebt ingesteld voor uw app aan serverzijde, kan dit komen doordat er [steekproeven](app-insights-sampling.md) worden uitgevoerd. 

## <a name="multi-step-web-tests"></a>Webtests met meerdere stappen
U kunt een scenario bewaken dat bestaat uit een reeks URL's. Bijvoorbeeld, als u een Verkoopwebsite bewaakt, kunt u testen dat toe te voegen items toohello winkelwagen goed werkt.

> [!NOTE] 
> Er worden kosten in rekening gebracht voor webtests met meerdere stappen. [Prijsoverzicht](http://azure.microsoft.com/pricing/details/application-insights/).
> 

een test met meerdere stappen toocreate, u Hallo scenario vastleggen met behulp van Visual Studio Enterprise en vervolgens uploaden Hallo tooApplication Insights opnemen. Application Insights opnieuw Hallo scenario met een interval wordt weergegeven en controleert of Hallo-antwoorden.

> [!NOTE]
> U kunt in uw tests geen gecodeerde functies of lussen gebruiken. Hallo test moet volledig zijn opgenomen in Hallo .webtest script. U kunt echter wel standaard-invoegtoepassingen gebruiken.
>

#### <a name="1-record-a-scenario"></a>1. Een scenario opnemen
Gebruik Visual Studio Enterprise toorecord een websessie.

1. Maak een project om de webprestaties te testen.

    ![Maak een project van de sjabloon Webprestatie- en belastingstest Hallo in Visual Studio Enterprise-editie.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * *Hallo webprestaties en belastingstest sjabloon niet wordt weergegeven?* Sluit Visual Studio Enterprise. Open **Visual Studio Installer** toomodify uw Visual Studio Enterprise-installatie. Selecteer onder **Afzonderlijke onderdelen** de optie **Hulpprogramma's voor webprestaties en belastingstests**.

2. Hallo .webtest-bestand te openen en begin met opnemen.

    ![Open Hallo .webtest-bestand en klik op opnemen.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. Acties van de gebruiker gewenste toosimulate in uw test Hallo: open de website, toevoegen van een product toohello winkelwagen, enzovoort. Stop vervolgens de test.

    ![Hallo WebTest webtestrecorder wordt uitgevoerd in Internet Explorer.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    Zorg ervoor dat het scenario niet te lang duurt. Er geldt een limiet van 100 stappen en 2 minuten.
4. Hallo-test om te bewerken:

   * Voeg validaties toocheck Hallo ontvangen tekst en reactiecodes.
   * Verwijder alle overbodige interacties. U kunt ook afhankelijke aanvragen voor afbeeldingen of tooad of trackingsites verwijderen.

     Houd er rekening mee dat u alleen Hallo testscript bewerken kunt: u kunt geen aangepaste code toevoegen of andere webtests aanroepen. Voeg geen lussen toe in Hallo test. U kunt standaardinvoegtoepassingen voor webtest gebruiken.
5. Hallo test worden uitgevoerd in Visual Studio toomake controleren of dat het werkt.

    Hallo webtestrunner opent een webbrowser en wordt herhaald Hallo acties die u hebt vastgelegd. Controleer of de test werkt zoals verwacht.

    ![Hallo .webtest-bestand openen in Visual Studio en klik op uitvoeren.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-hello-web-test-tooapplication-insights"></a>2. Hallo web test tooApplication Insights uploaden
1. Maak een WebTest in Hallo Application Insights-portal.

    ![Kies op de blade webtests hello, toevoegen.](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. Selecteer de test met meerdere stappen en Hallo .webtest-bestand uploaden.

    ![Selecteer de webtest met meerdere stappen.](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    Set Hallo testlocaties, frequentie en Waarschuwingsparameters in Hallo tests uit dezelfde manier als voor ping.

#### <a name="3-see-hello-results"></a>3. Hallo-resultaten te zien

Bekijk uw test resultaten en eventuele fouten in Hallo dezelfde manier als één url-tests uit.

Bovendien kunt u Hallo test resultaten tooview downloaden ze in Visual Studio.

#### <a name="too-many-failures"></a>Te veel fouten?

* Een veelvoorkomende reden voor fout is dat Hallo-test wordt uitgevoerd te lang. Het uitvoeren van de test mag niet langer dan twee minuten duren.

* Vergeet niet dat alle Hallo resources van een pagina moeten correct worden geladen Hallo test toosucceed, waaronder scripts, opmaakmodellen, afbeeldingen, enzovoort.

* Hallo WebTest moet volledig zijn opgenomen in Hallo .webtest script: u kunt gecodeerde functies gebruiken in Hallo test.

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a>Tijd en willekeurige cijfers invoegen in uw test met meerdere stappen
Stel dat u een hulpprogramma test dat tijdsafhankelijke gegevens ontvangt van een externe feed (bijvoorbeeld een feed met aandelenkoersen). Wanneer u uw WebTest opneemt, hebt u specifieke tijden toouse, maar u deze hebt ingesteld als parameters van Hallo testen, StartTime en EndTime.

![Een webtest met parameters](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

Wanneer u Hallo test uitvoert, moet EndTime altijd toobe Hallo tijd aanwezig en StartTime 15 minuten moet geleden.

Web-invoegtoepassingen voor Test kunt u Hallo toodo keren voorzien.

1. Voeg een webtestinvoegtoepassing toe voor elke gewenste variabele parameterwaarde. Kies in de werkbalk van Hallo web **Webtestinvoegtoepassing toevoegen**.

    ![Kies Webtestinvoegtoepassing toevoegen en selecteer een type.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    In dit voorbeeld gebruiken we twee exemplaren van Hallo invoegtoepassing datum / tijd. Een exemplaar is voor "15 minuten geleden" en een ander voor “nu”.
2. Open de eigenschappen van elke invoegtoepassing Hallo. Een naam geven en stel deze toouse Hallo huidige tijd. Stel voor een van de toepassingen Minuten toevoegen in op -15.

    ![Naam instellen > Huidige tijd gebruiken > Minuten toevoegen.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. Gebruik in Hallo web testparameters, {{plug-in name}} tooreference naam van de invoegtoepassing.

    ![Gebruik in Hallo testparameter {{plug-in name}}.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

Nu uw test toohello portal uploaden. Hallo dynamische waarden wordt gebruikt op elke Hallo test wordt uitgevoerd.

## <a name="dealing-with-sign-in"></a>Omgaan met aanmelden
Als uw gebruikers zich tooyour app, hebt u verschillende opties voor het aanmelden simuleren, zodat u pagina's achter aanmeldingspagina Hallo kunt testen. Hallo aanpak die u gebruikt, is afhankelijk van Hallo type beveiliging van Hallo-app.

In alle gevallen moet u een account maken in uw toepassing net voor Hallo doel van de testen. Hallo-machtigingen voor dit testaccount indien mogelijk beperken zodat er geen mogelijkheid Hallo webtests die invloed hebben op echte gebruikers.

### <a name="simple-username-and-password"></a>Eenvoudige gebruikersnaam en wachtwoord
Neem een WebTest in Hallo gebruikelijke manier. Verwijder eerst de cookies.

### <a name="saml-authentication"></a>SAML-verificatie
Hallo SAML-invoegtoepassing die beschikbaar is voor webtests gebruiken.

### <a name="client-secret"></a>Clientgeheim
Als uw app een aanmeldroute heeft die een klantgeheim omvat, gebruik dan deze route. Azure Active Directory (AAD) is een voorbeeld van een service die aanmelden met een clientgeheim bevat. In AAD is het clientgeheim Hallo Hallo App-sleutel.

Hier is een voorbeeldwebtest van een Azure web-app met een App Key:

![Voorbeeld clientgeheim](./media/app-insights-monitor-web-app-availability/110.png)

1. Token van AAD krijgen met klantgeheim (AppKey).
2. Bearer token uit antwoord halen.
3. Met behulp van bearer-token in autorisatie-header Hallo-API niet aanroepen.

Zorg ervoor dat Hallo WebTest een werkelijke client is-dat wil zeggen, een eigen app AAD heeft - en gebruik de clientId + App-sleutel. Uw test-service heeft een eigen app ook in AAD: Hallo appID URI van deze app wordt weergegeven in de WebTest Hallo in Hallo 'resource' aan.

### <a name="open-authentication"></a>Open verificatie
Een voorbeeld van open verificatie is het aanmelden met uw Microsoft- of Google-account. Veel apps dat gebruik OAuth Hallo geheime alternatieve client, zodat uw eerste clientgeheim tooinvestigate moet deze mogelijkheid.

Als uw test zich met behulp van OAuth aanmelden moet, is het Hallo algemeen de aanpak:

* Gebruik een hulpprogramma zoals Fiddler tooexamine Hallo verkeer tussen de webbrowser, Hallo verificatiesite en uw app.
* Twee of meer aanmeldingen uit via verschillende apparaten en browsers, uitvoeren of met lange periodes ertussen (tooallow tokens tooexpire).
* Door het vergelijken van verschillende sessies, identificeren Hallo-token is doorgegeven Hallo verifiëren van de site, die vervolgens tooyour appserver na het aanmelden doorgegeven.
* Neem een webtest op met Visual Studio.
* Parameter Hallo tokens, Hallo parameter instellen wanneer het Hallo-token wordt geretourneerd van Hallo verificator en gebruik deze in Hallo query toohello site.
  (Visual Studio probeert tooparameterize Hallo test, maar is niet correct in parameters omgezet Hallo-tokens.)


## <a name="performance-tests"></a>Prestatietests
U kunt een belastingtest op uw website uitvoeren. Zoals Hallo beschikbaarheidstest, kunt u eenvoudige aanvragen of aanvragen voor meerdere stappen van onze punten Hallo wereld verzenden. In tegenstelling tot een beschikbaarheidstest worden vele verzoeken verzonden, waarmee meerdere gelijktijdige gebruikers worden gesimuleerd.

Open in de overzichtsblade hello **instellingen**, **prestatietests**. Wanneer u een test maakt, u bent uitgenodigd tooconnect tooor een Visual Studio Team Services-account maken.

Wanneer het Hallo-test is voltooid, kunt u responstijden en het succespercentage worden weergegeven.


![Prestatietest](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> Gebruik tooobserve Hallo gevolgen van een prestatietest [Live Stream](app-insights-live-stream.md) en [Profiler](app-insights-profiler.md).
>

## <a name="automation"></a>Automatisering
* [Gebruik PowerShell-scripts tooset van een beschikbaarheidstest](app-insights-powershell.md#add-an-availability-test) automatisch.
* Stel een [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) in die wordt aangeroepen wanneer er een waarschuwing wordt gegenereerd.

## <a name="qna"></a>Vragen? Problemen?
* *Kan ik code aanroepen via mijn webtest?*

    Nee. Hallo stappen van Hallo test moet Hallo .webtest-bestand. U kunt geen andere webtests aanroepen of lussen gebruiken. Maar er zijn verschillende invoegtoepassingen die nuttig kunnen zijn.
* *Wordt HTTPS ondersteund?*

    ondersteunen TLS 1.1 en TLS 1.2.
* *Is er een verschil tussen webtests en beschikbaarheidstests?*

    Hallo mag twee termen worden verwezen door elkaar. Beschikbaarheidstests is een algemene term die uit één URL-ping Hallo Test bovendien toohello meerdere stappen webtests.
* *Ik graag beschikbaarheidstests toouse voor onze interne server die wordt uitgevoerd achter een firewall.*

    Er zijn twee mogelijke oplossingen:
    
    * Configureer uw firewall toopermit van binnenkomende aanvragen van Hallo [IP-adressen van onze webservices testen agents](app-insights-ip-addresses.md).
    * Schrijf uw eigen code tooperiodically test uw interne serverfout. Hallo-code als een achtergrondproces uitvoeren op een testserver achter de firewall. Uw testproces voor de kunt sturen de resultaten tooApplication Insights via [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API in Hallo core SDK-pakket. Hiervoor moet uw test toohave uitgaande toegang toohello Application Insights opname servereindpunt, maar dat is een veel kleinere beveiligingsrisico dan Hallo alternatieve van inkomende aanvragen toe te staan. Hallo resultaten worden niet weergegeven in Hallo beschikbaarheid web tests blades, maar wordt weergegeven als de resultaten van de beschikbaarheid in Analytics, zoeken en metriek Explorer.
* *Het uploaden van een webtest met meerdere stappen mislukt*

    Er is een limiet van 300 K.

    Lussen worden niet ondersteund.

    Verwijzingen tooother webtests worden niet ondersteund.

    Gegevensbronnen worden niet ondersteund.
* *Mijn test met meerdere stappen wordt niet voltooid*

    Er is een limiet van 100 aanvragen per test.

    Hallo-test wordt gestopt als deze wordt meer dan twee minuten uitgevoerd.
* *Hoe voer ik een test uit met clientcertificaten?*

    Dat wordt niet ondersteund.


## <a name="next"></a>Volgende stappen
[Diagnostische logboeken doorzoeken][diagnostic]

[Problemen oplossen][qna]

[IP-adressen van webtest-agents](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
