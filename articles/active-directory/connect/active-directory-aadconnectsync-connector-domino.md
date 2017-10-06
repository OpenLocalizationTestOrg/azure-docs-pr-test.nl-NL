---
title: aaaLotus Domino-Connector | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooconfigure Microsofts Lotus Domino-Connector.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: e07fd469-d862-470f-a3c6-3ed2a8d745bf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: affef1fec91eb39f7e91ec274fdd1b3a9c4a32fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="lotus-domino-connector-technical-reference"></a>Technische naslaginformatie voor Lotus Domino-Connector
Dit artikel wordt beschreven hello Lotus Domino-Connector. Hallo-artikel geldt toohello producten te volgen:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Hotfix 4.1.3671.0 moet gebruiken of later [KB3092178](https://support.microsoft.com/kb/3092178).

Voor MIM2016 en FIM2010R2 Hallo Connector is beschikbaar als een download van Hallo [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-lotus-domino-connector"></a>Overzicht van hello Lotus Domino-Connector
Hello Lotus Domino-Connector kunt u het Hallo-synchronisatieservice toointegrate met IBM Lotus Domino-server.

Hallo volgende kenmerken worden vanuit een perspectief op hoog niveau wordt ondersteund door Hallo huidige release van Hallo-connector:

| Functie | Ondersteuning |
| --- | --- |
| Gekoppelde gegevensbron |Server: <li>Lotus Domino 8.5.x</li><li>Lotus Domino 9.x</li>Client:<li>Lotus Domino 8.5.x</li><li>Lotus Notes 9.x</li> |
| Scenario's |<li>Object levenscyclusbeheer</li><li>Beheer van groepen</li><li>Wachtwoordbeheer</li> |
| Bewerkingen |<li>Volledige en Delta-Import</li><li>Exporteren</li><li>Ingesteld en het wachtwoord op http-wachtwoord wijzigen</li> |
| Schema |<li>Persoon (gebruiker Roaming, neem contact op met (personen met geen enkel certificaat))</li><li>Groep</li><li>Resource (Resource, kamer, Online vergadering)</li><li>Database-e-mail in</li><li>Dynamische detectie van kenmerken voor ondersteunde objecten</li> |

hello Lotus Notes client toocommunicate Hello Lotus Domino-connector gebruikt met Lotus Domino-Server. Als gevolg van deze afhankelijkheid moet een ondersteunde Lotus Notes-Client op Hallo synchronisatieserver worden geïnstalleerd. Hallo-communicatie tussen Hallo client en server Hallo wordt geïmplementeerd via hello Lotus Notes .NET Interop (Interop.domino.dll)-interface. Deze interface vergemakkelijkt de communicatie tussen Hallo Microsoft.NET platform en Lotus Notes client hello en biedt ondersteuning voor toegang tot tooLotus Domino documenten en weergaven. Voor de delta-import is het ook mogelijk dat die systeemeigen Hallo C++-interface (afhankelijk van de methode voor Hallo geselecteerd delta-import) wordt gebruikt.

### <a name="prerequisites"></a>Vereisten
Zorg voordat u Hallo Connector gebruikt, hebt u Hallo vereisten op Hallo synchronisatieserver te volgen:

* Microsoft.NET 4.5.2 of hoger
* Hello Lotus Notes-client moet worden geïnstalleerd op uw server voor de synchronisatie
* Hello Lotus Domino-Connector vereist Hallo standaard Lotus Domino LDAP-schema-database (schema.nsf) toobe aanwezig is op Hallo Domino-adreslijstserver. Als dit niet aanwezig is, kunt u deze installeren door uitgevoerd of Hallo LDAP-service op Hallo Domino-server opnieuw te starten.

### <a name="connected-data-source-permissions"></a>Verbonden gegevensbron machtigingen
tooperform van Hallo taken in Lotus Domino-connector ondersteund, moet u lid zijn van de volgende groepen:

* Beheerders met volledige toegang
* Beheerders
* Databasebeheerders

Hallo bevat volgende tabel Hallo machtigingen die vereist voor elke bewerking zijn:

| Bewerking | Toegangsrechten |
| --- | --- |
| Importeren |<li>Openbare documenten lezen</li><li> Volledige toegang beheerder (wanneer u lid van de groep administrators volledige toegang bent, automatisch hebt Hallo effectieve toegang tooin ACL.)</li> |
| Exporteren en het wachtwoord instellen |Effectieve toegang: <li>Documenten maken</li><li>Documenten verwijderen</li><li>Openbare documenten lezen</li><li>Openbare documenten schrijven</li><li>Repliceren of een kopie van documenten</li>Voor bewerkingen exporteren moet u ook Hallo rollen te volgen: <li>CreateResource</li><li>GroupCreator</li><li>GroupModifier</li><li>UserCreator</li><li>UserModifier</li> |

### <a name="direct-operations-and-adminp"></a>Directe bewerkingen en AdminP
Bewerkingen gaat u rechtstreeks toohello Domino directory of via Hallo AdminP niet verwerken. Hello volgende tabellen worden alle ondersteunde objecten, operations en, indien van toepassing, Hallo implementatie methode gekoppeld:

**Primaire adresboek**

| Object | Maken | Update | Verwijderen |
| --- | --- | --- | --- |
| Persoon |AdminP |Directe |AdminP |
| Groep |AdminP |Directe |AdminP |
| MailInDB |Directe |Directe |Directe |
| Resource |AdminP |Directe |AdminP |

**Secundaire adresboek**

| Object | Maken | Update | Verwijderen |
| --- | --- | --- | --- |
| Persoon |N.v.t. |Directe |Directe |
| Groep |Directe |Directe |Directe |
| MailInDB |Directe |Directe |Directe |
| Resource |N.v.t. |N.v.t. |N.v.t. |

Wanneer een resource is gemaakt, wordt een Notes-document gemaakt. Wanneer een resource wordt verwijderd, wordt op dezelfde manier hello Lotus Notes-document verwijderd.

### <a name="ports-and-protocols"></a>Poorten en protocollen
IBM Lotus Notes-client en Domino-servers communiceren met opmerkingen Remote Procedure Call (NRPC) waar NRPC TCP/IP moet gebruiken. Hallo standaardpoortnummer 1352 is, maar kan worden gewijzigd door Hallo Domino-beheerder.

### <a name="not-supported"></a>Niet ondersteund
Hallo volgende bewerkingen worden niet ondersteund door de huidige release Hallo van hello Lotus Domino-connector:

* Postvak verplaatsen tussen servers.

## <a name="create-a-new-connector"></a>Een nieuwe Connector maken
### <a name="client-software-installation-and-configuration"></a>De installatie van clientsoftware en configuratie
Lotus Notes moeten worden geïnstalleerd op de server Hallo **voordat** Hallo-Connector is geïnstalleerd.

Wanneer u installeert, moet u een **installatie voor één gebruiker**. Standaard Hallo **Multi-User installeren** werkt niet.  
![Notes1](./media/active-directory-aadconnectsync-connector-domino/notes1.png)

Installeren op de pagina onderdelen Hallo alleen hello Lotus Notes functies vereist en **één clientaanmelding**. Eenmalige aanmelding is vereist voor Hallo connector toobe kunnen toolog op toohello Domino-server.  
![Notes2](./media/active-directory-aadconnectsync-connector-domino/notes2.png)

**Opmerking:** Start Lotus Notes wanneer dezelfde server als Hallo account aan een gebruiker die zich bevindt op Hallo u gebruiken als Hallo van connector-serviceaccount. Zorg ervoor dat tooclose hello Lotus Notes-client ook op Hallo-server. Kan niet worden uitgevoerd op Hallo probeert dezelfde tijd Hallo Connector tooconnect toohello Domino-server.

### <a name="create-connector"></a>Connector maken
een connector voor Lotus Domino tooCreate in **Synchronization Service** Selecteer **beheeragent** en **maken**. Selecteer Hallo **Lotus Domino (Microsoft)** Connector.  
![CreateConnector](./media/active-directory-aadconnectsync-connector-domino/createconnector.png)

Als uw versie van de synchronisatieservice Hallo mogelijkheid tooconfigure biedt **architectuur**, zorg ervoor dat de connector Hallo tooits standaard waarde toorun is ingesteld in **proces**.

### <a name="connectivity"></a>Connectiviteit
Op pagina Verbindingsmogelijkheden hello, moet u hello Lotus Domino-servernaam opgeeft en Hallo-aanmeldingsreferenties opgeven.  
![Connectiviteit](./media/active-directory-aadconnectsync-connector-domino/connectivity.png)

Hallo Domino servereigenschap ondersteunt twee indelingen voor het Hallo-servernaam:

* Servernaam
* ServerName/DirectoryName

Hallo **ServerName/DirectoryName** is de gewenste indeling Hallo voor dit kenmerk omdat deze sneller een antwoord biedt als Hallo connector contactpersonen Hallo Domino-Server.

Hallo opgegeven UserID bestand wordt opgeslagen in de configuratiedatabase Hallo van Hallo-synchronisatieservice.

Voor **Delta-Import** hebt u deze opties:

* **Geen**. Hallo Connector wordt niet een delta-invoer.
* **Toevoegen/bijwerken**. Hallo-Connector heeft delta-import toevoegen en bijwerken van bewerkingen. Om te verwijderen, een **volledige Import** bewerking is vereist. Hallo .net interop maakt gebruik van deze bewerking.
* **Toevoegen, bijwerken, verwijderen**. Hallo-Connector heeft delta-import toevoegen, bijwerken en verwijderen van bewerkingen. Deze bewerking maakt gebruik van de native C++-interfaces Hallo.

In **schemaopties** er Hallo volgende opties:

* **Standaard Schema**. Hallo Connector detecteert Hallo-schema van Hallo Domino-server. Dit is de standaardoptie Hallo.
* **DSML Schema**. Alleen gebruikt als Hallo Domino-server wordt Hallo-schema niet beschikbaar. Vervolgens kunt u een bestand DSML met Hallo schema maken en importeer dit in plaats daarvan. Zie voor meer informatie over DSML [OASIS](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=dsml).

Wanneer u op Volgende klikt, worden Hallo gebruikersnaam en wachtwoord configuratieparameters gecontroleerd.

### <a name="global-parameters"></a>Globale Parameters
Op Hallo globale Parameters pagina configureert Hallo tijdzone en Hallo importeren en exporteren van de optie bij bewerking.  
![Globale Parameters](./media/active-directory-aadconnectsync-connector-domino/globalparameters.png)

Hallo **Domino servertijdzone** parameter definieert Hallo-locatie van uw Domino-Server.

Deze configuratieoptie is vereist toosupport **delta-import** operations omdat hij Hiermee Hallo-synchronisatieservice wijzigingen tussen de laatste twee invoer Hallo bepalen.

>[!Note]
Vanaf maart 2017 update Hallo globale parameters welkomstscherm omvat Hallo optie toodelete Hallo van de gebruiker van e-maildatabase bij het verwijderen van de gebruiker Hallo.

![Verwijderen van het postvak van gebruiker](./media/active-directory-aadconnectsync-connector-domino/AdminP.png)

#### <a name="import-settings-method"></a>Instellingen importeren, methode
Hallo **volledige Import uitvoeren door** volgende opties:

* Search
* Weergave (aanbevolen)

**Search** is met behulp van indexeren in Domino, maar er is gebruikelijk dat Hallo indexen niet in realtime bijgewerkt worden en Hallo-gegevens geretourneerd vanaf de Hallo-server niet altijd correct is. Voor een systeem met veel wijzigingen deze optie meestal niet goed werkt en false worden verwijderd in sommige situaties biedt. Echter, **search** sneller dan **weergave**.

**Weergave** wordt Hallo aanbevolen optie omdat de juiste status Hallo van gegevens biedt. Er is iets langer dan zoeken.

#### <a name="creation-of-virtual-contact-objects"></a>Maken van virtuele contact op met objecten
Hallo **maken van een \_object contactpersonen** volgende opties:

* Geen
* Niet-verwijzingsvariant waarden
* Naslaggids voor niet waarden

In Domino bevatten verwijzingskenmerken veel verschillende indelingen tooreference andere objecten. toobe kunnen toorepresent verschillende variaties, Hallo Connector implementeert \_contact op met objecten, ook wel bekend als **virtuele contactpersonen** (VC). Deze objecten zijn gemaakt, zodat u ze kunnen deelnemen aan tooexisting MV-objecten of geprojecteerd als nieuwe objecten. Op deze manier kunnen kenmerk verwijzingen worden bewaard.

Door deze instelling inschakelt en als het Hallo-inhoud van een verwijzingskenmerk is niet een DN-indeling een \_Contact-object is gemaakt. Een Lidkenmerk van een groep kan bijvoorbeeld de SMTP-adressen bevatten. Het is ook mogelijk toohave korte naam en andere kenmerken in verwijzingskenmerken. Selecteer voor dit scenario **niet referentiewaarden**. Deze configuratie is de meest voorkomende instelling Hallo voor Domino-implementaties.

Wanneer Lotus Domino geconfigureerde toohave afzonderlijke adresboeken met verschillende DN-namen die hetzelfde object Hallo, maakt u de mogelijke tooalso \_Neem contact op met de objecten voor alle verwijzing waarden die zijn gevonden in een adresboek. Selecteer voor dit scenario Hallo **referentie- en Non-referentiewaarden** optie.

Als er meerdere waarden in Hallo kenmerk **FullName** in Domino, vervolgens wilt u er ook tooenable Hallo aanmaken van virtuele contactpersonen dus verwijzingen omgezet worden kunnen. Dit kenmerk kan bijvoorbeeld meerdere waarden hebben na een huwelijk of echtscheiding. Schakel dit selectievakje in Hallo **inschakelen... Volledige naam heeft meerdere waarden** voor dit scenario.

Door op de juiste kenmerken hello, Hallo \_Neem contact op met objecten zou worden gekoppelde toohello MV-object.

Deze objecten hebben VC =\_contactpersoon tootheir DN-naam toegevoegd.

#### <a name="import-settings-conflict-object"></a>Instellingen importeren, object in conflict
**Conflict-Object uitsluiten**

In een grote Domino-implementatie is het mogelijk dat meerdere objecten dezelfde DN vanwege tooreplication problemen hebben Hallo. In dergelijke gevallen ziet Hallo connector twee objecten met verschillende UniversalIDs maar dezelfde DN-naam. Dit conflict zou leiden tot een tijdelijk object wordt gemaakt in Hallo connectorgebied overgebracht. Hallo Connector kunt negeren Hallo-objecten die zijn geselecteerd in Domino als slachtoffer van replicatie. Hallo-aanbeveling is tookeep dit selectievakje ingeschakeld.

#### <a name="export-settings"></a>Instellingen exporteren
Als hello optie **AdminP gebruiken voor het bijwerken van verwijzingen** niet is geselecteerd, dan is het exporteren van de referentie-kenmerken, zoals lid, een directe aanroep en gebruikt geen Hallo AdminP proces. Gebruik deze optie alleen als AdminP niet geconfigureerd toomaintain referentiële integriteit is.

#### <a name="routing-information"></a>Informatie over routering
In Domino is het mogelijk dat een verwijzingskenmerk routinggegevens ingesloten als een achtervoegsel toohello DN-naam heeft. Bijvoorbeeld, Hallo lid een kenmerk in een groep kan bevatten **CN =example/organization@ABC**. Hallo achtervoegsel @ABC Hallo routinggegevens is. Hallo route-informatie wordt gebruikt door Domino toosend e-mailberichten toohello juiste Domino systeem, wat erop kan een systeem in een andere organisatie. In Hallo routeringsgegevens veld, kunt u routering Hallo-achtervoegsels gebruikt binnen de organisatie Hallo binnen het bereik van Hallo Connector. Als een van deze waarden in een verwijzingskenmerk als achtervoegsel wordt gevonden, wordt de routinggegevens Hallo van Hallo verwijzing verwijderd. Als Hallo routering achtervoegsel op referentiewaarde overeenkomende tooone van deze waarden wordt opgegeven, niet kan worden een \_Contact-object is gemaakt. Deze \_Neem contact op met objecten zijn gemaakt met **RO = @<RoutingSuffix>**  ingevoegd in Hallo DN-naam. Voor deze \_Contact-objecten Hallo na kenmerken ook zijn toegevoegd tooallow lid worden van het juiste object tooa indien nodig: \_routingName, \_contactpersoon, \_displayName, en UniversalID.

#### <a name="additional-address-books"></a>Extra adresboeken
Als u nog geen **telefoonboek** geïnstalleerd, waarmee u Hallo-naam van de secundaire adresboeken en vervolgens kunt u deze adresboeken handmatig invoeren.

#### <a name="multivalued-transformation"></a>Met meerdere waarden transformatie
Er zijn veel kenmerken in Lotus Domino met meerdere waarden. Hallo bijbehorende metaverse-kenmerken worden doorgaans één waarden. Hallo importeren en de bewerking exportoptie Hallo configureert, kunnen Hallo connector toohelp met Hallo vereist vertaling van Hallo van invloed op een kenmerken.

**Exporteren**  
de bewerking exportoptie Hallo ondersteunt twee modi:

* Item toevoegen
* Item vervangen

**Item vervangen** – wanneer u deze optie, altijd Hallo-connector verwijderen Hallo huidige waarden van Hallo-kenmerk in Domino selecteert en vervang ze door Hallo opgegeven waarden. Hallo opgegeven mag waarden één waarde of meerdere waarden.

Voorbeeld: Hallo assistent kenmerk van een persoon-object heeft Hallo volgende waarden:

* CN = Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN = John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Als een nieuwe assistent met de naam **David Alexander** is toegewezen toothis persoon object, Hallo resultaat is:

* CN = David Alexander/OU=Contoso/O=Americas,NAB=names.nsf

**Item toevoegen** – wanneer u deze optie selecteert, Hallo connector behoudt Hallo bestaande waarden op Hallo-kenmerk in Domino en insert nieuwe waarden bovenaan Hallo Hallo gegevenslijst.

Voorbeeld: Hallo assistent kenmerk van een persoon-object heeft Hallo volgende waarden:

* CN = Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN = John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Als een nieuwe assistent met de naam **David Alexander** is toegewezen toothis persoon object, Hallo resultaat is:

* CN = David Alexander/OU=Contoso/O=Americas,NAB=names.nsf
* CN = Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN = John Smith/OU=Contoso/O=Americas,NAB=names.nsf

**Importeren**  
Hallo importeren bewerking optie ondersteunt twee modi:

* Standaard
* Met meerdere waarden tooSingle waarde

**Standaard** – wanneer u Hallo standaardoptie selecteert, alle waarden van alle Hallo kenmerken worden geïmporteerd.

**Met meerdere waarden tooSingle waarde** – wanneer u deze optie selecteert, een kenmerk met meerdere waarden wordt omgezet in een kenmerk met één waarde. Als meer dan één waarde bestaat, wordt de waarde Hallo bovenaan hello (deze waarde is meestal ook Hallo recente) gebruikt.

Voorbeeld: Hallo assistent kenmerk van een persoon-object heeft Hallo volgende waarden:

* CN = David Alexander/OU=Contoso/O=Americas,NAB=names.nsf
* CN = Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN = John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Hallo meest recente update toothis kenmerk is **David Alexander**. Omdat Hallo optie importeren-bewerking is tooMultivalued tooSingle waarde ingesteld, worden alleen connector geïmporteerd **David Alexander** naar Hallo connectorgebied overgebracht.

Hallo logica tooconvert met meerdere waarden kenmerken in kenmerken met één waarde is niet van toepassing toohello groep Lidkenmerk en toohello persoon fullname kenmerk.

Het ook mogelijk tooconfigure regels importeren en exporteren transformatie voor kenmerken met meerdere waarden per kenmerk, als een algemene uitzondering toohello-regel. tooconfigure deze optie, voer [objecttype]. [attributename] in Hallo **importeren kenmerk uitsluitingslijst** en **exporteren kenmerk uitsluitingslijst** tekstvakken. Bijvoorbeeld, wordt alle waarden, alleen de eerste waarde Hallo voor Hallo-assistent geïmporteerd als u Person.Assistant invoert en Hallo globale vlag tooimport is ingesteld.

#### <a name="certifiers"></a>Certifiers
Hallo-connector worden alle organisatie/organisatie-eenheden weergegeven. toobe kunnen tooexport objecten toohello primaire adresboek persoon, een certifier met het wachtwoord is vereist.

Als alle certifiers Hallo hetzelfde wachtwoord hello **wachtwoord voor alle Certifers** kan worden gebruikt. Vervolgens kunt u hier Hallo wachtwoord invoeren en alleen Hallo certifier bestand opgeven.

Als u alleen importeert, hebt nog u geen toospecify eventuele certifiers.

### <a name="configure-provisioning-hierarchy"></a>Hiërarchie inrichten configureren
Wanneer u hello Lotus Domino-connector configureert, moet u deze pagina dialoogvenster overslaan. Hello Lotus Domino-connector ondersteunt geen hiërarchie inrichten.  
![Hiërarchie inrichten](./media/active-directory-aadconnectsync-connector-domino/provisioninghierarchy.png)

### <a name="configure-partitions-and-hierarchies"></a>Partities en hiërarchieën configureren
Wanneer u partities en hiërarchieën configureren, moet u de primaire adresboek Hallo aangeroepen NAB=names.nsf selecteren. Bovendien toohello primaire adresboek, kunt u secundaire adresboeken indien ze bestaan.  
![Partities](./media/active-directory-aadconnectsync-connector-domino/partitions.png)

### <a name="select-attributes"></a>Kenmerken selecteren
Wanneer u de kenmerken configureert, moet u alle kenmerken die worden voorafgegaan door  **\_MMS\_**. Deze kenmerken zijn vereist wanneer u nieuwe objecten tooLotus Domino inrichten

![Kenmerken](./media/active-directory-aadconnectsync-connector-domino/attributes.png)

## <a name="object-lifecycle-management"></a>Object levenscyclusbeheer
Deze sectie biedt een overzicht van de verschillende objecten Hallo in Domino.

### <a name="person-objects"></a>Objecten van de persoon
Hallo persoon object stelt gebruikers in de organisatie en organisatie-eenheden. Toohello standaardkenmerken, Hallo Domino beheerder kunnen bovendien aangepaste kenmerken tooa persoon object toevoegen. Ten minste moet een object persoon alle verplichte kenmerken bevatten. Zie voor een volledige lijst van verplichte kenmerken [Lotus Notes-eigenschappen](#lotus-notes-properties). tooregister een persoon-object, Hallo volgende vereisten moet worden voldaan:

* Hallo-adresboek (names.nsf) moet zijn gedefinieerd en deze moet de primaire adresboek Hallo.
* U moet beschikken over Hallo O/organisatie-eenheid certifier-Id en het Hallo wachtwoord tooregister een bepaalde gebruiker Hallo organisatie / organisatie-eenheid.
* U moet een specifieke set met Lotus Notes eigenschappen voor een persoon-object instellen. Deze eigenschappen worden gebruikt voor het inrichten van Hallo persoon object. Zie voor meer informatie, Hallo sectie [Lotus Notes-eigenschappen](#lotus-notes-properties) verderop in dit document.
* Hallo eerste HTTP-wachtwoord voor een persoon is een kenmerk en een set tijdens het inrichten.
* Hallo persoon object moet een Hallo na drie ondersteunde typen:
  1. Normaal-gebruiker met een e-mail en een gebruiker-id-bestand
  2. Zwervende gebruiker (een normale gebruiker waarin alle zwervende databasebestanden)
  3. Contactpersonen (gebruiker met geen id-bestand)

Personen (met uitzondering van contactpersonen) kunnen verder worden gegroepeerd in ons gebruikers en internationale gebruikers, zoals gedefinieerd door de waarde van Hallo Hallo \_MMS\_IDRegType-eigenschap. Deze mensen tooaccess van de opmerkingen bij de Client hello Lotus Domino-servers gebruiken, hebben een opmerkingen-Id en een persoon-document. Als ze met opmerkingen bij de e-mail, vervolgens hebben ze ook een e-mailbestand. Hallo-gebruiker moet geregistreerde toobecome actief zijn. Zie voor meer informatie:

* [Opmerkingen bij de gebruikers instellen](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_SETTING_UP_NOTES_USERS.html)
* [Gebruikersregistratie](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_REGISTERING_USERS.html)
* [Het beheren van gebruikers](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_USERS_5151.html)
* [Naam van gebruikers](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_USER_AUTOMATICALLY.html)

Alle deze bewerkingen worden uitgevoerd in Lotus Domino en vervolgens geïmporteerd in het Hallo-synchronisatieservice.

### <a name="resources-and-rooms"></a>Ruimten en resources
Een bron is een ander type van een database in Lotus Domino. Resources kunnen worden vergaderruimten met verschillende soorten apparatuur, zoals projectors. Er zijn subtypen van bronnen die worden ondersteund door de connector voor Lotus Domino die zijn gedefinieerd door Hallo brontype kenmerk:

| Het type Resource | Kenmerk van het Type resource |
| --- | --- |
| Ruimte |1 |
| Resource (Other) |2 |
| Online vergaderingen |3 |

Hallo volgende is vereist voor Hallo Resource object type toowork:

* Reservering resourcedatabase moet al bestaan in Hallo verbonden Domino-server
* Hallo-site is al gedefinieerd voor Hallo Resource

Hallo reservering van de Resource-database bevat drie typen documenten:

* Profiel van uw site
* Resource
* Reservering

Zie voor meer informatie over het instellen van de database van de Resource-reservering [Hallo Resource reserveringen serverdatabase instellen](https://www-01.ibm.com/support/knowledgecenter/SSKTMJ_8.0.1/com.ibm.help.domino.admin.doc/DOC/H_SETTING_UP_THE_RESOURCE_RESERVATIONS_DATABASE.html).

**Maken, bijwerken, en Resources verwijderen**  
Hallo worden Create, Update en Delete-bewerkingen uitgevoerd door hello Lotus Domino-connector in Hallo reservering van de Resource-database. Resources worden gemaakt als documenten in Names.nsf (dat wil zeggen, Hallo primaire adresboek). Zie voor meer informatie over het bewerken en verwijderen van Resources [bewerken en verwijderen van de Resource-documenten](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_EDITING_AND_DELETING_RESOURCE_DOCUMENTS.html).

**Importeren en exporteren van de bewerking voor bronnen**  
Hallo Resources kan worden geïmporteerd tooand geëxporteerd uit de synchronisatieservice hello, zoals een ander objecttype. Selecteer Hallo objecttype als Resource tijdens de configuratie. Voor de exportbewerking is geslaagd, moet u de details voor resourcetype, conferentie Database en de naam van de Site hebben.

### <a name="mail-in-databases"></a>E-mail In Databases
Een Database Mail-In is een database die is ontworpen tooreceive e-mails. Het is een Lotus Domino-postvak is niet gekoppeld aan een specifieke Lotus Domino-gebruikersaccount (dat wil zeggen, het heeft geen eigen bestand ID en wachtwoord). Een e-mail in database heeft een unieke gebruikers-id ('korte naam') die zijn gekoppeld aan het bestand en een eigen e-mailadres.

Als er is een nodig voor een afzonderlijke Postvak met een eigen e-mailadres dat kan worden gedeeld met andere gebruikers (bijvoorbeeld group@contoso.com), een database mail in wordt gemaakt. Hallo toegang toothis postvak wordt geregeld via de lijst met ACL (Access Control), die Hallo-namen van Hallo opmerkingen bij de gebruikers die zijn toegestaan tooopen Hallo postvak bevat.

Zie voor een lijst van kenmerken vereist Hallo Hallo sectie [verplichte kenmerken](#mandatory-attributes) verderop in dit artikel.

Wanneer een database ontworpen tooreceive een e-mailbericht is, wordt een e-Mail In Database-document gemaakt in Lotus Domino. Dit document moet bestaan in de Directory Domino van elke server die een kopie van het Hallo-database opgeslagen. Zie voor een gedetailleerde beschrijving over het maken van een e-mail in databasedocument [maken van een e-Mail In Database-document](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_A_MAILIN_DATABASE_DOCUMENT_FOR_A_NEW_DATABASE_OVERVIEW.html).

Voordat u een e-Mail In Database maakt, moet al Hallo-database bestaan (moet zijn gemaakt door de beheerder Lotus) op Hallo Domino-server.

### <a name="group-management"></a>Beheer van groepen
U kunt een gedetailleerd overzicht van hello Lotus Domino groepsbeheer krijgen van Hallo resources te volgen:

* [Met behulp van groepen](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_USING_GROUPS_OVER.html)
* [Maken van een groep](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS_MIDTOPIC_55038956829238418.html)
* [Maken en wijzigen van groepen](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS.html)
* [Groepen beheren](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_GROUPS_1804.html)
* [Naam van een groep](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_GROUP_STEPS.html)

### <a name="password-management"></a>Wachtwoordbeheer
Er zijn twee typen van wachtwoorden voor een geregistreerde Lotus Domino-gebruiker:

1. Wachtwoord van gebruiker (opgeslagen in User.id-bestand)
2. Internet / HTTP-wachtwoord

Hello Lotus Domino-connector ondersteunt alleen bewerkingen met HTTP-wachtwoord.

Wachtwoordbeheer tooperform, moet u wachtwoordbeheer voor Hallo-connector in Hallo Management Agent Designer inschakelen. Selecteer tooenable-wachtwoordbeheer **inschakelen wachtwoordbeheer** op Hallo **uitbreidingen configureren** dialoogvenster pagina.  
![Extensies configureren](./media/active-directory-aadconnectsync-connector-domino/configureextensions.png)

Hello Lotus Domino-connector ondersteuning voor volgende bewerkingen worden uitgevoerd op internetwachtwoord:

* Instellen van het wachtwoord:-Wachtwoord instellen wordt een nieuw wachtwoord voor de HTTP-Internet op Hallo-gebruiker in Domino. Standaard is ook Hallo account ontgrendeld. Hallo ontgrendelen vlag wordt weergegeven op de WMI-interface Hallo Hallo synchronisatie-Engine.
* Wachtwoord wijzigen: In dit scenario wordt een gebruiker wellicht toochange Hallo wachtwoord of na vragen aan gebruiker toochange wachtwoord is na een opgegeven periode. Voor deze bewerking tootake plaats, zowel (Hallo oude en nieuwe wachtwoord Hallo) zijn verplicht. Nadat u gewijzigd, wordt in Lotus Domino Hallo nieuw wachtwoord bijgewerkt.

Zie voor meer informatie:

* [Met behulp van Hallo Internet accountvergrendeling](http://www.ibm.com/developerworks/lotus/library/domino8-lockout/)
* [Wachtwoorden voor het beheer van Internet](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_NOTES_AND_INTERNET_PASSWORD_SYNCHRONIZATION_7570_OVER.html)

## <a name="reference-information"></a>Referentie-informatie
Deze sectie vindt u zoals beschrijvingen van kenmerken en kenmerk vereisten voor hello Lotus Domino-connector.

### <a name="lotus-notes-properties"></a>Lotus Notes-eigenschappen
Wanneer u persoon objecten tooyour Lotus Domino directory inricht, moeten uw objecten een specifieke set eigenschappen hebben met specifieke waarden ingevuld. Deze waarden zijn alleen vereist voor bewerkingen maakt.

Hallo volgende tabel worden deze eigenschappen en bevat een beschrijving van deze.

| Eigenschap | Beschrijving |
| --- | --- |
| \_MMS_AltFullName |Hallo alternatieve volledige naam van gebruiker. |
| \_MMS_AltFullNameLanguage |Hallo taal toobe gebruikt voor het opgeven van Hallo alternatieve volledige naam van gebruiker. |
| \_MMS_CertDaysToExpire |aantal dagen vanaf Hallo vandaag voordat het certificaat van Hallo Hallo verloopt. Als niet wordt opgegeven, is Hallo standaarddatum twee jaar Hallo na de huidige datum. |
| \_MMS_Certifier |De eigenschap die Hallo de naam van de organisatie-hiërarchie van Hallo certifier bevat. Bijvoorbeeld: OU = OrganizationUnit, O = Org, C = land. |
| \_MMS_IDPath |Als de eigenschap Hallo leeg is, wordt geen gebruiker identificatie-bestand lokaal gemaakt op Hallo synchronisatieserver. Als het Hallo-eigenschap bevat een bestandsnaam, wordt een gebruikers-id-bestand gemaakt in Hallo madata map. Hallo-eigenschap kan ook een volledig pad bevatten. |
| \_MMS_IDRegType |Personen kunnen worden geclassificeerd als contactpersonen, ons en internationale gebruikers. Hallo bevat volgende tabel Hallo mogelijke waarden: <li>0 - Neem contact op met</li><li>1 - VS-gebruiker</li><li>2 - internationale gebruikers</li> |
| \_MMS_IDStoreType |Vereiste eigenschap voor de Verenigde Staten en internationale gebruikers. Hallo-eigenschap bevat een integerwaarde die aangeeft of Hallo gebruikers-id wordt opgeslagen als een bijlage in Hallo notities adresboek of in e-mailbestand van Hallo persoon. Als Hallo gebruikers-ID-bestand een bijlage van Hallo adresboek is, het eventueel kan worden gemaakt als een bestand met \_MMS_IDPath. <li>Lege - opslag-ID-bestand in de kluis-ID, geen identificatiebestand (gebruikt voor contactpersonen).</li><li> 1 - bijlage in Hallo notities adresboek. Hallo \_MMS_Password-eigenschap moet worden ingesteld voor gebruikers-id-bestanden die bijlagen</li><li>2 - ID in van de persoon mailbestand opslaan. Hallo \_MMS_UseAdminP toofalse toolet Hallo mail moet worden ingesteld tijdens Hallo persoon registratie bestand worden gemaakt. Hallo \_MMS_Password-eigenschap moet worden ingesteld voor identificatie van gebruikersbestanden.</li> |
| \_MMS_MailQuotaSizeLimit |Hallo aantal megabytes die zijn toegestaan voor Hallo e-databasebestand. |
| \_MMS_MailQuotaWarningThreshold |Hallo aantal megabytes die zijn toegestaan voor Hallo e-databasebestand voordat er een waarschuwing weergegeven. |
| \_MMS_MailTemplateName |Hallo e-sjabloonbestand dat gebruikte toocreate Hallo gebruiker e-bestand. Als een sjabloon wordt opgegeven, wordt met behulp van de opgegeven sjabloon Hallo Hallo mail-bestand gemaakt. Als er geen sjabloon is opgegeven, is Hallo standaardsjabloonbestand gebruikte toocreate Hallo-bestand. |
| \_MMS_OU |Optionele eigenschap Hallo OE-naam onder Hallo certifier is. Deze eigenschap mag niet leeg zijn voor contactpersonen. |
| \_MMS_Password |Vereiste eigenschap voor gebruikers. Hallo-eigenschap bevat Hallo wachtwoord voor Hallo identificatie-bestand van Hallo-object. |
| \_MMS_UseAdminP |De eigenschap moet set tootrue als e-mailbestand Hallo moet worden gemaakt door Hallo AdminP proces op Hallo Domino-server (exportproces asynchrone toohello). Als de eigenschap toofalse is ingesteld, is Hallo e-mailbestand gemaakt met Hallo Domino gebruiker (synchrone in Hallo exportproces). |

Voor een gebruiker met een identificatiebestand gekoppeld Hallo \_MMS_Password-eigenschap moet een waarde bevatten. Voor toegang tot e-mail via hello Lotus Notes client bevatten Hallo MailServer en MailFile eigenschappen van een gebruiker een waarde.

tooaccess via een webbrowser, e-mailberichten Hallo volgende eigenschappen moet waarden bevatten:

* MailFile - vereiste eigenschap met pad Hallo op hello Lotus Domino-server waar Hallo mail-bestand wordt opgeslagen.
* MailServer - vereiste eigenschap met de naam Hallo van hello Lotus Domino-server. Deze waarde is Hallo naam toouse tijdens het maken van hello Lotus e-mailbestand op Hallo Domino-server.
* HTTPPassword - optionele eigenschap die Hallo Web access wachtwoord voor Hallo-object bevat.

tooaccess Hallo Domino-Server zonder de mail-toepassing, Hallo HTTPPassword-eigenschap moet een waarde bevatten. Hallo MailFile eigenschap en Hallo MailServer-eigenschap kan niet leeg zijn.

Met \_MMS_ IDStoreType (store-id in e-mailbestand), 2 = Hallo MailSystem-eigenschap van NotesRegistrationclass tooREG_MAILSYSTEM_INOTES (3) is ingesteld.

### <a name="mandatory-attributes"></a>Verplichte kenmerken
Hello Lotus Domino-connector ondersteunt hoofdzakelijk de volgende typen objecten (documenttypen):

* Groep
* Database-e-mail In
* Persoon
* Neem contact op met (iemand die geen certifier)
* Resource

Deze sectie vindt Hallo kenmerken die verplicht voor elk ondersteund object tooexport tooa Domino-server zijn.

| Objecttype | Verplichte kenmerken |
| --- | --- |
| Groep |<li>ListName</li> |
| Main In Database |<li>Volledige naam</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |
| Persoon |<li>Achternaam</li><li>MailFile</li><li>Korte naam</li><li>\_MMS_Password</li><li>\_MMS_IDStoreType</li><li>\_MMS_Certifier</li><li>\_MMS_IDRegType</li><li>\_MMS_UseAdminP</li> |
| Neem contact op met (iemand die geen certifier) |<li>\_MMS_IDRegType</li> |
| Resource |<li>Volledige naam</li><li>ResourceType</li><li>ConfDB</li><li>Resourcecapaciteit</li><li>Site</li><li>Weergavenaam</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |

## <a name="common-issues-and-questions"></a>Veelvoorkomende problemen en vragen
### <a name="schema-detection-does-not-work"></a>Schema-detectie werkt niet
toobe kunnen toodetect Hallo-schema, is het nodig dat Hallo schema.nsf-bestand aanwezig is op Hallo Domino-server. Dit bestand wordt alleen weergegeven als LDAP is geïnstalleerd op Hallo-server. Als het Hallo-schema niet is gedetecteerd, controleert u of Hallo volgende:

* Hallo bestand schema.nsf is aanwezig op de hoofdmap Hallo Hallo Domino-Server
* Hallo gebruiker heeft machtigingen toosee hello schema.nsf bestand.
* Automatisch opnieuw opgestart van Hallo LDAP-server. Open **Lotus Domino Console** en gebruik **vertellen LDAP ReloadSchema** opdracht tooreload Hallo schema.

### <a name="not-all-secondary-address-books-are-visible"></a>Niet alle secundaire adresboeken zijn zichtbaar.
Hallo Domino-Connector is afhankelijk van de functie Hallo **telefoonboek** toobe kunnen toofind Hallo secundaire adresboeken. Als de secundaire adresboeken Hallo ontbreken, controleert u of als [telefoonboek](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_DIRECTORY_ASSISTANCE.html) is ingeschakeld en geconfigureerd op Hallo Domino-Server.

### <a name="custom-attributes-in-domino"></a>Aangepaste kenmerken in Domino
Er zijn verschillende manieren in Domino tooextend Hallo schema zodat deze wordt weergegeven als een aangepast kenmerk worden gebruikt door Hallo Connector.

**Methode 1: Lotus Domino-schema uitbreiden**

1. Maak een kopie van sjabloon van de Directory Domino {PUBNAMES. NTF} door [deze stappen](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (u moet geen Hallo IBM Lotus Domino standaarddirectory sjabloon aanpassen):
2. Sjabloon van een kopie van Domino directory Open Hallo {CONTOSO. De sjabloon NTF} die is gemaakt in de ontwerpfunctie Domino en als volgt te werk:
   * Klik op gedeelde elementen en vouw subformulieren
   * Dubbelklik op ${ObjectName} InheritableSchema subformulier (waarbij {ObjectName} Hallo naam is van Hallo standaard structurele objectklasse, bijvoorbeeld: persoon).
   * Geef een naam Hallo kenmerk gewenste tooadd in schema {MyPersonAtrribute} en bijbehorende toothat-kenmerk. Maken van een veld met Selecteer Hallo **maken** Menu en selecteer vervolgens **veld** in het menu van.
   * In Hallo instellen toegevoegd veld eigenschappen ervan door het Type, stijl, grootte, lettertype en andere gerelateerde parameters voor veld van het venster Eigenschappen te selecteren.
   * Houd Hallo kenmerk standaardwaarde is dezelfde als Hallo-naam opgegeven voor dit kenmerk (bijvoorbeeld als de kenmerknaam van het MyPersonAttribute is, de standaardwaarde Hallo Hello aanhouden dezelfde naam).
   * Hallo ${ObjectName} InheritableSchema subformulier opslaan met bijgewerkte waarden.
3. Vervang Hallo Domino Directory sjabloon {PUBNAMES. NTF} met Hallo nieuwe aangepaste sjabloon {CONTOSO. NTF} door [deze stappen](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
4. Domino Admin sluit en open Domino Console toorestart Hallo LDAP-service en tooReload Hallo LDAP Schema:
   * Invoegen in de Console Domino Hallo opdracht onder **Domino opdracht** tekst ingediend toorestart Hallo LDAP-service - [starten taak LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
   * tooreload LDAP schema gebruiken vertellen LDAP-command - LDAP-ReloadSchema vertellen
5. Open Domino Admin en selecteer personen en groepen tabblad toosee toegevoegd kenmerk wordt weergegeven in domino persoon toevoegen.
6. Open Schema.nsf van **bestanden** tabblad en Zie toegevoegde kenmerk wordt weergegeven in de klasse dominoPerson LDAP-object.

**Methode 2: Een auxClass met het aangepaste kenmerk maken en koppelen aan de klasse object Hallo**

1. Maak een kopie van sjabloon van de Directory Domino {PUBNAMES. NTF} door [deze stappen](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (nooit Hallo IBM Lotus Domino standaarddirectory sjabloon aanpassen):
2. Sjabloon van een kopie van Domino directory Open Hallo {CONTOSO. De sjabloon NTF} die is gemaakt in de ontwerpfunctie Domino.
3. Selecteer in het linkerdeelvenster Hallo Code gedeeld en subformulieren.
4. Klik op nieuwe subformulier
5. Hallo na toospecify Hallo eigenschappen voor de nieuwe subformulier Hallo:
   * Met de nieuwe subformulier Hallo open, kies de ontwerp - subformulier eigenschappen
   * Volgende toohello Name-eigenschap, voer een naam voor Hallo reserve objectklasse--bijvoorbeeld TestSubform.
   * De eigenschap Options Hallo houden 'Opnemen in subformulier Insert... dialoogvenster' geselecteerd
   * Hef de selectie Hallo opties voor de eigenschap "Render worden verzonden via de HTML-code in de notities."
   * Laat de eigenschap Hallo andere eigenschappen Hallo dezelfde en sluit Hallo subformulier dialoogvenster.
   * Opslaan en sluiten van de nieuwe subformulier Hallo.
6. Hallo na een veld toodefine Hallo reserve objectklasse tooadd:
   * Open Hallo subformulier die u hebt gemaakt.
   * Kies maken - veld.
   * Volgende tooName op Hallo basisbeginselen tabblad van Hallo veld in het dialoogvenster geeft u een naam, bijvoorbeeld: {MyPersonTestAttribute}.
   * In veld Hallo toegevoegd, moet u de eigenschappen instellen door het selecteren van het Type, stijl, grootte, lettertype en bijbehorende eigenschappen.
   * Houd Hallo kenmerk standaardwaarde is dezelfde als Hallo-naam opgegeven voor dit kenmerk (bijvoorbeeld als de kenmerknaam van het MyPersonTestAttribute is, de standaardwaarde Hallo Hello aanhouden dezelfde naam).
   * Hallo subformulier worden opgeslagen met de bijgewerkte waarden en Hallo te volgen:
     * Selecteer in het linkerdeelvenster Hallo Code gedeeld en vervolgens subformulieren
     * Selecteer nieuw subformulier hello, en kies ontwerp - ontwerpeigenschappen.
     * Klik op de derde tabblad Hallo van Hallo links en selecteer **doorgegeven deze verbieden van ontwerpwijziging**.
7. Open ${ObjectName} ExtensibleSchema subformulier ({ObjectName} is de naam Hallo van Hallo standaard structurele object-klasse, bijvoorbeeld – persoon).
8. Resource invoegen, selecteer Hallo subformulier (die u hebt gemaakt, bijvoorbeeld – TestSubform) en Hallo ${ObjectName} ExtensibleSchema subformulier opslaan.
9. Vervang Hallo Domino Directory sjabloon {PUBNAMES. NTF} met Hallo nieuwe aangepaste sjabloon {CONTOSO. NTF} door [deze stappen](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
10. Domino Admin sluit en open Domino Console toorestart Hallo LDAP-service en tooReload Hallo LDAP Schema:
    * Invoegen in de Console Domino Hallo opdracht onder **Domino opdracht** tekst ingediend toorestart Hallo LDAP-service - [starten taak LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
    * tooreload LDAP schema vertellen LDAP-opdracht gebruiken **vertellen LDAP ReloadSchema**.
11. Open Domino Admin en selecteer personen en groepen tabblad toosee toegevoegd kenmerk wordt weergegeven in domino persoon toevoegen (onder andere tab).
12. Open Schema.nsf van **bestanden** tabblad en Zie toegevoegde kenmerk wordt weergegeven onder TestSubform LDAP reserve objectklasse.

**Methode 3: Hallo aangepast kenmerk toohello ExtensibleObject klasse toevoegen**

1. Open {Schema.nsf}-bestand geplaatst in de hoofdmap Hallo
2. Selecteer LDAP-objectklassen in Hallo linkermenu onder **alle Schema-documenten** en klik op **toevoegen objectklasse** knop:
3. Geef LDAP-naam in de vorm van de Hallo van {zzzExtensibleSchema} (waarbij zzz Hallo-naam van Hallo standaard structurele object-klasse, bijvoorbeeld persoon is). Bijvoorbeeld, bieden tooextend Hallo schema voor de klasse object persoon, LDAP-naam {PersonExtensibleSchema}.
4. Klassenaam van het bovenliggende Object waarvoor u tooextend Hallo schema wilt bieden. Bijvoorbeeld, bieden tooextend Hallo schema voor de objectklasse persoon klassenaam van bovenliggend Object {dominoPerson}:
5. Geef een geldige OID bijbehorende toohello objectklasse.
6. Selecteer uitgebreide/aangepaste kenmerken bij verplichte of optionele kenmerktypen velden volgens Hallo vereiste:
7. Nadat het toevoegen van vereiste kenmerken toohello ExtensibleObjectClass, klikt u op **opslaan en sluiten**.
8. Een ExtensibleObjectClass wordt gemaakt voor de objectklasse respectieve standaard met uitgebreide kenmerken.

## <a name="troubleshooting"></a>Problemen oplossen
* Zie voor informatie over hoe logboekregistratie tooenable tootroubleshoot connector Hallo Hallo [hoe tooEnable ETW-tracering voor Connectors](http://go.microsoft.com/fwlink/?LinkId=335731).
