---
title: aaaGeneric LDAP-Connector | Microsoft Docs
description: Dit artikel wordt beschreven hoe algemene LDAP-Connector van Microsoft tooconfigure.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 984beeb0-4d91-4908-ad81-c19797c4891b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 25031b4da196bd073902b04b0705762bfa0118b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="generic-ldap-connector-technical-reference"></a>Algemene LDAP-Connector, technische naslaginformatie
Dit artikel wordt beschreven Hallo algemene LDAP-Connector. Hallo-artikel geldt toohello producten te volgen:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Hotfix 4.1.3671.0 moet gebruiken of later [KB3092178](https://support.microsoft.com/kb/3092178).

Voor MIM2016 en FIM2010R2 Hallo Connector is beschikbaar als een download van Hallo [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

Wanneer tooIETF RFC's wordt verwezen, dit document Hallo-indeling wordt gebruikt (RFC [RFC aantal] / [section in RFC document]), bijvoorbeeld (RFC 4512/4.3).
U vindt meer informatie op http://tools.ietf.org/html/rfc4500 (u moet tooreplace 4500 met de juiste RFC-nummer Hallo).

## <a name="overview-of-hello-generic-ldap-connector"></a>Overzicht van Hallo algemene LDAP-Connector
Hallo algemene LDAP-Connector kunt u toointegrate Hallo synchronization-service met een LDAP v3-server.

Bepaalde bewerkingen en schema-elementen, zijn zoals die nodig is tooperform delta-import, niet opgegeven in Hallo IETF RFC's. Voor deze bewerkingen worden alleen LDAP-adreslijsten expliciet worden opgegeven ondersteund.

Hallo volgende kenmerken worden vanuit een perspectief op hoog niveau wordt ondersteund door Hallo huidige release van Hallo-connector:

| Functie | Ondersteuning |
| --- | --- |
| Gekoppelde gegevensbron |Hallo Connector aan alle LDAP v3-servers (compatibel met RFC 4510) wordt ondersteund. Het is getest met de volgende Hallo: <li>Microsoft Active Directory Lightweight Directory Services (AD LDS)</li><li>Microsoft Active Directory globale catalogus (GC AD)</li><li>389 directory-Server</li><li>Apache Directory-Server</li><li>IBM Tivoli DS</li><li>Isode Directory</li><li>NetIQ eDirectory</li><li>Novell eDirectory</li><li>Open DJ</li><li>Open Active Directory</li><li>Open LDAP (openldap.org)</li><li>Oracle (eerder Sun) Directory Server Enterprise Edition</li><li>Server van de virtuele map RadiantOne (VDS)</li><li>Een Sun directoryserver</li>**Opmerkelijke mappen wordt niet ondersteund:** <li>Microsoft Active Directory Domain Services (AD DS) [Gebruik Hallo ingebouwde Active Directory-Connector in plaats daarvan]</li><li>Oracle Internet Directory (OID)</li> |
| Scenario's |<li>Object levenscyclusbeheer</li><li>Beheer van groepen</li><li>Wachtwoordbeheer</li> |
| Bewerkingen |Hallo volgende bewerkingen worden ondersteund op alle LDAP-mappen: <li>Volledige Import</li><li>Exporteren</li>Hallo volgende bewerkingen worden alleen ondersteund op de opgegeven mappen:<li>Delta-import</li><li>Wachtwoord instellen, wachtwoord wijzigen</li> |
| Schema |<li>Schema is gedetecteerd door Hallo LDAP-schema (RFC3673 en RFC4512/4.2)</li><li>Ondersteunt structurele klassen, aux klassen en klasse extensibleObject-object (RFC4512/4.3)</li> |

### <a name="delta-import-and-password-management-support"></a>Delta-ondersteuning voor importeren en het wachtwoord
Mappen voor de Delta-import en een wachtwoordbeheer ondersteund:

* Microsoft Active Directory Lightweight Directory Services (AD LDS)
  * Biedt ondersteuning voor alle bewerkingen voor de delta-import
  * Ondersteunt het instellen van wachtwoord
* Microsoft Active Directory globale catalogus (GC AD)
  * Biedt ondersteuning voor alle bewerkingen voor de delta-import
  * Ondersteunt het instellen van wachtwoord
* 389 directory-Server
  * Biedt ondersteuning voor alle bewerkingen voor de delta-import
  * Ondersteunt het instellen en wijzigen-wachtwoord
* Apache Directory-Server
  * Biedt geen ondersteuning voor delta-import omdat deze map beschikt niet over een permanente wijzigingenlogboek
  * Ondersteunt het instellen van wachtwoord
* IBM Tivoli DS
  * Biedt ondersteuning voor alle bewerkingen voor de delta-import
  * Ondersteunt het instellen en wijzigen-wachtwoord
* Isode Directory
  * Biedt ondersteuning voor alle bewerkingen voor de delta-import
  * Ondersteunt het instellen en wijzigen-wachtwoord
* Novell eDirectory en NetIQ eDirectory
  * Ondersteunt bewerkingen voor toevoegen, bijwerken en wijzig de naam voor de delta-import
  * Biedt geen ondersteuning voor Delete-bewerkingen voor de delta-import
  * Ondersteunt het instellen en wijzigen-wachtwoord
* Open DJ
  * Biedt ondersteuning voor alle bewerkingen voor de delta-import
  * Ondersteunt het instellen en wijzigen-wachtwoord
* Open Active Directory
  * Biedt ondersteuning voor alle bewerkingen voor de delta-import
  * Ondersteunt het instellen en wijzigen-wachtwoord
* Open LDAP (openldap.org)
  * Biedt ondersteuning voor alle bewerkingen voor de delta-import
  * Ondersteunt het instellen van wachtwoord
  * Biedt geen ondersteuning voor wachtwoord wijzigen
* Oracle (eerder Sun) Directory Server Enterprise Edition
  * Biedt ondersteuning voor alle bewerkingen voor de delta-import
  * Ondersteunt het instellen en wijzigen-wachtwoord
* Server van de virtuele map RadiantOne (VDS)
  * Versie 7.1.1 of hoger
  * Biedt ondersteuning voor alle bewerkingen voor de delta-import
  * Ondersteunt het instellen en wijzigen-wachtwoord
* Een Sun directoryserver
  * Biedt ondersteuning voor alle bewerkingen voor de delta-import
  * Ondersteunt het instellen en wijzigen-wachtwoord

### <a name="prerequisites"></a>Vereisten
Zorg voordat u Hallo Connector gebruikt, hebt u Hallo volgende op de server voor de synchronisatie Hallo:

* Microsoft.NET 4.5.2 of hoger

### <a name="detecting-hello-ldap-server"></a>Hallo LDAP-server te detecteren
Hallo Connector is afhankelijk van verschillende technieken toodetect en Identificeer Hallo LDAP-server. Hallo-Connector gebruikt Hallo hoofdmap DSE, leverancier naam/versie, en deze inspecteert Hallo schema toofind unieke objecten en kenmerken die bekend tooexist in bepaalde LDAP-servers. Deze gegevens als gevonden, wordt de gebruikte toopre-Hallo configuratieopties in Hallo Connector vullen.

### <a name="connected-data-source-permissions"></a>Verbonden gegevensbron machtigingen
tooperform importeren en exporteren van bewerkingen op Hallo-objecten in de verbonden directory hello, Hallo connector-account moet voldoende machtigingen hebben. Hallo-connector moet machtigingen toobe kunnen tooexport, lezen en schrijven machtigingen toobe kunnen tooimport. Machtiging configuratie wordt uitgevoerd binnen Hallo ervaringen van Hallo doelmap zelf.

### <a name="ports-and-protocols"></a>Poorten en protocollen
Hallo-connector gebruikt Hallo-poortnummer dat is opgegeven in configuratie hello, die standaard 389 voor LDAP en 636 voor LDAPS is.

Voor LDAPS, moet u SSL 3.0 of TLS gebruiken. SSL 2.0 wordt niet ondersteund en kan niet worden geactiveerd.

### <a name="required-controls-and-features"></a>Vereiste besturingselementen en onderdelen
Hallo moeten volgende LDAP-besturingselementen en-functies beschikbaar zijn op Hallo LDAP-server voor Hallo connector toowork correct:  
`1.3.6.1.4.1.4203.1.5.3`True/False-filters

Hallo True/False-filter is vaak niet gerapporteerd als ondersteund door de LDAP-adreslijsten en mogelijk weergegeven op Hallo **globale pagina** onder **verplichte functies niet gevonden**. Het gebruikte toocreate is **of** filters in de LDAP-query's, bijvoorbeeld bij het importeren van meerdere objecttypen. Als u meer dan een objecttype importeren kunt, ondersteunt deze functie met de LDAP-server.

Als u een map waarin een unieke id is Hallo anker Hallo volgende moet ook beschikbaar zijn (Zie voor meer informatie, Hallo [ankers configureren](#configure-anchors) sectie):  
`1.3.6.1.4.1.4203.1.5.1`Alle operationele kenmerken

Als Hallo directory meer objecten heeft dan wat in één aanroep toohello directory past, wordt het toouse paginering aanbevolen. Voor paginering toowork moet u een Hallo volgende opties:

**Optie 1:**  
`1.2.840.113556.1.4.319`pagedResultsControl

**Optie 2:**  
`2.16.840.1.113730.3.4.9`VLVControl  
`1.2.840.113556.1.4.473`SortControl

Als beide opties zijn ingeschakeld in de configuratie van de connector hello, wordt pagedResultsControl gebruikt.

`1.2.840.113556.1.4.417`ShowDeletedControl

ShowDeletedControl wordt alleen gebruikt met Hallo USNChanged delta-import methode toobe kunnen toosee verwijderd objecten.

Hallo-connector probeert aanwezig toodetect Hallo opties op het Hallo-server. Als Hallo opties kunnen niet worden gedetecteerd, wordt een waarschuwing aanwezig zijn op Hallo globale pagina in de eigenschappen van de connector Hallo is. Niet alle LDAP-servers aanwezig alle besturingselementen en-functies ze ondersteunen en zelfs als deze waarschuwing aanwezig is, Hallo connector werkt mogelijk zonder problemen.

### <a name="delta-import"></a>Delta-import
Delta-import is alleen beschikbaar wanneer u een map ondersteuning is gedetecteerd. Hallo volgende methoden worden momenteel gebruikt:

* LDAP-Accesslog. Zie [http://www.openldap.org/doc/admin24/overlays.html#Access logboekregistratie](http://www.openldap.org/doc/admin24/overlays.html#Access Logging)
* LDAP-Changelog. Zie [http://tools.ietf.org/html/draft-good-ldap-changelog-04](http://tools.ietf.org/html/draft-good-ldap-changelog-04)
* Tijdstempel. Novell/NetIQ eDirectory, Hallo-Connector maakt gebruik van laatste datum/tijd tooget gemaakt en objecten bijgewerkt. Novell/NetIQ eDirectory biedt geen dat een gelijkwaardige betekent tooretrieve verwijderde objecten. Deze optie kan ook worden gebruikt als geen andere delta-import-methode op Hallo LDAP-server actief is. Deze optie is niet de objecten kunnen tooimport verwijderd.
* USNChanged. Zie: [https://msdn.microsoft.com/library/ms677627.aspx](https://msdn.microsoft.com/library/ms677627.aspx)

### <a name="not-supported"></a>Niet ondersteund
Hallo volgende LDAP-kenmerken worden niet ondersteund:

* LDAP-verwijzingen tussen servers (RFC 4511/4.1.10)

## <a name="create-a-new-connector"></a>Een nieuwe Connector maken
tooCreate een algemene LDAP-connector in **synchronisatieservice** Selecteer **beheeragent** en **maken**. Selecteer Hallo **algemene LDAP (Microsoft)** Connector.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericldap/createconnector.png)

### <a name="connectivity"></a>Connectiviteit
U moet op pagina Verbindingsmogelijkheden Hallo Hallo Host, poort en Binding informatie opgeven. Afhankelijk van die Binding geselecteerd, extra is mogelijk informatie worden opgegeven in Hallo uit te voeren.

![Connectiviteit](./media/active-directory-aadconnectsync-connector-genericldap/connectivity.png)

* Hallo verbindingstime-out instelling wordt alleen gebruikt voor Hallo eerste verbinding toohello server bij het detecteren van Hallo schema.
* Als de Binding is anoniem vervolgens geen van beide gebruikersnaam / wachtwoord of certificaat worden gebruikt.
* Andere bindingen informatie invoeren voor beide in gebruikersnaam / wachtwoord of Selecteer een certificaat.
* Als u Kerberos-tooauthenticate gebruikt, ook geeft Hallo Realm of het domein van de gebruiker Hallo.

Hallo **aliassen kenmerk** in het tekstvak wordt gebruikt voor kenmerken die zijn gedefinieerd in het Hallo-schema met RFC4522 syntaxis. Deze kenmerken kunnen niet worden gedetecteerd tijdens de detectie van schema en Hallo Connector tooidentify moet helpen deze kenmerken. Hallo volgende moet worden ingevoerd op Hallo kenmerk aliassen vak toocorrectly identificeren bijvoorbeeld Hallo userCertificate kenmerk als een binair kenmerk:

`userCertificate;binary`

Hallo Hier volgt een voorbeeld van hoe deze configuratie als eruitzien kan:

![Connectiviteit](./media/active-directory-aadconnectsync-connector-genericldap/connectivityattributes.png)

Selecteer Hallo **operationele kenmerken opnemen in het schema** selectievakje tooalso omvatten kenmerken die zijn gemaakt door Hallo-server. Het gaat hierbij om kenmerken, zoals wanneer Hallo-object is gemaakt en tijd van laatste update.

Selecteer **uitbreidbare kenmerken die zijn opgenomen in het schema** extensible objecten (RFC4512/4.3) worden gebruikt als deze optie inschakelt, kunt elke kenmerk toobe op alle objecten gebruikt. Deze optie maakt Hallo schema zeer grote zodat tenzij Hallo verbonden directory maakt gebruik van deze functie Hallo aanbeveling tookeep Hallo-optie uitgeschakeld is.

### <a name="global-parameters"></a>Globale Parameters
Op Hallo globale Parameters pagina configureert u Hallo DN toohello delta wijzigingenlogboek en extra LDAP-functies. Hallo-pagina is al ingevuld met Hallo informatie verstrekt door Hallo LDAP-server.

![Connectiviteit](./media/active-directory-aadconnectsync-connector-genericldap/globalparameters.png)

Hallo bovenste gedeelte bevat informatie die door het Hallo-server zelf, zoals de naam van de server Hallo Hallo. Hallo Connector controleert ook of Hallo verplichte besturingselementen zijn aanwezig in de hoofdmap DSE Hallo. Als deze besturingselementen worden niet vermeld, wordt een waarschuwing wordt weergegeven. Sommige LDAP-adreslijsten takenlijst niet alle functies in de hoofdmap DSE hello en het is mogelijk dat Hallo Connector werkt zonder problemen, zelfs als er een waarschuwing aanwezig is.

Hallo **besturingselementen ondersteund** selectievakjes Hallo-gedrag voor bepaalde bewerkingen beheren:

* Met de structuur verwijderen is geselecteerd, een hiërarchie wordt verwijderd met een LDAP-aanroep. Hallo-connector heeft het verwijderen van een recursieve met structuur verwijderen uitgeschakeld, indien nodig.
* Met wisselbare resultaten hebt geselecteerd, biedt Hallo Connector een wisselbare import waarop Hallo grootte die is opgegeven op Hallo voeren stappen.
* Hallo VLVControl en SortControl is een alternatieve toohello pagedResultsControl tooread gegevens van Hallo LDAP-adreslijst.
* Als alle drie de opties (pagedResultsControl, VLVControl en SortControl) uitgeschakeld zijn importeert hello Connector vervolgens alle objecten in één bewerking die kan mislukken als het een grote map is.
* ShowDeletedControl wordt alleen gebruikt wanneer de methode Hallo Delta-import USNChanged is.

Hallo wijzigingenlogboek DN-naam is Hallo naamgevingscontext gebruikt door Hallo delta wijzigingenlogboek, bijvoorbeeld **cn = changelog**. Deze waarde moet worden opgegeven toobe kunnen toodo delta-import.

Hallo Hier volgt een lijst met standaard wijzigingenlogboek DNs:

| Directory | Delta-wijzigingenlogboek |
| --- | --- |
| Microsoft AD LDS en AD GC |Automatisch gedetecteerd. USNChanged. |
| Apache Directory-Server |Niet beschikbaar. |
| Directory 389 |Logboek wijzigen. Standaard waarde toouse: **cn = changelog** |
| IBM Tivoli DS |Logboek wijzigen. Standaard waarde toouse: **cn = changelog** |
| Isode Directory |Logboek wijzigen. Standaard waarde toouse: **cn = changelog** |
| Novell/NetIQ eDirectory |Niet beschikbaar. Tijdstempel. Hallo-Connector maakt gebruik van laatste bijgewerkte datum/tijd tooget toegevoegd en records bijgewerkt. |
| Open DJ Active Directory |Logboek wijzigen.  Standaard waarde toouse: **cn = changelog** |
| Open LDAP |Toegangslogboek. Standaard waarde toouse: **cn = accesslog** |
| Oracle DSEE |Logboek wijzigen. Standaard waarde toouse: **cn = changelog** |
| RadiantOne VDS |Virtuele map. Afhankelijk van Hallo directory verbonden tooVDS. |
| Een Sun directoryserver |Logboek wijzigen. Standaard waarde toouse: **cn = changelog** |

het kenmerk password Hallo is Hallo-naam van Hallo kenmerk Hallo Connector tooset Hallo wachtwoord in het wijzigen van wachtwoorden en set-bewerkingen voor wachtwoord moet gebruiken.
Deze waarde is standaard ingesteld te**userPassword** maar kan worden gewijzigd wanneer deze nodig is voor een bepaald LDAP-systeem.

In lijst van de extra partities hello is het mogelijk tooadd aanvullende naamruimten niet automatisch gedetecteerd. Bijvoorbeeld: deze instelling kan worden gebruikt als verschillende servers gezamenlijk een logische cluster, moet die allemaal worden geïmporteerd op Hallo hetzelfde moment. Net zoals Active Directory kunnen meerdere domeinen in één forest maar alle domeinen delen één schema, Hallo dezelfde kunnen worden gesimuleerd door aanvullende naamruimten Hallo in dit vak invoeren. Elke naamruimte kunt importeren uit verschillende servers en verder op de pagina configureren partities en hiërarchieën Hallo is geconfigureerd. Gebruik Ctrl + Enter tooget een nieuwe regel.

### <a name="configure-provisioning-hierarchy"></a>Hiërarchie inrichten configureren
Deze pagina is gebruikte toomap Hallo DN-naam, bijvoorbeeld OU toohello object onderdeeltype die moet worden ingericht, bijvoorbeeld organizationalUnit.

![Hiërarchie inrichten](./media/active-directory-aadconnectsync-connector-genericldap/provisioninghierarchy.png)

Inrichting hiërarchie configureert, kunt u configureren Hallo Connector tooautomatically maken een structuur wanneer deze nodig is. Bijvoorbeeld, als er een naamruimte-dc = contoso, dc = com- en een nieuw object cn Kees, ou = = Seattle, c = US, dc = contoso, dc = com is ingericht en vervolgens Hallo Connector een object van het type land voor VS en een organizationalUnit voor Seattle kunt maken als deze nog niet zijn aanwezig in het Hallo-directory.

### <a name="configure-partitions-and-hierarchies"></a>Partities en hiërarchieën configureren
Selecteer alle naamruimten op Hallo partities en hiërarchieën pagina met objecten u van plan bent tooimport en exporteren.

![Partities](./media/active-directory-aadconnectsync-connector-genericldap/partitions.png)

Voor elke naamruimte is het ook mogelijk tooconfigure connectiviteitsinstellingen die Hallo-waarden die zijn opgegeven op het welkomstscherm van de connectiviteit wilt overschrijven. Als deze waarden lege standaardwaarde tootheir gelaten worden, wordt Hallo-informatie van welkomstscherm van de verbinding gebruikt.

Het is ook mogelijk tooselect welke containers en organisatie-eenheden Hallo Connector moet uit importeren en naar exporteren.

Bij het uitvoeren van een zoekopdracht wordt dit gedaan via alle containers in Hallo-partitie. In gevallen waarin grote aantallen containers dit gedrag tooperformance vermindering leidt.

>[!NOTE]
Hallo maart 2017 update toohello algemene LDAP vanaf worden connector zoekopdrachten beperkt bereik tooonly Hallo geselecteerd containers. Dit kan worden gedaan door vinken Hallo 'alleen zoeken in geselecteerde containers, zoals wordt weergegeven in onderstaande afbeelding voor Hallo.

![Zoeken naar alleen geselecteerde containers](./media/active-directory-aadconnectsync-connector-genericldap/partitions-only-selected-containers.png)

### <a name="configure-anchors"></a>Ankers configureren
Deze pagina heeft altijd een vooraf geconfigureerde waarde en kan niet worden gewijzigd. Hallo server leverancier zijn vastgesteld, mogelijk Hallo anker worden ingevuld met een niet-wijzigbaar-kenmerk voor voorbeeld Hallo GUID voor een object. Als dit niet is gedetecteerd of toonot bekend is een niet-wijzigbaar kenmerk vervolgens Hallo connector dn (distinguished name) gebruikt als Hallo anker.

![vertrouwensankers](./media/active-directory-aadconnectsync-connector-genericldap/anchors.png)


Hallo Hieronder volgt een lijst van LDAP-servers en Hallo anker wordt gebruikt:

| Directory | Ankerkenmerk |
| --- | --- |
| Microsoft AD LDS en AD GC |objectGUID |
| 389 directory-Server |DN-naam |
| Apache Directory |DN-naam |
| IBM Tivoli DS |DN-naam |
| Isode Directory |DN-naam |
| Novell/NetIQ eDirectory |GUID |
| Open DJ Active Directory |DN-naam |
| Open LDAP |DN-naam |
| Oracle ODSEE |DN-naam |
| RadiantOne VDS |DN-naam |
| Een Sun directoryserver |DN-naam |

## <a name="other-notes"></a>Aanvullende opmerkingen
Deze sectie bevat informatie van aspecten die specifieke toothis Connector of om andere redenen zijn belangrijk tooknow.

### <a name="delta-import"></a>Delta-import
Hallo delta watermerk in Open LDAP is UTC-datum/tijd. Om deze reden moeten Hallo klokken tussen FIM-synchronisatieservice en Hallo Open LDAP worden gesynchroniseerd. Als dat niet het geval is, kunnen een aantal invoergegevens in Hallo delta wijzigingenlogboek worden weggelaten.

Hallo delta-import voor Novell eDirectory, wordt niet een verwijderd object gedetecteerd. Daarom is het nodig toorun een volledige periodiek toofind verwijderde objecten importeren.

Voor het wijzigen van mappen met een delta-log dat is gebaseerd op de datum/tijd, wordt ten zeerste aanbevolen toorun een volledige import op periodieke tijdstippen. Dit proces kan Hallo sync engine toofind en samenstellingstraject tussen Hallo LDAP-server en wat wordt momenteel Hallo connectorgebied overgebracht.

## <a name="troubleshooting"></a>Problemen oplossen
* Zie voor informatie over hoe logboekregistratie tooenable tootroubleshoot connector Hallo Hallo [hoe tooEnable ETW-tracering voor Connectors](http://go.microsoft.com/fwlink/?LinkId=335731).
