---
title: aaaGeneric SQL-Connector | Microsoft Docs
description: Dit artikel wordt beschreven hoe algemene SQL-Connector van Microsoft tooconfigure.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: fd8ccef3-6605-47ba-9219-e0c74ffc0ec9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2eab8f0894e83ab4738b9f2deb05b03cdc9a9d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-technical-reference"></a>Algemene technische documentatie van SQL-Connector
Dit artikel wordt beschreven Hallo algemene SQL-Connector. Hallo-artikel geldt toohello producten te volgen:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Hotfix 4.1.3671.0 moet gebruiken of later [KB3092178](https://support.microsoft.com/kb/3092178).

Voor MIM2016 en FIM2010R2 Hallo Connector is beschikbaar als een download van Hallo [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

toosee deze Connector in actie, Zie Hallo [algemene SQL-Connector stapsgewijze](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) artikel.

## <a name="overview-of-hello-generic-sql-connector"></a>Overzicht van Hallo algemene SQL-Connector
Hallo algemene SQL-Connector kunt u het Hallo-synchronisatieservice toointegrate met een databasesysteem die ODBC-connectiviteit biedt.  

Hallo volgende kenmerken worden vanuit een perspectief op hoog niveau wordt ondersteund door Hallo huidige release van Hallo-connector:

| Functie | Ondersteuning |
| --- | --- |
| Gekoppelde gegevensbron |Hallo Connector wordt ondersteund met alle 64-bits ODBC-stuurprogramma's. Het is getest met de volgende Hallo: <li>Microsoft SQL Server en SQL Azure</li><li>IBM DB2 10.x</li><li>IBM DB2 9.x</li><li>Oracle 10 & 11 g</li><li>MySQL 5.x</li> |
| Scenario's |<li>Object levenscyclusbeheer</li><li>Wachtwoordbeheer</li> |
| Bewerkingen |<li>Volledige Import- en Delta-Import, Export</li><li>Voor het exporteren: Toevoegen, verwijderen, bijwerken en vervangen</li><li>Wachtwoord instellen, wachtwoord wijzigen</li> |
| Schema |<li>Dynamische detectie van objecten en kenmerken</li> |

### <a name="prerequisites"></a>Vereisten
Zorg voordat u Hallo Connector gebruikt, hebt u Hallo volgende op de server voor de synchronisatie Hallo:

* Microsoft.NET 4.5.2 of hoger
* 64-bits ODBC-stuurprogramma's client

### <a name="permissions-in-connected-data-source"></a>Machtigingen in de gekoppelde gegevensbron
toocreate of Hallo ondersteund taken uitvoeren in algemene SQL-connector, moet u hebben:

* db_datareader
* db_datawriter

### <a name="ports-and-protocols"></a>Poorten en protocollen
Raadpleeg voor Hallo vereiste poorten voor Hallo ODBC-stuurprogramma toowork, Hallo database documentatie van de leverancier.

## <a name="create-a-new-connector"></a>Een nieuwe Connector maken
tooCreate een algemene SQL-connector in **synchronisatieservice** Selecteer **beheeragent** en **maken**. Selecteer Hallo **algemene SQL (Microsoft)** Connector.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/createconnector.png)

### <a name="connectivity"></a>Connectiviteit
Hallo Connector gebruikt een ODBC DSN-bestand voor connectiviteit. Maak Hallo DSN-bestand met **ODBC-gegevensbronnen** gevonden in het startmenu Hallo onder **Systeembeheer**. In het beheerprogramma hello, maakt een **DSN-bestand** zodat deze kan worden opgegeven toohello Connector.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/connectivity.png)

welkomstscherm connectiviteit is eerst Hallo wanneer u een nieuwe algemene SQL-Connector maakt. U moet eerst tooprovide Hallo volgende informatie:

* Bestandspad DSN-naam
* Authentication
  * Gebruikersnaam
  * Wachtwoord

Hallo-database moet een van deze verificatiemethoden kunnen ondersteunen:

* **Windows-verificatie**: Hallo verifiëren van de database maakt gebruik van Hallo Windows-referenties tooverify Hallo-gebruiker. Hallo gebruikersnaam en wachtwoord opgegeven is gebruikte tooauthenticate met Hallo-database. Dit account moet machtigingen toohello database.
* **SQL-verificatie**: Hallo verifiëren van de database maakt gebruik van Hallo gebruikersnaam/wachtwoord één Hallo connectiviteit scherm tooconnect toohello database gedefinieerd. Als u Hallo gebruiker naam/wachtwoord opslaan in de Hallo DSN-bestand, hebben voorrang op Hallo-referenties die zijn opgegeven op het welkomstscherm van de verbinding.
* **Azure SQL Database-verificatie**: Zie voor meer informatie [tooSQL Database met behulp van Azure Active Directory-verificatie verbinding](../../sql-database/sql-database-aad-authentication.md).

**DN-naam is anker**: als u deze optie selecteert, Hallo DN-naam wordt ook gebruikt als Hallo ankerkenmerk. Kan worden gebruikt voor een eenvoudige implementatie, maar heeft ook Hallo beperking te volgen:

* Connector ondersteunt slechts één objecttype. Daarom Hallo verwijzingen kenmerken kunnen alleen verwijzen naar hetzelfde objecttype.

**Exporttype: Object-vervangen**: tijdens het exporteren wanneer u alleen bepaalde kenmerken zijn gewijzigd, Hallo gehele object met alle kenmerken worden geëxporteerd en vervangt Hallo bestaand object.

### <a name="schema-1-detect-object-types"></a>Schema 1 (objecttypen detecteren)
Op deze pagina kunt u tooconfigure gaat hoe Hallo Connector gaat toofind Hallo verschillende objecttypen in Hallo-database is.

Elk objecttype wordt weergegeven als een partitie en geconfigureerd op verdere **configureren partities en hiërarchieën**.

![schema1a](./media/active-directory-aadconnectsync-connector-genericsql/schema1a.png)

**Object-Type detectiemethode**: Hallo Connector ondersteunt deze detectiemethoden voor object-type.

* **Vaste waarde**: U Hallo lijst verstrekken van objecttypen die met een door komma's gescheiden lijst. Bijvoorbeeld: `User,Group,Department`.  
  ![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)
* **Weergave-tabel/opgeslagen Procedure**: Hallo-naam van Hallo tabel, weergave/opgeslagen procedure en vervolgens Hallo kolomnaam waarmee Hallo lijst met objecttypen. Als u een opgeslagen procedure gebruikt, ook geeft parameters voor het Hallo-indeling **[Name]: [richting]: [waarde]**. Geef elke parameter in op een afzonderlijke regel (Gebruik Ctrl + Enter tooget een nieuwe regel).  
  ![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)
* **SQL-Query**: deze optie kunt u een SQL-query één kolom met objecttypen, bijvoorbeeld retourneert tooprovide `SELECT [Column Name] FROM TABLENAME`. Hallo geretourneerd in de kolom moet van het type tekenreeks (varchar).

### <a name="schema-2-detect-attribute-types"></a>Schema 2 (kenmerktypen detecteren)
Op deze pagina kunt gaat u tooconfigure Hallo hoe kenmerknamen en typen gaat toobe gedetecteerd. Hallo-configuratie-opties worden weergegeven voor elke objecttype gedetecteerd op de vorige pagina Hallo.

![schema2a](./media/active-directory-aadconnectsync-connector-genericsql/schema2a.png)

**Het kenmerk Type detectiemethode**: Hallo Connector ondersteunt deze kenmerk type detectiemethoden met elke gedetecteerde objecttype in Schema-1-scherm.

* **Weergave-tabel/opgeslagen Procedure**: Hallo-naam van Hallo tabel, weergave/opgeslagen procedure die gebruikt toofind Hallo kenmerknamen worden moet bieden. Als u een opgeslagen procedure gebruikt, ook geeft parameters voor het Hallo-indeling **[Name]: [richting]: [waarde]**. Geef elke parameter in op een afzonderlijke regel (Gebruik Ctrl + Enter tooget een nieuwe regel). toodetect hello kenmerknamen in een kenmerk met meerdere waarden opgeven voor een door komma's gescheiden lijst met tabellen of weergaven. Met meerdere waarden worden niet ondersteund wanneer de bovenliggende en onderliggende tabel dezelfde kolomnamen hebt.
* **SQL-query**: deze optie kunt u een SQL-query één kolom met de namen van kenmerken, bijvoorbeeld retourneert tooprovide `SELECT [Column Name] FROM TABLENAME`. Hallo geretourneerd in de kolom moet van het type tekenreeks (varchar).

### <a name="schema-3-define-anchor-and-dn"></a>Schema 3 (definiëren anker en DN-naam)
Deze pagina kunt u tooconfigure anker en DN-kenmerk voor elke gedetecteerde objecttype. U kunt meerdere kenmerken toomake Hallo anker unieke selecteren.

![schema3a](./media/active-directory-aadconnectsync-connector-genericsql/schema3a.png)

* Kenmerken met meerdere waarden en Booleaanse worden niet weergegeven.
* Hetzelfde kenmerk voor DN-naam en anker, niet gebruiken tenzij **DN-naam is anker** is geselecteerd op de pagina Verbindingsmogelijkheden Hallo.
* Als **DN-naam is anker** is geselecteerd op pagina Verbindingsmogelijkheden Hallo deze pagina alleen Hallo DN-kenmerk vereist. Dit kenmerk moet ook worden gebruikt als Hallo ankerkenmerk.

  ![schema3b](./media/active-directory-aadconnectsync-connector-genericsql/schema3b.png)

### <a name="schema-4-define-attribute-type-reference-and-direction"></a>Schema 4 (definiëren kenmerktype verwijzing en richting)
Deze pagina kunt u tooconfigure Hallo kenmerktype, zoals geheel getal, binair of Booleaanse waarde en richting voor elk kenmerk. Alle kenmerken van pagina **schema 2** met inbegrip van kenmerken met meerdere waarden worden weergegeven.

![schema4a](./media/active-directory-aadconnectsync-connector-genericsql/schema4a.png)

* **Gegevenstype**: toomap Hallo type toothose kenmerktypen bekend is bij Hallo synchronisatie-engine gebruikt. Hallo standaard is toouse Hallo hetzelfde type aangetroffen in de SQL-schema hello, maar de datum/tijd- en verwijzingen niet gemakkelijk waarneembaar zijn. Voor gebruikers, moet u toospecify **DateTime** of **verwijzing**.
* **Richting**: U kunt instellen Hallo kenmerk richting tooImport, exporteren of ImportExport. ImportExport is standaard.

![schema4b](./media/active-directory-aadconnectsync-connector-genericsql/schema4b.png)

Opmerkingen:

* Als een kenmerktype niet gedetecteerd door Hallo Connector is, wordt het gegevenstype String Hallo.
* **Geneste tabellen** kunnen worden beschouwd als één kolom databasetabellen. Oracle slaat Hallo rijen van een geneste tabel in willekeurige volgorde. Wanneer u de geneste tabel Hallo in een variabele PL-SQL ophaalt, zijn Hallo rijen echter opeenvolgende subscript beginnen bij 1 gegeven. Die biedt u toegang tot de matrix-achtige tooindividual rijen.
* **VARRYS** worden niet ondersteund in Hallo-connector.

### <a name="schema-5-define-partition-for-reference-attributes"></a>Schema 5 (partitie definiëren voor verwijzingskenmerken)
Op deze pagina configureert u voor alle verwijzingskenmerken welke partitie (objecttype) een kenmerk naar verwijst.

![schema5](./media/active-directory-aadconnectsync-connector-genericsql/schema5.png)

Als u **DN-naam is anker**, en vervolgens moet u Hallo Hallo een u van verwijst dezelfde objecttype. U kan niet verwijzen naar een ander objecttype.

>[!NOTE]
Vanaf Hallo maart 2017 update is nu een optie voor ' * ' wanneer deze optie is gekozen en vervolgens alle mogelijke lidtypen moeten worden geïmporteerd.

![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/any-option.png)

>[!IMPORTANT]
 Vanaf mei 2017 Hallo ' * ' aka **elke optie** is gewijzigd toosupport importeren en exporteren van de stroom. Als u deze optie toouse wilt moet uw met meerdere waarden tabelweergave een kenmerk met Hallo objecttype hebben.

![](./media/active-directory-aadconnectsync-connector-genericsql/any-02.png)

 </br> Als ' * ' is geselecteerd wordt Hallo-naam van de kolom met het objecttype Hallo Hallo ook moet worden opgegeven.</br> ![](./media/active-directory-aadconnectsync-connector-genericsql/any-03.png)

Na het importeren ziet u iets dergelijks toohello afbeelding hieronder:

  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/after-import.png)



### <a name="global-parameters"></a>Globale Parameters
Hallo globale Parameters pagina is gebruikte tooconfigure Delta-Import, datum/tijd-indeling, en -methode.

![globalparameters1](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters1.png)



Hallo algemene SQL-Connector ondersteunt Hallo volgende methoden voor Delta-Import:

* **Trigger**: Zie [genereren van Delta-weergaven met Triggers](https://technet.microsoft.com/library/cc708665.aspx).
* **Watermerk**: een algemene benadering die kan worden gebruikt voor elke database. Hallo watermerk query wordt vooraf ingevuld op basis van de leverancier van de Hallo-database. Een watermerk-kolom moet aanwezig zijn op elke tabel of weergave die wordt gebruikt. In deze kolom inserts en updates toohello tabellen als en de afhankelijke moet bijhouden (met meerdere waarden of onderliggende) tabellen. Hallo klokken tussen synchronisatieservice en de databaseserver Hallo moeten worden gesynchroniseerd. Als dat niet het geval is, wordt een aantal invoergegevens in Hallo delta-import kunnen worden weggelaten.  
  Beperking:
  * Watermerk strategie biedt geen verwijderde ondersteuningsobjecten.
* **Momentopname**: (werkt alleen met Microsoft SQL Server) [Delta weergaven met momentopnamen genereren](https://technet.microsoft.com/library/cc720640.aspx)
* **Het bijhouden van**: (werkt alleen met Microsoft SQL Server) [over bijhouden](https://msdn.microsoft.com/library/bb933875.aspx)  
  Beperkingen:
  * Anker & DN-kenmerk moet deel uitmaken van de primaire sleutel voor het geselecteerde object in de tabel Hallo Hallo.
  * SQL-query wordt niet ondersteund tijdens het importeren en exporteren met bijhouden.

**Extra Parameters**: Geef Hallo Server-tijdzone voor de Database waarmee wordt aangegeven waar uw Database-server zich bevindt. Deze waarde wordt gebruikt toosupport Hallo verschillende indelingen van kenmerken van datum en tijd.

Hallo Connector slaat altijd datum- en datum / tijd in UTC-notatie. toobe kunnen toocorrectly converteren Hallo datum en tijd, Hallo tijdzone van de databaseserver Hallo en Hallo-indeling gebruikt moet worden opgegeven. Hallo-indeling moet worden uitgedrukt in .net-indeling.

Tijdens het exporteren moet elke kenmerk op tijd toohello Connector in UTC-tijdnotatie worden opgegeven.

![globalparameters2](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters2.png)

**Configuratie van wachtwoord**: Hallo connector biedt mogelijkheden voor synchronisatie van wachtwoord en ondersteunt het instellen en wachtwoord te wijzigen.

Hallo Connector biedt twee methoden toosupport Wachtwoordsynchronisatie:

* **Opgeslagen Procedure**: deze methode moet twee opgeslagen procedures toosupport Set & wachtwoord wijzigen. Typ alle parameters voor toevoegen en wijzigen Hallo wachtwoord opnieuw in **ingesteld wachtwoord SP** en **wijzigen wachtwoord SP** Parameters respectievelijk conform onderstaand voorbeeld.
  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)
* **Wachtwoord extensie**: deze methode moet een wachtwoord uitbreidings-DLL (u moet tooprovide Hallo Extensienaam DLL die Hallo implementeert [IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) interface). Uitbreidingsassembly wachtwoord moet worden geplaatst in de map de extensie zodat Hallo-connector kunt Hallo dll-bestand tijdens runtime worden geladen.
  ![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)

U hebt ook tooenable Hallo wachtwoordbeheer op Hallo **extensie configureren** pagina.
![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)

### <a name="configure-partitions-and-hierarchies"></a>Partities en hiërarchieën configureren
Selecteer alle objecttypen op Hallo partities en hiërarchieën pagina. Elk objecttype is zijn eigen partitie.

![partitions1](./media/active-directory-aadconnectsync-connector-genericsql/partitions1.png)

U kunt ook negeren Hallo-waarden die zijn gedefinieerd op Hallo **connectiviteit** of **globale Parameters** pagina.

![partitions2](./media/active-directory-aadconnectsync-connector-genericsql/partitions2.png)

### <a name="configure-anchors"></a>Ankers configureren
Deze pagina is alleen-lezen omdat Hallo anker is al gedefinieerd. Hallo geselecteerde ankerkenmerk worden altijd toegevoegd met de Hallo object type tooensure blijft deze unieke over objecttypen.

![vertrouwensankers](./media/active-directory-aadconnectsync-connector-genericsql/anchors.png)

## <a name="configure-run-step-parameter"></a>Voer stap Parameter configureren
Deze stappen zijn geconfigureerd op Hallo uitvoeringsprofielen op Hallo Connector. Deze configuraties Hallo eigenlijke werk van de gegevens importeren en exporteren.

### <a name="full-and-delta-import"></a>Volledige en Delta-Import
Algemene SQL-Connector ondersteuning voor volledige en Delta-Import gebruik van deze methoden:

* Tabel
* Weergave
* Opgeslagen procedure
* SQL-Query

![runstep1](./media/active-directory-aadconnectsync-connector-genericsql/runstep1.png)

**Tabel of weergave**  
tooimport met meerdere waarden kenmerken voor een object, hebt u de naam van de tabel of weergave door komma's gescheiden Hallo tooprovide in **naam van meerwaardige tabelweergaven** en respectieve join-voorwaarden in Hallo **joinvoorwaarde**met Hallo bovenliggende tabel.

Voorbeeld: U tooimport Hallo werknemer object en alle bijbehorende kenmerken met meerdere waarden. Er zijn twee tabellen, met de naam werknemer (hoofdtabel) en afdeling (met meerdere waarden).
Hallo te volgen:

* Type **werknemer** in **tabel/weergave/SP**.
* Type afdeling in **naam van meerwaardige tabelweergaven**.
* Typ Hallo join-voorwaarde tussen werknemer & afdeling in **Join-voorwaarde**, bijvoorbeeld `Employee.DEPTID=Department.DepartmentID`.
  ![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)

**Opgeslagen procedures**  
![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)

* Als u veel gegevens hebt, is het raadzaam tooimplement paginering met uw opgeslagen Procedures.
* Voor de opgeslagen Procedure toosupport paginering moet u tooprovide Index Start en End-Index. Zie: [efficiënt paginering van grote hoeveelheden gegevens](https://msdn.microsoft.com/library/bb445504.aspx).
* @StartIndexen @EndIndex tijdens uitvoeringstijd worden vervangen door geconfigureerd op de waarde van de desbetreffende pagina bestandsgrootte **stap configureren** pagina. Bijvoorbeeld, wanneer Hallo connector haalt eerste pagina en de paginagrootte Hallo is ingesteld 500, in een dergelijke situatie @StartIndex zou dit 1 en @EndIndex 500. Deze waarden vergroten wanneer connector de volgende pagina's haalt en wijzig Hallo @StartIndex & @EndIndex waarde.
* tooexecute parameters van opgeslagen Procedure gebruikt, Geef parameters op Hallo in `[Name]:[Direction]:[Value]` indeling. Voer elke parameter in op een afzonderlijke regel (Gebruik Ctrl + Enter tooget een nieuwe regel).
* Algemene SQL-connector ondersteunt ook de importbewerking van gekoppelde Servers in Microsoft SQL Server. Gegevens moeten worden opgehaald uit een tabel in de gekoppelde server, moet tabel worden opgegeven in de indeling Hallo:`[ServerName].[Database].[Schema].[TableName]`
* Algemene SQL-Connector ondersteunt alleen objecten die vergelijkbaar structuur (zowel alias naam en het gegevenstype type) tussen de detectie van gegevens en schema's voor de stappen uitvoeren. Als Hallo geselecteerd object van het schema en de opgegeven informatie in stappen van uitvoering verschilt, is SQL-Connector kan geen toosupport dit soort scenario's.

**SQL-Query**  
![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)

![runstep5](./media/active-directory-aadconnectsync-connector-genericsql/runstep5.png)

* Meerdere resultatensets query's niet ondersteund.
* SQL-query ondersteunt Hallo paginering en geef start-Index en End Index als een variabele toosupport paginering.

### <a name="delta-import"></a>Delta-Import
![runstep6](./media/active-directory-aadconnectsync-connector-genericsql/runstep6.png)

Configuratie van delta-Import is vergeleken met de volledige Import meer configuratie vereist.

* Als u Hallo Trigger of momentopname benadering tootrack deltawijzigingen kiest, geeft u geschiedenistabel of momentopname van de database in **geschiedenistabel of momentopname van de databasenaam** vak.
* U moet ook de join-voorwaarde tooprovide tussen geschiedenistabel en bovenliggende tabel, bijvoorbeeld`Employee.ID=History.EmployeeID`
* tootrack hello transactie op Hallo bovenliggende tabel van de geschiedenistabel hello, moet u Hallo kolomnaam waarin de gegevens van de bewerking hello (toevoegen, bijwerken, verwijderen) opgeven.
* Als u watermerk tootrack deltawijzigingen kiest, geeft u Hallo kolomnaam met Hallo bewerkingsinformatie in **Water Mark kolomnaam**.
* Hallo **wijzigen typekenmerk** kolom is vereist voor het wijzigingstype Hallo. In deze kolom wordt een wijziging die in de primaire tabel Hallo plaatsvindt toegewezen of meerdere waarden tabel tooa type in Hallo delta-weergave wijzigen. Deze kolom mag Hallo Modify_Attribute wijzigingstype voor kenmerk niveau wijzigen of toevoegen, wijzigen of verwijderen Wijzig type voor een type op objectniveau wijzigen. Als deze iets anders dan Hallo standaardwaarde toevoegen, wijzigen of verwijderen, moet u deze waarden met deze optie kunt definiëren.

### <a name="export"></a>Exporteren
![runstep7](./media/active-directory-aadconnectsync-connector-genericsql/runstep7.png)

Ondersteuning voor algemene SQL-Connector exporteren met behulp van vier ondersteunde methoden, zoals:

* Tabel
* Weergave
* Opgeslagen procedure
* SQL-Query

**Tabel of weergave**  
Als u Hallo tabel of weergave optie kiest, genereert Hallo connector Hallo bijbehorende query's toodo Hallo exporteren.

**Opgeslagen procedures**  
![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)

Als u Hallo opgeslagen Procedure-optie kiest, moet exporteren drie verschillende opgeslagen procedures tooperform Insert/Update/Delete-bewerkingen.

* **Naam van de Serviceprovider toevoegen**: deze SP wordt uitgevoerd wanneer een object tooconnector voor invoeging in de bijbehorende tabel Hallo afkomstig is.
* **Werk de naam SP**: deze SP wordt uitgevoerd wanneer een object tooconnector voor update in de bijbehorende tabel Hallo afkomstig is.
* **De naam van de Serviceprovider verwijderen**: deze SP wordt uitgevoerd wanneer een object tooconnector voor verwijdering in de bijbehorende tabel Hallo afkomstig is.
* Het kenmerk is geselecteerd in Hallo schema gebruikt als een parameter waarde toohello opgeslagen procedure. Bijvoorbeeld: `EmployeeName: INPUT: @EmployeeName` (EmployeeName is geselecteerd in het Hallo-connector schema en Hallo connector vervangt de betreffende waarde Hallo tijdens de export)
* toorun parameters van opgeslagen procedure gebruikt, geef de parameters in `[Name]:[Direction]:[Value]` indeling. Voer elke parameter in op een afzonderlijke regel (Gebruik Ctrl + Enter tooget een nieuwe regel).

**SQL-query**  
![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)

Als u Hallo SQL query-optie kiest, exporteren is vereist dat drie verschillende vraagt tooperform Insert/Update/Delete-bewerkingen.

* **Query invoegen**: deze query wordt uitgevoerd wanneer een object tooconnector voor invoeging in de bijbehorende tabel Hallo afkomstig is.
* **Query bijwerken**: deze query wordt uitgevoerd wanneer een object tooconnector voor update in de bijbehorende tabel Hallo afkomstig is.
* **Query verwijdert**: deze query wordt uitgevoerd wanneer een object tooconnector voor verwijdering in de bijbehorende tabel Hallo afkomstig is.
* Kenmerk geselecteerd uit Hallo schema gebruikt als een parameter waarde toohello query, bijvoorbeeld`Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`

## <a name="troubleshooting"></a>Problemen oplossen
* Zie voor informatie over hoe logboekregistratie tooenable tootroubleshoot connector Hallo Hallo [hoe tooEnable ETW-tracering voor Connectors](http://go.microsoft.com/fwlink/?LinkId=335731).
