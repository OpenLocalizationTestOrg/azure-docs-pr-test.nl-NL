
# <a name="azure-and-internet-of-things"></a>Azure en internet der dingen (IoT)

Welkom bij Azure tooMicrosoft en Hallo Internet der dingen (IoT). Dit artikel bevat een IoT-oplossingsarchitectuur die beschrijft Hallo algemene eigenschappen van een IoT-oplossing die u kunt implementeren met behulp van Azure-services. IoT-oplossingen vereisen bidirectionele communicatie tussen apparaten, mogelijk nummering in hello miljoenen en een back-end oplossing beveiligen. Bijvoorbeeld, een back-end oplossing geautomatiseerde, voorspellende analyses toouncover insights gebruiken van de gebeurtenisstroom van uw apparaat-naar-cloud.

Azure IoT Hub is een essentiële bouwsteen bij de implementatie van de architectuur voor deze IoT-oplossing met behulp van Azure-services. IoT Suite biedt volledige end-to-end-implementaties van deze architectuur voor specifieke IoT-scenario's. Bijvoorbeeld:

* Hallo *externe controle* oplossing kunt u toomonitor Hallo status van apparaten, zoals snoep-machines.
* Hallo *voorspeld onderhoud* oplossing kunt u tooanticipate onderhoudsbehoeften van apparaten zoals pompen in externe gemalen stations en tooavoid ongeplande downtime.
* Hallo *verbonden factory* oplossing helpt u bij tooconnect en controleer uw industriële apparaten.

## <a name="iot-solution-architecture"></a>Architectuur voor een IoT-oplossing

Hallo volgende diagram toont de architectuur van een typische IoT-oplossing. Hallo diagram omvat geen Hallo namen van specifieke Azure-services, maar beschrijft de belangrijkste elementen in een algemene IoT-oplossingsarchitectuur Hallo. In deze architectuur verzamelen IoT-apparaten gegevens dat ze tooa cloudgateway verzenden. Hallo cloudgateway maakt Hallo gegevens beschikbaar voor verwerking door andere back-end-services uit waarbij gegevens geleverd tooother line-of-business-toepassingen of toohuman operators via een dashboard of een ander apparaat voor presentatie.

![Architectuur voor een IoT-oplossing][img-solution-architecture]

> [!NOTE]
> Zie voor een gedetailleerdere beschrijving van IoT-architectuur Hallo [Microsoft Azure IoT Reference Architecture][lnk-refarch].

### <a name="device-connectivity"></a>Connectiviteit van apparaten

In deze architectuur IoT-oplossing verzenden apparaten telemetriegegevens, zoals sensormetingen van een gemaal, tooa cloudeindpunt voor opslag en verwerking. In een scenario voor voorspeld onderhoud Hallo back-end oplossing Hallo stroom van sensor gegevens toodetermine gebruiken wanneer een pomp onderhoud moet. Apparaten kunnen ook ontvangen en toocloud naar apparaat-berichten door te lezen van berichten van een cloudeindpunt reageren. Bijvoorbeeld in Hallo voorspeld onderhoud scenario Hallo oplossing back-end mogelijk berichten verzenden tooother pompen in Hallo pompen station toobegin omleiden van de stromen vlak voordat de onderhoudswerkzaamheden toostart. Deze procedure zorgt ervoor Hallo onderhoudstechnicus kan aan de slag als hij aankomt.

Een van de grootste uitdagingen Hallo geconfronteerd met IoT-projecten is hoe tooreliably en veilig verbinding apparaten toohello back-end oplossing. IoT-apparaten hebben verschillende kenmerken als vergeleken tooother clients zoals browsers en mobiele apps. IoT-apparaten:

* Zijn vaak ingesloten systemen waarbij geen menselijke operator komt kijken.
* Kunnen worden geïmplementeerd op verafgelegen locaties, waar fysieke toegang kostbaar is.
* Kan alleen worden bereikt via Hallo back-end oplossing. Er is geen andere manier toointeract met Hallo-apparaat.
* Hebben mogelijk een beperkt vermogen en een beperkt aantal verwerkingsbronnen.
* Hebben mogelijk een onstabiele, trage of dure netwerkverbinding.
* Mogelijk moet toouse bedrijfseigen, aangepaste of branchespecifieke toepassingsprotocollen.
* Kunnen worden gemaakt met behulp van een groot aantal populaire hardware- en softwareplatforms.

Bovendien toohello bovenstaande vereisten een IoT-oplossing moet ook leveren schaal, beveiliging en betrouwbaarheid. Hallo is resulterende reeks connectiviteitsvereisten moeilijk en tijdrovend tooimplement met behulp van conventionele technologieën zoals webcontainers en berichtenbrokers. Azure IoT Hub en Hallo Azure IoT-apparaat-SDK's kunt eenvoudiger tooimplement oplossingen die aan deze vereisten voldoet.

Een apparaat kan communiceren rechtstreeks met het eindpunt van een cloudgateway of als het Hallo-apparaat kan Hallo communicatieprotocollen die Hallo cloud gateway ondersteunt niet gebruiken, deze verbinding kan maken via een tussenliggende gateway. Bijvoorbeeld, Hallo [protocolgateway van Azure IOT] [ lnk-protocol-gateway] protocolvertaling kunt uitvoeren als apparaten kunnen Hallo-protocollen die IoT Hub worden ondersteund niet gebruiken.

### <a name="data-processing-and-analytics"></a>Gegevensverwerking en -analyse

In de cloud hello is een IoT-oplossing back-end waar de meeste Hallo gegevensverwerking optreedt, zoals filteren en samenvoegen van telemetriegegevens en routeringservices in het tooother. Hallo IoT back-end oplossing:

* Ontvangt telemetrie op schaal van uw apparaten en bepaalt hoe tooprocess en op te slaan die gegevens. 
* Mogelijk kunt u de opdrachten toosend uit Hallo cloud toospecific apparaat.
* Biedt mogelijkheden voor het apparaat registreren waarmee u tooprovision apparaten en toocontrol welke apparaten tooconnect tooyour infrastructuur zijn toegestaan.
* Hiermee schakelt u tootrack Hallo status van uw apparaten en hun activiteiten bewaken.

In scenario voor voorspeld onderhoud Hallo opgeslagen Hallo back-end oplossing historische telemetriegegevens. Hallo back-end oplossing kunt gebruiken deze gegevens toouse tooidentify patronen die aangeven dat onderhoud van een specifieke pomp noodzakelijk.

IoT-oplossingen kunnen automatische feedbacklussen omvatten. Bijvoorbeeld, kan een analysemodule in Hallo back-end oplossing identificeren uit telemetrie die Hallo temperatuur van een specifiek apparaat hoger dan de normale bedrijfstemperatuurniveaus is. Hallo oplossing kunt vervolgens een opdracht toohello apparaat, instructie tootake corrigerende maatregelen verzenden.

### <a name="presentation-and-business-connectivity"></a>Presentatie en bedrijfsconnectiviteit

Hallo presentatie en connectiviteit laag kan eindgebruikers toointeract Hello IoT-oplossing en Hallo-apparaten. Deze kunnen gebruikers tooview en analyseren van Hallo gegevens verzameld vanaf hun apparaten. Deze weergaven kunnen Hallo vorm van dashboards of BI-rapporten die zowel historische gegevens kunnen weergeven of gegevens in bijna realtime krijgen. Bijvoorbeeld, een operator Hallo status van bepaald gemaal controleren en Zie eventueel waarschuwingen heeft gegeven Hallo-systeem. Deze laag maakt ook integratie van Hallo IoT back-end oplossing met bestaande line-of-business-toepassingen tootie in bedrijfsprocessen of werkstromen. Bijvoorbeeld, kunt Hallo-oplossing voor voorspeld onderhoud integreren met een werkroostersysteem dat books een technicus toovisit gemaal als Hallo oplossing een pomp waaraan onderhoud identificeert.

![Dashboard van de IoT-oplossing][img-dashboard]

[img-solution-architecture]: ./media/iot-azure-and-iot/iot-reference-architecture.png
[img-dashboard]: ./media/iot-azure-and-iot/iot-suite.png

[lnk-machinelearning]: http://azure.microsoft.com/documentation/services/machine-learning/
[Azure IoT Suite]: http://azure.microsoft.com/solutions/iot
[lnk-protocol-gateway]:  ../articles/iot-hub/iot-hub-protocol-gateway.md
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
