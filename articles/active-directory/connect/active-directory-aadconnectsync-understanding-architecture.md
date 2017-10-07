---
title: 'Azure AD Connect-synchronisatie: inzicht in Hallo-architectuur | Microsoft Docs'
description: In dit onderwerp beschrijft de architectuur Hallo van Azure AD Connect-synchronisatie en wordt uitgelegd Hallo termen die worden gebruikt.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 465bcbe9-3bdd-4769-a8ca-f8905abf426d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 9fb979fcf8feb7b4d406789102239480b0b4bc94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-architecture"></a>Azure AD Connect-synchronisatie: inzicht in Hallo-architectuur
Dit onderwerp worden de basisarchitectuur Hallo voor Azure AD Connect-synchronisatie. In veel aspecten is vergelijkbaar tooits voorgangers MIIS 2003, ILM 2007 en FIM 2010. Azure AD Connect-synchronisatie is Hallo evolutie van deze technologieën. Als u bekend met een van deze technologieën voor oudere bent, niet Hallo inhoud van dit onderwerp ook bekend tooyou. Als u nieuwe toosynchronization, wordt de in dit onderwerp voor u. Het is echter niet een vereiste tooknow Hallo details van dit onderwerp toobe geslaagde bij het maken van aanpassingen tooAzure AD Connect-synchronisatie (aangeroepen synchronisatie-engine in dit onderwerp).

## <a name="architecture"></a>Architectuur
Hallo synchronisatie-engine maakt van een geïntegreerde weergave van objecten die zijn opgeslagen in meerdere verbonden gegevensbronnen en gegevens van identiteit in die gegevensbronnen beheert. Deze geïntegreerde weergave wordt bepaald door de identiteitsgegevens Hallo opgehaald uit verbonden gegevensbronnen en een reeks regels die bepalen hoe tooprocess deze informatie.

### <a name="connected-data-sources-and-connectors"></a>Verbonden gegevensbronnen en -Connectors
Hallo synchronisatie-engine verwerkt identiteitsgegevens van opslagplaatsen voor verschillende gegevens, zoals Active Directory of een SQL Server-database. Elke gegevensopslagplaats die de gegevens in de indeling van een database-achtige ordent en biedt standaard gegevenstoegang methoden is een mogelijke gegevensbron kandidaat voor Hallo synchronisatie-engine. Hallo-opslagplaatsen voor gegevens die worden gesynchroniseerd door de synchronisatie-engine heten **verbonden gegevensbronnen** of **mappen verbonden** (CD).

synchronisatie-engine Hallo ingekapseld interactie met een verbonden gegevensbron binnen een module met de naam een **Connector**. Elk type van de gekoppelde gegevensbron heeft een specifieke Connector. Hallo Connector een vereiste bewerking vertaalt naar Hallo-indeling die verbonden gegevens Hallo bron begrijpt.

Met connectors kunt API-aanroepen tooexchange identiteitsgegevens (zowel lezen en schrijven) met een verbonden gegevensbron. Het is ook mogelijk tooadd een aangepaste Connector met Hallo extensible connectivity framework. Hallo volgende afbeelding ziet u hoe een Connector verbinding maakt met een verbonden data source toohello synchronisatie-engine.

![Arch1](./media/active-directory-aadconnectsync-understanding-architecture/arch1.png)

Kan gegevensstroom in beide richtingen, maar deze kan niet tegelijkertijd doorlopen in beide richtingen. Met andere woorden, kan een Connector geconfigureerde tooallow gegevens tooflow van Hallo verbonden data source toosync engine of van synchronisatie-engine toohello verbonden gegevensbron, maar slechts één van deze bewerkingen kan optreden op elk gewenst moment voor een object en kenmerk. Hallo richting kan afwijken voor verschillende objecten en voor verschillende kenmerken.

tooconfigure een Connector, die u opgeeft, Hallo objecttypen die u toosynchronize wilt. Hallo objecttypen geven definieert Hallo bereik van objecten die zijn opgenomen in het synchronisatieproces Hallo. de volgende stap Hallo is tooselect Hallo kenmerken toosynchronize, dat een kenmerk opnamelijst wordt genoemd. Deze instellingen kunnen op elk gewenst moment in antwoord toochanges tooyour bedrijfsregels worden gewijzigd. Wanneer u hello Azure AD Connect-installatiewizard gebruikt, worden deze instellingen voor u geconfigureerd.

tooexport objecten tooa verbonden gegevensbron, opnamelijst Hallo-kenmerk moet ten minste Hallo minimale vereiste toocreate typt u een specifiek object in een verbonden gegevensbron kenmerken. Bijvoorbeeld, Hallo **sAMAccountName** kenmerk moet worden opgenomen in Hallo kenmerk insluiting lijst tooexport een gebruiker object tooActive Directory omdat alle gebruikersobjecten in Active Directory moeten een **sAMAccountName**  kenmerk gedefinieerd. Hallo-installatiewizard wordt opnieuw, deze configuratie.

Als de gekoppelde gegevensbron Hallo gebruikmaakt van structurele onderdelen, zoals tooorganize-objecten, partities of containers, kunt u Hallo gebieden in de gekoppelde gegevensbron Hallo die worden gebruikt voor een bepaalde oplossing kunt beperken.

### <a name="internal-structure-of-hello-sync-engine-namespace"></a>Interne structuur van Hallo sync engine naamruimte
Hallo volledige synchronisatie-engine naamruimte bestaat uit twee naamruimten die voor het opslaan van identiteitsgegevens Hallo. Hallo twee naamruimten zijn:

* connectorruimte hello (CS)
* Hallo metaverse (MV)

Hallo **connectorruimte** is een faseringsgebied dat representaties van objecten uit een bron- en Hallo kenmerken van verbonden gegevens opgegeven in de kenmerkenlijst insluiting Hallo aangewezen Hallo bevat. Hallo synchronisatie-engine gebruikt Hallo connector ruimte toodetermine wat is er gewijzigd in Hallo verbonden bron- en toostage binnenkomende gewijzigde gegevens. Hallo synchronisatie-engine gebruikt ook Hallo connector ruimte toostage uitgaande wijzigingen voor export toohello verbonden gegevensbron. Hallo synchronisatie-engine onderhoudt een afzonderlijke connectorruimte als een faseringsgebied voor elke Connector.

Met behulp van een faseringsgebied Hallo synchronisatie-engine blijft onafhankelijk van Hallo verbonden gegevensbronnen en wordt niet beïnvloed door de beschikbaarheid en toegankelijkheid. Als gevolg hiervan kunt u gegevens van identiteit op elk gewenst moment door Hallo gegevens in faseringsgebied Hallo verwerken. Hallo synchronisatie-engine kan alleen Hallo wijzigingen aangebracht in de gekoppelde gegevensbron Hallo sinds Hallo laatste communicatie sessie beëindigd of push alleen Hallo wijzigingen tooidentity informatie die Hallo verbonden gegevensbron nog niet ontvangen, die beperkt aanvragen Hallo netwerkverkeer tussen Hallo synchronisatie-engine en de gekoppelde gegevensbron Hallo.

Synchronisatie-engine slaat bovendien statusinformatie over alle objecten dat deze in Hallo connectorgebied overgebracht fasen. Wanneer nieuwe gegevens worden ontvangen, evalueert synchronisatie-engine altijd of Hallo gegevens al is gesynchroniseerd.

Hallo **metaverse** is een opslagruimte die Hallo geaggregeerd identiteitsgegevens uit meerdere verbonden gegevensbronnen, zodat u één mondiale, geïntegreerde weergave van alle gecombineerde objecten bevat. Metaverse-objecten worden gemaakt op basis van gegevens van de Hallo-identiteit die is opgehaald uit Hallo verbonden gegevensbronnen en een reeks regels die u toelaten om toocustomize Hallo-synchronisatieproces.

Hallo volgende afbeelding ziet u Hallo connector ruimte naamruimte en Hallo metaverse naamruimte binnen Hallo synchronisatie-engine.

![Arch2](./media/active-directory-aadconnectsync-understanding-architecture/arch2.png)

## <a name="sync-engine-identity-objects"></a>Synchronisatie-engine identity-objecten
Hallo-objecten in de synchronisatie-engine Hallo zijn weergaven van de objecten in de gekoppelde gegevensbron Hallo of hello geïntegreerde weergave die engine voor het synchroniseren van die objecten. Elk synchronisatie-engine-object moet een globally unique identifier (GUID) hebben. GUID's bieden de integriteit van gegevens en snelle relaties tussen objecten.

### <a name="connector-space-objects"></a>Connector ruimteobjecten
Wanneer synchronisatie-engine met een verbonden gegevensbron communiceert, Hallo identiteitsgegevens in de gekoppelde gegevensbron Hallo leest en die informatie toocreate een representatie van Hallo identiteit object gebruikt in Hallo connectorgebied overgebracht. U kunt maken of deze objecten afzonderlijk verwijderen. U kunt alle objecten in een connectorruimte echter handmatig verwijderen.

Alle objecten in Hallo connectorgebied overgebracht hebben twee kenmerken:

* Een globally unique identifier (GUID)
* Een DN-naam (Distinguished Name)

Als Hallo verbonden gegevensbron wijst een uniek kenmerk toohello object en objecten in Hallo connectorgebied overgebracht kunnen ook geen ankerkenmerk hebben. Hallo ankerkenmerk identificatie unieke van een object in de gekoppelde gegevensbron Hallo. Hallo synchronisatie-engine gebruikt Hallo anker toolocate Hallo bijbehorende weergave van dit object in de gekoppelde gegevensbron Hallo. Synchronisatie-engine wordt ervan uitgegaan dat Hallo anker van een object nooit wijzigingen gedurende de levensduur Hallo van Hallo-object.

Veel van Hallo Connectors een bekende unieke id toogenerate een anker automatisch gebruikt voor elk object wanneer deze wordt geïmporteerd. Hallo Active Directory-Connector gebruikt bijvoorbeeld Hallo **objectGUID** kenmerk voor een anker. U kunt voor verbonden gegevensbronnen die niet in een duidelijk gedefinieerde unieke id voorzien, anker generatie opgeven als onderdeel van de configuratie van de Connector Hallo.

In dat geval Hallo anker wordt samengesteld uit een of meer unieke kenmerken van een object typt, noch van welke wijzigingen en die een unieke identificeert Hallo-object in Hallo connectorruimte (bijvoorbeeld een nummer of een gebruikers-ID).

Een connector space-object kan een van de volgende Hallo zijn:

* Een gefaseerde installatie-object
* Een tijdelijke aanduiding

### <a name="staging-objects"></a>Tijdelijke objecten
Een gefaseerde installatie object vertegenwoordigt een exemplaar van het objecttype van de gekoppelde gegevensbron Hallo aangewezen Hallo. Bovendien toohello GUID en Hallo DN-naam, een staging-object heeft altijd een waarde die Hallo-objecttype aangeeft.

Tijdelijke objecten die zijn geïmporteerd altijd hebben een waarde voor Hallo ankerkenmerk. Tijdelijke objecten die nieuw zijn ingericht met synchronisatie-engine en tijdens het Hallo van wordt gemaakt in de gekoppelde gegevensbron Hallo hebben niet een waarde voor Hallo ankerkenmerk.

Tijdelijke objecten ook uitvoeren huidige waarden van de kenmerken van bedrijven en operationele informatie die nodig is voor de synchronisatie-engine tooperform Hallo-synchronisatieproces. Operationele informatie bevat vlaggen die aangeven Hallo-type van updates die zijn voorbereid op Hallo staging-object. Als een staging-object heeft ontvangen van nieuwe identiteitsgegevens uit Hallo verbonden gegevensbron die nog niet zijn verwerkt, Hallo-object is gemarkeerd als **in behandeling zijnde importeren**. Als een gefaseerde installatie object nieuwe identiteitsgegevens die nog niet verbonden geëxporteerde toohello-gegevensbron is heeft, is gemarkeerd als **in behandeling zijnde uitvoer**.

Een gefaseerde installatie object kan ook een importeren of exporteren object. Hallo synchronisatie-engine maakt een object importeren met behulp van objectgegevens van de gekoppelde gegevensbron Hallo ontvangen. Wanneer synchronisatie-engine informatie over Hallo bestaan van een nieuw object op dat overeenkomt met een Hallo objecttypen in Hallo verbindingslijn is geselecteerd ontvangt, maakt deze een object importeren in Hallo connectorgebied overgebracht als een representatie van Hallo-object in de gekoppelde gegevensbron Hallo.

Hallo volgende afbeelding ziet u een importobject dat een object in de gekoppelde gegevensbron Hallo vertegenwoordigt.

![Arch3](./media/active-directory-aadconnectsync-understanding-architecture/arch3.png)

Hallo synchronisatie-engine maakt een object exporteren met behulp van de objectgegevens in Hallo metaverse. Objecten exporteren zijn geëxporteerde toohello verbonden gegevensbron tijdens Hallo volgende communicatie-sessie. Vanuit het perspectief van de Hallo van Hallo synchronisatie-engine wordt export objecten bestaan niet in de gekoppelde gegevensbron Hallo nog. Hallo ankerkenmerk voor een object exporteren is daarom niet beschikbaar. Nadat het Hallo-object van synchronisatie-engine ontvangt, maakt de gekoppelde gegevensbron Hallo een unieke waarde voor ankerkenmerk Hallo van Hallo-object.

Hallo volgende afbeelding ziet u hoe een export-object is gemaakt met behulp van de gegevens van identiteit in Hallo metaverse.

![Arch4](./media/active-directory-aadconnectsync-understanding-architecture/arch4.png)

synchronisatie-engine Hallo bevestigt Hallo exporteren van het Hallo-object door het object van de gekoppelde gegevensbron Hallo Hallo opnieuw importeren. Objecten exporteren worden objecten importeren wanneer synchronisatie-engine deze tijdens het Hallo volgende importeren uit die verbonden gegevensbron ontvangt.

### <a name="placeholders"></a>Tijdelijke aanduidingen
Hallo synchronisatie-engine maakt gebruik van een platte naamruimte toostore-objecten. Sommige verbonden gegevensbronnen zoals Active Directory gebruiken, een hiërarchische naamruimte. tootransform informatie van een hiërarchische naamruimte in een platte naamruimte tijdelijke aanduidingen toopreserve Hallo hiërarchie maakt gebruik van synchronisatie-engine.

Elke tijdelijke aanduiding vertegenwoordigt een onderdeel (bijvoorbeeld een organisatie-eenheid) van hiërarchische naam van een object dat niet is geïmporteerd in synchronisatie-engine, maar vereist tooconstruct Hallo hiërarchische naam is. Gemaakt door de verwijzingen in Hallo verbonden gegevensbron tooobjects die niet van objecten in Hallo connectorgebied overgebracht Faseren hiaten in te vullen.

Hallo synchronisatie-engine gebruikt ook de tijdelijke aanduidingen toostore verwijst naar objecten die nog niet is geïmporteerd. Bijvoorbeeld, als de synchronisatie is geconfigureerde tooinclude Hallo manager kenmerk voor Hallo *Abbie Spencer* object en hello ontvangen waarde is een object dat niet geïmporteerd, zoals is *CN Lee Sperry, CN = Users, DC = = fabrikam, DC = com*, Hallo manager informatie wordt opgeslagen als tijdelijke aanduidingen in Hallo connectorgebied overgebracht. Als het beheerobject hello later wordt geïmporteerd, wordt Hallo tijdelijke aanduiding voor object overschreven door Hallo staging-object dat Hallo manager vertegenwoordigt.

### <a name="metaverse-objects"></a>Metaverse-objecten
Metaverse-object Hallo geaggregeerd weergave bevat die synchronisatie-engine heeft Hallo staging-objecten in Hallo connectorgebied overgebracht. Synchronisatie-engine maakt metaverse-objecten met behulp van Hallo informatie in objecten importeren. Verschillende connector ruimteobjecten kunnen gekoppelde tooa één metaverse-object, maar een connector space-object mag geen gekoppelde toomore dan één metaverse-object.

Metaverse-objecten kunnen niet handmatig worden gemaakt of verwijderd. Hallo synchronisatie-engine wordt automatisch verwijderd metaverse-objecten die geen space-object voor een koppeling tooany-connector in Hallo connectorgebied overgebracht.

toomap objecten binnen een verbonden tooa bijbehorende gegevensbronobjecttype binnen Hallo metaverse, synchronisatie-engine biedt een uitgebreid schema met een vooraf gedefinieerde set objecttypen en de bijbehorende kenmerken. U kunt nieuwe objecttypen en kenmerken voor metaverse-objecten maken. Kenmerken kunnen worden één waarde of meerdere waarden en Hallo kenmerktypen kunnen tekenreeksen, verwijzingen, cijfers en Boole-waarden zijn.

### <a name="relationships-between-staging-objects-and-metaverse-objects"></a>Relaties tussen fasering en metaverse-objecten
Hallo-gegevensstroom wordt binnen Hallo sync engine naamruimte ingeschakeld door Hallo koppeling relatie tussen fasering en metaverse-objecten. Een gefaseerde installatie object die gekoppelde tooa metaverse-object heet een **gekoppelde object** (of **connectorobject**). Een gefaseerde installatie-object dat is geen gekoppelde tooa metaverse-object heet een **object niet langer lid** (of **disconnector object**). Hallo voorwaarden toegevoegd en geen lid meer zijn voorkeur toonot Verwar Hello Connectors die verantwoordelijk is voor het importeren en exporteren van gegevens uit een gekoppelde adreslijst.

Tijdelijke aanduidingen zijn nooit gekoppelde tooa metaverse-object

Een gekoppelde object bestaat uit een gefaseerde installatie object en de gekoppelde relatie tooa één metaverse-object. Gekoppelde objecten zijn gebruikte toosynchronize kenmerkwaarden tussen een object van de ruimte connector en metaverse-object.

Wanneer een gefaseerde installatie object verandert in een gekoppelde object tijdens de synchronisatie, kunnen de kenmerken vloeien tussen die Hallo staging-object en Hallo metaverse-object. Kenmerkstroom bidirectionele en is geconfigureerd met behulp van kenmerk importeren en exporteren kenmerk regels.

Een object van de ruimte één connector kan gekoppelde tooonly één metaverse-object zijn. Elke metaverse-object mag echter gekoppelde toomultiple connector ruimteobjecten in dezelfde Hallo of in verschillende connectorspaces, zoals wordt weergegeven in de volgende illustratie Hallo.

![Arch5](./media/active-directory-aadconnectsync-understanding-architecture/arch5.png)

Hallo relatie tussen Hallo staging-object gekoppeld en metaverse-object is permanent en kan worden verwijderd door regels die u opgeeft.

Een object niet langer lid is een test-object dat is geen gekoppelde tooany metaverse-object. Hallo-kenmerk waarden van een object niet langer lid niet zijn verwerkt alle verdere binnen Hallo metaverse. Hallo kenmerk waarden van het bijbehorende object in de gekoppelde gegevensbron Hallo Hallo niet worden bijgewerkt door synchronisatie-engine.

U kunt met behulp van afzonderlijke objecten opslaan van gegevens van identiteit in synchronisatie-engine en later verwerken. Een gefaseerde installatie object behouden als een object niet langer lid in Hallo connectorruimte heeft veel voordelen. Omdat het Hallo-systeem is al opgezet Hallo vereist informatie over dit object, maar het is niet nodig toocreate een weergave van dit object opnieuw tijdens Hallo naast importeren uit de gekoppelde gegevensbron Hallo. Op deze manier synchronisatie-engine heeft altijd een volledige momentopname van de gekoppelde gegevensbron hello, zelfs als er geen huidige verbinding toohello verbonden gegevensbron. Afzonderlijke objecten kunnen worden geconverteerd in gekoppelde objecten, en omgekeerd, afhankelijk van het Hallo-regels die u opgeeft.

Een object importeren wordt als een object niet langer lid gemaakt. Een export-object moet een gekoppelde object. Hallo system logische met deze regel wordt afgedwongen en wordt elke export-object is geen gekoppelde object verwijderd.

## <a name="sync-engine-identity-management-process"></a>Synchronisatieproces engine identity management
Hallo identiteit beheerproces bepaalt hoe de gegevens van identiteit tussen verschillende verbonden gegevensbronnen wordt bijgewerkt. Identiteitsbeheer gebeurt in drie processen:

* Importeren
* Synchronisatie
* Exporteren

Tijdens het importproces hello evalueert de synchronisatie-engine Hallo binnenkomende gegevens van identiteit van een verbonden gegevensbron. Wanneer wijzigingen worden gedetecteerd, deze nieuwe tijdelijke objecten maakt of bestaande staging objecten in Hallo connectorruimte voor de synchronisatie bijgewerkt.

Tijdens het synchronisatieproces hello, synchronisatie-engine Hallo metaverse tooreflect wijzigingen die zijn opgetreden in connectorruimte Hallo-updates en Hallo connector ruimte tooreflect wijzigingen die zijn opgetreden in Hallo metaverse-updates.

Tijdens het exportproces hello duwt synchronisatie-engine om wijzigingen die zijn voorbereid op tijdelijke objecten en die zijn gemarkeerd als in behandeling zijnde uitvoer.

Hallo volgende afbeelding toont waar elk van de processen Hallo optreedt als identiteit informatiestromen van één verbonden data source tooanother.

![Arch6](./media/active-directory-aadconnectsync-understanding-architecture/arch6.png)

### <a name="import-process"></a>Importeren
Tijdens het importproces hello evalueert de synchronisatie-engine updates tooidentity informatie. Synchronisatie-engine Hallo identiteitsgegevens ontvangen van de gekoppelde gegevensbron Hallo Hallo identiteit informatie over een staging-object wordt vergeleken en bepaalt of updates voor Hallo staging-object is vereist. Als het benodigde tooupdate Hallo staging-object met nieuwe gegevens, worden Hallo staging-object is gemarkeerd als in behandeling zijnde importeren.

Door objecten in Hallo connectorgebied overgebracht voordat de synchronisatie voor gefaseerde installatie, kan de synchronisatie-engine alleen Hallo identiteit informatie die gewijzigd verwerken. Deze procedure biedt Hallo volgende voordelen:

* **Efficiënte synchronisatie**. Hallo en de hoeveelheid gegevens verwerkt tijdens de synchronisatie wordt geminimaliseerd.
* **Efficiënte hersynchronisatie**. U kunt wijzigen hoe de synchronisatie-engine identiteitsgegevens zonder herstellen van verbindingen Hallo sync engine toohello gegevensbron worden verwerkt.
* **Mogelijkheid toopreview synchronisatie**. U kunt synchronisatie tooverify uw veronderstellingen over Hallo identity management proces kloppen bekijken.

Voor elk object dat is opgegeven in Hallo Connector, probeert de synchronisatie-engine Hallo eerst toolocate een representatie van Hallo-object in connectorruimte Hallo Hallo Connector. Synchronisatie-engine onderzoekt alle tijdelijke objecten in Hallo connectorgebied overgebracht en een bijbehorende staging-object met een overeenkomende ankerkenmerk toofind probeert. Als er geen bestaande staging-object een overeenkomende kenmerk verankeren heeft, synchronisatie-engine probeert toofind een bijbehorende test-object met Hallo DN dezelfde-naam.

Wanneer synchronisatie-engine een gefaseerde installatie object die overeenkomt met de door de DN-naam, maar niet door anker vindt, hello speciaal gedrag volgende gebeurt:

* Als Hallo-object zich bevindt in Hallo connectorruimte heeft geen anker en vervolgens synchronisatie-engine dit object verwijdert uit Hallo connectorruimte en markeert Hallo metaverse-object is het gekoppelde tooas **opnieuw inrichten op de volgende synchronisatie uitvoeren**. Het maakt vervolgens Hallo nieuw import-object.
* Als het Hallo-object in de Hallo connector schijfruimte gevonden met een anker heeft, vervolgens synchronisatie-engine wordt ervan uitgegaan dat dit object is gewijzigd of verwijderd uit Hallo verbonden directory. Een tijdelijke, nieuwe DN-naam voor Hallo connector ruimte object wilt toewijzen zodat deze inkomende hello-object kunt voorbereiden. Hallo oude object wordt vervolgens **tijdelijke**, wachten tot Hallo Connector tooimport Hallo hernoemen of verwijderen van een tooresolve Hallo situatie.

Als de synchronisatie-engine wordt gezocht naar een staging-object dat overeenkomt met toohello object opgegeven in het Hallo-Connector, bepaalt wat voor soort wijzigingen tooapply. Bijvoorbeeld, synchronisatie-engine kan hernoemen of verwijderen van Hallo-object in de gekoppelde gegevensbron Hallo of deze kenmerkwaarden Hallo-object kan alleen worden bijgewerkt.

Tijdelijke objecten met de bijgewerkte gegevens zijn gemarkeerd als in behandeling zijnde importeren. Er zijn verschillende typen wacht op invoer beschikbaar. Afhankelijk van Hallo resultaat van het importproces Hallo heeft een gefaseerde installatie-object in Hallo connectorgebied overgebracht een Hallo in behandeling zijnde importeren typen te volgen:

* **Geen**. Er zijn geen wijzigingen tooany van kenmerken Hallo Hallo staging-object zijn beschikbaar. Synchronisatie-engine vlag dit type niet als in behandeling zijnde importeren.
* **Voeg**. Hallo staging-object is een nieuw object importeren in Hallo connectorgebied overgebracht. Dit type vlaggen synchronisatie-engine als in behandeling zijnde importeren voor verdere verwerking in Hallo metaverse.
* **Update**. Synchronisatie-engine in Hallo connectorgebied overgebracht gevonden met een bijbehorende test-object en dit type als in behandeling zijnde importeren vlaggen zodat updates toohello kenmerken kunnen worden verwerkt in Hallo metaverse. Updates bevatten object wijzigen.
* **Verwijder**. Synchronisatie-engine in Hallo connectorgebied overgebracht gevonden met een bijbehorende test-object en het markeren van dit type als in behandeling zijnde importeren zodat hello gekoppelde object kan worden verwijderd.
* **Verwijderen/toevoegen**. Synchronisatie-engine in gevonden met een bijbehorende test-object Hallo connectorgebied overgebracht, maar Hallo objecttypen komen niet overeen. In dit geval een verwijderen toevoegen wijziging tijdelijk worden opgeslagen. Een delete-toevoegen wijziging geeft aan toohello synchronisatie-engine die een volledige hersynchronisatie van dit object moet worden uitgevoerd omdat verschillende sets van regels toothis object van toepassing wanneer Hallo objecttype wordt gewijzigd.

Hallo instelling in behandeling zijnde importeren status van een gefaseerde installatie object, is het mogelijk tooreduce Hallo aanzienlijke hoeveelheid gegevens verwerkt tijdens de synchronisatie omdat hierdoor kan Hallo system tooprocess alleen objecten die gegevens zijn bijgewerkt.

### <a name="synchronization-process"></a>Synchronisatieproces
Synchronisatie bestaat uit twee verwante processen:

* Inkomende synchronisatie, wanneer de inhoud Hallo van Hallo metaverse wordt bijgewerkt door Hallo gegevens in Hallo connectorgebied overgebracht.
* Uitgaande synchronisatie, wanneer de inhoud Hallo Hallo connector ruimte wordt bijgewerkt met gegevens in Hallo metaverse.

Met Hallo informatie gefaseerde in Hallo connectorruimte, maakt hello inkomende synchronisatie in Hallo metaverse Hallo geïntegreerd weergave van het Hallo-gegevens die zijn opgeslagen in Hallo verbonden gegevensbronnen. Alle tijdelijke objecten of alleen de met een in behandeling zijnde importeren informatie worden samengevoegd, afhankelijk van hoe Hallo regels zijn geconfigureerd.

Hallo uitgaande synchronisatie proces updates exporteren objecten als metaverse objecten wijzigen.

Inkomende synchronisatie maakt Hallo geïntegreerd weergave in de metaverse Hallo Hallo identiteit informatie die wordt ontvangen van Hallo verbonden gegevensbronnen. Synchronisatie-engine kan op elk gewenst moment de identiteitsgegevens verwerken met behulp van Hallo meest recente gegevens van identiteit of deze van Hallo gegevensbron verbonden heeft.

**Inkomende synchronisatie**

Inkomende synchronisatie bevat Hallo processen te volgen:

* **Inrichten** (ook wel **projectie** als het is belangrijk toodistinguish dit proces van inrichting van de uitgaande synchronisatie). Hallo synchronisatie-engine maakt een nieuw metaverse-object op basis van een gefaseerde installatie object en deze koppelingen. Inrichten is een bewerking op objectniveau.
* **Deelnemen aan**. Synchronisatie-engine Hallo koppelt u een gefaseerde installatie object tooan bestaande metaverse-object. Een join is een bewerking op objectniveau.
* **Importeren van de kenmerkstroom**. Synchronisatie-engine-updates Hallo kenmerkwaarden, kenmerkstroom van Hallo-object in de metaverse Hallo aangeroepen. Kenmerkstroom importeren is een kenmerk niveau bewerking uitgevoerd waarvoor een koppeling tussen een gefaseerde installatie object en metaverse-object.

Inrichten is alleen Hallo-proces dat objecten in Hallo metaverse maakt. Inrichten van invloed op import alleen objecten die niet langer lid objecten. Synchronisatie-engine maakt tijdens het inrichten, een metaverse-object dat overeenkomt met de objecttype toohello van Hallo importeren object en er wordt een koppeling tussen beide objecten, waardoor het maken van een gekoppelde object.

Hallo join proces stelt ook een koppeling tussen objecten importeren en metaverse-object. Hallo verschil tussen join en in te richten is dat Hallo join proces dat Hallo importeren object gekoppelde tooan bestaande metaverse-object vereist, waarbij Hallo inrichten proces maakt een nieuw metaverse-object zijn.

Synchronisatie-engine probeert toojoin een import object tooa metaverse-object op basis van criteria die is opgegeven in de configuratie van de Synchronisatieregel Hallo.

Tijdens het Hallo inrichten en join processen, synchronisatie-engine gekoppeld. een object niet langer lid tooa metaverse-object, waardoor ze lid zijn. Nadat deze op objectniveau bewerkingen zijn voltooid, kunt de synchronisatie-engine Hallo kenmerkwaarden van Hallo gekoppeld metaverse-object bijwerken. Dit proces heet kenmerkstroom importeren.

Kenmerkstroom importeren wordt uitgevoerd op alle objecten voor importeren die nieuwe gegevens bevatten en gekoppelde tooa metaverse-object.

**Uitgaande synchronisatie**

Uitgaande synchronisatie updates exporteren objecten als een metaverse-object wijzigen, maar wordt niet verwijderd. Hallo-doel van de uitgaande synchronisatie is tooevaluate of wijzigingen toometaverse objecten updates toostaging objecten in Hallo-connectorspaces vereisen. In sommige gevallen worden Hallo wijzigingen vereisen kunnen dat tijdelijke in alle connectorspaces objecten bijgewerkt. Tijdelijke objecten die zijn gewijzigd, zijn gemarkeerd als in behandeling zijnde uitvoer, waardoor ze objecten exporteren. Deze objecten worden later gepusht toohello verbonden gegevensbron tijdens het exportproces Hallo exporteren.

Uitgaande synchronisatie heeft drie processen:

* **Inrichten**
* **Opheffen van inrichting**
* **Kenmerkstroom exporteren**

Inrichting en het opheffen van inrichting zijn beide bewerkingen op objectniveau. Opheffen van inrichting, is afhankelijk van de inrichting omdat alleen inrichting kunt starten. Opheffen van inrichting wordt geactiveerd wanneer de inrichting verwijdert Hallo koppeling tussen een metaverse-object en een export-object.

Inrichting wordt altijd geactiveerd wanneer wijzigingen toegepast tooobjects in Hallo metaverse zijn. Wanneer wijzigingen worden aangebracht toometaverse objecten, kunt synchronisatie-engine uitvoeren na taken tijdens het inrichtingsproces Hallo Hallo:

* Gekoppelde objecten, waarbij een metaverse-object gekoppelde tooa nieuwe export-object is gemaakt.
* Wijzig de naam van een gekoppelde object.
* Meld de koppelingen tussen een metaverse-object en staging-objecten, het maken van een object niet langer lid.

Als inrichting sync engine toocreate een nieuw connectorobject is vereist, is Hallo staging-object toowhich hello metaverse-object is gekoppeld altijd een object exporteren, omdat Hallo object nog niet in de gekoppelde gegevensbron Hallo bestaat.

Als de synchronisatie-engine toodisjoin een lid-object maken van een object niet langer lid, inrichten vereist wordt opheffen van inrichting geactiveerd. Hallo opheffen van inrichting proces verwijdert Hallo-object.

Tijdens het opheffen van inrichting verwijdert verwijderen van een object exporteren fysiek niet Hallo-object. Hallo is object gemarkeerd als **verwijderd**, wat betekent dat Hallo delete-bewerking is voorbereid op Hallo-object.

Kenmerkstroom exporteren vindt ook plaats tijdens Hallo uitgaande synchronisatieproces soortgelijke wijze als toohello dat importeren kenmerkstroom treedt op tijdens inkomende synchronisatie. Kenmerkstroom exporteren doet zich alleen tussen de metaverse en export-objecten die zijn gekoppeld.

### <a name="export-process"></a>Exportproces
Synchronisatie-engine onderzoekt alle export-objecten die zijn gemarkeerd als in behandeling zijnde uitvoer in Hallo connectorgebied overgebracht tijdens het exportproces hello, en vervolgens verzendt updates toohello verbonden gegevensbron.

Hallo synchronisatie-engine kunt bepalen Hallo succes van het exporteren van een maar voldoende kan niet bepalen Hallo identity management-proces is voltooid. Objecten in de gekoppelde gegevensbron Hallo kunnen altijd worden gewijzigd door andere processen. Omdat de synchronisatie-engine heeft een permanente verbinding toohello verbonden gegevensbron geen, maar het is niet voldoende toomake veronderstellingen over Hallo eigenschappen van een object in de gekoppelde gegevensbron Hallo op basis van een succesvolle export-melding alleen.

Bijvoorbeeld een proces in Hallo zich verbonden gegevensbron kunnen de kenmerken wijzigen Hallo object back-tootheir oorspronkelijke waarden (dat wil zeggen, Hallo verbonden gegevensbron kan Hallo waarden overschrijven direct na het Hallo-gegevens wordt doorgeschoven, is uit door de synchronisatie-engine en heeft toegepast in de gekoppelde gegevensbron Hallo).

Hallo sync engine winkels exporteren en importeren van statusinformatie over elk staging-object. Als Hallo kenmerken die zijn opgegeven in de kenmerkenlijst insluiting Hallo zijn gewijzigd sinds de laatste export hello, Hallo opslag van importeren en exporteren status kunnen synchronisatie-engine tooreact op de juiste wijze. Synchronisatie-engine gebruikt Hallo importeren proces tooconfirm kenmerkwaarden die verbonden geëxporteerde toohello-gegevensbron zijn. Een vergelijking tussen Hallo geïmporteerd en de geëxporteerde gegevens zoals weergegeven in Hallo volgende afbeelding kunt sync engine toodetermine of Hallo exporteren geslaagd is of als moet worden herhaald toobe.

![Arch7](./media/active-directory-aadconnectsync-understanding-architecture/arch7.png)

Als de synchronisatie-engine exporteert kenmerk C, die een waarde van 5 heeft, bijvoorbeeld tooa verbonden gegevensbron, C = 5 worden opgeslagen in het geheugen van de status exporteren. Elke aanvullende exporteren op dit object resulteert in een poging tooexport C = 5 toohello verbonden gegevensbron opnieuw omdat synchronisatie-engine wordt ervan uitgegaan dat deze waarde niet permanent toegepaste toohello object is (dat wil zeggen, tenzij een andere waarde onlangs is geïmporteerd van Hallo verbonden gegevensbron). Hallo export geheugen wordt gewist wanneer C = 5 tijdens een importbewerking op Hallo-object is ontvangen.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md) configuratie.

Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).

