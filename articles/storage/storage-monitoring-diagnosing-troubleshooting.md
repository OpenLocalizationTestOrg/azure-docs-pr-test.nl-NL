---
title: aaaMonitor, opsporen en oplossen van Azure Storage | Microsoft Docs
description: Gebruik functies zoals storage analytics, clientzijde aan te melden, en andere tooidentify hulpprogramma's van derden diagnosticeren en oplossen van problemen met Azure Storage met.
services: storage
documentationcenter: 
author: fhryo-msft
manager: jahogg
editor: tysonn
ms.assetid: d1e87d98-c763-4caa-ba20-2cf85f853303
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: fhryo-msft
ms.openlocfilehash: a33b3af7527223169be7cf3fed76c4765ff80e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-diagnose-and-troubleshoot-microsoft-azure-storage"></a>Microsoft Azure Storage bewaken, problemen opsporen en oplossen
[!INCLUDE [storage-selector-portal-monitoring-diagnosing-troubleshooting](../../includes/storage-selector-portal-monitoring-diagnosing-troubleshooting.md)]

## <a name="overview"></a>Overzicht
Diagnose van en het oplossen van problemen in een gedistribueerde toepassing die wordt gehost in een cloudomgeving kunnen worden complexer dan in traditionele omgevingen. Toepassingen kunnen worden geïmplementeerd in een PaaS of IaaS-infrastructuur on-premises, op een mobiel apparaat of in een combinatie hiervan. Normaal gesproken netwerkverkeer van uw toepassing lopen mogelijk langs openbare en particuliere netwerken en toepassingen kan gebruikmaken van meerdere opslagtechnologieën zoals Microsoft Azure Storage-tabellen, Blobs, wachtrijen of bestanden in de toevoeging tooother gegevens worden opgeslagen zoals als relationele en documenteren van databases.

toomanage dergelijke toepassingen met succes u moet deze proactief controleren en inzicht in hoe toodiagnose en alle aspecten van hun afhankelijke technologieën en ze problemen oplossen. Als een gebruiker van Azure Storage-services, u moet continu Hallo opslagservices uw toepassing wordt gebruikt voor eventuele onverwachte wijzigingen in gedrag (zoals langzamer dan gebruikelijk reactietijden) bewaken en logboekregistratie toocollect gebruik meer gedetailleerde gegevens en tooanalyze een probleem in de diepte. Hallo diagnostische gegevens die u van controle en logboekregistratie verkrijgen kunt u toodetermine Hallo hoofdoorzaak Hallo uitgeven van uw toepassing aangetroffen. Vervolgens kunt u Hallo probleem op te lossen en Hallo passende stappen kunt tooremediate bepalen het. Azure Storage is een kern Azure-service en vormt een belangrijk onderdeel van de meeste Hallo-oplossingen klanten toohello Azure-infrastructuur te implementeren. Azure Storage bevat mogelijkheden toosimplify bewaking, onderzoeken en het oplossen van opslagproblemen in uw cloud-gebaseerde toepassingen.

> [!NOTE]
> Hello Azure File storage biedt geen ondersteuning voor logboekregistratie op dit moment.
> 

Zie voor een praktische gids tooend-to-end het oplossen van problemen in toepassingen met Azure Storage, [End-to-End problemen oplossen met metrische gegevens van Azure Storage en logboekregistratie, AzCopy en Message Analyzer](storage-e2e-troubleshooting.md).

* [Inleiding]
  * [Rangschikking van deze handleiding]
* [bewaking van uw opslagservice]
  * [Bewaking servicestatus]
  * [Bewaking van capaciteit]
  * [Controleprogramma beschikbaarheid]
  * [Prestaties bewaken]
* [diagnose van opslagproblemen]
  * [Health service-problemen]
  * [Prestatieproblemen]
  * [Fouten opsporen]
  * [Emulator opslagproblemen]
  * [Logboekregistratieprogramma's voor opslag]
  * [Met behulp van hulpprogramma's voor logboekregistratie]
* [End-to-end tracering]
  * [Logboekgegevens correleren]
  * [Aanvraag-ID van client]
  * [Server aanvraag-ID]
  * [Tijdstempels]
* [richtlijnen voor probleemoplossing]
  * [metrische gegevens tonen AverageE2ELatency hoge en lage AverageServerLatency]
  * [Metrische gegevens tonen lage AverageE2ELatency en lage AverageServerLatency maar Hallo client ondervindt hoge latentie]
  * [Prestatiegegevens geven hoge AverageServerLatency aan]
  * [U ervaart onverwachte vertragingen bij de levering van berichten in een wachtrij]
  * [metrische gegevens tonen een toename in PercentThrottlingError]
  * [metrische gegevens tonen een toename in PercentTimeoutError]
  * [Prestatiegegevens geven een toename in PercentNetworkError aan]
  * [Hallo client ontvangt berichten HTTP 403 (verboden)]
  * [Hallo-client is ontvangen HTTP 404 (niet gevonden)-berichten]
  * [Hallo client ontvangt berichten van de HTTP-409 (Conflict)]
  * [metrische gegevens tonen lage PercentSuccess of analytics logboekvermeldingen bewerkingen hebben met transactiestatus ClientOtherErrors]
  * [Capaciteit metrische gegevens tonen een onverwachte toename in opslaggebruik capaciteit]
  * [Er is sprake van virtuele Machines met een groot aantal gekoppelde VHD's onverwacht opnieuw wordt opgestart]
  * [Het probleem zich voordoet Hallo-opslagemulator gebruiken voor ontwikkeling of tests]
  * [U ondervindt problemen met het installeren van hello Azure SDK voor .NET]
  * [U hebt een ander probleem met storage-service]
  * [Problemen met Azure File storage oplossen met Windows en Linux](storage-troubleshoot-file-connection-problems.md)
* [bijlagen]
  * [bijlage 1: met behulp van HTTP en HTTPS-verkeer van toocapture Fiddler]
  * [bijlage 2: Wireshark toocapture netwerkverkeer met]
  * [bijlage 3: met behulp van Microsoft Message Analyzer toocapture netwerkverkeer]
  * [Bijlage 4: Tooview Excel-gegevens metrische gegevens en logboekbestanden gebruiken]
  * [Bijlage 5: Bewaking met Application Insights voor Visual Studio teamservices]

## <a name="introduction"></a>Inleiding
Problemen met betrekking tot deze handleiding ziet u hoe toouse functies zoals Azure Storage Analytics, client-side '-logboekregistratie in hello Azure Storage-clientbibliotheek en andere hulpprogramma's van derden-tooidentify vaststellen en oplossen van Azure Storage.

![][1]

Deze handleiding is bedoeld toobe lezen voornamelijk door ontwikkelaars van online services die gebruikmaken van Azure Storage-Services en IT-professionals die verantwoordelijk is voor het beheren van dergelijke online services. Hallo doelstellingen van deze handleiding zijn:

* toohelp hello status en prestaties van uw Azure Storage-accounts te behouden.
* tooprovide u met de Hallo nodig processen en hulpprogramma's voor toohelp u besluit als een probleem of een probleem in een toepassing is gekoppeld tooAzure opslag.
* tooprovide u met bruikbare richtlijnen voor het oplossen van problemen tooAzure opslag gekoppeld.

### <a name="how-this-guide-is-organized"></a>Rangschikking van deze handleiding
sectie Hallo '[bewaking van uw opslagservice]' wordt beschreven hoe toomonitor Hallo status en prestaties van uw Azure Storage-services met Azure Storage Analytics metrische gegevens (metrische gegevens Storage).

sectie Hallo '[diagnose van opslagproblemen]' wordt beschreven hoe toodiagnose problemen met behulp van Azure Storage Analytics Logging (logboekregistratie van opslag). Ook wordt beschreven hoe tooenable met behulp van logboekregistratie voor client-side ' hello faciliteiten in een van de clientbibliotheken Hallo zoals Hallo Storage-clientbibliotheek voor .NET of hello Azure SDK voor Java.

sectie Hallo '[End-to-end tracering]' wordt beschreven hoe correleren van Hallo gegevens in de verschillende logboekbestanden en metrische gegevens.

sectie Hallo '[richtlijnen voor probleemoplossing]' bevat richtlijnen voor probleemoplossing voor een aantal Hallo algemene opslag problemen kunnen optreden.

Hallo '[bijlagen]' bevatten informatie over het gebruik van andere hulpprogramma's zoals Wireshark en Netmon voor analyse van netwerk-pakketgegevens, Fiddler voor het analyseren van HTTP/HTTPS-berichten en Microsoft Message Analyzer voor het correleren van gegevens vastleggen.

## <a name="monitoring-your-storage-service"></a>Bewaking van uw storage-service
Als u bekend zijn met Windows performance monitoring bent, kunt u metrische gegevens Storage zien als wordt een Azure Storage-equivalent van de Prestatiemeter van Windows. In de opslag metrische gegevens vindt u een uitgebreide set met metrische gegevens (items in Prestatiemeter van Windows-terminologie) zoals beschikbaarheid van de service, het totale aantal aanvragen tooservice of percentage van geslaagde aanvragen tooservice. Zie voor een volledige lijst van beschikbare metrische gegevens Hallo [Storage Analytics metrische gegevens tabelschema](http://msdn.microsoft.com/library/azure/hh343264.aspx). U kunt opgeven of u wilt dat Hallo opslag service toocollect en cumulatieve metrische gegevens elk uur of elke minuut. Voor meer informatie over hoe tooenable metrische gegevens en monitor uw storage-accounts, Zie [metrische gegevens storage inschakelen en weergeven van metrische gegevens](http://go.microsoft.com/fwlink/?LinkId=510865).

U kunt kiezen welke per uur metrische gegevens gewenste toodisplay in Hallo [Azure-portal](https://portal.azure.com) en regels configureren waarmee beheerders per e-mail wordt gewaarschuwd wanneer een per uur metrische gegevens een bepaalde drempelwaarde overschrijdt. Zie voor meer informatie [waarschuwingsmeldingen ontvangen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). 

Hallo storage-service met een zo goed mogelijke poging metrische gegevens verzamelt, maar kunt elke opslagbewerking niet registreren.

In hello Azure-portal, kunt u metrische gegevens zoals beschikbaarheid, totaal aantal aanvragen en gemiddelde latentie cijfers voor een opslagaccount weergeven. Een meldingsregel is ook ingesteld tooalert beheerder als beschikbaarheid onder een bepaalde mate zakt. Van deze gegevens weer te geven, een mogelijke gebied voor onderzoek Hallo tabel service Verwerkingsfrequentie wordt dan 100% is (Zie Hallo sectie voor meer informatie '[metrische gegevens tonen lage PercentSuccess of analytics logboekvermeldingen bewerkingen hebben met transactiestatus ClientOtherErrors]').

Uw Azure-toepassingen tooensure ze zijn in orde en zoals verwacht door het uitvoeren, moet u continu controleren:

* Tot stand brengen van sommige basislijn metrische gegevens voor de toepassing die wordt kunt u gegevens van de huidige toocompare en belangrijke wijzigingen in gedrag van Azure storage en uw toepassing hello identificeren. Hallo-waarden van de metrische gegevens van uw basislijn, in veel gevallen worden specifieke toepassing en moet u deze instellen wanneer u de prestaties van uw toepassing testen bent.
* Opname minuut metrische gegevens en het gebruik ervan toomonitor actief voor onverwachte fouten en afwijkingen zoals pieken in fout tellingen of aanvraag tarieven.
* Per uur metrische gegevens opnemen en gebruik ze zoals gemiddelde waarden toomonitor gemiddelde aantallen van de fout en tarieven aanvragen.
* Onderzoeken van mogelijke problemen met diagnostische hulpprogramma's zoals verderop in de sectie Hallo '[diagnose van opslagproblemen]. "

Hallo grafieken in Hallo volgende afbeelding ziet u hoe Hallo gemiddelde die voor de per uur metrische gegevens optreedt kunt verbergen pieken in de activiteit. Hallo per uur metrische gegevens weergegeven tooshow een constante snelheid van aanvragen, tijdens het Hallo minuut metrieken onthullen Hallo schommelingen die echt plaatsvinden.

![][3]

Hallo rest van deze sectie wordt beschreven welke metrische gegevens, moet u controleren en waarom.

### <a name="monitoring-service-health"></a>Bewaking servicestatus
U kunt Hallo [Azure-portal](https://portal.azure.com) tooview Hallo status van Hallo Storage-service (en andere Azure-services) in alle Azure-regio's Hallo wereld Hallo. Hiermee kunt u toosee onmiddellijk als een probleem buiten uw invloedssfeer invloed op Hallo opslagservice in Hallo regio die u voor uw toepassing gebruiken.

Hallo [Azure-portal](https://portal.azure.com) biedt ook meldingen van incidenten die invloed hebben op Hallo verschillende Azure-services.
Opmerking: Deze informatie is eerder beschikbaar is, samen met de historische gegevens, op Hallo [servicedashboard Azure](http://status.azure.com).

Tijdens het Hallo [Azure-portal](https://portal.azure.com) verzamelt informatie uit binnen Hallo Azure-datacenters (binnen-out bewaking), u kunt ook een benadering van buitenaf toogenerate synthetische transacties dat periodiek overstap toegang tot uw Azure gehoste webtoepassing vanaf meerdere locaties. services die worden aangeboden door Hallo [Dynatrace](http://www.dynatrace.com/en/synthetic-monitoring) en Application Insights for Visual Studio Team Services zijn voorbeelden van deze benadering buiten in. Zie voor meer informatie over Application Insights voor Visual Studio Team Services, bijlage Hallo '[bijlage 5: bewaking met Application Insights for Visual Studio teamservices](#appendix-5). "

### <a name="monitoring-capacity"></a>Bewaking van capaciteit
Metrische gegevens Storage alleen capaciteitsmetrieken voor Hallo blob-service worden opgeslagen omdat blobs doorgaans rekening voor Hallo grootste gedeelte van de opgeslagen gegevens (Hallo schrijven, het is momenteel niet mogelijk toouse metrische gegevens Storage toomonitor Hallo capaciteit van de tabellen en wachtrijen) . U vindt deze gegevens in Hallo **$MetricsCapacityBlob** tabel als u bewaking voor Hallo Blob-service hebt ingeschakeld. Metrische gegevens Storage registreert deze gegevens eenmaal per dag en kunt u Hallo-waarde van Hallo **RowKey** toodetermine of Hallo rij bevat voor een entiteit die is gekoppeld toouser gegevens (waarde **gegevens**) of analytics gegevens ( waarde **analytics**). Elke entiteit opgeslagen bevat informatie over Hallo hoeveelheid gebruikte ruimte (**capaciteit** gemeten in bytes) en het huidige aantal containers hello (**ContainerCount**) en -blobs ( **ObjectCount**) in Hallo storage-account wordt gebruikt. Voor meer informatie over Hallo capaciteitsmetrieken opgeslagen in Hallo **$MetricsCapacityBlob** tabel, Zie [Storage Analytics metrische gegevens tabelschema](http://msdn.microsoft.com/library/azure/hh343264.aspx).

> [!NOTE]
> Deze waarden voor een vroegtijdige waarschuwing dat u beperkingen van de capaciteit van uw opslagaccount Hallo nadert, moet u controleren. In hello Azure-portal, kunt u regels voor waarschuwingen toonotify u als cumulatieve opslaggebruik overschrijdt of onder de drempels die u valt opgeeft toevoegen.
> 
> 

Zie voor informatie over het schatten van de grootte van verschillende opslagobjecten zoals blobs Hallo Hallo blogbericht [wat Azure Storage facturering – bandbreedte, transacties en capaciteit](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx).

### <a name="monitoring-availability"></a>Controleprogramma beschikbaarheid
Hallo beschikbaarheid van de opslagservices Hallo moet u controleren in uw opslagaccount door de bewaking van Hallo-waarde in Hallo **beschikbaarheid** kolom in per uur of minuut metrieken tabellen Hallo: **$ MetricsHourPrimaryTransactionsBlob**, **$MetricsHourPrimaryTransactionsTable**, **$MetricsHourPrimaryTransactionsQueue**, **$ MetricsMinutePrimaryTransactionsBlob**, **$MetricsMinutePrimaryTransactionsTable**, **$MetricsMinutePrimaryTransactionsQueue**, **$ MetricsCapacityBlob**. Hallo **beschikbaarheid** kolom bevat een percentagewaarde die Hallo beschikbaarheid van Hallo service of Hallo API-bewerking dat wordt vertegenwoordigd door Hallo rij aangeeft (Hallo **RowKey** toont als Hallo rij bevat. metrische gegevens voor de service Hallo als geheel of voor het uitvoeren van een specifieke API).

Een waarde op die kleiner is dan 100% Hiermee wordt aangegeven dat bepaalde opslag-aanvragen mislukken. U kunt zien waarom ze zijn mislukt door in andere kolommen in Hallo metrische gegevens die Hallo getallen aanvragen met verschillende fouttypen zoals weergeven Hallo **ServerTimeoutError**. U kunt verwachten toosee **beschikbaarheid** vallen tijdelijk dan 100% om redenen als tijdelijke servertime terwijl Hallo service partities toobetter verdelen aanvraag verplaatst; Hallo Pogingslogica in uw clienttoepassing Deze voorwaarden onregelmatige moet kunnen verwerken. Hallo artikel [Storage Analytics geregistreerde bewerkingen en statusberichten](http://msdn.microsoft.com/library/azure/hh343260.aspx) lijsten Hallo transactietypen die metrische gegevens Storage bevat in de **beschikbaarheid** berekening.

In Hallo [Azure-portal](https://portal.azure.com), kunt u regels voor waarschuwingen toonotify toevoegen u als **beschikbaarheid** voor een service valt onder de drempelwaarde die u opgeeft.

Hallo '[richtlijnen voor probleemoplossing]' van deze handleiding beschrijft een aantal algemene opslag service problemen gerelateerde tooavailability.

### <a name="monitoring-performance"></a>Prestaties bewaken
toomonitor hello prestaties van de opslagservices hello, kunt u Hallo per uur na het metrische gegevens uit Hallo en metrische gegevens tabellen minuut.

* waarden in Hallo Hallo **AverageE2ELatency** en **AverageServerLatency** kolommen Hallo gemiddelde tijd Hallo storage-service weergeven of type API-bewerking duurt tooprocess aanvragen. **AverageE2ELatency** is een meting van end-to-end-latentie met Hallo tijd tooread Hallo aanvraag en antwoord Hallo in toevoeging toohello tijd tooprocess Hallo aanvraag verzenden (dus inclusief netwerklatentie zodra Hallo aanvragen Hallo opslagservice bereikt;) **AverageServerLatency** is een meting NET Hallo verwerkingstijd en daarom sluit eventuele gerelateerde netwerklatentie toocommunicating met Hallo-client. Zie de sectie Hallo '[metrische gegevens tonen AverageE2ELatency hoge en lage AverageServerLatency]' verderop in deze handleiding voor een beschrijving van waarom er mogelijk een aanzienlijk verschil tussen deze twee waarden.
* waarden in Hallo Hallo **TotalIngress** en **TotalEgress** kolommen weergeven Hallo totale hoeveelheid gegevens, in bytes binnenkort in tooand gaat buiten uw storage-service of via een specifiek type van de API-bewerking.
* waarden in Hallo Hallo **TotalRequests** ontvangen van de kolom weergeven Hallo totaal aantal aanvragen dat Hallo opslagservice van API-bewerking. **TotalRequests** is Hallo totaal aantal aanvragen dat Hallo storage-service ontvangt.

Normaal gesproken bewaakt u onverwachte wijzigingen in een van deze waarden als een indicatie dat er een probleem waarvoor onderzoek vereist.

In Hallo [Azure-portal](https://portal.azure.com), kunt u toevoegen waarschuwingsregels toonotify u eventuele Hallo maatstaven voor prestaties voor deze service onder vallen of een groter zijn dan een drempel die u opgeeft.

Hallo '[richtlijnen voor probleemoplossing]' van deze handleiding beschrijft een aantal algemene opslag service problemen gerelateerde tooperformance.

## <a name="diagnosing-storage-issues"></a>Diagnose van opslagproblemen
Er zijn een aantal manieren dat u mogelijk op de hoogte van een probleem of een probleem in uw toepassing, deze omvatten:

* Een ernstige fout die ervoor zorgt Hallo toepassing toocrash of toostop werken dat.
* Belangrijke wijzigingen van basislijnwaarden in Hallo metrische gegevens die u controleren wilt, zoals beschreven in de vorige sectie Hallo '[bewaking van uw opslagservice]. "
* Rapporten van gebruikers van uw toepassing die een bepaalde bewerking niet voltooid zoals verwacht of dat bepaalde functie niet werkt.
* Fouten die zijn gegenereerd binnen de toepassing die worden weergegeven in logboekbestanden of via een andere meldingsmethode.

Normaal gesproken problemen gerelateerde tooAzure storage-services worden onderverdeeld in een van de vier hoofdcategorieën:

* Uw toepassing heeft een prestatieprobleem gerapporteerd door uw gebruikers of door wijzigingen in maatstaven voor prestaties Hallo getoond.
* Er is een probleem met hello Azure Storage-infrastructuur in een of meer regio's.
* Uw toepassing wordt uitgevoerd als een fout gerapporteerd door uw gebruikers of door een toename in een Hallo fout aantal metrische gegevens die u bewaken getoond.
* Tijdens de ontwikkeling en tests u mogelijk gebruikmaken van de emulator van de lokale opslag Hallo; Sommige problemen die gerelateerd zijn specifiek toousage van Hallo opslagemulator kunnen optreden.

Hallo volgende secties worden Hallo stappen u moet toodiagnose volgen en oplossen van problemen in elk van de volgende vier categorieën. sectie Hallo '[richtlijnen voor probleemoplossing]' verderop in deze handleiding biedt meer details voor enkele veelvoorkomende problemen kunnen optreden.

### <a name="service-health-issues"></a>Health service-problemen
Problemen met de status van de service zijn meestal buiten het besturingselement. Hallo [Azure-portal](https://portal.azure.com) bevat informatie over actieve problemen met Azure-services met inbegrip van opslagservices. Als u hebt gekozen voor geografisch redundante opslag met leestoegang wanneer u uw opslagaccount hebt gemaakt, kan klikt u vervolgens in Hallo-gebeurtenis van uw gegevens tijdelijk niet beschikbaar zijn op de primaire locatie hello, uw toepassing overschakelen tijdelijk toohello alleen-lezen kopie op de secundaire locatie Hallo. toodo dit door uw toepassing moet kunnen tooswitch tussen het gebruik van de primaire en secundaire opslaglocaties Hallo en kunnen toowork in een modus met verminderde functionaliteit met alleen-lezen gegevens. Hello Azure Storage-clientbibliotheken kunnen u een beleid voor opnieuw proberen dat uit de secundaire opslag lezen kan als van de primaire opslag gelezen mislukt toodefine. Uw toepassing moet ook toobe Houd er rekening mee dat de gegevens op de secundaire locatie Hallo Hallo uiteindelijk consistent is. Zie voor meer informatie Hallo blogbericht [opslagopties van Azure voor redundantie en geografisch redundante opslag met leestoegang](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

### <a name="performance-issues"></a>Prestatieproblemen
prestaties van een toepassing Hello kan subjectieve, met name vanuit het perspectief van een gebruiker zijn. Het is daarom belangrijk toohave basislijn metrische gegevens beschikbaar toohelp u identificeren waar mogelijk een prestatieprobleem. Veel factoren mogelijk Hallo prestaties van een Azure storage-service van de toepassing clientperspectief Hallo beïnvloeden. Deze factoren kunnen werken in opslagservice hello, Hallo-client of Hallo-netwerkinfrastructuur. het is daarom belangrijk toohave een strategie voor het identificeren van de oorsprong van het prestatieprobleem Hallo Hallo.

Nadat u waarschijnlijk locatie Hallo Hallo oorzaak van het prestatieprobleem Hallo van Hallo metrische gegevens hebt geïdentificeerd, kunt u vervolgens gebruik Hallo logboek bestanden toofind gedetailleerde informatie toodiagnose en Hallo probleem verder oplossen.

sectie Hallo '[richtlijnen voor probleemoplossing]' verderop in deze handleiding biedt meer informatie over algemene prestaties gerelateerd problemen die u kunt tegenkomen.

### <a name="diagnosing-errors"></a>Fouten opsporen
Gebruikers van uw toepassing kunnen melding van fouten die zijn gerapporteerd door de clienttoepassing Hallo. Metrische gegevens Storage registreert ook de aantallen voor verschillende fouttypen van uw storage-services zoals **NetworkError**, **ClientTimeoutError**, of **AuthorizationError**. Terwijl de opslag metrische gegevens worden alleen tellingen van verschillende fouttypen registreert, kunt u meer informatie over afzonderlijke aanvragen door te onderzoeken serverzijde en clientzijde netwerk Logboeken. Hallo HTTP-statuscode geretourneerd door Hallo storage-service krijgt doorgaans een indicatie van waarom Hallo-aanvraag is mislukt.

> [!NOTE]
> Houd er rekening mee dat u kunt toosee onregelmatige fouten verwachten: bijvoorbeeld fouten vanwege tootransient netwerkomstandigheden of toepassingsfouten.
> 
> 

Hallo zijn volgende resources nuttig voor opslag-gerelateerde status en foutcodes begrijpen:

* [Algemene REST API-foutcodes](http://msdn.microsoft.com/library/azure/dd179357.aspx)
* [Foutcodes voor BLOB-Service](http://msdn.microsoft.com/library/azure/dd179439.aspx)
* [Foutcodes voor wachtrij](http://msdn.microsoft.com/library/azure/dd179446.aspx)
* [Foutcodes voor tabel-Service](http://msdn.microsoft.com/library/azure/dd179438.aspx)
* [Foutcodes voor bestand](https://msdn.microsoft.com/library/azure/dn690119.aspx)

### <a name="storage-emulator-issues"></a>Emulator opslagproblemen
Hello Azure SDK bevat een opslagemulator die u op een werkstation ontwikkeling uitvoeren kunt. Deze emulator simuleert meeste Hallo gedrag van hello Azure storage-services en is handig als u tijdens de ontwikkeling en tests, zodat u toorun toepassingen die gebruikmaken van Azure storage-services zonder Hallo nodig hebt voor een Azure-abonnement en Azure storage-account.

Hallo '[richtlijnen voor probleemoplossing]' van deze handleiding beschrijft enkele veelvoorkomende problemen aangetroffen met Hallo-opslagemulator.

### <a name="storage-logging-tools"></a>Logboekregistratieprogramma's voor opslag
Logboekregistratie van opslag biedt serverzijde registratie van aanvragen van de opslag in uw Azure storage-account. Zie voor meer informatie over hoe tooenable serverzijde logboekregistratie en toegang Hallo gegevens vastleggen, [opslag vastleggen inschakelen en toegang tot logboekgegevens](http://go.microsoft.com/fwlink/?LinkId=510867).

Hallo Storage-clientbibliotheek voor .NET kunt u toocollect clientzijde logboekgegevens die is gekoppeld toostorage bewerkingen wordt uitgevoerd door uw toepassing. Zie voor meer informatie [clientzijde logboekregistratie Hello Storage-clientbibliotheek voor .NET](http://go.microsoft.com/fwlink/?LinkId=510868).

> [!NOTE]
> In sommige gevallen (zoals SAS autorisatiefouten), kan een gebruiker waarvoor u er zijn geen aanvraaggegevens in Hallo serverzijde opslag Logboeken vindt fout gemeld. U kunt Hallo mogelijkheden voor logboekregistratie van Hallo Storage-clientbibliotheek tooinvestigate gebruiken als Hallo oorzaak van het probleem Hallo op Hallo-client of -hulpprogramma's voor tooinvestigate Hallo netwerk netwerkbewaking gebruiken.
> 
> 

### <a name="using-network-logging-tools"></a>Met behulp van hulpprogramma's voor logboekregistratie
U kunt vastleggen Hallo-verkeer tussen Hallo-client en server tooprovide gedetailleerde informatie over Hallo gegevens Hallo client en server zijn uitwisselen en Hallo onderliggende netwerkomstandigheden. Nuttige hulpprogramma's voor logboekregistratie omvatten:

* [Fiddler](http://www.telerik.com/fiddler) is een gratis web proxy waarmee u tooexamine Hallo headers en gegevens over de nettolading van HTTP en HTTPS-aanvraag en antwoord berichten foutopsporing. Zie voor meer informatie [bijlage 1: met behulp van Fiddler toocapture HTTP en HTTPS-verkeer](#appendix-1).
* [Microsoft Network Monitor (Netmon)](http://www.microsoft.com/download/details.aspx?id=4865) en [Wireshark](http://www.wireshark.org/) zijn gratis netwerk protocol analyzers waarmee u tooview gedetailleerde informatie voor een breed scala aan netwerkprotocollen pakket. Zie voor meer informatie over Wireshark '[bijlage 2: met behulp van Wireshark toocapture netwerkverkeer](#appendix-2)'.
* Microsoft Message Analyzer is een hulpprogramma van Microsoft die vervangt Netmon en die bovendien toocapturing netwerk pakketgegevens, kunt u tooview en analyseren van Hallo logboekgegevens vastgelegd vanaf andere hulpprogramma's. Zie voor meer informatie '[bijlage 3: met behulp van Microsoft Message Analyzer toocapture netwerkverkeer](#appendix-3)'.
* Als u tooperform een basisconnectiviteit test toocheck wilt dat de clientcomputer toohello Azure storage-service via Hallo netwerk verbinding kan maken, dit is niet met behulp van standaard Hallo **ping** hulpprogramma op Hallo-client. U kunt echter hello gebruiken [ **tcping** hulpprogramma](http://www.elifulkerson.com/projects/tcping.php) toocheck connectiviteit.

In veel gevallen Hallo logboekgegevens van registratie van opslag en Hallo Storage-clientbibliotheek is voldoende toodiagnose een probleem, maar in sommige scenario's, moet u mogelijk Hallo die meer gedetailleerde informatie die deze hulpprogramma's voor network logboekregistratie kunnen bieden. Bijvoorbeeld met behulp van Fiddler tooview HTTP en HTTPS-berichten kunt u tooview header en -nettolading gegevens afkomstig tooand Hallo opslagservices, waardoor u tooexamine hoe een clienttoepassing probeert opnieuw opslagbewerkingen. Protocol analyzers zoals Wireshark werken op pakketniveau Hallo zodat u tooview TCP-gegevens, waarmee u tootroubleshoot verloren pakketten en verbindingsproblemen. Berichtanalyse kan werken op HTTP- en TCP-lagen.

## <a name="end-to-end-tracing"></a>End-to-end-tracering
End-to-end-tracering met een aantal logboekbestanden is een techniek nuttig voor het onderzoeken van mogelijke problemen. U kunt Hallo datum/tijd informatie van de metrische gegevens gebruiken als een indicatie van waar toostart bekijkt hello logboekbestanden voor Hallo gedetailleerde informatie waarmee u Hallo probleem op te lossen.

### <a name="correlating-log-data"></a>Logboekgegevens correleren
Tijdens het weergeven van Logboeken van clienttoepassingen netwerk traceert en serverzijde opslag logboekregistratie het kritieke toobe kunnen toocorrelate aanvragen over de verschillende logboekbestanden Hallo is. Hallo-logboekbestanden bevatten een aantal verschillende velden die handig als de correlatie-id's zijn. Hallo client aanvraag-id is Hallo nuttigst veld toouse toocorrelate vermeldingen in verschillende Hallo-Logboeken. Maar in sommige gevallen, het kan ook nuttig toouse Hallo server aanvraag-id of tijdstempels. Hallo bevatten volgende secties meer informatie over deze opties.

### <a name="client-request-id"></a>Aanvraag-ID van client
Hallo Storage-clientbibliotheek genereert automatisch een unieke client aanvraag-id voor elke aanvraag.

* In Hallo client-side '-log dat Hallo Storage-clientbibliotheek maakt, Hallo client aanvraag-id wordt weergegeven in Hallo **aanvraag-ID van Client** veld van elke logboekvermelding betreffende toohello aanvraag.
* In een netwerktracering zoals een vastgelegd door Fiddler Hallo client aanvraag-id is zichtbaar in aanvraagberichten als Hallo **x-ms-client-request-id** waarde van de HTTP-header.
* In Hallo serverzijde opslag logboekregistratie logboek weergegeven Hallo client aanvraag-id in kolom-ID Hallo Client-aanvraag.

> [!NOTE]
> Het is mogelijk voor meerdere aanvragen tooshare Hallo dezelfde aanvraag-id van client omdat Hallo-client kan deze waarde toewijzen (Hoewel Hallo Storage-clientbibliotheek wijst automatisch een nieuwe waarde). In geval van nieuwe pogingen van client Hallo Hallo alle pogingen Hallo delen dezelfde client aanvraag-id. In geval van een batch verzonden vanaf de client Hallo Hallo heeft Hallo batch een aanvraag-id van één client.
> 
> 

### <a name="server-request-id"></a>Aanvraag-ID van server
Hallo storage-service wordt automatisch gegenereerd server aanvraag-id's.

* In Hallo serverzijde opslag logboekregistratie logboek Hallo server aanvraag-id weergegeven Hallo **aanvraag-ID header** kolom.
* In een netwerktracering zoals een vastgelegd door Fiddler Hallo server aanvraag-id wordt weergegeven in antwoordberichten als Hallo **x-ms-aanvraag-id** waarde van de HTTP-header.
* In Hallo client-side '-log dat Hallo Storage-clientbibliotheek maakt, Hallo server aanvraag-id wordt weergegeven in Hallo **bewerking tekst** kolom voor Hallo logboekvermelding details van de serverreactie hello wordt weergegeven.

> [!NOTE]
> Hallo opslagservice altijd toegewezen een unieke server aanvraag-id tooevery aanvraag die wordt ontvangen, zodat elke nieuwe poging van de client hello en elke bewerking die is opgenomen in een batch een unieke server aanvraag-id heeft.
> 
> 

Als hello Storage-clientbibliotheek genereert een **StorageException** Hallo Hallo-client **RequestInformation** eigenschap bevat een **RequestResult** -object met een **ServiceRequestID** eigenschap. U kunt ook toegang tot een **RequestResult** object uit een **OperationContext** exemplaar.

Hallo voorbeeldcode laat zien hoe een aangepaste tooset **ClientRequestId** waarde door het koppelen van een **OperationContext** object Hallo aanvraag toohello storage-service. U ziet ook hoe tooretrieve hello **ServerRequestId** waarde uit het antwoord Hallo-bericht.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Create an Operation Context that includes custom ClientRequestId string based on constants defined within hello application along with a Guid.
OperationContext oc = new OperationContext();
oc.ClientRequestID = String.Format("{0} {1} {2} {3}", HOSTNAME, APPNAME, USERID, Guid.NewGuid().ToString());

try
{
    CloudBlobContainer container = blobClient.GetContainerReference("democontainer");
    ICloudBlob blob = container.GetBlobReferenceFromServer("testImage.jpg", null, null, oc);  
    var downloadToPath = string.Format("./{0}", blob.Name);
    using (var fs = File.OpenWrite(downloadToPath))
    {
        blob.DownloadToStream(fs, null, null, oc);
        Console.WriteLine("\t Blob downloaded toofile: {0}", downloadToPath);
    }
}
catch (StorageException storageException)
{
    Console.WriteLine("Storage exception {0} occurred", storageException.Message);
    // Multiple results may exist due tooclient side retry logic - each retried operation will have a unique ServiceRequestId
    foreach (var result in oc.RequestResults)
    {
            Console.WriteLine("HttpStatus: {0}, ServiceRequestId {1}", result.HttpStatusCode, result.ServiceRequestID);
    }
}
```

### <a name="timestamps"></a>Tijdstempels
U kunt ook de tijdstempels toolocate logboekvermeldingen gerelateerd, maar wees voorzichtig met eventuele tijdsverschil tussen Hallo-client en server die zich kan voordoen. Plus of min 15 minuten voor de overeenkomende serverzijde vermeldingen op basis van Hallo tijdstempel op Hallo-client moet worden gezocht. Houd er rekening mee dat Hallo blob-metagegevens voor Hallo blobs met metrische gegevens Hallo tijdsbereik voor Hallo metrische gegevens die zijn opgeslagen in blob Hallo; geeft aan Dit is handig als er veel metrische gegevens blobs voor Hallo dezelfde minuut of uur.

## <a name="troubleshooting-guidance"></a>Richtlijnen voor probleemoplossing
Deze sectie helpt u met de Hallo diagnose en het oplossen van enkele veelvoorkomende problemen Hallo van uw toepassing kan optreden wanneer u hello Azure storage-services. Gebruik de lijst Hallo hieronder toolocate Hallo informatie relevante tooyour specifiek probleem.

**Het oplossen van de beslissingsstructuur**

---
Uw probleem toohello prestaties van een van de opslagservices Hallo relateren?

* [metrische gegevens tonen AverageE2ELatency hoge en lage AverageServerLatency]
* [Metrische gegevens tonen lage AverageE2ELatency en lage AverageServerLatency maar Hallo client ondervindt hoge latentie]
* [Prestatiegegevens geven hoge AverageServerLatency aan]
* [U ervaart onverwachte vertragingen bij de levering van berichten in een wachtrij]

---
Uw probleem toohello beschikbaarheid van een van de opslagservices Hallo relateren?

* [metrische gegevens tonen een toename in PercentThrottlingError]
* [metrische gegevens tonen een toename in PercentTimeoutError]
* [Prestatiegegevens geven een toename in PercentNetworkError aan]

---
 De clienttoepassing ontvangt een HTTP-4XX (zoals 404) antwoord van een storage-service?

* [Hallo client ontvangt berichten HTTP 403 (verboden)]
* [Hallo-client is ontvangen HTTP 404 (niet gevonden)-berichten]
* [Hallo client ontvangt berichten van de HTTP-409 (Conflict)]

---
[metrische gegevens tonen lage PercentSuccess of analytics logboekvermeldingen bewerkingen hebben met transactiestatus ClientOtherErrors]

---
[Capaciteit metrische gegevens tonen een onverwachte toename in opslaggebruik capaciteit]

---
[Er is sprake van virtuele Machines met een groot aantal gekoppelde VHD's onverwacht opnieuw wordt opgestart]

---
[Het probleem zich voordoet Hallo-opslagemulator gebruiken voor ontwikkeling of tests]

---
[U ondervindt problemen met het installeren van hello Azure SDK voor .NET]

---
[U hebt een ander probleem met storage-service]

---
### <a name="metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency"></a>Metrische gegevens tonen AverageE2ELatency hoge en lage AverageServerLatency
de afbeelding hieronder van Hallo Hallo [Azure-portal](https://portal.azure.com) controlehulpprogramma toont een voorbeeld waarin hello **AverageE2ELatency** aanzienlijk hoger is dan Hallo **AverageServerLatency**.

![][4]

Opmerking Hallo opslagservice berekent alleen Hallo metriek **AverageE2ELatency** voor geslaagde aanvragen en, in tegenstelling tot **AverageServerLatency**, Hallo duurt voordat een client hello toosend Hallo bevat gegevens en de bevestiging van Hallo storage-service ontvangen. Daarom een verschil tussen **AverageE2ELatency** en **AverageServerLatency** kan ofwel vanwege toohello client toepassing wordt toorespond of vervaldatum tooconditions op Hallo netwerk vertragen.

> [!NOTE]
> U kunt ook weergeven **E2ELatency** en **ServerLatency** voor afzonderlijke opslagbewerkingen in Hallo opslag logboekregistratie gegevens vastleggen.
> 
> 

#### <a name="investigating-client-performance-issues"></a>Het onderzoeken van prestatieproblemen van client
Mogelijke oorzaken voor Hallo client reageert traag zijn met een beperkt aantal beschikbare verbindingen of threads of te weinig bronnen zoals CPU, geheugen of netwerk bandbreedte wordt. Hebt u mogelijk kunnen tooresolve Hallo probleem doordat Hallo client code toobe efficiënter (bijvoorbeeld via asynchrone aanroepen toohello storage-service) of met behulp van een grotere virtuele Machine (met meer kernen en meer geheugen).

Voor Hallo table en queue services Hallo Nagle algoritme kan ook worden veroorzaakt hoge **AverageE2ELatency** zoals vergeleken te**AverageServerLatency**: Zie voor meer informatie Hallo boeken [van Nagle Algoritme is niet beschrijvende kleine aanvragen](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx). U kunt Hallo Nagle-algoritme in code uitschakelen met behulp van Hallo **ServicePointManager** klasse in Hallo **System.Net** naamruimte. U moet dit doen voordat u een tabel van de toohello aanroepen of wachtrijservices in uw toepassing omdat dit geldt niet voor verbindingen die al zijn geopend. Hallo volgende voorbeeld is afkomstig uit Hallo **Application_Start** methode in een werkrol.

```csharp
var storageAccount = CloudStorageAccount.Parse(connStr);
ServicePoint tableServicePoint = ServicePointManager.FindServicePoint(storageAccount.TableEndpoint);
tableServicePoint.UseNagleAlgorithm = false;
ServicePoint queueServicePoint = ServicePointManager.FindServicePoint(storageAccount.QueueEndpoint);
queueServicePoint.UseNagleAlgorithm = false;
```

U moet controleren Hallo clientzijde logboeken toosee hoeveel aanvragen indienen van de clienttoepassing en controle voor algemene .NET gerelateerde knelpunten in uw client zoals CPU, .NET-garbagecollection, netwerkgebruik of geheugen. Als een beginpunt voor het oplossen van .NET-clienttoepassingen Zie [foutopsporing en tracering Profiling](http://msdn.microsoft.com/library/7fe0dd2y).

#### <a name="investigating-network-latency-issues"></a>Netwerklatentieproblemen onderzoeken
Hoge end-to-end-latentie veroorzaakt door Hallo is doorgaans vanwege tootransient voorwaarden. U kunt beide tijdelijke en permanente netwerkproblemen zoals verloren pakketten met hulpprogramma's zoals Wireshark of Microsoft Message Analyzer onderzoeken.

Zie voor meer informatie over het gebruik van Wireshark tootroubleshoot netwerkproblemen '[bijlage 2: Wireshark toocapture netwerkverkeer met]. "

Zie voor meer informatie over het gebruik van Microsoft Message Analyzer tootroubleshoot netwerkproblemen '[bijlage 3: met behulp van Microsoft Message Analyzer toocapture netwerkverkeer]. "

### <a name="metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency"></a>Metrische gegevens tonen lage AverageE2ELatency en lage AverageServerLatency maar Hallo client ondervindt hoge latentie
In dit scenario is de meest waarschijnlijke oorzaak Hallo een vertraging in Hallo opslag aanvragen Hallo opslagservice is bereikt. U moet onderzoeken waarom aanvragen van Hallo client zijn niet waardoor het via toohello blob-service.

Een mogelijke reden voor Hallo client vertragen verzenden van aanvragen is dat er een beperkt aantal beschikbare verbindingen of threads zijn.

Controleer ook of Hallo-client uitvoeren van meerdere pogingen en onderzoek van Hallo reden als dit Hallo geval. toodetermine of Hallo-client meerdere pogingen uitvoert, kunt u:

* Bekijk Hallo Opslaganalyse logboekbestanden. Als meerdere pogingen plaatsvinden, ziet u meerdere bewerkingen met dezelfde aanvraag-ID van client Hallo maar aanvraag-id's met een andere server.
* Raadpleeg Logboeken Hallo-client. Uitgebreide logboekregistratie wordt aangegeven dat een nieuwe poging is opgetreden.
* Fouten opsporen in uw code en controleer de eigenschappen van Hallo Hallo **OperationContext** object gekoppeld aan Hallo-aanvraag. Als het Hallo-bewerking heeft uit te voeren, Hallo **RequestResults** eigenschap meerdere unieke serveraanvraag id's bevat. U kunt ook controleren Hallo start en eindtijden voor elke aanvraag. Zie voor meer informatie, Hallo-codevoorbeeld in de sectie Hallo [Server aanvraag-ID].

Als er geen problemen in Hallo-client zijn, moet u onderzoeken van mogelijke netwerkproblemen zoals pakketverlies. U kunt hulpprogramma's zoals Wireshark of Microsoft Message Analyzer tooinvestigate netwerkproblemen.

Zie voor meer informatie over het gebruik van Wireshark tootroubleshoot netwerkproblemen '[bijlage 2: Wireshark toocapture netwerkverkeer met]. "

Zie voor meer informatie over het gebruik van Microsoft Message Analyzer tootroubleshoot netwerkproblemen '[bijlage 3: met behulp van Microsoft Message Analyzer toocapture netwerkverkeer]. "

### <a name="metrics-show-high-AverageServerLatency"></a>Metrische gegevens tonen hoge AverageServerLatency
In geval van hoog niveau Hallo **AverageServerLatency** voor aanvragen voor het downloaden van blob, moet u Hallo toosee opslag logboekregistratie logboeken als er herhaalde verzoeken om Hallo dezelfde blob-(of set van BLOB's). Voor blob uploaden aanvragen, moet u onderzoeken welke blok grootte Hallo client gebruikt (bijvoorbeeld blokken die minder dan 64 kB groot kan leiden tot overhead tenzij Hallo leest zich ook in minder dan 64 kB segmenten geüpload), en als meerdere clients uploadt blokkeert toohello dezelfde BLOB-parallel. Controleer ook Hallo per minuut metrische gegevens voor pieken in het aantal aanvragen die resulteren in meer dan Hallo per schaalbaarheidsdoelen van tweede Hallo: Zie ook '[metrische gegevens tonen een toename in PercentTimeoutError]. "

Als u hoog ziet **AverageServerLatency** voor blob downloadverzoeken wanneer er worden herhaald aanvragen Hallo dezelfde blob of een reeks blobs, vervolgens moet u overwegen deze blobs met Azure Cache opslaan in cache of hello Azure Content Delivery Network (CDN). Voor het uploaden van aanvragen, kunt u Hallo doorvoer verbeteren met behulp van een groter blok. Voor query's tootables, is het ook mogelijk tooimplement caching aan clientzijde op clients waarmee Hallo dezelfde bewerkingen opvragen en waar Hallo gegevens niet regelmatig worden gewijzigd.

Hoge **AverageServerLatency** waarden kunnen ook een symptoom van tabellen slecht geschreven worden of query's dat hierdoor in scanbewerkingen of die Hallo volgen toevoegen/toevoegen anti-patroon. Zie '[metrische gegevens tonen een toename in PercentThrottlingError]' voor meer informatie.

> [!NOTE]
> U kunt een uitgebreide controlelijst voor prestaties controlelijst hier vinden: [Microsoft Azure Storage prestaties en schaalbaarheid controlelijst](storage-performance-checklist.md).
> 
> 

### <a name="you-are-experiencing-unexpected-delays-in-message-delivery"></a>U ondervinden onverwachte vertragingen in de levering van berichten in een wachtrij
Als er een vertraging tussen het Hallo op een toepassing wordt een bericht tooa wachtrij en Hallo tijdstip deze beschikbaar tooread uit Hallo wachtrij wordt toegevoegd en moet u rekening houden met Hallo stappen toodiagnose Hallo na:

* Controleer of de toepassing hello is met succes toe te voegen Hallo berichten toohello wachtrij. Controleer Hallo toepassing wordt niet opnieuw geprobeerd Hallo **AddMessage** methode meerdere keren voordat slaagt. Hallo Storage-clientbibliotheek Logboeken wordt een herhaalde pogingen van opslagbewerkingen weergegeven.
* Controleer of er is geen klok scheeftrekken tussen Hallo-werkrol die de berichtenwachtrij toohello hello en Hallo-werkrol die het Hallo-bericht leest uit Hallo wachtrij die het maakt worden weergegeven alsof er een vertraging bij de verwerking is toegevoegd.
* Controleer als Hallo-werkrol die Hallo-berichten uit de wachtrij Hallo lezen is mislukt. Als een client wachtrij Hallo aanroept **GetMessage** methode mislukt maar toorespond met een bevestiging, het Hallo-bericht onzichtbaar voor de wachtrij Hallo blijft totdat Hallo **invisibilityTimeout** periode is verstreken. Hallo-bericht wordt op dit moment beschikbaar voor het opnieuw verwerken.
* Controleer als de wachtrijlengte Hallo gedurende een bepaalde periode groeit. Dit kan gebeuren als er niet voldoende werknemers beschikbaar tooprocess alle Hallo-berichten dat andere werknemers op Hallo wachtrij zijn geplaatst. U moet ook controleren Hallo metrische gegevens toosee als delete-aanvragen mislukken en Hallo aantal op berichten, dit kan duiden op in wachtrij herhaald mislukte pogingen toodelete Hallo-bericht.
* Bekijk Hallo opslag logboekregistratie logboekbestanden voor elke wachtrij-bewerkingen die hoger dan verwacht **E2ELatency** en **ServerLatency** waarden gedurende een langere periode dan normaal.

### <a name="metrics-show-an-increase-in-PercentThrottlingError"></a>Metrische gegevens tonen een toename in PercentThrottlingError
Bandbreedtebeperking fouten optreden wanneer u Hallo schaalbaarheidsdoelen van een opslagservice overschrijdt. Hallo storage-service biedt deze tooensure geen enkele client of de tenant Hallo-service op Hallo kosten van anderen kunt gebruiken. Zie voor meer informatie [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) voor meer informatie over schaalbaarheidsdoelen voor storage-accounts en prestatiedoelen voor partities binnen de storage-accounts.

Als hello **PercentThrottlingError** metriek een toename in Hallo percentage verzoeken die met een bandbreedteregeling fout mislukken weergeven, moet u tooinvestigate een van twee scenario's:

* [Tijdelijke toename van PercentThrottlingError]
* [Permanente toename PercentThrottlingError fout]

Een toename van **PercentThrottlingError** vaak gebeurt op Hallo dezelfde tijd als een toename van het aantal aanvragen dat opslag Hallo of wanneer u in eerste instantie worden, laden uw toepassing testen. Dit kan ook zelf in Hallo-client als '503 Server bezet' of '500 time-out voor de bewerking' HTTP statusberichten opslagbewerkingen manifest.

#### <a name="transient-increase-in-PercentThrottlingError"></a>Tijdelijke toename van PercentThrottlingError
Als u pieken in het Hallo-waarde van ziet **PercentThrottlingError** die overeenkomen met perioden van hoge activiteit voor de toepassing hello, moet u een exponentiële (niet-lineair) terug uit een strategie voor nieuwe pogingen implementeren in uw client: dit wordt Hallo onmiddellijke belasting van partitie hello te verminderen en helpen uw toepassing toosmooth uit pieken in het verkeer. Zie voor meer informatie over hoe beleid voor opnieuw proberen tooimplement met behulp van Storage-clientbibliotheek Hallo [Microsoft.WindowsAzure.Storage.RetryPolicies Namespace](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.retrypolicies.aspx).

> [!NOTE]
> U ziet misschien ook pieken in het Hallo-waarde van **PercentThrottlingError** die niet samenvallen met perioden van hoge activiteit voor de toepassing hello: Hallo hoogstwaarschijnlijk hier is Hallo opslagservice partities tooimprove load verplaatsen Netwerktaakverdeling.
> 
> 

#### <a name="permanent-increase-in-PercentThrottlingError"></a>Permanente toename PercentThrottlingError fout
Als u ziet een consistent hoge waarde voor **PercentThrottlingError** na een permanente toename in de transactie-volumes, of als u uw eerste load uitvoert tests op uw toepassing, moet u tooevaluate hoe uw toepassing partities opslag gebruikt en of het Hallo-schaalbaarheidsdoelen voor een opslagaccount bijna is bereikt. Bijvoorbeeld, als u ziet beperking van fouten in een wachtrij (die telt als een enkele partitie), moet vervolgens u aanvullende wachtrijen toospread Hallo transacties met voor meerdere partities. Als u beperking van fouten in een tabel ziet, moet u met behulp van een andere partitionering schema toospread tooconsider uw transacties tussen meerdere partities met behulp van een breed scala aan partitie sleutelwaarden. Een veelvoorkomende oorzaak van dit probleem is Hallo toevoegen/append anti-patroon waarbij u Hallo datum als partitiesleutel Hallo selecteren en vervolgens alle gegevens op een bepaalde dag tooone partitie worden geschreven: belast, kan dit resulteren in een knelpunt schrijven. U moet overwegen van een ander partitionering ontwerp of evalueren of met behulp van blob-opslag is mogelijk een betere oplossing. U moet ook controleren als Hallo bandbreedtebeperking optreedt als gevolg van pieken in het verkeer en onderzoeken manieren van het vloeiend maken van het patroon van aanvragen.

Als u uw transacties over meerdere partities verdelen, moet u nog steeds op de hoogte van de limieten voor schaalbaarheid Hallo instellen voor Hallo storage-account zijn. Bijvoorbeeld, als u op elke verwerking Hallo maximaal 2.000 1KB-berichten per seconde tien wachtrijen gebruikt, kunt u zich op Hallo algehele limiet van 20.000 berichten per seconde voor het Hallo-opslagaccount. Als u tooprocess meer dan 20.000 entiteiten per seconde moet, moet u rekening houden met behulp van meerdere opslagaccounts. U moet ook Houd er rekening mee dat formaat Hallo met uw verzoeken, en entiteiten invloed is op wanneer de opslagservice Hallo uw clients bandbreedte: als u grotere aanvragen en entiteiten hebt, u sneller kan worden beperkt.

Inefficiënt Queryontwerp kunt u ook toohit hello schaalbaarheidsbeperkingen voor Tabelpartities veroorzaken. Bijvoorbeeld, moet een query met een filter selecteert die alleen één procent Hallo entiteiten in een partitie, maar die scant alle Hallo entiteiten in een partitie tooaccess elke entiteit. Elke entiteit lezen meetelt Hallo kunt u het totale aantal transacties in de betreffende partitie; Daarom kunt u eenvoudig hello schaalbaarheidsdoelen bereiken.

> [!NOTE]
> De prestatietests, zou moeten uitwijzen queryontwerpen inefficiënt in uw toepassing.
> 
> 

### <a name="metrics-show-an-increase-in-PercentTimeoutError"></a>Metrische gegevens tonen een toename in PercentTimeoutError
De metrische gegevens tonen een toename van **PercentTimeoutError** voor een van uw storage-services. Op Hallo dezelfde tijdstip, hello client ontvangt een groot aantal statusberichten '500 time-out voor de bewerking' http-van-opslagbewerkingen.

> [!NOTE]
> Mogelijk ziet u time-outfouten tijdelijk als Hallo opslagservice saldo's aanvragen laden door een nieuwe partitie tooa-server te verplaatsen.
> 
> 

Hallo **PercentTimeoutError** meetwaarde is een aggregatie van Hallo metrische gegevens te volgen: **ClientTimeoutError**, **AnonymousClientTimeoutError**,  **SASClientTimeoutError**, **ServerTimeoutError**, **AnonymousServerTimeoutError**, en **SASServerTimeoutError**.

Hallo servertime worden veroorzaakt door een fout op Hallo-server. Hallo clienttime-outs gebeuren omdat een bewerking op de server Hallo Hallo time-out is opgegeven door de client Hallo; heeft overschreden bijvoorbeeld, een client met Hallo Storage-clientbibliotheek kunt instellen voor een time-out voor een bewerking door Hallo **ServerTimeout** eigenschap Hallo **QueueRequestOptions** klasse.

Time-outs van de server wijzen op een probleem met Hallo storage-service die verder onderzoek vereist. U kunt metrische gegevens toosee gebruiken als u Hallo schaalbaarheidslimieten voor het Hallo-service en tooidentify roept eventuele pieken in het verkeer dat dit probleem veroorzaakt. Als het probleem hello wordt onderbroken, kan dit worden veroorzaakt door tooload balancing activiteit in Hallo-service. Als Hallo probleem permanent is en niet wordt veroorzaakt door uw toepassing hello limieten voor schaalbaarheid van Hallo-service roept, moet u een probleem op te verhogen. Voor clienttime-outs, moet u beslissen als Hallo time-out tooan geschikte waarde is ingesteld in Hallo-client en beide Hallo time-outwaarde wijzigen in Hallo client instellen of onderzoeken hoe u kunt Hallo de prestaties verbeteren van Hallo-bewerkingen in het Hallo-storage-service voor voorbeeld door uw tabel query's optimaliseren of verkleinen van Hallo van uw berichten.

### <a name="metrics-show-an-increase-in-PercentNetworkError"></a>Metrische gegevens tonen een toename in PercentNetworkError
De metrische gegevens tonen een toename van **PercentNetworkError** voor een van uw storage-services. Hallo **PercentNetworkError** meetwaarde is een aggregatie van Hallo metrische gegevens te volgen: **NetworkError**, **AnonymousNetworkError**, en  **SASNetworkError**. Deze optreden wanneer Hallo storage-service een netwerkfout opgetreden detecteert bij het Hallo-client een opslag-aanvraag indient.

Hallo meest voorkomende oorzaak van deze fout is een client verbinding wordt verbroken voordat een time-out is verlopen in Hallo storage-service. U moet Hallo code in uw client-toounderstand waarom en wanneer de client Hallo verbreekt de opslagservice Hallo onderzoeken. U kunt ook Wireshark, Microsoft Message Analyzer of Tcping tooinvestigate problemen met de netwerkverbinding van de client hello gebruiken. Deze hulpprogramma's worden beschreven in Hallo [bijlagen].

### <a name="the-client-is-receiving-403-messages"></a>Hallo client ontvangt berichten HTTP 403 (verboden)
Als u de clienttoepassing die fouten HTTP 403 (verboden), is een waarschijnlijke oorzaak dat clientcomputers Hallo een verlopen Shared Access Signature (SAS) wordt gebruikt wanneer het verzendt een aanvraag voor opslag (Hoewel andere mogelijke oorzaken klok scheeftrekken, ongeldig sleutels bevatten en leeg headers). Als een verlopen SAS-sleutel Hallo oorzaak is, ziet u niet alle vermeldingen in serverzijde Hallo opslag logboekregistratie logboekgegevens. Hallo ziet volgende tabel u een voorbeeld Hallo clientzijde logboek is gegenereerd door Hallo Storage-clientbibliotheek die ziet u dit probleem optreedt:

| Bron | Uitgebreidheid | Uitgebreidheid | Aanvraag-id van client | Bewerking tekst |
| --- | --- | --- | --- | --- |
| Microsoft.WindowsAzure.Storage |Informatie |3 |85d077ab-... |Bewerking wordt gestart met de primaire locatie per locatie modus PrimaryOnly. |
| Microsoft.WindowsAzure.Storage |Informatie |3 |85d077ab-... |Vanaf synchrone aanvragen toohttps://domemaildist.blob.core.windows.netazureimblobcontainer/blobCreatedViaSAS.txt?sv=2014-02-14&amp;sr = c&amp;si = mypolicy&amp;sig OFnd4Rd7z01fIvh % 2BmcR6zbudIH2F5Ikm % = 2FyhNYZEmJNQ % 3D&amp;api-version = 2014-02-14. |
| Microsoft.WindowsAzure.Storage |Informatie |3 |85d077ab-... |Wachten op reactie. |
| Microsoft.WindowsAzure.Storage |Waarschuwing |2 |85d077ab-... |Uitzondering geretourneerd tijdens het wachten op reactie: Hallo externe server heeft een fout geretourneerd: (403) verboden... |
| Microsoft.WindowsAzure.Storage |Informatie |3 |85d077ab-... |Het antwoord is ontvangen. Statuscode = 403, aanvraag-ID = 9d67c64a-64ed-4b0d-9515-3b14bbcdc63d, Content-MD5 =, ETag =. |
| Microsoft.WindowsAzure.Storage |Waarschuwing |2 |85d077ab-... |Uitzondering geretourneerd tijdens het Hallo: Hallo externe server heeft een fout geretourneerd: (403) verboden... |
| Microsoft.WindowsAzure.Storage |Informatie |3 |85d077ab-... |Controleren als Hallo-bewerking moet opnieuw worden geprobeerd. Aantal nieuwe pogingen = 0, HTTP-statuscode = 403, uitzondering = Hallo van de externe server heeft een fout geretourneerd: (403) verboden... |
| Microsoft.WindowsAzure.Storage |Informatie |3 |85d077ab-... |de volgende locatie Hallo is tooPrimary, op basis van Hallo locatie modus ingesteld. |
| Microsoft.WindowsAzure.Storage |Fout |1 |85d077ab-... |Beleid voor opnieuw proberen is niet toegestaan voor een nieuwe poging. Mislukt met de externe server Hallo heeft een fout geretourneerd: (403) verboden. |

In dit scenario moet u onderzoeken waarom Hallo SAS-token verloopt voordat Hallo client Hallo token toohello server verzendt:

* U moet een begintijd die bij het maken van een SAS voor een client toouse onmiddellijk normaal gesproken niet instellen. Als er kleine Hallo klok verschillen tussen Hallo host genereren Hallo SAS met behulp van huidige tijd- en opslagservice hello, dan is het mogelijk voor Hallo opslag service tooreceive een SA's dat is nog niet geldig.
* U moet een zeer korte verlooptijd niet instellen op een SAS. Opnieuw klok kleine verschillen tussen Hallo host genereren van SAS Hallo en Hallo storage-service kan leiden tot tooa SAS blijkbaar verloopt eerder dan verwacht.
* Hallo versieparameter in Hallo SAS-sleutel (bijvoorbeeld **AVP = 2015-04-05**) overeen Hallo versie Hallo Storage-clientbibliotheek die u gebruikt? Het is raadzaam dat u altijd de meest recente versie Hallo Hallo gebruiken [Storage-clientbibliotheek](https://www.nuget.org/packages/WindowsAzure.Storage/).
* Als u uw opslagtoegangssleutels opnieuw genereert, kan dit tot bestaande SAS-tokens ongeldig. Dit kan een probleem zijn als het genereren van SAS-tokens met een lange verlooptijd van de client toepassingen toocache.

Als u Hallo Storage-clientbibliotheek toogenerate SAS-tokens gebruikt, is het eenvoudig toobuild een geldig token. Echter, als u met behulp van Hallo REST API voor Storage en construeren Hallo SAS-tokens handmatig moet lees zorgvuldig door Hallo onderwerp [toegang delegeren met Shared Access Signature](http://msdn.microsoft.com/library/azure/ee395415.aspx).

### <a name="the-client-is-receiving-404-messages"></a>Hallo-client is ontvangen HTTP 404 (niet gevonden)-berichten
Als Hallo clienttoepassing een HTTP 404 (niet gevonden)-bericht van Hallo-server ontvangt, betekent dit dat Hallo object Hallo de client probeerde toouse (zoals een entiteit, tabel, blob, container of wachtrij) bestaat niet in Hallo storage-service. Er zijn een aantal mogelijke redenen hiervoor, zoals:

* [Hallo-client of een ander proces het eerder verwijderd Hallo-object]
* [Een probleem met de autorisatie Shared Access Signature (SAS)]
* [Client-side JavaScript-code heeft geen machtiging tooaccess Hallo-object]
* [Netwerkfout]

#### <a name="client-previously-deleted-the-object"></a>Hallo-client of een ander proces het eerder verwijderd Hallo-object
Eenvoudig tooidentify in Hallo serverzijde registreert in scenario's waarbij Hallo client probeert tooread, bijwerken of verwijderen van gegevens in een storage-service is het meestal een eerdere bewerking die Hallo-object in kwestie van Hallo storage-service worden verwijderd. Hallo-logboekgegevens toont heel vaak dat een andere gebruiker of proces verwijderde Hallo-object. Hallo-serverzijde opslag logboekregistratie logboek hello type bewerking en aangevraagd-object-sleutelkolommen ziet u wanneer een client een object verwijderd.

In Hallo scenario waarin tooinsert een object van een client wordt geprobeerd deze mogelijk niet direct duidelijk waarom dit in een HTTP 404 (niet gevonden) antwoord resulteert gezien het feit dat hello client een nieuw object maakt. Als Hallo client een blob deze moet kunnen toofind Hallo blob-container, worden maakt als Hallo-client is een bericht dat moet kunnen toofind een wachtrij maakt, en als het Hallo-client is het toevoegen van een rij moet deze kunnen toofind Hallo tabel zijn.

U kunt Hallo clientzijde logboek vanaf Hallo Storage-clientbibliotheek toogain die een meer begrip van gedetailleerde als Hallo client specifieke aanvragen toohello storage-service verzendt gebruiken.

Hallo volgende clientzijde logboek is gegenereerd door de Storage-clientbibliotheek Hallo ziet u Hallo probleem wanneer Hallo client Hallo container voor Hallo blob die het maakt niet kunt vinden. Dit logboek bevat details van Hallo opslagbewerkingen te volgen:

| Aanvraag-id | Bewerking |
| --- | --- |
| 07b26a5d-... |**DeleteIfExists** methode toodelete Hallo blob-container. Let op: deze bewerking bevat een **HEAD** toocheck Hallo bestaan van de container Hallo aanvragen. |
| e2d06d78... |**CreateIfNotExists** methode toocreate Hallo blob-container. Let op: deze bewerking bevat een **HEAD** aanvraag waarmee wordt gecontroleerd of Hallo bestaan van Hallo-container. Hallo **HEAD** retourneert een 404-bericht, maar blijft. |
| de8b1c3c-... |**UploadFromStream** methode toocreate Hallo blob. Hallo **plaatsen** aanvraag is mislukt met een 404-bericht |

Logboekvermeldingen:

| Aanvraag-id | Bewerking tekst |
| --- | --- |
| 07b26a5d-... |Synchrone aanvraag toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer wordt gestart. |
| 07b26a5d-... |StringToSign HEAD...x-ms-client-request-id:07b26a5d-...x-ms-date:Tue, 03 Jun 2014 = 10:33:11 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |Wachten op reactie. |
| 07b26a5d-... |Het antwoord is ontvangen. Statuscode 200, aanvraag-ID = = eeead849... Content-MD5 =, ETag = &quot;0x8D14D2DC63D059B&quot;. |
| 07b26a5d-... |Antwoordheaders zijn verwerkt, teruglopende met rest Hallo van Hallo-bewerking. |
| 07b26a5d-... |Antwoordtekst downloaden. |
| 07b26a5d-... |De bewerking is voltooid. |
| 07b26a5d-... |Synchrone aanvraag toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer wordt gestart. |
| 07b26a5d-... |StringToSign DELETE...x-ms-client-request-id:07b26a5d-...x-ms-date:Tue, 03 Jun 2014 = 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |Wachten op reactie. |
| 07b26a5d-... |Het antwoord is ontvangen. Statuscode = 202, aanvraag-ID = 6ab2a4cf-..., Content-MD5 =, ETag =. |
| 07b26a5d-... |Antwoordheaders zijn verwerkt, teruglopende met rest Hallo van Hallo-bewerking. |
| 07b26a5d-... |Antwoordtekst downloaden. |
| 07b26a5d-... |De bewerking is voltooid. |
| e2d06d78-... |Asynchrone aanvraag toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer wordt gestart.</td> |
| e2d06d78-... |StringToSign HEAD...x-ms-client-request-id:e2d06d78-...x-ms-date:Tue, 03 Jun 2014 = 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |Wachten op reactie. |
| de8b1c3c-... |Synchrone aanvraag toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer/blobCreated.txt wordt gestart. |
| de8b1c3c-... |StringToSign PUT =... 64.qCmF+TQLPhq/YYK50mP9ZQ==...x-MS-BLOB-type:BlockBlob.x-MS-Client-Request-id:de8b1c3c-...x-MS-Date:TUE, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer/blobCreated.txt. |
| de8b1c3c-... |Aanvraaggegevens toowrite wordt voorbereid. |
| e2d06d78-... |Uitzondering geretourneerd tijdens het wachten op reactie: Hallo externe server heeft een fout geretourneerd: (404) niet gevonden... |
| e2d06d78-... |Het antwoord is ontvangen. Statuscode 404, aanvraag-ID = = 353ae3bc-..., Content-MD5 =, ETag =. |
| e2d06d78-... |Antwoordheaders zijn verwerkt, teruglopende met rest Hallo van Hallo-bewerking. |
| e2d06d78-... |Antwoordtekst downloaden. |
| e2d06d78-... |De bewerking is voltooid. |
| e2d06d78-... |Asynchrone aanvraag toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer wordt gestart. |
| e2d06d78-... |StringToSign PUT =... 0...x-MS-Client-Request-id:e2d06d78-...x-MS-Date:TUE, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |Wachten op reactie. |
| de8b1c3c-... |Aanvraag voor het schrijven van gegevens. |
| de8b1c3c-... |Wachten op reactie. |
| e2d06d78-... |Uitzondering geretourneerd tijdens het wachten op reactie: Hallo externe server heeft een fout geretourneerd: (409) Conflict... |
| e2d06d78-... |Het antwoord is ontvangen. Statuscode = 409, aanvraag-ID = c27da20e-..., Content-MD5 =, ETag =. |
| e2d06d78-... |Antwoordtekst voor fout bij het downloaden. |
| de8b1c3c-... |Uitzondering geretourneerd tijdens het wachten op reactie: Hallo externe server heeft een fout geretourneerd: (404) niet gevonden... |
| de8b1c3c-... |Het antwoord is ontvangen. Statuscode 404, aanvraag-ID = = 0eaeab3e-..., Content-MD5 =, ETag =. |
| de8b1c3c-... |Uitzondering geretourneerd tijdens het Hallo: Hallo externe server heeft een fout geretourneerd: (404) niet gevonden... |
| de8b1c3c-... |Beleid voor opnieuw proberen is niet toegestaan voor een nieuwe poging. Mislukt met de externe server Hallo heeft een fout geretourneerd: (404) niet gevonden... |
| e2d06d78-... |Beleid voor opnieuw proberen is niet toegestaan voor een nieuwe poging. Mislukt met de externe server Hallo heeft een fout geretourneerd: (409) Conflict... |

In dit voorbeeld toont Hallo logboek Hallo client-aanvragen van Hallo is interleaving **CreateIfNotExists** methode (aanvraag-id e2d06d78...) met Hallo aanvragen van Hallo **UploadFromStream** methode ( de8b1c3c-...); Dit gebeurt omdat Hallo clienttoepassing asynchroon deze methoden is aangeroepen. U moet de asynchrone code Hallo in Hallo client tooensure gemaakt Hallo container voordat u probeert tooupload alle gegevens tooa blob in de container wijzigen. In het ideale geval moet u alle uw containers van tevoren maken.

#### <a name="SAS-authorization-issue"></a>Een probleem met de autorisatie Shared Access Signature (SAS)
Als de client-toepassing hello toouse een SAS-sleutel die omvat niet de vereiste machtigingen voor de bewerking Hallo Hallo probeert, retourneert Hallo storage-service een HTTP 404 (niet gevonden) bericht toohello client. Op Hallo dezelfde tijdstip, ziet u ook een andere waarde dan nul voor **SASAuthorizationError** in Hallo metrische gegevens.

Hallo volgende tabel ziet u een voorbeeld logboekbericht serverzijde uit Hallo opslag logboekregistratie logboekbestand:

| Naam | Waarde |
| --- | --- |
| Begintijd van de aanvraag | 2014-05-30T06:17:48.4473697Z |
| Bewerkingstype     | GetBlobProperties            |
| De status van aanvraag     | SASAuthorizationError        |
| HTTP-statuscode   | 404                          |
| Verificatietype| SAS                          |
| Servicetype       | Blob                         |
| Aanvraag-URL        | https://domemaildist.BLOB.Core.Windows.NET/azureimblobcontainer/blobCreatedViaSAS.txt |
| nbsp;              |   ? AVP 2014-02-14 = & sr = c & si = mypolicy & sig XXXXX =&;api-versie 2014-02-14 = |
| Koptekst van de aanvraag-id  | a1f348d5-8032-4912-93ef-b393e5252a3b |
| Aanvraag-ID van client  | 2d064953-8436-4ee0-aa0c-65cb874f7929 |


U moet onderzoeken waarom de clienttoepassing probeert tooperform een bewerking er geen machtigingen heeft voor.

#### <a name="JavaScript-code-does-not-have-permission"></a>Client-side JavaScript-code heeft geen machtiging tooaccess Hallo-object
Als u van een JavaScript-client gebruikmaakt en Hallo storage-service HTTP 404-berichten retourneert, controleert u Hallo volgende JavaScript-fouten in de browser Hallo:

```
SEC7120: Origin http://localhost:56309 not found in Access-Control-Allow-Origin header.
SCRIPT7002: XMLHttpRequest: Network Error 0x80070005, Access is denied.
```

> [!NOTE]
> Hallo F12 ontwikkelhulpprogramma's kunt u in Internet Explorer tootrace Hallo-berichten uitgewisseld tussen Hallo-browser- en opslagservice Hallo als u de client-side JavaScript problemen wilt oplossen.
> 
> 

Deze fouten optreden omdat Hallo webbrowser Hallo implementeert [hetzelfde oorsprong beleid](http://www.w3.org/Security/wiki/Same_Origin_Policy) beveiligingsbeperkingen waarmee wordt voorkomen dat een webpagina een API aanroepen in een ander domein dan Hallo domein Hallo pagina is afkomstig uit.

toowork rond Hallo JavaScript probleem, kunt u de Cross-Origin Resource delen (CORS) configureren voor het openen van de client Hallo Hallo storage-service. Zie voor meer informatie [Cross-Origin-Resource delen (CORS) ondersteuning voor Azure Storage-Services](http://msdn.microsoft.com/library/azure/dn535601.aspx).

Hallo volgende codevoorbeeld ziet u hoe tooconfigure uw blob-service tooallow JavaScript uitgevoerd in de Contoso-domein tooaccess Hallo een blob in de blob storage-service:

```csharp
CloudBlobClient client = new CloudBlobClient(blobEndpoint, new StorageCredentials(accountName, accountKey));
// Set hello service properties.
ServiceProperties sp = client.GetServiceProperties();
sp.DefaultServiceVersion = "2013-08-15";
CorsRule cr = new CorsRule();
cr.AllowedHeaders.Add("*");
cr.AllowedMethods = CorsHttpMethods.Get | CorsHttpMethods.Put;
cr.AllowedOrigins.Add("http://www.contoso.com");
cr.ExposedHeaders.Add("x-ms-*");
cr.MaxAgeInSeconds = 5;
sp.Cors.CorsRules.Clear();
sp.Cors.CorsRules.Add(cr);
client.SetServiceProperties(sp);
```

#### <a name="network-failure"></a>Netwerkfout
In sommige gevallen kunnen verloren netwerkpakketten toohello opslagservice HTTP 404-berichten toohello client retourneren leiden. Bijvoorbeeld wanneer uw clienttoepassing van een entiteit uit de tabelservice Hallo verwijderen ziet u een opslagrapportage uitzondering genereert Hallo-client een ' HTTP 404 (niet gevonden) ' statusbericht van Hallo tabel-service. Als u Hallo-tabel in Hallo table storage-service onderzoeken, ziet u dat Hallo service Hallo entiteit hebt verwijderd, zoals aangevraagd.

Hallo uitzonderingsdetails in Hallo client opnemen Hallo aanvraag-id (7e84f12d...) dat door Hallo tabelservice voor Hallo-aanvraag is toegewezen: kunt u deze informatie toolocate Hallo-aanvraaggegevens in Hallo serverzijde opslag Logboeken door te zoeken in Hallo  **aanvraag-id-header** kolom in het logboekbestand Hallo. U kunt ook Hallo metrische gegevens tooidentify wanneer de fouten, zoals dit optreden en zoek vervolgens Hallo-logboekbestanden op basis van Hallo Hallo tijdmetrieken deze fout vastgelegd. Dit logboek vermelding bevat die Hallo verwijderen is mislukt met een statusbericht 'HTTP (404) Client andere fout'. Hallo dezelfde logboekvermelding bevat ook Hallo aanvraag-id gegenereerd door de client Hallo in Hallo **client-request-id** kolom (813ea74f...).

Hallo-serverzijde logboekbestand bevat ook een andere vermelding met Hallo dezelfde **client-request-id** waarde (813ea74f...) voor een geslaagde bewerking voor verwijderen Hallo dezelfde entiteit en Hallo van dezelfde client. Deze geslaagde bewerking heeft plaatsgevonden zeer kort voordat Hallo mislukte delete-aanvraag.

Hallo meest waarschijnlijke oorzaak van dit scenario is die Hallo-client heeft een aanvraag verwijderen voor Hallo entiteit toohello tabel-service, die is voltooid, maar heeft geen een bevestiging ontvangen van server hello (mogelijk vanwege een tijdelijk netwerkprobleem tooa) verzonden. Hallo-client vervolgens automatisch opnieuw geprobeerd Hallo-bewerking (met behulp van dezelfde Hallo **client-request-id**), en deze nieuwe poging is mislukt omdat het Hallo-entiteit al is verwijderd.

Als dit probleem zich blijft voordoen, moet u onderzoeken waarom Hallo client tooreceive bevestigingen van Hallo tabel-service is mislukt. Als Hallo probleem onregelmatige, moet u Hallo 'HTTP (404) is niet gevonden' fout-trap en aanmelden Hallo-client, maar Hallo client toocontinue toestaan.

### <a name="the-client-is-receiving-409-messages"></a>Hallo client ontvangt berichten van de HTTP-409 (Conflict)
Hallo volgende tabel ziet u een uitpakken uit Hallo serverzijde logboek voor twee clientbewerkingen: **DeleteIfExists** gevolgd door onmiddellijk **CreateIfNotExists** met behulp van dezelfde naam van de blob-container Hallo. Opmerking dat elke clientbewerking op de eerste in twee aanvragen verzonden toohello server resulteert, een **GetContainerProperties** aanvraag toocheck als Hallo-container bestaat, gevolgd door Hallo **DeleteContainer** of  **CreateContainer** aanvraag.

| tijdstempel | Bewerking | Resultaat | Containernaam | Aanvraag-id van client |
| --- | --- | --- | --- | --- |
| 05:10:13.7167225 |GetContainerProperties |200 |mmcont |c9f52c89-... |
| 05:10:13.8167325 |DeleteContainer |202 |mmcont |c9f52c89-... |
| 05:10:13.8987407 |GetContainerProperties |404 |mmcont |bc881924-... |
| 05:10:14.2147723 |CreateContainer |409 |mmcont |bc881924-... |

Hallo-code in de clienttoepassing Hallo verwijderd en vervolgens onmiddellijk opnieuw gemaakt een blob-container Hallo met dezelfde naam: Hallo **CreateIfNotExists** methode (Client aanvraag ID bc881924-...) uiteindelijk mislukt met de Hallo HTTP 409 (Conflict) Fout bij. Wanneer een client wordt verwijderd voor blob-containers, tabellen of wachtrijen die een korte voordat periode weer de naam van de Hallo beschikbaar is.

Hallo-clienttoepassing moet unieke containernamen gebruiken wanneer er nieuwe containers maakt als Hallo verwijderen/opnieuw patroon geldt.

### <a name="metrics-show-low-percent-success"></a>Metrische gegevens tonen lage PercentSuccess of analytics logboekvermeldingen bewerkingen hebben met de status van ClientOtherErrors
Hallo **PercentSuccess** metriek Hallo procent van de bewerkingen die met succes zijn uitgevoerd op basis van hun HTTP-statuscode worden vastgelegd. Bewerkingen met statuscodes van 2XX tellen als geslaagd, terwijl de bewerkingen met statuscodes in 3XX, 4XX en 5XX bereiken worden geteld als mislukt en lagere Hallo **PercentSucess** metrische waarde. In logboekbestanden Hallo serverzijde opslag, deze bewerkingen worden geregistreerd met een transactiestatus **ClientOtherErrors**.

Het is belangrijk toonote dat deze bewerkingen zijn voltooid en daarom niet van invloed op andere metrische gegevens zoals beschikbaarheid. Enkele voorbeelden van bewerkingen die met succes uitvoeren, maar dat kan leiden tot mislukte HTTP-statuscodes zijn:

* **ResourceNotFound** (niet gevonden 404), bijvoorbeeld uit een GET aanvraag tooa blob die niet bestaat.
* **ResouceAlreadyExists** (Conflict 409), bijvoorbeeld van een **CreateIfNotExist** bewerking waarbij Hallo resource al bestaat.
* **ConditionNotMet** (niet gewijzigd 304), bijvoorbeeld van een voorwaardelijke bewerking zoals wanneer een client verzendt een **ETag** waarde en een HTTP- **If-None-Match** header toorequest een installatiekopie alleen als deze is bijgewerkt sinds de laatste bewerking Hallo.

U vindt een lijst met algemene REST-API-foutcodes die Hallo storage-services op pagina Hallo retourneren [algemene foutcodes voor REST-API](http://msdn.microsoft.com/library/azure/dd179357.aspx).

### <a name="capacity-metrics-show-an-unexpected-increase"></a>Capaciteit metrische gegevens tonen een onverwachte toename in opslaggebruik capaciteit
Als er plotseling, onverwachte wijzigingen in het capaciteitsverbruik in uw opslagaccount, kunt u onderzoeken Hallo redenen door eerst te zoeken naar metrische gegevens over uw beschikbaarheid; bijvoorbeeld, kan een toename van het aantal mislukte aanvragen voor verwijderen Hallo tooan toename in Hallo bedrag van blob-opslag die u als de toepassing specifieke opschoonacties vereisen die mogelijk hebben verwachte toobe vrijmaken van ruimte werkt niet gebruikt zoals verwacht (voor leiden bijvoorbeeld omdat Hallo SAS-tokens die worden gebruikt voor het vrijmaken van ruimte verlopen).

### <a name="you-are-experiencing-unexpected-reboots"></a>U ondervindt onverwacht opnieuw wordt opgestart van Azure Virtual Machines waarvoor een groot aantal gekoppelde VHD 's
Als een Azure-virtuele Machine (VM) heeft een groot aantal gekoppelde VHD's die in Hallo hetzelfde opslagaccount kan u Hallo schaalbaarheidsdoelen voor een afzonderlijke opslagaccount veroorzaakt Hallo VM toofail overschrijdt. Controleer Hallo minuut metrieken voor Hallo storage-account (**TotalRequests**/**TotalIngress**/**TotalEgress**) pieken die groter zijn dan de schaalbaarheidsdoelen Hallo voor een opslagaccount. Zie de sectie Hallo '[metrische gegevens tonen een toename in PercentThrottlingError]' voor hulp bij het bepalen of beperking van uw opslagaccount is opgetreden.

In het algemeen elke afzonderlijke invoer of uitvoerbewerking op een VHD van een virtuele Machine vertaalt te**downloaden pagina** of **pagina plaatsen** bewerkingen op Hallo onderliggende pagina-blob. Daarom kunt u Hallo geschatte IOP's voor uw omgeving tootune hoeveel VHD's die u kunt hebben in een één opslagaccount op basis van Hallo specifiek gedrag van uw toepassing. We raden niet meer dan 40 schijven in een één opslagaccount hebben. Zie [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) voor meer informatie over huidige schaalbaarheidsdoelen Hallo voor storage-accounts, met name Hallo totale aanvraag en de totale bandbreedte voor Hallo type opslagaccount u gebruikt .
Als u voor uw opslagaccount hello schaalbaarheidsdoelen overschrijdt, schakelt u uw VHD's in meerdere verschillende accounts tooreduce Hallo opslagactiviteiten voor elke afzonderlijke account.

### <a name="your-issue-arises-from-using-the-storage-emulator"></a>Het probleem zich voordoet Hallo-opslagemulator gebruiken voor ontwikkeling of tests
U doorgaans Hallo-opslagemulator gebruiken tijdens het ontwikkelen en testen van tooavoid Hallo vereiste voor een Azure storage-account. Hallo veelvoorkomende zijn problemen die optreden kunnen wanneer u van de opslagemulator Hallo gebruikmaakt:

* [Functie 'X' werkt niet in de opslagemulator Hallo]
* [Fout 'Hallo-waarde van een Hallo HTTP-headers is niet de juiste indeling Hallo' wanneer met behulp van Hallo-opslagemulator]
* [Actieve Hallo opslagemulator vereist beheerdersbevoegdheden]

#### <a name="feature-X-is-not-working"></a>Functie 'X' werkt niet in de opslagemulator Hallo
Hallo opslagemulator ondersteunt niet alle Hallo functies van hello Azure storage-services zoals Hallo file-service. Zie voor meer informatie [gebruik hello Azure-Opslagemulator voor ontwikkeling en testen](storage-use-emulator.md).

Voor deze functies die Hallo storage emulator niet ondersteunen, hello Azure storage-service in de cloud hello gebruiken.

#### <a name="error-HTTP-header-not-correct-format"></a>Fout 'Hallo-waarde van een Hallo HTTP-headers is niet de juiste indeling Hallo' wanneer met behulp van Hallo-opslagemulator
U test uw toepassing dat Hallo Storage-clientbibliotheek tegen emulator en een methode-aanroepen van lokale opslag Hallo zoals **CreateIfNotExists** mislukken met fout Hallo-bericht 'hello waarde van een Hallo HTTP-headers zich niet in Hallo juiste indeling." Dit geeft aan dat Hallo Hallo-versie van de storage-clientbibliotheek Hallo u biedt geen ondersteuning voor versie van Hallo-opslagemulator die u gebruikt. Hallo Storage-clientbibliotheek voegt Hallo header **x-ms-version** tooall Hallo aanvragen maakt. Als de opslagemulator Hallo Hallo-waarde in hello wordt niet herkend **x-ms-version** -kop, het Hallo-aanvraag wordt geweigerd.

U kunt Hallo Tapewisselaarclient opslag logboeken toosee Hallo waarde Hallo gebruiken **header x-ms-version** is het verzenden. U ziet ook Hallo-waarde van Hallo **header x-ms-version** als u Fiddler tootrace Hallo aanvragen van de clienttoepassing.

Dit scenario treedt meestal op als u installeren en gebruiken van de meest recente versie Hallo Hallo Storage-clientbibliotheek zonder bij te werken Hallo-opslagemulator. U moet installeren Hallo meest recente versie van de opslagemulator Hallo of cloud-opslag gebruiken in plaats van de emulator Hallo voor ontwikkeling en tests.

#### <a name="storage-emulator-requires-administrative-privileges"></a>Actieve Hallo opslagemulator vereist beheerdersbevoegdheden
U wordt gevraagd om beheerdersreferenties wanneer u de opslagemulator Hallo uitvoert. Dit gebeurt alleen als u de opslagemulator Hallo voor Hallo eerst initialiseren. Nadat u hebt de opslagemulator Hallo geïnitialiseerd, hoeft u geen beheerdersbevoegdheden toorun deze opnieuw.

Zie voor meer informatie [gebruik hello Azure-Opslagemulator voor ontwikkeling en testen](storage-use-emulator.md). Houd er rekening mee dat kunt u ook de opslagemulator Hallo in Visual Studio, wordt ook hebt u beheerdersbevoegdheden nodig initialiseren.

### <a name="you-are-encountering-problems-installing-the-Windows-Azure-SDK"></a>U ondervindt problemen met het installeren van hello Azure SDK voor .NET
Wanneer u tooinstall Hallo SDK, mislukt dit poging tooinstall hello opslagemulator op uw lokale machine. Hallo installatielogboek bevat een van de Hallo volgende berichten:

* CAQuietExec: Fout: kan geen tooaccess SQL-exemplaar
* CAQuietExec: Fout: kan geen toocreate database

Hallo oorzaak is een probleem met een bestaande installatie van de LocalDB. Standaard gebruikt de opslagemulator hello LocalDB toopersist gegevens wanneer deze hello Azure storage-services simuleert. U kunt uw LocalDB-exemplaar herstellen door het uitvoeren van de volgende opdrachten in een opdrachtpromptvenster op voordat u probeert tooinstall Hallo SDK Hallo.

```
sqllocaldb stop v11.0
sqllocaldb delete v11.0
delete %USERPROFILE%\WAStorageEmulatorDb3*.*
sqllocaldb create v11.0
```

Hallo **verwijderen** opdracht wordt geen oude databasebestanden uit eerdere installaties van de opslagemulator Hallo verwijderd.

### <a name="you-have-a-different-issue-with-a-storage-service"></a>U hebt een ander probleem met storage-service
Als Hallo vorige secties Hallo probleem met de storage-service niet opgeeft, moet u overstapt op Hallo benadering toodiagnosing te volgen en uw probleem op te lossen.

* Controleer uw toosee metrische gegevens als er een wijziging van de verwachte basislijn gedrag. Van metrische gegevens voor hello, hebt u mogelijk kunnen toodetermine of Hallo probleem tijdelijke of permanente is en welke opslagbewerkingen Hallo probleem invloed op.
* U kunt Hallo metrische gegevens toohelp u uw logboekgegevens serverzijde voor meer gedetailleerde informatie over eventuele fouten die optreden zoeken gebruiken. Deze informatie kunt u Hallo probleem kunt oplossen.
* Als het Hallo-gegevens in Hallo serverzijde Logboeken is niet voldoende tootroubleshoot Hallo probleem is, kunt u Hallo Storage-clientbibliotheek clientzijde logboeken tooinvestigate Hallo gedrag van uw clienttoepassing en hulpprogramma's zoals Fiddler, Wireshark, en Microsoft Message Analyzer tooinvestigate uw netwerk.

Zie voor meer informatie over het gebruik van Fiddler '[bijlage 1: met behulp van HTTP en HTTPS-verkeer van toocapture Fiddler]. "

Zie voor meer informatie over het gebruik van Wireshark '[bijlage 2: Wireshark toocapture netwerkverkeer met]. "

Zie voor meer informatie over het gebruik van Microsoft Message Analyzer '[bijlage 3: met behulp van Microsoft Message Analyzer toocapture netwerkverkeer]. "

## <a name="appendices"></a>Bijlagen
Hallo bijlagen beschrijven verschillende hulpprogramma's die mogelijk nuttig bij het opsporen en het oplossen van problemen met Azure Storage (en andere services). Deze hulpprogramma's maken geen deel uit van Azure Storage en andere producten van derden zijn. Als zodanig Hallo-hulpprogramma's beschreven in deze bijlagen niet wordt gedekt door een ondersteuningsovereenkomst mogelijk met Microsoft Azure of Azure Storage en daarom als onderdeel van uw evaluatieproces onderzoekt u Hallo-licentieverlening en ondersteuningsopties beschikbaar is via Hallo-providers van deze hulpprogramma's.

### <a name="appendix-1"></a>Bijlage 1: Gebruik Fiddler toocapture HTTP en HTTPS-verkeer
[Fiddler](http://www.telerik.com/fiddler) een handig hulpmiddel voor het analyseren van Hallo HTTP en HTTPS-verkeer tussen uw clienttoepassing en hello Azure storage-service die u gebruikt.

> [!NOTE]
> Fiddler decodering HTTPS-verkeer; u moet zorgvuldig Hallo Fiddler documentatie lezen toounderstand hoe dit wordt uitgevoerd, en toounderstand Hallo beveiligingsgebied.
> 
> 

Deze bijlage bevat een kort overzicht van hoe tooconfigure Fiddler toocapture verkeer tussen de lokale computer Hallo waarin u Fiddler hebt geïnstalleerd en hello Azure storage-services.

Wanneer u Fiddler hebt gestart, begint het vastleggen van HTTP en HTTPS-verkeer op uw lokale machine. Hallo Hieronder volgen enkele nuttige opdrachten voor het beheren van Fiddler:

* Stop en start het vastleggen van verkeer. In het hoofdmenu hello, ga te**bestand** en klik vervolgens op **verkeer vastleggen** tootoggle vastleggen in- of uitschakelen.
* Van de vastgelegde verkeersgegevens opslaan. In het hoofdmenu hello, ga te**bestand**, klikt u op **opslaan**, en klik vervolgens op **alle sessies**: Hiermee kunt u toosave Hallo verkeer in een sessie archiefbestand. U kunt een sessie-archief voor analyse later opnieuw laden of verzenden als tooMicrosoft ondersteuning aangevraagd.

toolimit hello hoeveelheid verkeer die Fiddler worden vastgelegd, kunt u filters die u in Hallo configureert **Filters** tabblad Hallo volgende schermafbeelding ziet u een filter waarmee alleen verkeer dat wordt verzonden toohello vastgelegd  **contosoemaildist.Table.Core.Windows.NET** opslag eindpunt:

![][5]

### <a name="appendix-2"></a>Bijlage 2: Wireshark toocapture netwerkverkeer met behulp van
[Wireshark](http://www.wireshark.org/) een netwerkprotocolanalyse waarmee u tooview wordt gedetailleerde informatie voor een breed scala aan netwerkprotocollen pakket.

Hallo volgende procedure laat zien u hoe toocapture pakketgegevens voor verkeer van de lokale computer Hallo gedetailleerde waar u Wireshark toohello tabelservice geïnstalleerd in uw Azure storage-account.

1. Start Wireshark op uw lokale machine.
2. In Hallo **Start** sectie, selecteer Hallo lokale netwerkinterface of interfaces die verbonden toohello zijn internet.
3. Klik op **vastleggen opties**.
4. Voeg een filter toohello **vastleggen Filter** textbox. Bijvoorbeeld: **hosten contosoemaildist.table.core.windows.net** Wireshark toocapture configureert alleen pakketten tooor van Hallo tabel service-eindpunt in Hallo verzonden **contosoemaildist** opslag account. Bekijk Hallo [volledige lijst met Filters vastleggen](http://wiki.wireshark.org/CaptureFilters).
   
   ![][6]
5. Klik op **Start**. Wireshark wordt nu alle hello-pakketten verzenden tooor van Hallo tabel service-eindpunt vastgelegd tijdens het gebruik van uw client-toepassing op uw lokale machine.
6. Wanneer u klaar bent, op Hallo hoofdmenu Klik **vastleggen** en vervolgens **stoppen**.
7. Hallo toosave opgenomen gegevens in een Wireshark vastleggen bestand, op Hallo hoofdmenu Klik **bestand** en vervolgens **opslaan**.

WireShark worden eventuele fouten die zijn opgenomen in Hallo Markeer **packetlist** venster. U kunt ook Hallo **Expert Info** venster (Klik op **analyseren**, vervolgens **Expert Info**) tooview een samenvatting van fouten en waarschuwingen.

![][7]

U kunt ook hebt gekozen tooview Hallo TCP-gegevens zoals toepassingslaag Hallo ziet dit door met de rechtermuisknop op Hallo TCP-gegevens en **TCP-stroom Volg**. Dit is vooral handig als u uw dump zonder een filter vastleggen zijn vastgelegd. Zie voor meer informatie [volgende TCP-stromen](http://www.wireshark.org/docs/wsug_html_chunked/ChAdvFollowTCPSection.html).

![][8]

> [!NOTE]
> Zie voor meer informatie over het gebruik van Wireshark hello [Wireshark gebruikershandleiding](http://www.wireshark.org/docs/wsug_html_chunked).
> 
> 

### <a name="appendix-3"></a>Bijlage 3: Met behulp van Microsoft Message Analyzer toocapture netwerkverkeer
U kunt Microsoft Message Analyzer toocapture HTTP en HTTPS-verkeer gebruiken in een vergelijkbare manier tooFiddler en het netwerkverkeer in een vergelijkbare manier tooWireshark opnemen.

#### <a name="configure-a-web-tracing-session-using-microsoft-message-analyzer"></a>Een websessie tracering met behulp van Microsoft Message Analyzer configureren
tooconfigure een sessie voor web-tracering voor HTTP en HTTPS-verkeer met behulp van Microsoft Message Analyzer Hallo Microsoft Message Analyzer toepassing uitvoeren en klik vervolgens op Hallo **bestand** menu, klikt u op **vastleggen/Trace**. Selecteer in het Hallo-lijst met beschikbare trace-scenario's, **webproxy**. Klik dan in Hallo **Scenario traceringsconfiguratie** Configuratiescherm Hallo **HostnameFilter** textbox Hallo namen van de eindpunten van uw opslag toevoegen (kunt u deze namen in Hallo opzoeken [Azure-portal](https://portal.azure.com)). Bijvoorbeeld, als hello naam van uw Azure storage-account is **contosodata**, moet u de volgende toohello Hallo toevoegen **HostnameFilter** textbox:

```
contosodata.blob.core.windows.net contosodata.table.core.windows.net contosodata.queue.core.windows.net
```

> [!NOTE]
> Hallo hostnamen wordt gescheiden door een spatie.
> 
> 

Wanneer u klaar toostart verzamelen van traceringsgegevens bent, klikt u op Hallo **starten met** knop.

Voor meer informatie over Microsoft Message Analyzer Hallo **webproxy** traceren, Zie [Provider van Microsoft-PEF-WebProxy](http://technet.microsoft.com/library/jj674814.aspx).

Hallo ingebouwde **webproxy** tracering in Microsoft Message Analyzer is gebaseerd op Fiddler; het kan vastleggen clientzijde HTTPS-verkeer en niet-versleutelde HTTPS-berichten worden weergegeven. Hallo **webproxy** werkt door het configureren van een lokale proxy voor alle HTTP en HTTPS-verkeer dat hieraan toegang toounencrypted berichten traceren.

#### <a name="diagnosing-network-issues-using-microsoft-message-analyzer"></a>Diagnose van netwerkproblemen met behulp van Microsoft Message Analyzer
Bovendien toousing Microsoft Message Analyzer Hallo **webproxy** trace toocapture details van Hallo HTTP/HTTPs-verkeer tussen Hallo-clienttoepassing en Hallo storage-service, kunt u ook Hallo ingebouwde  **Lokale Link-laag** toocapture pakket netwerkgegevens traceren. Dit kunt u toocapture gegevens vergelijkbaar toothat die u kunt met Wireshark vastleggen en analyseren problemen zoals netwerk verloren pakketten.

Hallo volgende schermafbeelding ziet u een voorbeeld **lokale Link-laag** traceren met een aantal **informatief** berichten in Hallo **DiagnosisTypes** kolom. Te klikken op een pictogram in Hallo **DiagnosisTypes** kolom Hallo worden details weergegeven van het Hallo-bericht. In dit voorbeeld doorgegeven Hallo server bericht #305 omdat er geen een bevestiging is ontvangen van Hallo-client:

![][9]

Wanneer u Hallo traceersessie in Microsoft Message Analyzer maakt, kunt u filters tooreduce Hallo hoeveelheid ruis in Hallo tracering opgeven. Op Hallo **vastleggen / traceren** pagina waar het definiëren van Hallo trace, klikt u op Hallo **configureren** vervolgens te koppelen**Microsoft Windows-NDIS PacketCapture**. Hallo volgende Schermafbeelding toont een configuratie waarmee TCP-verkeer voor Hallo IP-adressen van drie opslagservices gefilterd:

![][10]

Zie voor meer informatie over Microsoft Message Analyzer lokale Link-laag trace Hallo [Provider van Microsoft-PEF-NDIS-PacketCapture](http://technet.microsoft.com/library/jj659264.aspx).

### <a name="appendix-4"></a>Bijlage 4: Tooview Excel-gegevens metrische gegevens en logboekbestanden gebruiken
Veel hulpprogramma's kunnen u toodownload Hallo opslag metrische gegevens uit Azure-tabelopslag in een gescheiden indeling die maakt het eenvoudig tooload Hallo gegevens in Excel voor weer te geven en analyse. Logboekgegevens van de opslag van Azure blob-opslag is al een gescheiden indeling die u in Excel laden kunt. U moet echter tooadd juiste kolomkoppen op basis van informatie op Hallo [Storage Analytics logboekindeling](http://msdn.microsoft.com/library/azure/hh343259.aspx) en [Storage Analytics metrische gegevens tabelschema](http://msdn.microsoft.com/library/azure/hh343264.aspx).

tooimport uw opslag logboekregistratie gegevens in Excel nadat u dit downloaden van blob-opslag:

* Op Hallo **gegevens** menu, klikt u op **van tekst**.
* Bladeren toohello logboekbestand tooview en klik op **importeren**.
* In stap 1 van Hallo **Wizard Tekst importeren**, selecteer **gescheiden**.

In stap 1 van Hallo **Wizard Tekst importeren**, selecteer **puntkomma** als enige scheidingsteken Hallo en kiest u dubbele aanhalingstekens als Hallo **tekstscheidingsteken**. Klik vervolgens op **voltooien** en kies waar tooplace Hallo gegevens in uw werkmap.

### <a name="appendix-5"></a>Bijlage 5: Bewaking met Application Insights voor Visual Studio teamservices
U kunt ook Hallo Application Insights-functie voor Visual Studio Team Services gebruiken als onderdeel van de beschikbaarheidsbewaking van prestaties en. Dit hulpprogramma kunt doen:

* Zorg ervoor dat uw web-service beschikbaar is en reageert. Of uw app is een website of een apparaat-app die gebruikmaakt van een webservice, kunt u uw URL om de paar minuten testen vanaf locaties Hallo wereld en laat u weten of er een probleem is.
* Analyseer snel eventuele prestatieproblemen of uitzonderingen in uw webservice. Ontdek als CPU of andere bronnen worden uitgerekt, krijgen die stack-traces van uitzonderingen en eenvoudig doorzoeken logboektraceringen. Als hello van app prestaties aansluitingen hieronder acceptabele grenzen, we kunnen u een e-mail sturen. U kunt zowel .NET en Java-web-services bewaken.

U vindt meer informatie op [wat is Application Insights?](../application-insights/app-insights-overview.md).

<!--Anchors-->
[Inleiding]: #introduction
[Rangschikking van deze handleiding]: #how-this-guide-is-organized

[bewaking van uw opslagservice]: #monitoring-your-storage-service
[Bewaking servicestatus]: #monitoring-service-health
[Bewaking van capaciteit]: #monitoring-capacity
[Controleprogramma beschikbaarheid]: #monitoring-availability
[Prestaties bewaken]: #monitoring-performance

[diagnose van opslagproblemen]: #diagnosing-storage-issues
[Health service-problemen]: #service-health-issues
[Prestatieproblemen]: #performance-issues
[Fouten opsporen]: #diagnosing-errors
[Emulator opslagproblemen]: #storage-emulator-issues
[Logboekregistratieprogramma's voor opslag]: #storage-logging-tools
[Met behulp van hulpprogramma's voor logboekregistratie]: #using-network-logging-tools

[End-to-end tracering]: #end-to-end-tracing
[Logboekgegevens correleren]: #correlating-log-data
[Aanvraag-ID van client]: #client-request-id
[Server aanvraag-ID]: #server-request-id
[Tijdstempels]: #timestamps

[richtlijnen voor probleemoplossing]: #troubleshooting-guidance
[metrische gegevens tonen AverageE2ELatency hoge en lage AverageServerLatency]: #metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency
[Metrische gegevens tonen lage AverageE2ELatency en lage AverageServerLatency maar Hallo client ondervindt hoge latentie]: #metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency
[Prestatiegegevens geven hoge AverageServerLatency aan]: #metrics-show-high-AverageServerLatency
[U ervaart onverwachte vertragingen bij de levering van berichten in een wachtrij]: #you-are-experiencing-unexpected-delays-in-message-delivery

[metrische gegevens tonen een toename in PercentThrottlingError]: #metrics-show-an-increase-in-PercentThrottlingError
[Tijdelijke toename van PercentThrottlingError]: #transient-increase-in-PercentThrottlingError
[Permanente toename PercentThrottlingError fout]: #permanent-increase-in-PercentThrottlingError
[metrische gegevens tonen een toename in PercentTimeoutError]: #metrics-show-an-increase-in-PercentTimeoutError
[Prestatiegegevens geven een toename in PercentNetworkError aan]: #metrics-show-an-increase-in-PercentNetworkError

[Hallo client ontvangt berichten HTTP 403 (verboden)]: #the-client-is-receiving-403-messages
[Hallo-client is ontvangen HTTP 404 (niet gevonden)-berichten]: #the-client-is-receiving-404-messages
[Hallo-client of een ander proces het eerder verwijderd Hallo-object]: #client-previously-deleted-the-object
[Een probleem met de autorisatie Shared Access Signature (SAS)]: #SAS-authorization-issue
[Client-side JavaScript-code heeft geen machtiging tooaccess Hallo-object]: #JavaScript-code-does-not-have-permission
[Netwerkfout]: #network-failure
[Hallo client ontvangt berichten van de HTTP-409 (Conflict)]: #the-client-is-receiving-409-messages

[metrische gegevens tonen lage PercentSuccess of analytics logboekvermeldingen bewerkingen hebben met transactiestatus ClientOtherErrors]: #metrics-show-low-percent-success
[Capaciteit metrische gegevens tonen een onverwachte toename in opslaggebruik capaciteit]: #capacity-metrics-show-an-unexpected-increase
[Er is sprake van virtuele Machines met een groot aantal gekoppelde VHD's onverwacht opnieuw wordt opgestart]: #you-are-experiencing-unexpected-reboots
[Het probleem zich voordoet Hallo-opslagemulator gebruiken voor ontwikkeling of tests]: #your-issue-arises-from-using-the-storage-emulator
[Functie 'X' werkt niet in de opslagemulator Hallo]: #feature-X-is-not-working
[Fout 'Hallo-waarde van een Hallo HTTP-headers is niet de juiste indeling Hallo' wanneer met behulp van Hallo-opslagemulator]: #error-HTTP-header-not-correct-format
[Actieve Hallo opslagemulator vereist beheerdersbevoegdheden]: #storage-emulator-requires-administrative-privileges
[U ondervindt problemen met het installeren van hello Azure SDK voor .NET]: #you-are-encountering-problems-installing-the-Windows-Azure-SDK
[U hebt een ander probleem met storage-service]: #you-have-a-different-issue-with-a-storage-service

[bijlagen]: #appendices
[bijlage 1: met behulp van HTTP en HTTPS-verkeer van toocapture Fiddler]: #appendix-1
[bijlage 2: Wireshark toocapture netwerkverkeer met]: #appendix-2
[bijlage 3: met behulp van Microsoft Message Analyzer toocapture netwerkverkeer]: #appendix-3
[Bijlage 4: Tooview Excel-gegevens metrische gegevens en logboekbestanden gebruiken]: #appendix-4
[Bijlage 5: Bewaking met Application Insights voor Visual Studio teamservices]: #appendix-5

<!--Image references-->
[1]: ./media/storage-monitoring-diagnosing-troubleshooting/overview.png
[3]: ./media/storage-monitoring-diagnosing-troubleshooting/hour-minute-metrics.png
[4]: ./media/storage-monitoring-diagnosing-troubleshooting/high-e2e-latency.png
[5]: ./media/storage-monitoring-diagnosing-troubleshooting/fiddler-screenshot.png
[6]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-1.png
[7]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-2.png
[8]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-3.png
[9]: ./media/storage-monitoring-diagnosing-troubleshooting/mma-screenshot-1.png
[10]: ./media/storage-monitoring-diagnosing-troubleshooting/mma-screenshot-2.png
