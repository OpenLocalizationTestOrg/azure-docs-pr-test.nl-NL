---
title: aaaImport gegevens in Azure Search in de portal Hallo | Microsoft Docs
description: Gebruik Hallo Wizard importeren Azure Search in hello Azure Portal toocrawl Azure gegevens uit NoSQL Azure Cosmos DB, Blob storage, table storage, SQL-Database en SQL Server op Azure Virtual machines.
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: Azure Portal
ms.assetid: f40fe07a-0536-485d-8dfa-8226eb72e2cd
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 00b0e59594560c0cdaea748df196518e9fba3834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-tooazure-search-using-hello-portal"></a>Importeren van gegevens tooAzure zoeken met behulp van Hallo-portal
Hello Azure portal biedt een **gegevens importeren** wizard op Hallo Azure Search-dashboard voor het laden van gegevens in een index. 

  ![Gegevens importeren op de opdrachtbalk Hallo][1]

Intern Hallo wizard configureert en roept een *indexeerfunctie*, verschillende stappen Hallo indexeren proces automatiseren: 

* Verbinding maken met de externe gegevensbron tooan in Hallo hetzelfde Azure-abonnement
* Een bewerkbaar indexschema dat is gebaseerd op Hallo bron gegevensstructuur genereren
* JSON-documenten in een index met behulp van een rijenset die is opgehaald uit de gegevensbron Hallo laden

U kunt deze werkstroom met voorbeeldgegevens uitproberen in Azure Cosmos DB. Ga naar [aan de slag met Azure Search in Azure Portal Hallo](search-get-started-portal.md) voor instructies.

> [!NOTE]
> U kunt starten Hallo **gegevens importeren** wizard van hello Azure Cosmos DB dashboard toosimplify voor de gegevensbron te indexeren. In de navigatie aan de linkerkant, gaat u te**verzamelingen** > **toevoegen Azure Search** tooget gestart.

## <a name="data-sources-supported-by-hello-import-data-wizard"></a>Gegevensbronnen die worden ondersteund door Hallo Wizard gegevens importeren
de wizard gegevens importeren Hallo ondersteunt Hallo gegevensbronnen te volgen: 

* Azure SQL Database
* Relationele SQL Server-gegevens op een virtuele machine van Azure
* Azure Cosmos DB
* Azure Blob Storage
* Azure Table Storage

Een platte gegevensset is een vereiste invoer. U kunt slechts importeren uit één tabel, databaseweergave of gelijkwaardige gegevensstructuur. Voordat u Hallo-wizard uitvoert, moet u deze gegevensstructuur maken.

## <a name="connect-tooyour-data"></a>Verbinding maken met tooyour gegevens
1. Meld u aan toohello [Azure-portal](https://portal.azure.com) en open Hallo servicedashboard. U kunt klikken op **meer services** in Hallo jump balk toosearch voor bestaande 'zoekservices' in het huidige abonnement Hallo. 
2. Klik op **importgegevens** op Hallo opdrachtbalk blade tooslide open Hallo-gegevens importeren.  
3. Klik op **tooyour gegevens verbinding** toospecify een gegevensbrondefinitie die wordt gebruikt door een indexeerfunctie. Voor gegevensbronnen intra-abonnement, Hallo wizard meestal detecteert en lezen verbindingsinformatie, de algehele configuratievereisten voor het minimaliseren.

|  |  |
| --- | --- |
| **Bestaande gegevensbron** |Als u al indexeerfuncties hebt gedefinieerd in uw zoekservice, kunt u een bestaande gegevensbrondefinitie voor een andere import selecteren. |
| **Azure SQL Database** |Servicenaam, referenties voor een databasegebruiker met leesmachtiging en de naam van een database kan worden opgegeven op de pagina Hallo of via een ADO.NET-verbindingsreeks. Kies Hallo connection string optie tooview of aanpassen van eigenschappen. <br/><br/>Hallo tabel of weergave waarmee Hallo rijenset moet worden opgegeven op de pagina Hallo. Deze optie wordt weergegeven nadat Hallo verbinding slaagt, geeft een vervolgkeuzelijst zodat u een selectie kunt maken. |
| **SQL Server op virtuele Azure-machine** |Geef een FQDN-servicenaam, gebruikers-ID en wachtwoord en de database als een verbindingsreeks op. toouse deze gegevensbron, u moet eerder geïnstalleerd een certificaat in Hallo lokale archief die Hallo-verbinding versleutelt. Zie voor instructies [SQL VM verbinding tooAzure Search](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md). <br/><br/>Hallo tabel of weergave waarmee Hallo rijenset moet worden opgegeven op de pagina Hallo. Deze optie wordt weergegeven nadat Hallo verbinding slaagt, geeft een vervolgkeuzelijst zodat u een selectie kunt maken. |
| **Azure Cosmos DB** |Hallo-account, database en verzameling onder meer. Alle documenten in de verzameling Hallo worden opgenomen in het Hallo-index. U kunt een query-tooflatten definiëren of Hallo rijenset filteren of toodetect gewijzigd documenten voor latere vernieuwingsbewerkingen uitvoeren. |
| **Azure Blob Storage** |Deze vereisten zijn Hallo storage-account en een container. Als blob-namen virtuele naamconventie voor groepering doeleinden volgt, kunt u eventueel Hallo virtuele map deel van naam Hallo opgeven als een map onder de container. Zie [Blob Storage indexeren](search-howto-indexing-azure-blob-storage.md) voor meer informatie. |
| **Azure-tabelopslag** |Deze vereisten zijn Hallo storage-account en een tabelnaam. U kunt eventueel een query tooretrieve een subset van Hallo tabellen opgeven. Zie [Table Storage indexeren](search-howto-indexing-azure-tables.md) voor meer informatie. |

## <a name="customize-target-index"></a>Doelindex aanpassen
Een voorlopige index is doorgaans afgeleid van Hallo gegevensset. Toevoegen, bewerken of verwijderen van velden toocomplete Hallo schema. Bovendien kenmerken instellen op Hallo veld niveau toodetermine de daaropvolgende zoekgedrag.

1. In **doelindex aanpassen**, geef Hallo naam en een **sleutel** gebruikte toouniquely elk document identificeren. Hallo sleutel moet een tekenreeks zijn. Als veldwaarden spaties of streepjes bevatten worden zeker tooset geavanceerde opties in **uw gegevens importeren** toosuppress Hallo validatiecontrole voor deze tekens bevatten.
2. Bekijk en herzien Hallo resterende velden. De veldnaam en het veldtype worden doorgaans automatisch ingevuld. U kunt Hallo gegevenstype wijzigen totdat Hallo index is gemaakt. Als u het daarna nog verandert, moet het opnieuw worden opgebouwd.
3. Stel indexkenmerken in voor elk veld:
   
   * Ophalen mogelijk wordt Hallo veld in de zoekresultaten.
   * Met Filterbaar kunt Hallo veld toobe waarnaar wordt verwezen in filterexpressies.
   * Sorteerbaar kan Hallo veld toobe gebruikt in een sortering.
   * Geschikt voor facetten kan Hallo veld voor meervoudige navigatie.
   * Met Doorzoekbaar kunt u in het veld zoeken in volledige tekst.
4. Klik op Hallo **Analyzer** tabblad als u wilt dat een taalanalyse op veldniveau Hallo toospecify. Op dit moment kunnen alleen taalanalysefuncties worden opgegeven. Voor het gebruik van een aangepaste analysefunctie of een niet-taal-analysefunctie zoals sleutelwoord, patroon, enzovoort is code vereist.
   
   * Klik op **doorzoekbaar** toodesignate volledige tekst zoeken op Hallo veld en Hallo Analyzer vervolgkeuzelijst lijst inschakelt.
   * Hallo analyzer die u wilt kiezen. Zie [Een index voor documenten in meerdere talen maken](search-language-support.md) voor meer informatie.
5. Klik op Hallo **suggestie** tooenable automatisch aangevulde Querysuggesties op geselecteerde velden.

## <a name="import-your-data"></a>Uw gegevens importeren
1. In **uw gegevens importeren**, Geef een naam op voor de indexeerfunctie Hallo. Intrekken van dat product Hallo Hallo gegevens importeren wordt de wizard een indexeerfunctie. Later, als u wilt dat tooview of te bewerken, selecteert u deze van Hallo portal in plaats van door opnieuw uit te voeren Hallo-wizard. 
2. Geef de planning hello, die is gebaseerd op Hallo regionale tijdzone waarin Hallo-service is ingericht.
3. Geavanceerde opties toospecify drempelwaarden instellen op of verkennen kan worden voortgezet als een document wordt verwijderd. Bovendien kunt u opgeven of **sleutel** velden toocontain spaties en slashes zijn toegestaan.  
4. Klik op **OK** toocreate Hallo index en Hallo gegevens importeren.

U kunt controleren in Hallo-portal te indexeren. Wanneer deze documenten zijn geladen, worden Hallo document aantal zal toenemen voor Hallo-index die u hebt gedefinieerd. Soms duurt het enkele minuten duren voordat Hallo portalpagina toopick van de meest recente updates Hallo.

Hallo-index is gereed tooquery zodra alle Hallo documenten zijn geladen.

## <a name="query-an-index-using-search-explorer"></a>Gegevens uit een index opvragen met Search Explorer

Hallo portal bevat **Search Explorer** zodat u kunt een index een query zonder toowrite code. U kunt [Search Explorer](search-explorer.md) op elke index toepassen.

Hallo zoekervaring is op basis van standaardinstellingen, zoals Hallo [eenvoudige syntaxis](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) en standaardinstellingen [searchMode queryparameter (https://docs.microsoft.com/rest/api/searchservice/search-documents). 

Resultaten worden geretourneerd in JSON, een uitgebreide indeling zodat u kunt het hele document Hallo inspecteren.

## <a name="edit-an-existing-indexer"></a>Een bestaande indexeerfunctie bewerken
Zoals vermeld, wizard importeren Hallo maakt een **indexeerfunctie**, die u kunt wijzigen als een zelfstandige construct in Hallo-portal.

Dubbelklik in het servicedashboard Hallo op Hallo indexeerfunctie tegel tooslide uit een lijst met alle indexeerfuncties voor uw abonnement. Dubbelklik op een van de Hallo indexeerfuncties toorun, bewerken of verwijderen. U kunt Hallo index vervangen door een andere bestaande gegevensbron Hallo wijzigen en opties instellen voor drempelwaarden fout tijdens het indexeren.

## <a name="edit-an-existing-index"></a>Een bestaande index bewerken
Hallo-wizard ook gemaakt een **index**. In de Azure Search vereist structurele updates tooan index opnieuw opbouwen van die index. Opnieuw opbouwen houdt verwijderen Hallo-index, Hallo index met behulp van een herziene schema met de gewenste wijzigingen aan Hallo en laden van gegevens opnieuw te maken. Structurele updates zijn onder andere het wijzigen van een gegevenstype en het wijzigen van de naam of verwijderen van een veld.

Bewerkingen waarvoor de index niet opnieuw hoeft te worden gemaakt, zijn onder andere het toevoegen van een nieuw veld, wijzigen van scoringsprofielen, wijziging van de suggestiefunctie en wijzigen van de taalanalysefunctie. Zie [Update Index](https://msdn.microsoft.com/library/azure/dn800964.aspx) (Index bijwerken) voor meer informatie.


## <a name="next-steps"></a>Volgende stappen
Deze koppelingen toolearn meer over indexeerfuncties bekijken:

* [Azure SQL Database indexeren](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB indexeren](search-howto-index-documentdb.md)
* [Blob Storage indexeren](search-howto-indexing-azure-blob-storage.md)
* [Table Storage indexeren](search-howto-indexing-azure-tables.md)

<!--Image references-->
[1]: ./media/search-import-data-portal/search-import-data-command.png

