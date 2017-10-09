# <a name="internet-of-things-security-architecture"></a>Internet der dingen-beveiligingsarchitectuur
Bij het ontwerpen van een systeem is belangrijk toounderstand Hallo mogelijke bedreigingen toothat systeem en dienovereenkomstig juiste beveiliging niet toevoegen als Hallo system is ontworpen en ontworpen. Het is vooral belangrijk toodesign Hallo product van Hallo begin rekening met beveiliging omdat informatie over hoe een hacker mogelijk kunnen toocompromise een systeem zorgt ervoor geschikt oplossingen zijn in plaats van Hallo begin. 

## <a name="security-starts-with-a-threat-model"></a>Beveiliging begint met een risicomodel
Microsoft heeft lang threat modellen gebruikt voor de producten en van het bedrijf Hallo threat modeling proces openbaar beschikbaar heeft gesteld. Hallo bedrijf ervaring laat zien dat Hallo modellering heeft onverwachte voordelen na Hallo direct inzicht in welke bedreigingen Hallo zijn de meeste betreffende. Bijvoorbeeld, maakt het ook een avenue voor een open discussie met anderen buiten Hallo ontwikkelingsteam, wat toonew ideeën en verbeteringen in Hallo product leiden kan.

Hallo-doel van risicomodel is toounderstand hoe een aanvaller mogelijk kunnen toocompromise een systeem en controleer vervolgens of de juiste oplossingen zijn geïnstalleerd. Risicomodel forceert Hallo ontwerp team tooconsider oplossingen zoals Hallo systeem is ontworpen in plaats van na de implementatie van een systeem. Dit is zeer belangrijk omdat met terugwerkende kracht beveiliging verdediging tooa talloze apparaten in het veld Hallo onbruikbare, foutgevoelig en laat klanten risico.

Veel ontwikkelteams doen een uitstekende taak vastleggen Hallo functionele vereisten voor Hallo system die profiteren van klanten. Identificeren van niet-duidelijk manieren dat iemand Hallo system mogelijk misbruik is echter moeilijker. Risicomodel kunt ontwikkelteams begrijpen wat een aanvaller kan doen en waarom. Risicomodel is een gestructureerde proces waarbij een discussie over de beveiliging van Hallo ontwerpbeslissingen maakt in het Hallo-systeem, evenals wijzigingen toohello ontwerp die zijn aangebracht langs Hallo manier die van invloed beveiliging. Hoewel een risicomodel gewoon een document is, vertegenwoordigt deze documentatie ook een ideaal manier tooensure continuïteit van de retentie van opgedane kennis hebt geleerd, en helpen vrijgeven nieuw team snel. Ten slotte een resultaat van risicomodel tooenable is tooconsider u andere aspecten van beveiliging, zoals welke beveiligingsverplichtingen u tooprovide tooyour klanten wenst. Deze verplichtingen in combinatie met risicomodel wordt kennis en station testen van uw oplossing voor het Internet der dingen (IoT).

### <a name="when-toothreat-model"></a>Wanneer toothreat model
[Risicomodel](http://www.microsoft.com/security/sdl/adopt/threatmodeling.aspx) aanbiedingen Hallo grootste waarde als het in de ontwerpfase Hallo is verwerkt. Wanneer u ontwerpt, hebt u Hallo grootste flexibiliteit toomake wijzigingen tooeliminate bedreigingen. Bedreigingen elimineren standaard is het gewenste resultaat Hallo. Het is veel eenvoudiger dan beperkingen toe te voegen, deze testen en blijven ze actueel blijven en bovendien die verwijdering is niet altijd mogelijk. Wordt het moeilijker tooeliminate bedreigingen zoals een product meer wordt volwassen en op zijn beurt uiteindelijk waarvoor meer werk en veel moeilijker voor-en nadelen dan threat modeling vroeg stadium in Hallo-ontwikkeling.

### <a name="what-toothreat-model"></a>Welke toothreat-model
U moet thread-model Hallo oplossing als een geheel en ook focus in Hallo gebieden te volgen:

* Hallo-beveiliging en privacy-functies
* Hallo-functies waarvoor fouten beveiliging relevante zijn
* Hallo-functies die grens van een vertrouwensrelatie touch 

### <a name="who-threat-models"></a>Wie dreiging modellen
Risicomodel is een proces zoals elke andere.  Het is een goed idee tootreat Hallo threat modeldocument zoals elk ander onderdeel van de oplossing Hallo en te valideren. Veel ontwikkelteams doen een uitstekende taak vastleggen Hallo functionele vereisten voor Hallo system die profiteren van klanten. Identificeren van niet-duidelijk manieren dat iemand Hallo system mogelijk misbruik is echter moeilijker. Risicomodel kunt ontwikkelteams begrijpen wat een aanvaller kan doen en waarom.

### <a name="how-toothreat-model"></a>Hoe toothreat model
Hallo threat modeling proces bestaat uit vier stappen; Hallo stappen zijn:

* Model Hallo-toepassing
* Bedreigingen opsommen
* Bedreigingen te verhelpen
* Hallo oplossingen valideren

#### <a name="hello-process-steps"></a>Hallo processtappen
Drie regels van miniatuur tookeep rekening moet houden bij het bouwen van een risicomodel:

1. Diagram van een buiten-referentiearchitectuur maken. 
2. Breedte eerst worden gestart. Krijgt u een overzicht en Hallo systeem als geheel deep wilt voordat begrijpen.  Dit zorgt ervoor dat u dieper in de juiste hello wordt geplaatst.
3. Hallo proces schijf, laat u station Hallo-proces niet. Als u een probleem niet vinden in Hallo fase modelleren en tooexplore wilt Ga hiervoor!  Niet van mening bent dat u moet de toofollow deze stappen slavishly.  

#### <a name="threats"></a>Bedreigingen
Hallo vier core elementen van een risicomodel zijn:

* Processen (webservices, Win32-services, * nix daemons, enzovoort. Houd er rekening mee dat sommige complexe entiteiten (bijvoorbeeld veld gateways en sensoren) kunnen worden gescheiden, zoals een proces wanneer een technische Inzoomen op in de volgende gebieden niet mogelijk is.
* Gegevens worden opgeslagen (anywhere gegevens worden opgeslagen, zoals een configuratiebestand of de database)
* Gegevensstroom (waarbij gegevens worden verplaatst tussen andere elementen in de toepassing hello)
* Externe entiteiten (Alles die communiceert met Hallo-systeem, maar is niet onder het beheer van de toepassing hello hello, zijn bijvoorbeeld gebruikers en feeds satelliet)

Alle elementen in het architectuurdiagram Hallo zijn onderwerp toovarious bedreigingen; Hallo STRIDE verkorte weergave zullen worden gebruikt. Lees [Threat Modeling opnieuw, STRIDE](https://blogs.msdn.microsoft.com/larryosterman/2007/09/04/threat-modeling-again-stride/) tooknow meer over Hallo STRIDE elementen.

Andere elementen van Hallo toepassing diagram zijn onderwerp toocertain STRIDE bedreigingen:

* Processen zijn onderwerp tooSTRIDE
* Gegevensstromen zijn onderwerp tooTID
* Opgeslagen gegevens zijn onderwerp tooTID en soms op R, als Hallo gegevensarchieven logboekbestanden.
* Externe entiteiten zijn onderwerp tooSRD

## <a name="security-in-iot"></a>Beveiliging in IoT
Verbonden speciale apparaten hebben een groot aantal potentiële surface gebieden van interactie en interactie patronen, die allemaal tooprovide een framework voor het beveiligen van digitale toegang toothose apparaten moet worden beschouwd. Hallo term 'digitale toegang' is gebruikte hier toodistinguish van bewerkingen die worden uitgevoerd via directe apparaatinteractie indien toegangsbeveiliging via beheer op fysieke toegang wordt verleend. Als bijvoorbeeld Hallo apparaat in een ruimte met een vergrendeling op Hallo deur. Hoewel fysieke toegang kan niet worden geweigerd met behulp van software en hardware, te maatregelen nemen tooprevent fysieke toegang van toonaangevende toosystem storing. 

Omdat we Hallo interactie patronen verkennen, kijken we 'apparaat control' en 'apparaatgegevens' met dezelfde mate van aandacht Hallo. 'Apparaat control' kan worden geclassificeerd als alle informatie die met Hallo doel van het wijzigen van of het gedrag van het naar de staat of de Hallo staat van de omgeving invloed tooa apparaat wordt geleverd door een partij. 'Apparaatgegevens' kunnen worden geclassificeerd als alle informatie op dat een apparaat tooany andere partij over de status en Hallo waargenomen status van de omgeving verzendt.

In de volgorde toooptimize best practices voor beveiliging, wordt het aanbevolen dat een typische IoT-architectuur in verschillende onderdeel/zones worden verdeeld als onderdeel van Hallo threat modeling oefening. Deze zones volledig in deze sectie worden beschreven, en omvatten:

* Apparaat
* Veldgateway
* Cloud gateways, en
* Services.

Zones zijn brede manier toosegment een oplossing. elke zone heeft vaak een eigen gegevens en verificatie en autorisatie-vereisten. Zones kunnen ook worden gebruikt tooisolation beschadigen en Hallo gevolgen van het lage vertrouwensrelatie zones op hoger vertrouwen zones te beperken.

Elke zone wordt gescheiden door een grens vertrouwen die wordt vermeld als Hallo rode lijn in het onderstaande diagram kunt Hallo scheidingspunten. Deze vertegenwoordigt een migratie van gegevens van/vanuit één bron tooanother. Tijdens deze overgang mogelijk Hallo gegevens onderwerp tooSpoofing, Tampering, Repudiation, Information Disclosure, Denial of Service en verhoging van bevoegdheden (STRIDE).

![IoT-beveiligingszones](media/iot-security-architecture/iot-security-architecture-fig1.png) 

Hallo onderdelen afgebeeld binnen elke grens zijn ook ondergaan tooSTRIDE, het inschakelen van een volledige 360 threat modeling weergave van Hallo-oplossing. de volgende secties voor Hallo uitwerken op elk Hallo-onderdelen en specifieke beveiligingsproblemen en oplossingen die moeten worden ingesteld.

Hallo-secties die volgt behandeld standaardonderdelen gewoonlijk in deze zones.

### <a name="hello-device-zone"></a>Hallo apparaat Zone
Hallo apparaat-omgeving is Hallo onmiddellijke fysieke ruimte rond Hallo apparaat waar fysieke toegang en/of 'lokale netwerk' peer-to-peer digitale toegang krijgen toohello tot apparaat haalbaar is. 'Lokale netwerk' wordt aangenomen dat toobe een netwerk dat is uniek en geïsoleerd van – maar bevat beperkt bereik draadloze radio-technologie waarmee peer-to-peer-communicatie van apparaten mogelijk te – hello openbare Internet overbrugd. Dit gebeurt *niet* bevatten netwerk virtualisatietechnologie Hallo illusie van een lokaal netwerk maken en deze ook bevat geen openbare operator-netwerken die toocommunicate twee apparaten op openbaar netwerk ruimte vereisen Als ze tooenter een peer-to-peer-communicatie relatie waren.

### <a name="hello-field-gateway-zone"></a>Hallo veld Gateway Zone
Veldgateway is een apparaat/apparaat of bepaalde server voor computersoftware die als communicatie factor en potentieel als een apparaat besturingselement systeem en het apparaat gegevensverwerking hub fungeert. Hallo veld gateway zone bevat Hallo veldgateway zelf en alle apparaten die zijn gekoppeld tooit. Zoals Hallo-naam aangeeft, veld gateways buiten toegewezen gegevensverwerking faciliteiten fungeren, meestal locatie gebonden, worden mogelijk onderwerp toophysical inbraakdetectie en operationele redundantie wordt beperkt. Alle toosay die een veldgateway is meestal een ding een kan touch en sabotage achterhoofd wat de functie is. 

Een veldgateway wijkt af van een router alleen verkeer in dat deze een actieve rol bij het beheren van toegang heeft gehad en informatiestromen, wat betekent dat een toepassing is verholpen entiteit en de netwerkverbinding of terminal-sessie. Een NAT-apparaat of de firewall, in tegenstelling komen niet in aanmerking als veld gateways omdat ze zijn geen expliciete verbinding of sessie aansluitingen, maar in plaats daarvan een route (of blok)-verbindingen of tot stand gebracht via deze sessies. Hallo veldgateway heeft twee verschillende surface gebieden. Een bespreekt Hallo-apparaten die aangesloten tooit zijn Hallo binnen Hallo zone vertegenwoordigt en Hallo andere bespreekt alle externe partijen is Hallo rand van Hallo zone.   

### <a name="hello-cloud-gateway-zone"></a>Hallo cloud gateway zone
Cloudgateway is een systeem waarmee externe communicatie van en toodevices of veld gateways uit diverse verschillende sites in de ruimte openbaar netwerk, meestal naar een cloud-gebaseerde beheer- en analyse systeem, een federatieve van dergelijke systemen. In sommige gevallen kan een cloudgateway onmiddellijk toegang toospecial doel apparaten uit aansluitingen zoals tablets en telefoons vergemakkelijken. Hier 'cloud' bedoeld toorefer tooa dedicated gegevensverwerkingssysteem is niet gebonden toohello dezelfde site als Hallo apparaten of gateways veld gekoppelde in de context van Hallo besproken. Ook in een Zone Cloud operationele maatregelen te voorkomen dat bepaalde fysieke toegang en niet per se blootgestelde tooa 'openbare cloud'-infrastructuur.  

Een cloudgateway kan mogelijk worden toegewezen aan een overlay tooinsulate Hallo cloud netwerkvirtualisatiegateway en alle bijbehorende gekoppelde apparaten of veld gateways van ander netwerkverkeer. Hallo cloudgateway zelf is noch een controlesysteem apparaat, noch een verwerking of opslagfaciliteit voor gegevens van apparaten; deze interface faciliteiten met Hallo cloudgateway. Hallo cloud gateway zone omvat Hallo cloudgateway zelf samen met alle veld gateways en apparaten direct of indirect tooit gekoppeld. Hallo-edge van Hallo zone is een afzonderlijke oppervlak waar alle externe partijen via communiceren.

### <a name="hello-services-zone"></a>Hallo services zone
Een 'service' is gedefinieerd voor deze context als alle software-onderdelen of module die in aanraking met apparaten via een gateway veld- of cloud voor gegevensverzameling en -analyse, evenals voor opdracht en controle komt.  Services worden tussenstation. Ze onder hun identiteit naar gateways en andere subsystemen fungeren, opslaan en analyseren van gegevens, autonoom probleem opdrachten toodevices op basis van gegevens insights of schema's en informatie en controle mogelijkheden tooauthorized eindgebruikers weer te geven.

### <a name="information-devices-vs-special-purpose-devices"></a>Informatie-apparaten en apparaten voor speciale doeleinden
Pc's, telefoons en tablets zijn voornamelijk interactieve informatie-apparaten. Telefoons en tablets zijn expliciet rond het optimaliseren van de levensduur van de batterij geoptimaliseerd. Ze bij voorkeur uitschakelen gedeeltelijk wanneer niet direct communiceert met een persoon, of wanneer niet tooa bepaalde locatie biedt services zoals muziek afspelen of begeleiden van hun eigenaar. Vanuit het oogpunt van systemen van fungeren deze technologie informatie apparaten hoofdzakelijk als proxy's naar mensen. Ze zijn 'mensen actuators' voorstellen acties en 'mensen sensoren' verzamelen van de invoer. 

Apparaten voor speciale doeleinden zijn van eenvoudige temperatuur sensoren toocomplex factory productie regels met duizenden onderdelen in deze, verschillend. Deze apparaten zijn veel meer bereik in het doel en zelfs als ze een gebruikersinterface bieden, ze grotendeels bereik toointerfacing met zijn of activa in de fysieke wereld Hallo worden geïntegreerd. Ze meten en rapporteren milieu omstandigheden, kleppen inschakelen servos beheren, alarmen geluid, switch lichten en veel andere taken uitvoeren. Ze helpen toodo werken waarvoor een apparaat informatie te algemeen, te duur, te groot of te brokkelig is. Hallo concrete doel bepaalt het technische ontwerp onmiddellijk als goed Hallo beschikbaar financieel budget voor hun productie en de levensduur van de geplande bewerking. Hallo combinatie van deze twee belangrijke factoren handtekeningcertificaatsleutel Hallo beschikbaar operationele energie budget, fysieke footprint en dus beschikbare opslag, rekencapaciteit en -mogelijkheden.  

Als er iets 'gaan verkeerde' automatisch of externe instelbare apparaten bijvoorbeeld fysieke defecte producten of besturingselement logica defecte producten toowillful niet-geautoriseerde inbraakdetectie en manipuleren. Hallo productie veel mogelijk worden vernietigd, gebouwen mogelijk looted of gebrand omlaag en personen gewonde of zelfs die mogelijk zijn. Dit is natuurlijk een geheel andere klasse van de schade dan iemand bezetten een gestolen creditcard limiet. Hallo beveiligingsbalk voor apparaten die zo zijn verplaatst en ook voor sensorgegevens dat uiteindelijk resultaten in opdrachten die ertoe leiden dingen toomove dat, moet hoger zijn dan in een e-commerce of scenario voor bankieren. 

### <a name="device-control-and-device-data-interactions"></a>Apparaatbeheer en -interacties van apparaat-gegevens
Verbonden speciale apparaten hebben een groot aantal potentiële surface gebieden van interactie en interactie patronen, die allemaal tooprovide een framework voor het beveiligen van digitale toegang toothose apparaten moet worden beschouwd. Hallo term 'digitale toegang' is gebruikte hier toodistinguish van bewerkingen die worden uitgevoerd via directe apparaatinteractie indien toegangsbeveiliging via beheer op fysieke toegang wordt verleend. Als bijvoorbeeld Hallo apparaat in een ruimte met een vergrendeling op Hallo deur. Hoewel fysieke toegang kan niet worden geweigerd met behulp van software en hardware, te maatregelen nemen tooprevent fysieke toegang van toonaangevende toosystem storing. 

Omdat we Hallo interactie patronen verkennen, kijken we 'apparaat control' en 'apparaatgegevens' met dezelfde mate van aandacht tijdens risicomodel Hallo. 'Apparaat control' kan worden geclassificeerd als alle informatie die met Hallo doel van het wijzigen van of het gedrag van het naar de staat of de Hallo staat van de omgeving invloed tooa apparaat wordt geleverd door een partij. 'Apparaatgegevens' kunnen worden geclassificeerd als alle informatie op dat een apparaat tooany andere partij over de status en Hallo waargenomen status van de omgeving verzendt. 

## <a name="threat-modeling-hello-azure-iot-reference-architecture"></a>Threat modeling hello Azure IoT reference architecture
Hallo-framework bovenstaande toodo threat modellering voor Azure IoT maakt gebruik van Microsoft. In onderstaande Hallo sectie gebruiken we daarom Hallo concrete voorbeeld van Azure IoT Reference Architecture toodemonstrate hoe toothink over de bedreiging modellering voor IoT en hoe tooaddress bedreigingen Hallo aangeduid. In ons geval geïdentificeerd we vier gebieden van de focus:

* Apparaten en gegevensbronnen,
* Data-Transport
* Apparaat en de verwerking van gebeurtenissen en
* Presentatie

![Threat Modeling voor Azure IoT](media/iot-security-architecture/iot-security-architecture-fig2.png) 

Hallo diagram hieronder biedt een vereenvoudigde weergave van de IoT-architectuur van Microsoft die gebruikmaken van een gegevensstroom-Diagram model dat wordt gebruikt door Hallo Microsoft Threat Modeling Tool:

![Threat Modeling voor Azure IoT met MS Threat Modeling hulpprogramma](media/iot-security-architecture/iot-security-architecture-fig3.png)

Het is belangrijk toonote die architectuur Hallo scheidt Hallo apparaat en de gateway-mogelijkheden. Hierdoor kunnen Hallo gebruiker tooleverage gatewayapparaten die veiliger zijn: kan communiceren met de Hallo cloudgateway met behulp van veilige protocollen hiervoor meestal groter verwerkingsoverhead dat een systeemeigen apparaat - zoals een thermostaat - kan zijn Geef op de eigen. In de zone van de Azure-services Hallo, gaan we ervan uit dat Hallo die cloudgateway wordt vertegenwoordigd door Hallo service Azure IoT Hub.

### <a name="device-and-data-sourcesdata-transport"></a>Apparaat- en bronnen/data-transport
Deze sectie behandelt die hierboven worden beschreven door Hallo lens van risicomodel Hallo-architectuur en een overzicht van hoe we enkele van de intrinsieke zorgen Hallo adresseert. Gaan we in op Hallo core elementen van een risicomodel:

* Processen (die in onze besturingselement en externe items)
* Communicatie (ook wel gegevensoverdrachten)
* Opslag (ook wel gegevensarchieven)

#### <a name="processes"></a>Processen
In elk van de Hallo categorieën die worden beschreven in hello Azure IoT-architectuur die we proberen een aantal verschillende bedreigingen in verschillende fasen/gegevens Hallo bestaat in toomitigate: proces, communicatie en opslag. Hieronder wordt een overzicht geven van Hallo meestgebruikte voor Hallo 'proces' categorie, gevolgd door een overzicht van hoe deze kunnen worden beste verholpen: 

**Adresvervalsing (spoofing) (S)**: een aanvaller kan cryptografische sleutelmateriaal extraheren uit een apparaat, hetzij op Hallo software of hardware niveau en vervolgens toegang krijgen tot Hallo-systeem met een ander fysiek of virtueel apparaat onder de identiteit Hallo Hallo apparaat Hallo sleutelmateriaal is onttrokken. Een goede illustratie is extern besturingselementen die elke TV kunt inschakelen en die populaire prankster hulpprogramma's zijn.

**Denial of Service (D)**: een apparaat kan worden gerenderd waarvoor niet werkt of communiceren door interactie aangaan met keuzerondjes frequenties of knippen bedrading. Bijvoorbeeld, rapporteert een toezicht camera die de stroom of netwerk verbinding opzettelijk toenemende had niet gegevens, op alle.

**Manipulatie (T)**: een aanvaller kan geheel of gedeeltelijk vervangen Hallo software op Hallo apparaat uitvoeren, waardoor Hallo vervangen software tooleverage Hallo legitieme identiteit van het Hallo-apparaat als hello sleutel materiaal of Hallo cryptografische sleutel materialen houden faciliteiten zijn beschikbaar toohello illegale programma. Bijvoorbeeld kan een aanvaller gebruikmaken van de uitgepakte sleutel wezenlijke toointercept en gegevens van het apparaat op Hallo communicatiepad Hallo onderdrukken en vervang deze door false gegevens die is geverifieerd met sleutelmateriaal Hallo gestolen.

**Vrijgeven van informatie (I)**: als het apparaat Hallo gezelschapsdieren software wordt uitgevoerd, dergelijke gezelschapsdieren software gegevens toounauthorized partijen kan mogelijk lekken. Een aanvaller kan bijvoorbeeld gebruikmaken van de uitgepakte sleutel wezenlijke tooinject zelf in Hallo communicatiepad tussen Hallo-apparaat en een controller- of -gateway of cloud gateway toosiphon uitschakelen informatie.

**Uitbreiding van bevoegdheden (E)**: een apparaat dat specifieke functie uitvoert kan geforceerde toodo iets anders zijn. Bijvoorbeeld, een klep geprogrammeerde tooopen helft manier kan zijn dat alle Hallo tooopen misleiden manier.

| **Onderdeel** | **Threat** | **Risicobeperking** | **Risico 's** | **Implementatie** |
| --- | --- | --- | --- | --- |
| Apparaat |S |Identiteit toohello apparaat toe te wijzen en Hallo apparaat verifiëren |Apparaat of een deel van Hallo apparaat vervangen door een ander apparaat. Hoe weet we dat we het juiste apparaat toohello praten? |Hallo-apparaat met behulp van Transport Layer Security (TLS) of IPSec-verificatie. Infrastructuur moet ondersteuning met behulp van vooraf gedeelde sleutel (PSK) op apparaten die volledige asymmetrische cryptografie kunnen niet worden verwerkt. Gebruikmaken van Azure AD [OAuth](http://www.rfc-editor.org/in-notes/internet-drafts/draft-ietf-ace-oauth-authz-01.txt) |
| TRID |Toepassing tamperproof mechanismen toohello apparaat bijvoorbeeld doordat het moeilijk tooimpossible tooextract sleutels en andere cryptografische materiaal van Hallo-apparaat. |Hallo risico is als iemand Hallo-apparaat (fysieke storing) is geknoeid. Hoe worden we zeker, dat het apparaat niet is geknoeid. |de meest effectieve risicobeperking Hallo is een vertrouwde platform module (TPM)-functie waarmee het opslaan van sleutels in speciale op chip circuits uit welke Hallo sleutels kunnen niet worden gelezen, maar kunnen alleen worden gebruikt voor cryptografische bewerkingen die Hallo-sleutel gebruikt, maar nooit vermelden Hallo-sleutel . Geheugen-codering van Hallo-apparaat. Sleutelbeheer voor Hallo-apparaat. Voor ondertekening van programmacode Hallo. | |
| E |Toegangsbeheer van Hallo apparaat hebben. Autorisatieschema voor. |Als het Hallo-apparaat kunt u afzonderlijke acties toobe uitgevoerd op basis van opdrachten vanaf een externe bron, of zelfs geknoeid sensoren, is het toegestaan Hallo aanval tooperform operations anders niet toegankelijk. |Autorisatieschema voor Hallo apparaat hebben | |
| Veldgateway |S |Verificatie van Hallo veld gateway tooCloud Gateway (cert gebaseerd, PSK, Claim gebaseerd,...) |Als iemand Veldgateway vervalsen kan, klikt u vervolgens het kan worden weergegeven als een apparaat. |TLS RSA/PSK, IPSec, [RFC 4279](https://tools.ietf.org/html/rfc4279). Alle Hallo dezelfde sleutelopslag en problemen attestation van apparaten in het algemeen – beste gebruik van TPM. 6LowPAN-extensie voor IPSec-toosupport draadloze Sensor netwerken (WSN). |
| TRID |Hallo Veldgateway beveiligen tegen knoeien (TPM)? |Adresvervalsing (spoofing) aanvallen die ertoe verleiden om Hallo cloudgateway gegevensclassificatie dat is het toofield praten kan gateway leiden tot het vrijgeven van informatie en geknoei met gegevens |Geheugen-versleuteling, TPM van, verificatie. | |
| E |Mechanisme voor toegangsbeheer voor Veldgateway | | | |

Hier volgen enkele voorbeelden van bedreigingen die in deze categorie:

Adresvervalsing (spoofing): Kan een aanvaller cryptografische sleutelmateriaal vanaf een apparaat uitpakken, op het Hallo-software of hardware-niveau en vervolgens toegang Hallo systeem met een ander fysiek of virtueel apparaat onder Hallo identiteit Hallo apparaat Hallo sleutelmateriaal is overgenomen uit.

**DOS-aanval**: een apparaat kan worden gerenderd waarvoor niet werkt of communiceren door interactie aangaan met keuzerondjes frequenties of knippen bedrading. Bijvoorbeeld, rapporteert een toezicht camera die de stroom of netwerk verbinding opzettelijk toenemende had niet gegevens, op alle.

**Knoeien**: een aanvaller kan geheel of gedeeltelijk vervangen Hallo software op Hallo apparaat uitvoeren, waardoor Hallo vervangen software tooleverage Hallo legitieme identiteit van het Hallo-apparaat als hello sleutel materiaal of Hallo cryptografische sleutel materialen houden faciliteiten zijn beschikbaar toohello illegale programma.

**Knoeien**: een toezicht camera die wordt weergegeven een afbeelding zichtbare spectrum van een leeg gang kan worden gericht op een foto van een dergelijke hotellobby. Een sensor rook of brand kan iemand een lichter onder het bedrijf rapportage. In beide gevallen Hallo apparaat mogelijk technisch volledig betrouwbare naar Hallo-systeem, maar er gezelschapsdieren informatie wordt gerapporteerd.

**Knoeien**: een aanvaller kan gebruikmaken van de uitgepakte sleutel wezenlijke toointercept en gegevens van het apparaat op Hallo communicatiepad Hallo onderdrukken en vervang deze door false gegevens die is geverifieerd met sleutelmateriaal Hallo gestolen.

**Knoeien**: een aanvaller kan geheel of gedeeltelijk vervangen Hallo software op Hallo apparaat uitvoeren, waardoor Hallo vervangen software tooleverage Hallo legitieme identiteit van het Hallo-apparaat als hello sleutel materiaal of Hallo cryptografische sleutel materialen houden faciliteiten zijn beschikbaar toohello illegale programma.

**Vrijgeven van informatie**: als het apparaat Hallo gezelschapsdieren software wordt uitgevoerd, dergelijke gezelschapsdieren software gegevens toounauthorized partijen kan mogelijk lekken.

**Vrijgeven van informatie**: een aanvaller kan gebruikmaken van de uitgepakte sleutel wezenlijke tooinject zelf in Hallo communicatiepad tussen Hallo-apparaat en een controller- of -gateway of cloud gateway toosiphon uitschakelen informatie.

**DOS-aanval**: Hallo-apparaat kan worden uitgeschakeld of omgezet in een modus waarbij de communicatie is niet mogelijk (dit is opzettelijk in veel industriële machines).

**Knoeien**: Hallo-apparaat opnieuw geconfigureerde toooperate in een status kan zijn onbekende toohello system (buiten bekende kalibreren parameters) te beheren en zodoende op gegevens die kan worden geïnterpreteerd

**Onrechtmatige uitbreiding van toegangsrechten**: een apparaat dat specifieke functie uitvoert kan geforceerde toodo iets anders zijn. Bijvoorbeeld, een klep geprogrammeerde tooopen helft manier kan zijn dat alle Hallo tooopen misleiden manier.

**DOS-aanval**: Hallo apparaat kan worden omgezet in een status waar communicatie niet mogelijk is.

**Knoeien**: Hallo-apparaat opnieuw geconfigureerde toooperate in een status kan zijn onbekende toohello system (buiten bekende kalibreren parameters) te beheren en zodoende op gegevens die kan worden geïnterpreteerd.

**Adresvervalsing (spoofing) / Tampering/Repudiation**: als niet zijn beveiligd (dit is zelden Hallo geval is bij de consument afstand besturingselementen) een aanvaller anoniem Hallo status van een apparaat kunt bewerken. Een goede illustratie is extern besturingselementen die elke TV kunt inschakelen en die populaire prankster hulpprogramma's zijn.

#### <a name="communication"></a>Communicatie
Bedreigingen rond communicatiepad tussen apparaten, apparaten en gateways veld en apparaat en cloud-gateway. Hallo in de volgende tabel bevat enkele richtlijnen rond open sockets Hallo apparaat/VPN:

| **Onderdeel** | **Threat** | **Risicobeperking** | **Risico 's** | **Implementatie** |
| --- | --- | --- | --- | --- |
| Apparaat IoT-Hub |TID |(D) TLS (PSK/RSA) tooencrypt Hallo verkeer |Afgeluisterd of interactie aangaan Hallo communicatie tussen Hallo-apparaat en Hallo-gateway |Beveiliging op protocolniveau Hallo. Met aangepaste protocollen, moeten we toofigure hoe tooprotect ze. In de meeste gevallen plaatsvindt Hallo communicatie van Hallo apparaat toohello IoT Hub (apparaat start Hallo verbinding). |
| Apparaat-apparaat |TID |(D) TLS (PSK/RSA) tooencrypt Hallo verkeer. |Lezen van gegevens tijdens de overdracht tussen apparaten. Gemanipuleerde Hallo-gegevens. Hallo-apparaat overbelasting met nieuwe verbindingen |Beveiliging op protocolniveau hello (MQTT/AMQP/HTTP/CoAP. Met aangepaste protocollen, moeten we toofigure hoe tooprotect ze. Hallo Risicobeperking voor Hallo DoS bedreiging is toopeer apparaten via een cloud- of -gateway en hebben ze alleen act als clients naar Hallo-netwerk. Hallo peering kan leiden tot een rechtstreekse verbinding tussen de peers Hallo na gelet zijn brokered door Hallo-gateway |
| Externe entiteit apparaat |TID |Sterke koppelen van Hallo externe entiteit toohello apparaat |Eavesdropping hello verbinding toohello apparaat. Storende Hallo communicatie met Hallo-apparaat |Hallo externe entiteit toohello apparaat NFC/Bluetooth RP veilig koppelen. Hallo operationele Configuratiescherm Hallo-apparaat (fysiek) beheren |
| Veld Gateway Cloudgateway |TID |TLS (PSK/RSA) tooencrypt Hallo verkeer. |Afgeluisterd of interactie aangaan Hallo communicatie tussen Hallo-apparaat en Hallo-gateway |Beveiliging op protocolniveau hello (MQTT/AMQP/HTTP/CoAP). Met aangepaste protocollen, moeten we toofigure hoe tooprotect ze. |
| De Cloudgateway apparaat |TID |TLS (PSK/RSA) tooencrypt Hallo verkeer. |Afgeluisterd of interactie aangaan Hallo communicatie tussen Hallo-apparaat en Hallo-gateway |Beveiliging op protocolniveau hello (MQTT/AMQP/HTTP/CoAP). Met aangepaste protocollen, moeten we toofigure hoe tooprotect ze. |

Hier volgen enkele voorbeelden van bedreigingen die in deze categorie:

**DOS-aanval**: beperkte apparaten zijn doorgaans onder DoS threat wanneer ze actief naar binnenkomende verbindingen of ongevraagde datagrammen in een netwerk, luisteren omdat een aanvaller kunt veel verbindingen parallel openen en die niet worden deze service of -service Deze zeer traag of hello apparaat kan worden overspoeld met ongevraagd verkeer. In beide gevallen kunt Hallo-apparaat effectief vastlopen op Hallo-netwerk.

**Adresvervalsing (spoofing), vrijgeven van informatie**: beperkte apparaten en apparaten voor speciale doeleinden vaak beschikken over een voor alle beveiligings-voorzieningen zoals wachtwoord of PINCODE beveiliging of ze geheel afhankelijk van de vertrouwende Hallo-netwerk, wat betekent dat ze toegang worden verleend tooinformation wanneer een apparaat op Hallo hetzelfde netwerk, en dat het netwerk wordt vaak alleen beveiligd door een gedeelde sleutel. Dat betekent dat als Hallo gedeeld geheim toodevice netwerk wordt vermeld, is mogelijk toocontrol Hallo apparaat of gegevens die van Hallo apparaat te observeren.  

**Adresvervalsing (spoofing)**: een aanvaller kan onderscheppen of gedeeltelijk overschrijven Hallo broadcast en vervalste Hallo Maker (man-in het midden Hallo)

**Knoeien**: een aanvaller kan intercept gedeeltelijk Hallo uitzending overschrijven of onjuiste gegevens verzenden 

**Vrijgeven van informatie:** een aanvaller kan op een uitzending afluisteren en informatie zonder toestemming verkrijgen **Denial of Service:** een aanvaller kan jam Hallo signaal en informatie distributie weigeren

#### <a name="storage"></a>Storage
Elk gateway-apparaat en het veld heeft een vorm van opslag (tijdelijke voor queuing Hallo gegevens, besturingssysteem (OS) installatiekopie opslag).

| **Onderdeel** | **Threat** | **Risicobeperking** | **Risico 's** | **Implementatie** |
| --- | --- | --- | --- | --- |
| Apparaatopslag |TRID |Versleuteling van opslag, ondertekening Hallo-Logboeken |Lezen van gegevens vanaf Hallo opslag (PII-gegevens), gemanipuleerde telemetrische gegevens. Gemanipuleerde in de wachtrij of opdracht besturingselement gegevens uit de cache. Knoeien met configuration of firmware updatepakketten kan terwijl in de cache opgeslagen of lokaal in de wachtrij leiden tooOS en/of system-onderdelen wordt aangetast |Versleuteling, message authentication code (MAC) of digitale handtekening. Waar mogelijk, sterk toegangsbeheer via toegang tot bedrijfsbronnen (ACL's) of machtigingen beheren. |
| De installatiekopie van het besturingssysteem van het apparaat |TRID | |Gemanipuleerde OS / vervangen van Hallo OS-onderdelen |OS-partitie, alleen-lezen, ondertekend installatiekopie van het besturingssysteem, versleuteling |
| Veldgateway-opslag (queuing Hallo gegevens) |TRID |Versleuteling van opslag, ondertekening Hallo-Logboeken |Lezen van gegevens vanaf Hallo opslag (PII-gegevens), telemetriegegevens, gemanipuleerde gemanipuleerde in de wachtrij of opdracht besturingselement gegevens uit de cache. Knoeien met configuration of firmware updatepakketten (dat is bestemd voor apparaten of veldgateway) kan terwijl in de cache opgeslagen of lokaal in de wachtrij leiden tooOS en/of system-onderdelen wordt aangetast |BitLocker |
| Installatiekopie van het veld Gateway besturingssysteem |TRID | |Gemanipuleerde OS / vervangen van Hallo OS-onderdelen |OS-partitie, alleen-lezen, ondertekend installatiekopie van het besturingssysteem, versleuteling |

### <a name="device-and-event-processingcloud-gateway-zone"></a>Apparaat- en gebeurtenis verwerking/cloud gateway zone
Een cloudgateway is een systeem waarmee externe communicatie van en toodevices of veld gateways uit diverse verschillende sites in de ruimte openbaar netwerk, meestal naar een cloud-gebaseerde beheer- en analyse systeem, een federatieve van dergelijke systemen. In sommige gevallen kan een cloudgateway onmiddellijk toegang toospecial doel apparaten uit aansluitingen zoals tablets en telefoons vergemakkelijken. In de context van Hallo besproken is hier 'cloud' bedoeld toorefer tooa dedicated gegevensverwerkingssysteem is niet gebonden toohello dezelfde site als Hallo gekoppelde apparaten of veld gateways en operationele maatregelen te voorkomen dat fysieke toegang gericht maar is niet noodzakelijkerwijs tooa ' openbare ' cloudinfrastructuur.  Een cloudgateway kan mogelijk worden toegewezen aan een overlay tooinsulate Hallo cloud netwerkvirtualisatiegateway en alle bijbehorende gekoppelde apparaten of veld gateways van ander netwerkverkeer. Hallo cloudgateway zelf is noch een controlesysteem apparaat, noch een verwerking of opslagfaciliteit voor gegevens van apparaten; deze interface faciliteiten met Hallo cloudgateway. Hallo cloud gateway zone omvat Hallo cloudgateway zelf samen met alle veld gateways en apparaten direct of indirect tooit gekoppeld.

Cloudgateway is voornamelijk aangepaste ingebouwde stukje software uitgevoerd als een service met blootgestelde eindpunten toowhich veldgateway en apparaten verbinding maken. Het moet als zodanig ontworpen beveiligd zijn. Volg [SDL](http://www.microsoft.com/sdl) processen voor het ontwerpen en bouwen van deze service. 

#### <a name="services-zone"></a>Services-zone
Een besturingssysteem (of domeincontroller) is een softwareoplossing interfaces met een apparaat of een veldgateway of cloudgateway voor Hallo doel voor het beheren van een of meer apparaten en/of toocollect en/of store en/of het analyseren van gegevens met een apparaat voor presentatie, of daaropvolgende controledoeleinden. Besturingssystemen zijn Hallo alleen entiteiten in Hallo bereik van deze discussie die onmiddellijk interactie met mensen vergemakkelijken. Hallo uitzondering worden tussenliggende fysieke besturingselement vlakken aan apparaten, zoals een switch waarmee een persoon tooturn Hallo apparaat uitschakelen of andere eigenschappen wijzigen en waarvoor er is geen functioneel equivalent die digitaal toegankelijk zijn. 

Tussenliggende fysieke besturingselement bevat, zijn de locaties waar elk soort van bestuur logica Hallo-functie van het oppervlak fysieke Hallo van handtekeningcertificaatsleutel zodat een equivalente functie extern kan worden gestart of invoer conflicten met externe invoer vermeden – dergelijke worden kunnen intermediated besturingselement verwerkingsinformatie zijn lokale controlesysteem conceptueel gekoppelde tooa dat maakt gebruik van dezelfde onderliggende functionaliteit Hallo zoals elk ander systeem beheer op afstand die Hallo apparaat gekoppelde tooin parallelle kan zijn. Bovenste bedreigingen toohello cloud computing kunnen worden gelezen als [Cloud Security Alliance (CSA)](https://cloudsecurityalliance.org/research/top-threats/) pagina.

## <a name="additional-resources"></a>Aanvullende bronnen
Raadpleeg toohello volgende artikelen voor aanvullende informatie:

* [SDL-hulpmiddel voor het modelleren van Threat](https://www.microsoft.com/sdl/adopt/threatmodeling.aspx)
* [Microsoft Azure IoT reference architecture](https://azure.microsoft.com/updates/microsoft-azure-iot-reference-architecture-available/)

