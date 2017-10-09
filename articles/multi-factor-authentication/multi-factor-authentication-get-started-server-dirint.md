---
title: aaaDirectory integratie tussen Azure multi-factor Authentication en Active Directory
description: Dit is hello Azure multi-factor authentication-pagina waarop wordt beschreven hoe toointegrate hello Azure multi-factor Authentication-Server met Active Directory zodat u Hallo mappen kunt synchroniseren.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: def7a534-cfb2-492a-9124-87fb1148ab1f
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fbff518b4641010d5f7745096e0ff658864d0805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="directory-integration-between-azure-mfa-server-and-active-directory"></a>Adreslijstintegratie tussen Azure MFA-server en Active Directory
Hallo Active Directory-integratie sectie van hello Azure MFA-Server toointegrate gebruiken met Active Directory of een andere LDAP-adreslijst. U kunt kenmerken toomatch Hallo directory-schema configureren en automatische Gebruikerssynchronisatie instellen.

## <a name="settings"></a>Instellingen
Standaard hello Azure multi-factor Authentication (MFA)-Server is geconfigureerd tooimport of gebruikers uit Active Directory synchroniseren.  Hallo Active Directory-integratie tabblad kunt u toooverride Hallo standaardgedrag en toobind tooa andere LDAP-adreslijst, een ADAM-adreslijst of een specifieke Active Directory-domeincontroller.  Het biedt tevens voor Hallo gebruik van LDAP-verificatie tooproxy LDAP- of LDAP-BIND als RADIUS-doel, vooraf-verificatie voor IIS-verificatie of primaire verificatie voor de Gebruikersportal.  Hallo volgende tabel beschrijft de afzonderlijke instellingen Hallo.

![Instellingen](./media/multi-factor-authentication-get-started-server-dirint/dirint.png)

| Functie | Beschrijving |
| --- | --- |
| Active Directory gebruiken |Selecteer Hallo Active Directory gebruiken optie toouse Active Directory voor importeren en synchroniseren.  Dit is de standaardinstelling Hallo. <br>Opmerking: Voor Active Directory toowork integratie juist join Hallo computer tooa domein en meld u aan met een domeinaccount. |
| Vertrouwde domeinen opnemen |Controleer **vertrouwde domeinen opnemen** toohave Hallo agent poging tooconnect toodomains die worden vertrouwd door de huidige domein, een ander domein in Hallo forest of domeinen die zijn betrokken bij een forestvertrouwensrelatie Hallo.  Wanneer u geen importeert of synchroniseert gebruikers uit een Hallo domeinen vertrouwde, schakelt u Hallo selectievakje tooimprove prestaties.  Hallo standaard is geselecteerd. |
| Specifieke LDAP-configuratie gebruiken |Selecteer Hallo LDAP gebruiken optie toouse Hallo LDAP-instellingen zijn opgegeven voor het importeren en synchroniseren. Opmerking: Wanneer LDAP gebruiken is geselecteerd, Hallo gebruikersinterface verwijzingen van verandert tooLDAP Active Directory. |
| Knop Bewerken |de knop bewerken Hallo kunt Hallo huidige LDAP-configuratie-instellingen toomodified. |
| Query's voor kenmerkbereik gebruiken |Geeft aan of query's voor het kenmerkbereik moeten worden gebruikt.  Met kenmerkbereikquery's kunnen adreslijsten efficiënt worden doorzocht in aanmerking komende records op basis van Hallo vermeldingen in het kenmerk van een andere record.  Hello Azure multi-factor Authentication-Server gebruikt query's tooefficiently Hallo gebruikers kenmerkbereikquery die lid zijn van een beveiligingsgroep.   <br>Opmerking: er zijn enkele gevallen waarbij query's voor het kenmerkbereik worden ondersteund, maar niet mogen worden gebruikt.  Active Directory kan bijvoorbeeld problemen met query's voor het kenmerkbereik hebben wanneer een beveiligingsgroep leden uit meer dan één domein bevat. In dit geval Schakel Hallo selectievakje uit. |

Hallo volgende tabel beschrijft Hallo LDAP-configuratie-instellingen.

| Functie | Beschrijving |
| --- | --- |
| Server |Geef Hallo hostnaam of IP-adres van Hallo Hallo LDAP-adreslijst wordt uitgevoerd.  U kunt ook een back-upserver opgeven, gescheiden door een puntkomma. <br>Opmerking: wanneer het bindingstype SSL is, is een volledig gekwalificeerde hostnaam vereist. |
| Basis-DN |Voer Hallo DN-naam van Hallo basisdirectory-object waaruit alle directoryquery's worden gestart.  Bijvoorbeeld: dc=abc, dc=com. |
| Bindingstype query |Selecteer Hallo geschikte bindingstype voor gebruik bij het binden van toosearch Hallo LDAP-adreslijst.  Dit wordt gebruikt voor import, synchronisatie en gebruikersnaamomzetting. <br><br>  Anoniem: Er wordt een anonieme binding uitgevoerd.  Bindings-DN en bindingswachtwoord worden niet gebruikt.  Dit werkt alleen als Hallo LDAP-directory anonieme binding toestaat en machtigingen toestaan Hallo query's naar Hallo relevante records en kenmerken.  <br><br> Eenvoudig: bindings-DN en Bindingswachtwoord worden doorgegeven als tekst zonder opmaak toobind toohello LDAP-adreslijst.  Dit is voor testdoeleinden, tooverify die Hallo van server bereikbaar is en dat Hallo bind Hallo juiste toegang heeft. Nadat het relevante certificaat Hallo is geïnstalleerd, in plaats daarvan SSL gebruiken.  <br><br> SSL: bindings-DN en Bindingswachtwoord worden versleuteld met SSL toobind toohello LDAP-adreslijst.  Installeer lokaal een certificaat dat is die Hallo vertrouwensrelaties van LDAP-directory.  <br><br> Windows - Bindingsgebruikersnaam en Bindingswachtwoord worden gebruikte toosecurely verbinding tooan Active Directory-domeincontroller of ADAM-adreslijst.  Als Bindingsgebruikersnaam leeg blijft, is het Hallo aangemelde gebruikersaccount gebruikt toobind. |
| Bindingstype - Verificaties |Selecteer Hallo geschikte bindingstype voor gebruik bij het uitvoeren van LDAP-bindingsverificaties.  Zie Hallo bind type bindingstypen onder bindingstype - query's.  Dit kan bijvoorbeeld voor anonieme binding toobe gebruikt voor query's, terwijl het bindingtype SSL wordt gebruikt toosecure LDAP-bindingsverificaties. |
| Bindings-DN of Bind gebruikersnaam |Voer Hallo DN-naam van de gebruikersrecord Hallo voor Hallo account toouse bij het binden van toohello LDAP-adreslijst.<br><br>Hallo DN-bindingsnaam wordt alleen gebruikt wanneer het bindingstype eenvoudig of SSL is.  <br><br>Geef Hallo gebruikersnaam van Hallo Windows-account toouse bij het binden van de LDAP-adreslijst toohello wanneer het bindingstype Windows is.  Als bindingsgebruikersnaam leeg blijft, is Hallo aangemelde gebruikersaccount gebruikt toobind. |
| Bindingswachtwoord |Voer Hallo binding van het wachtwoord voor Hallo bindings-DN of gebruikersnaam gebruikte toobind toohello LDAP-adreslijst wordt.  tooconfigure hello wachtwoord voor Hallo multi-Factor Authentication Server-AdSync Service, synchronisatie inschakelen en controleer of het Hallo-service wordt uitgevoerd op de lokale machine Hallo.  Hallo-wachtwoord wordt opgeslagen in Hallo Windows opgeslagen gebruikersnamen en wachtwoorden onder Hallo account Hallo die multi-Factor Authentication Server AdSync-Service wordt uitgevoerd als.  Hallo-wachtwoord wordt ook opgeslagen onder Hallo account Hallo multi-factor Authentication-Server gebruikersinterface wordt uitgevoerd en onder Hallo account Hallo multi-Factor Authentication Server-Service wordt uitgevoerd.  <br><br>Aangezien Hallo wachtwoord alleen wordt opgeslagen in de Windows opgeslagen gebruikersnamen en wachtwoorden Hallo lokale server, moet u deze stap op elke multi-factor Authentication-Server die toegang toohello wachtwoord moet herhalen. |
| Maximale grootte query |Hallo maximale grootte opgeven voor Hallo kunt u het maximum aantal gebruikers dat een directoryzoekopdracht retourneert.  Deze limiet moet overeenkomen met de Hallo-configuratie op Hallo LDAP-adreslijst.  Bij grote zoekopdrachten waar paginering niet wordt ondersteund, probeert importeren en synchroniseren van gebruikers in batches tooretrieve.  Als de maximale grootte Hallo hier is groter dan Hallo limiet die is geconfigureerd voor de LDAP-adreslijst hello opgegeven, kunnen sommige gebruikers wellicht niet opgehaald. |
| Knop Testen |Klik op **Test** tootest binding toohello LDAP-server.  <br><br>U hoeft niet tooselect hello **LDAP gebruiken** optie tootest binding. Hierdoor Hallo binding toobe getest voordat u Hallo LDAP-configuratie gebruiken. |

## <a name="filters"></a>Filters
Filters kunt u tooset criteria tooqualify registreert bij het uitvoeren van een directoryzoekopdracht.  Door het Hallo-filter instellen kunt u het bereik Hallo objecten u wilt dat toosynchronize.  

![Filters](./media/multi-factor-authentication-get-started-server-dirint/dirint2.png)

Azure multi-factor Authentication heeft Hallo drie filteropties te volgen:

* **Containerfilter** -opgeven Hallo filtercriteria tooqualify containerrecords gebruikt bij het uitvoeren van een directoryzoekopdracht.  Voor Active Directory en ADAM wordt meestal (|(objectClass=organizationalUnit)(objectClass=container)) gebruikt.  Gebruik voor andere LDAP-adreslijsten filtercriteria die elk type containerobject naar gelang het adreslijstschema Hallo kwalificeren.  <br>Opmerking: als dit veld leeg blijft, wordt standaard ((objectClass=organizationalUnit)(objectClass=container)) gebruikt.
* **Beveiligingsgroepfilter** -opgeven Hallo filtercriteria tooqualify beveiligingsgroeprecords gebruikt bij het uitvoeren van een directoryzoekopdracht.  Voor Active Directory en ADAM wordt meestal (&(objectCategory=group)(groupType:1.2.840.113556.1.4.804:=-2147483648)) gebruikt.  Gebruik voor andere LDAP-adreslijsten filtercriteria die elk type beveiligingsgroepobject naar gelang het adreslijstschema Hallo kwalificeren.  <br>Opmerking: als dit veld leeg blijft, wordt standaard (&(objectCategory=group)(groupType:1.2.840.113556.1.4.804:=-2147483648)) gebruikt.
* **Gebruikersfilter** -opgeven Hallo filtercriteria tooqualify gebruikersrecords gebruikt bij het uitvoeren van een directoryzoekopdracht.  Voor Active Directory en ADAM wordt meestal (&(objectClass=user)(objectCategory=person)) gebruikt.  Gebruik voor andere LDAP-adreslijsten moet (objectClass = inetOrgPerson) of iets dergelijks zijn, afhankelijk van het Hallo-directory-schema. <br>Opmerking: als dit veld leeg blijft, wordt standaard (&(objectCategory=person)(objectClass=user)) gebruikt.

## <a name="attributes"></a>Kenmerken
U kunt kenmerken, indien nodig, aanpassen voor een specifieke directory.  Dit kunt u aangepaste kenmerken tooadd en verfijnen Hallo synchronisatie tooonly Hallo kenmerken die u nodig hebt. Hallo-naam van Hallo attricute gebruiken zoals gedefinieerd in Hallo directory-schema voor Hallo-waarde van elk kenmerkveld bevindt. Hallo bevat volgende tabel aanvullende informatie over elke functie.

Kenmerken kunnen handmatig worden ingevoerd en zijn niet vereist toomatch een kenmerk in de kenmerkenlijst Hallo.

![Kenmerken](./media/multi-factor-authentication-get-started-server-dirint/dirint3.png)

| Functie | Beschrijving |
| --- | --- |
| Unieke id |Voer de naam op Hallo van Hallo-kenmerk die als unieke id van de container, beveiligingsgroep en gebruikersrecords Hallo fungeert.  In Active Directory is dit doorgaans objectGUID. Andere LDAP-implementaties maken mogelijk gebruik van entryUUID of iets soortgelijks.  Hallo standaardwaarde is objectGUID. |
| Type unieke id |Selecteer Hallo Hallo kenmerk unieke id.  In Active Directory is Hallo objectGUID kenmerk van het type GUID. Andere LDAP-implementaties maken mogelijk gebruik van het type ASCII-bytematrix of Tekenreeks.  Hallo standaardwaarde is GUID. <br><br>Het is belangrijk tooset dit type correct sinds het synchronisatie-Items wordt verwezen door hun unieke id. Hallo Type unieke id is gebruikte toodirectly find Hallo-object in de map Hallo.  Instelling van dit type tooString wanneer Hallo directory daadwerkelijk Hallo-waarde als een bytematrix van ASCII-tekens slaat voorkomt u dat de synchronisatie niet goed werken. |
| DN-naam |Voer de naam op Hallo van Hallo-kenmerk die Hallo DN-naam voor elke record bevat.  In Active Directory is dit doorgaans distinguishedName. Andere LDAP-implementaties maken mogelijk gebruik van entryDN of iets soortgelijks.  Hallo standaardwaarde is distinguishedName. <br><br>Als geen kenmerk met alleen Hallo DN-naam niet bestaat, kan de kenmerk adspath hello worden gebruikt.  Hallo "LDAP: / /\<server\>/ ' gedeelte van Hallo pad wordt automatisch weggelaten, alleen Hallo DN-naam van Hallo object verlaten. |
| Containernaam |Voer de naam op Hallo van Hallo-kenmerk dat de naam Hallo in een containerrecord bevat.  Hallo-waarde van dit kenmerk wordt weergegeven in Hallo Containerhiërarchie wanneer uit Active Directory wordt geïmporteerd of synchronisatie-items worden toegevoegd.  Hallo standaardwaarde is name. <br><br>Als verschillende containers verschillende kenmerken voor hun namen gebruiken, gebruik puntkomma's tooseparate meerdere containernaamkenmerken.  eerste containernaamkenmerk Hallo gevonden in een containerobject gebruikte toodisplay is de naam ervan. |
| Naam beveiligingsgroep |Voer de naam op Hallo van Hallo-kenmerk dat Hallo-naam in een beveiligingsgroepsrecord bevat.  Hallo-waarde van dit kenmerk wordt weergegeven in de lijst beveiligingsgroep Hallo wanneer uit Active Directory wordt geïmporteerd of synchronisatie-items worden toegevoegd.  Hallo standaardwaarde is name. |
| Gebruikersnaam |Voer de naam op Hallo van Hallo-kenmerk dat Hallo gebruikersnaam in een gebruikersrecord bevat.  Hallo-waarde van dit kenmerk wordt gebruikt als gebruikersnaam Hallo die multi-Factor Authentication-Server.  Een tweede kenmerk kan worden opgegeven als een back-toohello eerst.  Hallo tweede kenmerk wordt alleen gebruikt als Hallo eerste kenmerk geen waarde voor Hallo gebruiker bevat.  Hallo standaardwaarden zijn userPrincipalName en sAMAccountName. |
| Voornaam |Voer de naam op Hallo van Hallo-kenmerk dat de voornaam Hallo in een gebruikersrecord bevat.  Hallo standaardwaarde is givenName. |
| Achternaam |Voer de naam op Hallo van Hallo-kenmerk dat de achternaam Hallo in een gebruikersrecord bevat.  Hallo standaardwaarde is sn. |
| E-mailadres |Voer de naam op Hallo van Hallo-kenmerk die Hallo e-mailadres in een gebruikersrecord bevat.  E-mailadres is gebruikte toosend Welkom en update e-mailberichten toohello gebruiker.  Hallo standaardwaarde is mail. |
| Gebruikersgroep |Voer de naam op Hallo van Hallo-kenmerk dat de gebruikersgroep Hallo in een gebruikersrecord bevat.  Gebruikersgroep kan worden gebruikt toofilter gebruikers in Hallo-agent en in rapporten op Hallo multi-Factor Authentication Server-beheerportal. |
| Beschrijving |Voer de naam op Hallo van Hallo-kenmerk dat Hallo beschrijving in een gebruikersrecord bevat.  Beschrijving wordt alleen gebruikt voor zoekopdrachten.  Hallo standaardwaarde is description. |
| Taal telefoonoproep |Voer naam Hallo van Hallo-kenmerk die Hallo korte naam van toouse van Hallo taal voor telefoonoproepen voor Hallo-gebruiker bevat. |
| Taal sms-bericht |Voer naam Hallo van Hallo-kenmerk dat Hallo korte naam van Hallo taal toouse voor SMS-berichten voor Hallo-gebruiker bevat. |
| Taal mobiele app |Voer naam Hallo van Hallo-kenmerk dat Hallo korte naam van Hallo taal toouse voor tekstberichten van telefoon-app voor Hallo-gebruiker bevat. |
| Taal OATH-token |Voer naam Hallo van Hallo-kenmerk dat Hallo korte naam van Hallo taal toouse voor tekstberichten voor Hallo-gebruiker bevat. |
| Telefoon (werk) |Voer de naam op Hallo van Hallo-kenmerk die Hallo zakelijke telefoonnummer in een gebruikersrecord bevat.  Hallo standaardwaarde is telephoneNumber. |
| Telefoon (thuis) |Voer de kenmerknaam Hallo van Hallo-kenmerk dat Hallo privételefoonnummer in een gebruikersrecord bevat.  Hallo standaardwaarde is homePhone. |
| Pager |Voer de naam op Hallo van Hallo-kenmerk dat het pagernummer Hallo in een gebruikersrecord bevat.  Hallo standaardwaarde is pager. |
| Mobiele telefoon |Voer de kenmerknaam Hallo van Hallo-kenmerk dat Hallo mobiele telefoonnummer in een gebruikersrecord bevat.  Hallo standaardwaarde is mobile. |
| Fax |Voer de naam op Hallo van Hallo-kenmerk dat het faxnummer Hallo in een gebruikersrecord bevat.  Hallo standaardwaarde is facsimileTelephoneNumber. |
| IP-telefoon |Voer de naam op Hallo van Hallo-kenmerk dat Hallo IP-telefoonnummer in een gebruikersrecord bevat.  Hallo standaardwaarde is ipPhone. |
| Aangepast telefoonnummer |Voer de kenmerknaam Hallo van Hallo-kenmerk dat een aangepast telefoonnummer in een gebruikersrecord bevat.  Hallo standaardwaarde is leeg. |
| Toestelnummer |Voer de kenmerknaam Hallo van Hallo-kenmerk dat Hallo-toestelnummer in een gebruikersrecord bevat.  Hallo-waarde van Hallo toestelnummerveld wordt gebruikt als Hallo extensie toohello primaire telefoonnummer.  Hallo standaardwaarde is leeg. <br><br>Als het Hallo-extensie-kenmerk niet is opgegeven, kunnen toestelnummers worden opgenomen als onderdeel van het telefoonkenmerk Hallo. In dit geval worden voorafgegaan door Hallo-extensie met een 'x' zodat dit correct wordt geparseerd.  Bijvoorbeeld: 555-123-4567 x890 zou leiden tot 555-123-4567 als Hallo telefoonnummer en 890 als Hallo-uitbreiding. |
| Knop Standaardwaarden herstellen |Klik op **standaardwaarden herstellen** tooreturn alle kenmerken back tootheir standaardwaarde.  Hallo gesproken werken standaardwaarden correct met Hallo normale Active Directory- of ADAM-schema. |

tooedit kenmerken, klikt u op **bewerken** op het tabblad Hallo-kenmerken.  Hiermee wordt een venster waarin u Hallo kenmerken kunt bewerken. Selecteer Hallo **...**  volgende tooany kenmerk tooopen een venster waarin u welke toodisplay kenmerken kiezen kunt.

![Kenmerken bewerken](./media/multi-factor-authentication-get-started-server-dirint/dirint4.png)

## <a name="synchronization"></a>Synchronisatie
Synchronisatie houdt hello Azure MFA-gebruikersdatabase gesynchroniseerd met Hallo gebruikers in Active Directory of een andere Lightweight Directory Access Protocol (LDAP)-directory. Hallo-proces is vergelijkbaar tooimporting gebruikers handmatig uit Active Directory, maar pollt periodiek naar Active Directory-gebruiker en tooprocess beveiligingsgroep wordt gewijzigd.  Ook worden gebruikers ingeschakeld of verwijderd die zijn verwijderd uit een container, beveiligingsgroep of Active Directory.

Hallo multi-factor Authentication-service ADSync is een Windows-service die Hallo periodieke polling van Active Directory uitvoert.  Dit is geen toobe verward met Azure AD Sync of Azure AD Connect.  Hallo multi-factor Authentication-Service ADSync is Hoewel gebouwd op een vergelijkbare codebasis, het specifieke toohello Azure multi-factor Authentication-Server.  Wordt geïnstalleerd in een status gestopt en wordt gestart door de service van de multi-factor Authentication-Server wanneer geconfigureerd Hallo toorun.  Als u een multi-factor Authentication-Server-configuratie hebt, kan Hallo multi-factor Authentication-Service ADSync alleen worden uitgevoerd op één server.

Hallo multi-factor Authentication-service ADSync maakt gebruik van Hallo DirSync LDAP-serverextensie die is geleverd door Microsoft tooefficiently poll op wijzigingen.  Deze DirSync-controlcaller moet Hallo "directory get changes" rechts en DS-Replication-Get-Changes uitgebreide beheertoegangsrecht hebben.  Deze rechten worden standaard toohello accounts Administrator en LocalSystem op domeincontrollers worden toegewezen.  Hallo multi-factor Authentication-service AdSync is geconfigureerde toorun als LocalSystem standaard.  Daarom is het eenvoudigste toorun Hallo-service op een domeincontroller.  Als u configureert Hallo service tooalways een volledige synchronisatie uitvoeren, kan het uitgevoerd als een account met minder machtigingen.  Dit is minder efficiënt, maar vereist minder accountmachtigingen.

Als Hallo LDAP-adreslijst wordt ondersteund en is geconfigureerd voor DirSync, vervolgens polling voor gebruiker-en beveiligingsgroepwijzigingen werkt Hallo hetzelfde als bij Active Directory.  Als de LDAP-adreslijst Hallo Hallo DirSync control niet ondersteunt, wordt een volledige synchronisatie tijdens elke cyclus uitgevoerd.

![Synchronisatie](./media/multi-factor-authentication-get-started-server-dirint/dirint5.png)

Hallo bevat volgende tabel aanvullende informatie over elk van de instellingen op het tabblad Synchronisatie Hallo.

| Functie | Beschrijving |
| --- | --- |
| Synchronisatie met Active Directory inschakelen |Wanneer dit selectievakje inschakelt, periodiek Hallo multi-Factor Authentication Server-service Active Directory van wijzigingen. <br><br>Opmerking: ten minste één synchronisatie-Item moet worden toegevoegd en nu synchroniseren moet worden uitgevoerd voordat Hallo multi-Factor Authentication Server-service wordt gestart met het verwerken van wijzigingen. |
| Synchronisatie-interval |Geef Hallo tijd interval Hallo multi-Factor Authentication Server-service wachten moet tussen navragen en verwerken van wijzigingen. <br><br> Opmerking: de opgegeven Hallo-interval is Hallo tijd tussen het begin van elke cyclus Hallo.  Als wijzigingen Hallo tijd verwerking hello-interval overschrijdt, navraag Hallo service onmiddellijk gedaan. |
| Gebruikers verwijderen die niet meer in Active Directory zijn |Wanneer dit selectievakje inschakelt, Hallo service multi-factor Authentication-Server verwijderde Active Directory-tombstones van gebruikers worden verwerkt en verwijderen Hallo gerelateerde multi-factor Authentication-Server gebruiker. |
| Altijd een volledige synchronisatie uitvoeren |Wanneer dit selectievakje inschakelt, Hallo service multi-factor Authentication-Server altijd een volledige synchronisatie wordt uitgevoerd.  Wanneer dit selectievakje uitschakelt, zal Hallo multi-Factor Authentication Server-service een incrementele synchronisatie uitvoeren door het opvragen van alleen gebruikers die zijn gewijzigd.  Hallo standaard is uitgeschakeld. <br><br>Wanneer dit selectievakje uitschakelt, voert Azure MFA-Server incrementele synchronisatie alleen wanneer Hallo directory Hallo DirSync control ondersteunt en Hallo account binding toohello directory machtigingen tooperform DirSync incrementele query's heeft.  Als Hallo account heeft geen juiste machtigingen Hallo of meerdere domeinen bij Hallo synchronisatie betrokken zijn, wordt een volledige synchronisatie uitgevoerd in Azure MFA-Server. |
| Goedkeuring door beheerder vereisen wanneer het aantal uitgeschakelde of verwijderde gebruikers de drempelwaarde overschrijdt |Synchronisatie-items worden geconfigureerde toodisable of gebruikers die niet langer lid zijn van de container of gebruikersgroep Hallo-item verwijderen.  Als beveiliging kan goedkeuring van de beheerder vereist zijn wanneer Hallo aantal gebruikers toodisable of verwijder een drempelwaarde overschrijdt.  Als deze optie wordt ingeschakeld, is goedkeuring vereist voor de opgegeven drempelwaarde.  Hallo standaardwaarde is 5 en Hallo bereik is 1 too999. <br><br> Goedkeuring wordt vergemakkelijkt door eerst te verzenden een e-mailmelding tooadministrators. Hallo e-mailmelding bevat instructies voor het controleren en goedkeuren van Hallo uitschakeling en verwijdering van gebruikers.  Wanneer de gebruikersinterface van Hallo multi-factor Authentication-Server wordt gestart, wordt om goedkeuring gevraagd. |

Hallo **nu synchroniseren** knop kunt u een volledige synchronisatie voor Hallo synchronisatie toorun items dat is opgegeven.  Een volledige synchronisatie is vereist wanneer synchronisatie-items worden toegevoegd, gewijzigd, verwijderd of opnieuw gerangschikt.  Het is ook vereist voordat Hallo multi-factor Authentication-service AdSync operationeel is aangezien hiermee Hallo beginpunt waaruit incrementele wijzigingen Hallo service navraagt.  Als wijzigingen zijn aangebracht toosynchronization items, maar nog niet een volledige synchronisatie is uitgevoerd, kunt u zich na vragen aan gebruiker tooSynchronize nu.

Hallo **verwijderen** knop Hallo beheerder toodelete kan een of meer synchronisatie-items uit de itemlijst Hallo multi-factor Authentication-Server.

> [!WARNING]
> Nadat een synchronisatie-itemrecord is verwijderd, kan het niet worden hersteld. U moet tooadd Hallo synchronisatie item records opnieuw als u deze per ongeluk hebt verwijderd.

Hallo synchronisatie-item of de synchronisatie-items zijn verwijderd uit multi-factor Authentication-Server.  Hallo synchronisatie-items worden niet meer door Hallo service multi-factor Authentication-Server worden verwerkt.

Hallo-knoppen voor omhoog en omlaag kunnen Hallo beheerder toochange Hallo volgorde van Hallo synchronisatie-items.  Hallo is volgorde belangrijk omdat hello dezelfde gebruiker lid is van meer dan één synchronisatie-item (bijvoorbeeld een container en een beveiligingsgroep).  Hallo instellingen toegepaste toohello gebruiker tijdens de synchronisatie, zijn afkomstig van de eerste synchronisatie-item Hallo Hallo lijst toowhich Hallo gebruiker is gekoppeld.  Daarom moeten Hallo synchronisatie-items in volgorde van prioriteit worden geplaatst.

> [!TIP]
> Na het verwijderen van synchronisatie-items moet een volledige synchronisatie worden uitgevoerd.  Na het rangschikken van synchronisatie-items moet een volledige synchronisatie worden uitgevoerd.  Klik op **nu synchroniseren** tooperform een volledige synchronisatie.

## <a name="multi-factor-auth-servers"></a>Multi-Factor Auth-servers
Extra multi-factor Auth-Servers kan worden ingesteld tooserve als een back-up-RADIUS-proxy, LDAP-proxy of voor IIS-verificatie. Hallo-synchronisatie wordt gedeeld door alle Hallo-agents. Slechts één van deze agenten hebben echter Hallo multi-Factor Authentication Server-service die wordt uitgevoerd. Op dit tabblad kunt u tooselect hello multi-factor Authentication-Server die moet worden ingeschakeld voor synchronisatie.

![Multi-Factor Auth-servers](./media/multi-factor-authentication-get-started-server-dirint/dirint6.png)
