---
title: aaaWhat de nieuw in Azure Data Catalog | Microsoft Docs
description: Dit artikel bevat dat een overzicht van nieuwe mogelijkheden toegevoegd tooAzure Data Catalog.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 1201f8d4-6f26-4182-af3f-91e758a12303
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/22/2017
ms.author: maroche
ms.openlocfilehash: f60130487ece39e110446b68544945089d2ab37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="whats-new-in-azure-data-catalog"></a>Wat is er nieuw in Azure Data Catalog
Updates te**Azure Data Catalog** regelmatig worden vrijgegeven. Niet elke versie bevat nieuwe gebruikersgerichte functies, zoals sommige versies zijn gericht op de mogelijkheden van de back-end-service. Deze pagina licht nieuwe mogelijkheden van de gebruiker gerichte toegevoegde toohello Azure Data Catalog-service.

## <a name="whats-new-for-august-2017"></a>Wat is er nieuw voor augustus 2017 
Vanaf augustus 2017 zijn Hallo na mogelijkheden toegevoegd tooAzure Data Catalog:

*   Een nieuwe developer-voorbeeld is beschikbaar voor het maken en beheren van metagegevens van de relatie met behulp van Hallo REST-API van Data Catalog. Hallo *relatiegegevens importeren in Data Catalog* voorbeeld is beschikbaar op Hallo [voorbeelden van Data Catalog codetabel](https://azure.microsoft.com/resources/samples/?service=data-catalog&sort=0). 
* Ondersteuning voor het uitpakken van lid worden van de metagegevens van de relatie van gegevensbronnen Teradata bij het registreren van de gerelateerde tabellen met hulpprogramma voor registratie van gegevensbronnen Hallo.
* Ondersteuning voor SQL Server tabelgewaardeerde functie (TVF)-objecten bij het registreren van gegevensbronnen van SQL Server met behulp van hulpprogramma voor registratie van gegevensbronnen Hallo.
* Meerdere updates en verfijningen tooincrease Hallo prestaties en bruikbaarheid van Hallo Data Catalog-portal.

## <a name="whats-new-for-july-2017"></a>Wat is er nieuw voor juli 2017 
Vanaf juli 2017 hebt Hallo volgende mogelijkheden toegevoegd tooAzure Data Catalog:
*   Ondersteuning voor gedetailleerdere controle over de bewerkingen voor metagegevens dit is toegestaan met inbegrip van:
    - Beheerders van de catalogus kunnen beperken voor gebruikers de mogelijkheid toocontribute tags en verwante metagegevens toohello catalogus, alleen-lezentoegang toohello catalogus inschakelt.
    - Catalogus-beheerders kunnen gebruikers de mogelijkheid tooregister nieuwe gegevensbronnen in de catalogus Hallo beperken.
    - Catalogus beheerders kunnen gebruikers de mogelijkheid tootake eigendom van metagegevens van de asset gegevens in de catalogus Hallo beperken.
    - Er kunnen machtigingen worden verleend tooAzure Active Directory-beveiligingsgroepen en gebruikers voor eenvoudig beheer van machtigingen.
* Ondersteuning voor relaties tussen geregistreerde gegevensassets en detecterende gerelateerde gegevens activa in Hallo Data Catalog-portal, met inbegrip van:
    - Uitpakken van de metagegevens van de relatie van SQL Server (met inbegrip van Azure SQL Database), Oracle en MySQL Hallo gegevensbronnen bij gebruik van hulpprogramma voor registratie van gegevensbronnen Data Catalog.
    - Detectie van activa gerelateerde gegevens bij het bekijken van metagegevens van de asset in Hallo Data Catalog-portal.
    - Operations-toodefine detecteren en beheren van relaties tussen gegevensassets met behulp van Hallo REST-API van Data Catalog.

Zie voor meer informatie over het beheren van machtigingen in Data Catalog [hoe toosecure toegang krijgen tot de catalogus en gegevens activa toodata](data-catalog-how-to-secure-catalog.md).
Zie voor meer informatie over de relaties in Data Catalog [hoe tooview gegevensassets in Azure Data Catalog gerelateerd](data-catalog-how-to-view-related-data-assets.md).

## <a name="whats-new-for-june-2017"></a>Wat is er nieuw voor juni 2017 
Vanaf juni 2017 hebt Hallo volgende mogelijkheden toegevoegd tooAzure Data Catalog:
*   Ondersteuning voor Sybase Apache Cassandra en MongoDB-gegevensbronnen. Gebruikers kunnen nu registreren en detecteren Cassandra en MongoDB-databases en tabellen en Sybase-databases en tabellen en weergaven.

> [!NOTE]
> Wanneer het registreren van MongoDB en Cassandra tabellen die kolommen met complexe gegevenstypen zoals records en matrices, deze kolommen bevatten worden niet opgenomen in de metagegevens van de Hallo tooData catalogus toegevoegd.

## <a name="whats-new-for-may-2017"></a>Wat is er nieuw voor mei 2017 
Vanaf mei 2017 hebt Hallo volgende mogelijkheden toegevoegd tooAzure Data Catalog:
*   Een nieuwe developer-voorbeeld is beschikbaar voor Hallo bulkbewerkingen voor importeren van zakelijke woordenlijst van termen. Hallo verklarende woordenlijst bulkimport voorbeeld is beschikbaar op Hallo [pagina met Data Catalog developer-voorbeelden](https://docs.microsoft.com/azure/data-catalog/data-catalog-samples). 
*   Ondersteuning voor het bewerken van ODBC-verbindingsgegevens in hello Azure Data Catalog-portal. Eigenaren van asset en beheerders van Data Catalog kunnen u nu Hallo-verbindingsgegevens voor de geregistreerde ODBC-gegevensbronnen bewerken zonder toore registreren Hallo-gegevensbronnen.
*   Ondersteuning voor klikbaar URL's in de zakelijke woordenlijst definities en beschrijvingen. Wanneer URL's worden opgenomen in de eigenschappen van de beschrijving en de definitie van de hello voor bedrijven termen, Hallo URL's weergegeven als hyperlinks in Hallo Data Catalog-portal.
*   Ondersteuning voor het weergeven van de expert benoemt bovendien tooexpert e-mailadressen. Wanneer bekijkt hello eigenschappen voor een gegevensasset-experts in Hallo Data Catalog-portal, wordt de volledige naam van de expert Hallo van Azure Active Directory weergegeven in knopinfo Hallo.

## <a name="whats-new-for-april-2017"></a>Wat is er nieuw voor April 2017 
Vanaf April 2017 hebt Hallo volgende mogelijkheden toegevoegd tooAzure Data Catalog:
*   Ondersteuning voor ODBC-gegevensbronnen. Gebruikers kunnen nu registreren en ODBC-databases, tabellen en weergaven Hallo Data Catalog hulpprogramma voor registratie met detecteren.

## <a name="whats-new-for-march-2017"></a>Wat is er nieuw voor maart 2017 
Vanaf maart 2017 hebt Hallo volgende mogelijkheden toegevoegd tooAzure Data Catalog:
*   Ondersteuning voor het gebruik van AAD-beveiligingsgroepen voor beheerders van Data Catalog.
*   Azure Data Catalog is nu beschikbaar in een nieuwe Azure-regio. Klanten kunnen inrichten hello Azure Data Catalog in Hallo West-Centraal VS regio, in aanvulling tooEast VS, VS-West, West-Europa en Australië-Oost, Noord-Europa en Zuidoost-Azië. Zie voor meer informatie [Azure-gebieden](https://azure.microsoft.com/regions/).

## <a name="whats-new-for-february-2017"></a>Wat is er nieuw voor februari 2017 
Vanaf februari 2017 hebt Hallo volgende mogelijkheden toegevoegd tooAzure Data Catalog:
*   Ondersteuning voor geavanceerde instellingen in Hallo Data Catalog hulpprogramma voor registratie. Gebruikers kunnen opdracht time-outwaarden opgeven bij het registreren van gegevensbronnen van grote hoeveelheden gegevens.
*   Ondersteuning voor FTP- en PostgreSQL-gegevensbronnen. Gebruikers kunnen nu registreren en FTP-bestanden en mappen, en PostgreSQL databases, tabellen en weergaven te detecteren.

## <a name="whats-new-for-january-2017"></a>Wat is er nieuw voor januari 2017 
Vanaf januari 2017 hebt Hallo volgende mogelijkheden toegevoegd tooAzure Data Catalog:
*   Azure Data Catalog is nu [CSA STER](https://www.microsoft.com/trustcenter/compliance/csa-star-certification) compatibel.
*   Integratie met [ophalen en transformeren in Excel 2016 en Power Query voor Excel](https://support.office.com/article/Introduction-to-Microsoft-Power-Query-for-Excel-6E92E2F4-2079-4E1F-BAD5-89F6269CD605). Excel-gebruikers kunnen delen van query's en query's met Azure Data Catalog uit detecteren in Excel. Deze functionaliteit is beschikbaar toousers met Power BI Pro licenties.

## <a name="whats-new-for-december-2016"></a>Wat is er nieuw voor December 2016
Vanaf December 2016, zijn Hallo na mogelijkheden toegevoegd tooAzure Data Catalog:
*   Azure Data Catalog is nu [HIPAA](https://www.microsoft.com/trustcenter/Compliance/HIPAA) en [Modelbepalingen EU](https://www.microsoft.com/TrustCenter/Compliance/EU-Model-Clauses) compatibel.
*   Ondersteuning voor het bewerken van informatie van de gegevensbronverbinding. Eigenaren van asset en beheerders van Data Catalog kunnen u nu Hallo-verbindingsgegevens voor de geregistreerde gegevensbronnen bewerken zonder toore registreren Hallo-gegevensbronnen.
*   Ondersteuning voor Salesforce.com-gegevensbronnen. Gebruikers kunnen nu registreren en Salesforce-objecten te detecteren.


## <a name="whats-new-for-november-2016"></a>Wat is er nieuw voor November 2016
Vanaf November 2016, zijn Hallo na mogelijkheden toegevoegd tooAzure Data Catalog:
*   Azure Data Catalog is nu [ISO/IEC 27001](https://www.microsoft.com/trustcenter/compliance/iso-iec-27001) en [ISO/IEC 27018](https://www.microsoft.com/TrustCenter/Compliance/iso-iec-27018) compatibel.
*   Ondersteuning voor de handmatige registratie Hallo van ODBC-gegevensbronnen met Hallo Data Catalog-portal en REST-API.

## <a name="whats-new-for-september-2016"></a>Wat is er nieuw voor September 2016
Vanaf September 2016 zijn Hallo na mogelijkheden toegevoegd tooAzure Data Catalog:

* Ondersteuning voor IBM DB2-gegevensbronnen. Gebruikers kunnen nu registreren en detecteren DB2-databases, tabellen en weergaven.
* Ondersteuning voor Azure Cosmos DB-gegevensbronnen. Gebruikers kunnen nu registreren en detecteren Cosmos-DB-databases en verzamelingen.
* Ondersteuning voor het aanpassen van de catalogusnaam Hallo in Hallo Data Catalog-portal. Catalogus-beheerders kunnen nu een tekst die wordt weergegeven in de portal titel hello, zoals de naam van de organisatie Hallo.

## <a name="whats-new-for-august-2016"></a>Wat is er nieuw voor augustus 2016
Vanaf augustus 2016 zijn Hallo na mogelijkheden toegevoegd tooAzure Data Catalog:

* Verbeteringen voor de registratie van gegevensbronnen van SQL Server Master Data Services (MDS). Gebruikers kunnen nu opnemen voor profielen voor voorbeelden en gegevens bij het registreren van Hallo Data Catalog hulpprogramma voor registratie met MDS-entiteiten.
* Ondersteuning voor de beheerder gedefinieerde organisatie opgeslagen zoekopdrachten. Als u een zoekopdracht opslaat in Hallo Data Catalog-portal, kunnen Data Catalog-beheerders nu toosave zoekopdrachten voor persoonlijk gebruik of voor alle gebruikers van de catalogus kiezen. Opgeslagen zoekopdrachten organisatie worden gedeeld met alle gebruikers van de catalogus en gestandaardiseerde beginpunten kunnen opgeven voor detectie van gegevensbronnen.
* Weergave van eigenschappen toohello in Hallo Data Catalog-portal-updates. Eigenschappen van de asset alle gegevens worden nu weergegeven en beheerd in een enkele, formaat deelvenster tooprovide een consistente en detecteerbaar ervaring.

## <a name="whats-new-for-july-2016"></a>Wat is er nieuw voor juli 2016
Vanaf juli 2016, zijn Hallo na mogelijkheden toegevoegd tooAzure Data Catalog:

* Ondersteuning voor SQL Server Master Data Services (MDS)-gegevensbronnen. Gebruikers kunnen nu registreren en MDS-modellen en entiteiten te detecteren.
* Ondersteuning voor SQL Server opgeslagen procedures. Gebruikers kunnen nu worden geregistreerd en opgeslagen procedure-objecten in SQL Server-gegevensbronnen te detecteren.
* Ondersteuning voor extra talen in hello Azure Data Catalog-portal en Hallo hulpprogramma voor registratie, voor een totaal van 18 ondersteunde talen. Hallo gebruikerservaring van Azure Data Catalog is gelokaliseerd op basis van het taalvoorkeuren Hallo instellen in Windows of in de webbrowser Hallo.
* Updates en verfijning voor Hallo Data Catalog portal startpagina, met inbegrip van betere prestaties en een gestroomlijnde gebruikerservaring.

## <a name="whats-new-for-june-2016"></a>Wat is er nieuw voor juni 2016
Vanaf juni 2016 zijn Hallo na mogelijkheden toegevoegd tooAzure Data Catalog:

* Ondersteuning voor het formaat van kolommen in de lijstweergave Hallo wijzigen bij het detecteren van gegevensassets in Hallo Data Catalog-portal. Gebruikers kunnen nu de grootte van afzonderlijke kolommen toomore gemakkelijk lezen langdurige asset metagegevens zoals labels en beschrijvingen.
* Power Query voor Excel is toohello "Openen in" menu toegevoegd in Hallo Data Catalog-portal. Gebruikers kunnen nu ondersteunde gegevensbronnen in Excel 2016 of openen in Excel 2010 en Excel 2013 Hello [Power Query voor Excel](https://support.office.com/article/Introduction-to-Microsoft-Power-Query-for-Excel-6E92E2F4-2079-4E1F-BAD5-89F6269CD605) invoegtoepassing geïnstalleerd.
* Ondersteuning voor Azure Table Storage-gegevensbronnen. Gebruikers kunnen nu registreren en tabelobjecten in Azure Storage-gegevensbronnen te detecteren.

## <a name="whats-new-for-may-2016"></a>Wat is er nieuw voor mei 2016
Vanaf mei 2016, zijn Hallo na mogelijkheden toegevoegd tooAzure Data Catalog:

* Een zakelijke woordenlijst waarmee beheerders van de catalogus toodefine business voorwaarden en hiërarchieën toocreate een algemene zakelijke woordenlijst. Gebruikers, geregistreerde gegevensassets met woordenlijst van termen toomake kunnen labelen deze eenvoudiger toodiscover en inhoud van catalogus Hallo Hallo begrijpen. Zie voor meer informatie [hoe tooset van zakelijke woordenlijst Hallo voor Governed Tagging](data-catalog-how-to-business-glossary.md)  
* Verbeteringen toohello Data Catalog zakelijke woordenlijst waarmee gebruikers tooupdate meerdere termen in één bewerking. Gebruikers kunnen meerdere voorwaarden tooedit Hallo na velden selecteren:
  * Bovenliggende Term: een nieuwe bovenliggende term voor Hallo-gebruiker kunt selecteren en alle geselecteerde voorwaarden zijn bijgewerkte toobe onderliggende elementen van Hallo geselecteerd bovenliggende term. Als Hallo geselecteerd voorwaarden die alle hebben hello en dat de bovenliggende vervolgens dezelfde bovenliggende activiteit wordt weergegeven in Hallo textbox, anders Hallo bovenliggende term veld set tooblank is.   
  * Tags en belanghebbenden: gebruikers kunnen toevoegen en verwijderen van tags en belanghebbenden voor meerdere termen in de Hallo dezelfde ervaring als meerdere gegevensassets tagging gebruiken.

> [!NOTE]
> Hallo zakelijke woordenlijst is alleen beschikbaar in Standard-editie van Azure Data Catalog Hallo. Hallo biedt editie Free geen mogelijkheden voor geregeld tagging of een zakelijke woordenlijst.

## <a name="whats-new-for-march-2016"></a>Wat is er nieuw voor maart 2016
Vanaf maart 2016 zijn Hallo na mogelijkheden toegevoegd tooAzure Data Catalog: g:

* Een geconsolideerde REST-API-eindpunt voor programmatisch toegang tot de zoekmogelijkheden Hallo en catalogus activa-beheermogelijkheden van hello Azure Data Catalog-service. Deze zoekopdracht API-eindpunt en catalogus API-eindpunt is afgeschaft en op 21 maart 2016 afgeschaft. Er zijn geen wijzigingen toohello semantiek van Hallo API. Hallo-eindpunt URI gewijzigd. Zie voor meer informatie, Hallo [Azure Data Catalog REST API Reference](https://msdn.microsoft.com/library/azure/mt267595.aspx). Zie voor voorbeelden van de API, [voorbeelden van Azure Data Catalog developer](data-catalog-samples.md).

## <a name="whats-new-for-february-2016"></a>Wat is er nieuw voor februari 2016
Vanaf februari 2016 hebt Hallo volgende mogelijkheden toegevoegd tooAzure Data Catalog:

* Een nieuw vernieuwde bronselectie optreden in hello Azure Data Catalog hulpprogramma voor registratie. Hallo hulpprogramma voor registratie van gegevensbronnen is bijgewerkte toomake it eenvoudiger u toolocate en selecteer een van de gegevensbronnen Hallo ondersteund door Azure Data Catalog.
* Ondersteuning voor 10 extra talen in hello Azure Data Catalog-portal en het hulpprogramma voor registratie van gegevensbronnen Hallo. Bovendien tooEnglish, Hallo ervaring met Azure Data Catalog is nu beschikbaar in het Duits, Spaans, Frans, Italiaans, Japans, Koreaans, Portugees (Brazilië), Russische, vereenvoudigd Chinees en traditioneel Chinees. Hello Azure Data Catalog gebruikerservaring is gelokaliseerd gebaseerd op het taalvoorkeuren Hallo instellen in Windows of in de webbrowser van Hallo gebruiker.
* Ondersteuning voor de geo-replicatie van gegevens van Azure Data Catalog voor zakelijke continuïteit en herstel na noodgevallen. Alle inhoud van de Azure Data Catalog, met inbegrip van gegevensbron metagegevens en crowdsourcing aantekeningen worden nu gerepliceerd tussen twee Azure-regio's op geen toocustomers extra kosten. Hello Azure-regio's zijn vooraf gekoppeld ten minste 500 mijl uit elkaar, en volg Hallo toewijzing zoals beschreven in [zakelijke continuïteit en herstel na noodgevallen (BCDR): Azure-gebieden gekoppeld](../best-practices-availability-paired-regions.md).
* Ondersteuning voor het wijzigen van hello Azure-abonnement gebruikt door Azure Data Catalog. Azure Data Catalog-beheerders kunnen voor facturatie Hallo instellingenpagina in hello Azure Data Catalog portal tooselect een ander Azure-abonnement gebruiken.

## <a name="whats-new-for-january-2016"></a>Wat is er nieuw voor januari 2016
Vanaf januari 2016 zijn Hallo na mogelijkheden toegevoegd tooAzure Data Catalog:

* Ondersteuning voor het handmatig extra gegevensbronnen te registreren. U kunt nu 'Handmatig bericht maken' in hello Azure Data Catalog-portal gebruiken of Hallo REST-API van Azure Data Catalog tooregister Hallo gegevensbronnen te volgen:
  * OData - functie, entiteitset en Entiteitscontainer
  * HTTP - bestand, eindpunt, rapport en de Site
  * Bestandssysteem - bestand
  * SharePoint - lijst
  * FTP - bestanden en mappen
  * SalesForce.com - Object
  * DB2 - tabel, weergave en Database
  * PostgreSQL - tabel, weergave en Database
* Ondersteuning voor 'Openen in SQL Server Data Tools' voor SQL Server (inclusief Azure SQL DB en Azure SQL Data Warehouse)-gegevensbronnen.  
* Ondersteuning voor het registreren en SAP HANA-weergaven en pakketten detecteren. U kunt registreren SAP HANA gegevens bronnen met hello Azure Data Catalog data source hulpprogramma voor registratie en kunnen aantekeningen toevoegen aan en geregistreerde SAP HANA-gegevensbronnen met hello Azure Data Catalog portal detecteren.
* Hallo mogelijkheid toopin en losmaken van gegevensassets in hello Azure Data Catalog-portal. U kunt toopin gegevens activa toomake ze gemakkelijker toorediscover en opnieuw kunnen worden gebruikt.
* Een nieuw vernieuwde introductiepagina in hello Azure Data Catalog-portal. Hallo nieuwe introductiepagina bevat inzicht in de Hallo huidige gebruikers activiteit - inclusief onlangs gepubliceerde activa vastgemaakt activa en opgeslagen zoekopdrachten- en inzicht in het Hallo-activiteit in Hallo catalogus als geheel.
* Ondersteuning voor permanente gebruikersinstellingen in hello Azure Data Catalog-portal. Instellingen voor gebruikerservaring - inclusief weergave van raster of tegel, aantal resultaten per pagina Hallo en markeren in- of uitschakelen - blijven bestaan tussen gebruikerssessies.
* Azure Data Catalog is nu beschikbaar in twee nieuwe Azure-regio's. Klanten kunnen inrichten hello Azure Data Catalog in Hallo Noord-Europa en Zuidoost-Azië gebieden in toevoeging tooEast VS, VS-West, West-Europa en Australië-Oost. Zie voor meer informatie [Azure-gebieden](https://azure.microsoft.com/regions/).

> [!NOTE]
> 'Openen in SQL Server Data Tools' vereist Visual Studio 2013 met Update 4 en SQL Server Tooling toobe geïnstalleerd. Bezoek tooinstall Hallo meest recente versie van SQL Server Data Tools [Download SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).


## <a name="whats-new-for-december-2015"></a>Wat is er nieuw voor December 2015
Vanaf December 2015 zijn Hallo na mogelijkheden toegevoegd tooAzure Data Catalog:

* Ondersteuning voor gegevens profielen voor gegevensbronnen voor Azure SQL Data Warehouse. Bij het registreren van Azure SQL Data Warehouse-tabellen en weergaven, kunnen gebruikers metrische gegevens tooinclude gegevens profiel kiezen met opgehaald uit de gegevensbron Hallo Hallo-metagegevens.
* Ondersteuning voor het registreren en detectie van MySQL-objecten en -databases. Gebruikers kunnen zich registreren MySQL gegevens bronnen hello Azure Data Catalog gegevens met bron-hulpprogramma voor registratie en kunnen aantekeningen toevoegen aan en geregistreerde MySQL gegevensbronnen met hello Azure Data Catalog portal detecteren.
* Ondersteuning voor het SPNEGO- en Windows-verificatie voor Teradata-gegevensbronnen. Wanneer u registreert Teradata-tabellen en weergaven, kunnen gebruikers tooconnect tooTeradata SPNEGO en Windows, en LDAP en TD2-verificatie te kiezen.
* Ondersteuning voor Azure Data Lake Store-gegevensbronnen. Gebruikers kunnen nu registreren en gegevensbronnen voor Azure Data Lake Store met Azure Data Catalog detecteren.
* Ondersteuning voor het netwerk proxy-instellingen handmatig opgeven in hello Azure Data Catalog hulpprogramma voor registratie. Gebruikers 'Proxy-instellingen wijzigen' kunnen kiezen uit Hallo-hulpprogramma welkomstpagina en Hallo proxy-adres en poort toobe gebruikt door Hallo hulpprogramma kunnen opgeven.

## <a name="whats-new-for-november-2015"></a>Wat is er nieuw voor November 2015
Vanaf November 2015 hebt Hallo volgende mogelijkheden toegevoegd tooAzure Data Catalog:

* Hallo mogelijkheid tooview en kopieer verbindingsreeksen uit binnen hello Azure Data Catalog-portal voor SQL-Server (met inbegrip van Azure SQL Database) en Oracle-gegevensbronnen. Gebruikers kunnen klikken op de koppeling 'Verbindingsreeksen weergeven' in Hallo-verbindingsgegevens voor een SQL Server of Oracle tabel, weergave of database toosee Hallo verbindingsreeksen tooconnect toohello gegevensbron gebruikt. ADO.NET, ODBC, OLEDB en JDBC verbindingsreeksen zijn beschikbaar voor SQL Server-gegevensbronnen. ODBC en OLEDB-verbindingsreeksen zijn beschikbaar voor Oracle-gegevensbronnen.
* Ondersteuning voor het opnemen van gegevens profielen bij het registreren van Teradata-tabellen en weergaven.
* Ondersteuning voor 'Openen in Power BI Desktop' voor SQL Server (inclusief Azure SQL DB en Azure SQL Data Warehouse), SQL Server Analysis Services, Azure Storage en HDFS-bronnen.  
* Ondersteuning voor LDAP-verificatie voor Teradata-gegevensbronnen. Wanneer u registreert Teradata-tabellen en weergaven, kunnen gebruikers kiezen tooconnect tooTeradata met behulp van LDAP, en TD2 verificatie.
* Ondersteuning voor 'Openen in Excel' voor Teradata-gegevensbronnen.
* Ondersteuning voor recente zoektermen in hello Azure Data Catalog-portal. Wanneer u zoekt in de portal hello, worden gebruikers in recent gebruikte termen tooaccelerate Hallo detectie zoekervaring kunnen selecteren.
* Ondersteuning voor het voorbeeld voor Teradata-gegevensbronnen. Wanneer u registreert Teradata-tabellen en weergaven, kunnen gebruikers tooinclude momentopname records met Hallo metagegevens opgehaald uit de gegevensbron Hallo kiezen.
* Ondersteuning voor 'Openen in Excel' voor gegevensbronnen voor Azure SQL Data Warehouse.
* Ondersteuning voor het definiëren en te bewerken op kolomniveau schema's voor handmatig geregistreerde gegevensassets. Nadat een gegevensasset met hello Azure Data Catalog portal handmatig is gemaakt, kunnen gebruikers in de eigenschappen van asset gegevens Hallo kolomdefinities toevoegen.
* Ondersteuning voor 'is'-query's bij het zoeken van Azure Data Catalog, tooenable Hallo detectie van geregistreerde gegevensassets die beschikken over specifieke metagegevens. Azure Data Catalog-querysyntaxis bevat nu:

| Querysyntaxis | Doel |
| --- | --- |
| `has:previews` |Zoeken naar gegevensassets die een voorbeeld |
| `has:documentation` |Zoeken naar gegevensassets waarvoor documentatie is opgegeven |
| `has:tableDataProfiles` |Zoeken naar gegevensassets met profielgegevens op tabelniveau gegevens |
| `has:columnsDataProfiles` |Zoeken naar gegevensassets met informatie over het profiel van de gegevens op kolomniveau |


> [!NOTE]
> 'Openen in Power BI Desktop' vereist een actuele versie van Hallo Power BI Desktop toepassing toobe is geïnstalleerd. Als u problemen ondervindt of fouten bij het gebruik van deze functie, zorg ervoor dat er Hallo meest recente versie van Power BI Desktop van [PowerBI.com](https://powerbi.com).


## <a name="whats-new-for-october-2015"></a>Wat is er nieuw voor oktober 2015
Vanaf oktober 2015 hebt Hallo volgende mogelijkheden toegevoegd tooAzure Data Catalog:

* Ondersteuning voor versleuteling in rust van gegevens previews en gegevens profielen voor geregistreerde gegevensbronnen. Azure Data Catalog versleutelt transparant preview records en -gegevens profielen gegevensbronnen die zijn geregistreerd bij de service hello, zonder dat u hoeft voor sleutelbeheer door beheerders van de catalogus.
* Ondersteuning voor Teradata-gegevensbronnen. Gebruikers kunnen nu registreren en Teradata-tabellen en weergaven te detecteren.
* Ondersteuning voor on-premises Hive-gegevensbronnen. Gebruikers kunnen nu registreren en Hive-tabellen voor Apache Hive in Hadoop on-premises gegevensbronnen detecteren.
* Ondersteuning voor opgeslagen zoekopdrachten in hello Azure Data Catalog-portal. Gebruikers kunnen opslaan zoektermen en filter selecties tooeasily Herhaal de vorige zoekopdrachten en nuttige weergaven van de inhoud van catalogus Hallo definiëren. Gebruiker kan ook een opgeslagen zoekopdracht markeren als hun standaard-zoekactie. Wanneer een gebruiker op Hallo 'Vergrootglas' zoekpictogram van hello Azure Data Catalog portal startpagina of van de pagina voor Hallo 'aan de slag', wordt Hallo gebruiker genomen rechtstreeks toohello opgeslagen zoekopdracht is gemarkeerd als standaard.
* Ondersteuning voor RTF-documentatie voor de geregistreerde gegevensassets en containers in hello Azure Data Catalog-portal. Gebruikers kunnen nu documentatie te verschaffen voor gegevensassets zoals tabellen, weergaven en rapporten en -containers zoals databases en -modellen voor scenario's waarbij labels en beschrijvingen niet voldoende zijn.
* Ondersteuning voor het handmatig registreren van bekende typen gegevensbronnen. Gebruikers kunnen de informatie van gegevensbron met behulp van hello Azure Data Catalog-portal voor alle typen gegevensbronnen ondersteund door Azure Data Catalog handmatig invoeren.
* Ondersteuning voor het machtigen van Azure Active Directory-beveiligingsgroepen. Catalogus-beheerders kunnen toegang toosecurity catalogusgroepen, gebruikersaccounts, waardoor het gemakkelijker toomanage toegang tooAzure Data Catalog inschakelen.
* Ondersteuning voor het openen van Hive-gegevensbronnen in Excel van hello Azure Data Catalog-portal.

> [!NOTE]
> Voor de huidige release Hallo wordt alleen Teradata TD2 verificatie ondersteund. Extra authenticatie mechanismen worden ondersteund in toekomstige versies.

> [!NOTE]
> toouse Hallo 'Openen in Excel' functie voor Hive-gegevensbronnen gebruikers moeten hebben geïnstalleerd Hallo ODBC-stuurprogramma voor Hive.

## <a name="whats-new-for-september-2015"></a>Wat is er nieuw voor September 2015
Vanaf September 2015 hebt Hallo volgende mogelijkheden toegevoegd tooAzure Data Catalog:

* Ondersteuning voor het opnemen van gegevens profielen bij het registreren van gegevensbronnen Hive.
* Ondersteuning voor het detecteren van programmatisch Hallo catalogus API, waardoor het gemakkelijker voor toointegrate toepassingen met Azure Data Catalog.
* Een nieuwe 'aan de slag' gegevensbron detectie ervaring in hello Azure Data Catalog-portal. Wanneer gebruikers Hallo "ontdekken" pagina van de hello Azure Data Catalog beheerportal invoeren zonder een zoekterm invoert, worden ze weergegeven met een overzicht van Hallo catalogus inhoud, inclusief de meestgebruikte Hallo labels, experts gegevensbrontypen en objecttypen.
* Ondersteuning voor het registreren en detectie van Azure SQL Data Warehouse-objecten en -databases. Zie voor meer informatie over Azure SQL Data Warehouse [SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
* Ondersteuning voor het registreren en detectie van SQL Server Analysis Services-modellen en SQL Server Reporting Services-servers als containers. Bij het registreren van SSAS en SSRS objecten maakt Azure Data Catalog een vermelding voor Hallo SSAS model en SSRS-server, en voor het Hallo-rapporten en andere objecten. Hallo-containers kunnen worden gedetecteerd en aangetekend met hello Azure Data Catalog-portal. Gebruikers kunnen ook zoeken en filteren Hallo-inhoud van een model of de server in toevoeging toosearching en de inhoud van catalogus Hallo Hallo filteren.
* Ondersteuning voor het registreren en het detecteren van SQL Server Analysis Services-objecten via HTTP/HTTPS. Gebruikers kunnen nu verbinding maken met een URL (zoals https://servername/olap/msmdpump.dll) in plaats van een servernaam tooSSAS-servers en kunnen u basisverificatie en anonieme verbindingen in toevoeging tooWindows verificatie gebruiken. Zie voor meer informatie over HTTP/HTTPS-verbindingen tooSSAS [HTTP-toegang configureren tooAnalysis Services](https://msdn.microsoft.com/library/gg492140.aspx).
* Ondersteuning voor de gegevensbronnen Hive in HDInsight. Gebruikers kunnen nu worden geregistreerd en het detecteren van Hive-tabellen voor Apache Hive in Hadoop op HDInsight-gegevensbronnen. Zie voor meer informatie over Hive in HDInsight hello [HDInsight-documentatiecentrum](../hdinsight/hdinsight-use-hive.md).
* Ondersteuning voor het registreren en Oracle-databases en clusters van HDFS als containers detecteren. Bij het registreren van Oracle-tabellen en weergaven of HDFS, wordt een vermelding voor het Hallo-database, tabellen en weergaven gemaakt in Azure Data Catalog. Hallo-database kan worden gedetecteerd en aangetekend met hello Azure Data Catalog-portal. Gebruikers kunnen ook zoeken en filteren Hallo inhoud van een database van de cluster of bovendien toosearching en inhoud van catalogus Hallo Hallo filteren.
* Ondersteuning voor onbekende typen gegevensbronnen handmatig registreren. Gebruikers kunnen handmatig invoeren voor gegevensbroninformatie hello Azure Data Catalog Portal gebruikt, zodat de gegevensbronnen niet expliciet worden ondersteund door Hallo hulpprogramma voor registratie van gegevensbronnen kan worden aangetekend en gedetecteerd.
* Ondersteuning voor het registreren en detectie van SQL Server-databases als containers. Bij het registreren van SQL Server-tabellen en weergaven, wordt een vermelding voor het Hallo-database, tabellen en weergaven gemaakt in Azure Data Catalog. Hallo-database kan worden gedetecteerd en aangetekend met hello Azure Data Catalog-portal. Gebruikers kunnen ook zoeken en filteren Hallo-inhoud van een database in toevoeging toosearching en inhoud van catalogus Hallo Hallo filteren.

> [!NOTE]
> SSAS en SSRS-objecten die ingeschreven voorafgaande toohello September 18 release zijn moeten opnieuw worden geregistreerd met hulpprogramma voor registratie van gegevensbronnen Hallo voordat hello model of de server is toegevoegd toohello catalogus. Opnieuw registreren van een gegevensbron heeft geen invloed op alle aantekeningen die zijn toegevoegd door gebruikers in hello Azure Data Catalog-portal.

> [!NOTE]
> Oracle-tabellen en weergaven en HDFS-bestanden en mappen die ingeschreven voorafgaande toohello 11 September release zijn moeten opnieuw worden geregistreerd met behulp van hulpprogramma voor registratie van gegevensbronnen Hallo voordat hello database of het cluster wordt toegevoegd toohello catalogus. Opnieuw registreren van een gegevensbron heeft geen invloed op alle aantekeningen die zijn toegevoegd door gebruikers in hello Azure Data Catalog-portal.

> [!NOTE]
> SQL Server-tabellen en weergaven die ingeschreven voorafgaande toohello 4 September release zijn moeten opnieuw worden geregistreerd met behulp van hulpprogramma voor registratie van gegevensbronnen Hallo voordat Hallo databasevermelding toohello catalogus is toegevoegd. Opnieuw registreren van een gegevensbron heeft geen invloed op alle aantekeningen die zijn toegevoegd door gebruikers in hello Azure Data Catalog-portal.

## <a name="whats-new-for-august-2015"></a>Wat is er nieuw voor augustus 2015
Vanaf augustus 2015 geldt zijn Hallo na mogelijkheden toegevoegd tooAzure Data Catalog:

* Ondersteuning voor profileren van gegevens van SQL Server en Oracle-gegevensbronnen. -Gebruikers kiezen tooinclude gegevens profielgegevens voor Hallo-objecten wordt geregistreerd bij het registreren van SQL Server en Oracle-tabellen en weergaven. Hallo gegevens profiel bevat statistieken op objectniveau en op kolomniveau.
* Ondersteuning voor Hadoop HDFS-gegevensbronnen. Gebruikers kunnen nu registreren en detecteren HDFS-bestanden en mappen.
* Ondersteuning voor het bieden van informatie van het toegangsverzoek voor geregistreerde gegevensbronnen. Gebruikers bieden nu instructies voor het aanvragen van toegang, waaronder e-koppelingen of URL's voor een geregistreerde gegevensasset, tooeasily integreren met bestaande hulpprogramma's en processen.
* Hulpprogramma voor tips voor labels en deskundigen, toomake deze eenvoudiger toodiscover wat gebruikers welke metagegevens voor geregistreerde gegevensassets hebt opgegeven.
* Een nieuwe 'Gebruiker' knop en het menu tooour navigatiebalk bovenaan toegevoegd. Dit menu krijgt Hallo gebruiker Hallo account gebruikt toolog op Data Catalog tooAzure en toosign uit indien gewenst. Dit menu ook de catalogusnaam hello, namelijk waardevolle toodevelopers weergegeven met behulp van REST-API van Azure Data Catalog Hallo.
* Standard-editie alleen: Bij het toevoegen van eigenaren toodata activa Azure Data Catalog ondersteunt nu de gebruikersaccounts en beveiligingsgroepen als eigenaars. een beveiligingsgroep als eigenaar van de geselecteerde gegevensassets tooadd, kunt u de weergavenaam van de groep van beide Hallo of van de groep Hallo UPN e-mailadres, indien van toepassing.
* Ondersteuning voor Azure Blob Storage-gegevensbronnen. Gebruikers kunnen nu registreren en Azure Storage-blobs en mappen te detecteren.

