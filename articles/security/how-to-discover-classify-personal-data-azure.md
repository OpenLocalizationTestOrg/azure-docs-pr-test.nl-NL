---
title: aaaDiscover, identificeren en classificeren van persoonlijke gegevens in Microsoft Azure | Microsoft Docs
description: "Meer informatie over het zoeken, classificeren, detecteren en gegevens worden geïdentificeerd"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: af4ced1c57699dc751d55cfdf3229c7d294648a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="discover-identify-and-classify-personal-data-in-microsoft-azure"></a>Detecteren, identificeren en classificeren van persoonlijke gegevens in Microsoft Azure

In dit artikel biedt richtlijnen voor hoe toodiscover, identificeren en classificeren van persoonlijke gegevens in verschillende Azure-hulpprogramma's en services, inclusief het gebruik van Azure Data Catalog, Azure Active Directory, SQL-Database, Power Query voor Hadoop-clusters in Azure HDInsight, Azure Gegevensbeveiliging, Azure Search en SQL-query's voor Azure Cosmos DB.

## <a name="scenario-problem-statement-and-goal"></a>Scenario, Probleemstelling en doelstellingen

Een bedrijf VS gebaseerde Sport verzamelt tal van privégegevens en andere gegevens. Dit omvat klanten en werknemersgegevens. Hallo bedrijf blijft in meerdere databases en slaat ze op in verschillende plaatsen in de Azure-omgeving. Bovendien tooselling apparatuur sport, ze ook hosten en beheren van de registratie voor bijzondere Sport gebeurtenissen rond Hallo wereld, waaronder in Hallo EU, en in sommige gevallen Hallo klantgegevens die zij verzamelen medische informatie bevat.

Omdat Hallo bedrijf als host fungeert voor veel internationale bicycling rondleidingen jaarlijks en tijdelijk personeel in locaties hele Hallo wereld heeft, wordt een aantal Hallo gegevenssets behoorlijk groot zijn. Hallo bedrijf heeft ook developer gebouwd toepassingen die worden gebruikt door klanten en werknemers.

Hallo bedrijf wil tooaddress Hallo problemen te volgen:

- Klanten en werknemers persoonlijke gegevens moeten worden geclassificeerd/onderscheiden van Hallo andere gegevens Hallo bedrijf verzamelt gegevens in de juiste volgorde tooensure-toegang en beveiliging.
- Hallo beheerder gegevens moet tooeasily Hallo-locatie van de klant persoonlijke gegevens op verschillende gebieden van hello Azure-omgeving detecteren.
- Klanten en werknemers persoonlijke gegevens die wordt weergegeven in gedeelde documenten en e-mailberichten moeten worden gemarkeerd toohelp ervoor te zorgen dat deze wordt beveiligd.
- app-ontwikkelaars van het bedrijf Hallo moeten een manier tooeasily zoekopdracht voor klanten en werknemers persoonlijke gegevens in de web- en mobiele apps.
- Ontwikkelaars moeten ook tooquery hun documentdatabase voor persoonlijke gegevens.

### <a name="company-goals"></a>Bedrijfsdoelstellingen

- Alle klanten en werknemers persoonlijke gegevens moet gelabeld/aangetekend in Azure Data Catalog kunnen eenvoudig worden gevonden. In het ideale geval zijn klanten en werknemers persoonlijke gegevens gelabeld/aangetekend afzonderlijk.
- Persoonlijke gegevens van klanten en werknemers gebruikersprofielen en werkgegevens die zich in Azure Active Directory moet eenvoudig bevindt.
- Persoonlijke gegevens die zich in meerdere SQL-databases moet gemakkelijk worden opgevraagd. 
- Enkele van de grote gegevenssets van Hallo bedrijf worden beheerd via Azure HDInsight en opgeslagen in Hadoop. Ze moeten worden geïmporteerd in Excel zodat ze kunnen worden opgevraagd voor persoonlijke gegevens.
- Persoonlijke gegevens die worden gedeeld in documenten en e-mailberichten moeten worden geclassificeerd met het label en beveiligd met Azure Information Protection.
- Hallo moet van bedrijf app-ontwikkelaars kunnen toodiscover klanten en werknemers persoonlijke gegevens in deze hebt gemaakt, Hallo-apps die ze met Azure Search doen kunnen.
- Ontwikkelaars moet kunnen toofind persoonlijke gegevens in het documentdatabase.

## <a name="azure-active-directory-data-discovery"></a>Azure Active Directory: Gegevens te zoeken

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) van Microsoft cloud-gebaseerde, multitenant directory en identity management-service is. U kunt vinden, klanten en werknemers gebruikersprofielen en gebruikersgegevens werk die persoonlijke gegevens bevatten in uw [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD)-omgeving met behulp van Hallo [Azure-portal](https://portal.azure.com/).

Dit is vooral handig als u wilt dat toofind of persoonlijke gegevens voor een specifieke gebruiker wijzigen. U kunt ook toevoegen of wijzigen van gebruikersprofiel en werkgegevens. U moet zich aanmelden met een account met globale beheerdersrechten voor Hallo-directory.

### <a name="how-do-i-locate-or-view-user-profile-and-work-information"></a>Hoe zoeken of gebruikersprofiel weergeven ik informatie over en?

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.

2. Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.

   ![hoe ik gebruikersprofiel kunnen vinden en werkgegevens](media/how-to-discover-classify-personal-data-azure/user-profile.png)

3. Op Hallo **gebruikers en groepen** blade Selecteer **gebruikers**.

  ![Openen gebruikers en groepen](media/how-to-discover-classify-personal-data-azure/users-groups.png)

4. Op Hallo **gebruikers en groepen - gebruikers** blade, selecteer een gebruiker in de lijst Hallo en selecteer vervolgens het volgende op de blade voor de geselecteerde gebruiker Hallo Hallo **profiel** tooview gebruikersprofielgegevens die mogelijk persoonlijke gegevens bevatten .

  ![gebruiker selecteren](media/how-to-discover-classify-personal-data-azure/select-user.png)

5. Als u tooadd moet of gebruikersprofielgegevens wijzigt, kunt u doen en selecteer vervolgens in de opdrachtbalk Hallo **opslaan.**
6. Selecteer op de blade voor de geselecteerde gebruiker Hallo Hallo **Info werken** tooview werk gebruikersgegevens die mogelijk persoonlijke gegevens bevatten.

 ![werkgegevens weergeven](media/how-to-discover-classify-personal-data-azure/work-info.png)

7. Als u tooadd moet of werk gebruikersinformatie kunt wijzigen, kunt u doen en selecteer vervolgens in de opdrachtbalk Hallo **opslaan.**

## <a name="azure-sql-database-data-discovery"></a>Azure SQL Database: Gegevens te zoeken

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is een cloud-database die kan softwareontwikkelaars maken en onderhouden van toepassingen. Persoonlijke gegevens vindt u in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) met behulp van de standaard SQL-query's. Azure SQL-elastische query (preview) kan gebruikers tooperform cross-databasequery's.

Een gedetailleerde [SQL-database](../sql-database/sql-database-technical-overview.md) zelfstudie wordt uitgelegd hoe veel aspecten van het gebruik van een SQL-database, inclusief hoe toobuild een en hoe toorun query's. Hallo Hieronder volgt een samenvatting van Hallo-informatie beschikbaar is in de zelfstudie Hallo met koppelingen toospecific secties.

### <a name="how-do-i-build-a-sql-database"></a>Hoe maak ik een SQL-database

Er zijn drie manieren toodo het:

- Een Azure SQL database kan worden gemaakt in Hallo [Azure-portal](https://portal.azure.com/). In de zelfstudie hello gebruikt u een specifieke set berekenings- en bronnen binnen een resourcegroep en de logische server. Gebruikt u voorbeeldgegevens van een fictieve bedrijf AdventureWorks. U hebt ook een firewallregel op serverniveau maken. toolearn hoe toodo deze, gaat u naar Hallo [maken van een Azure SQL database in Azure-portal Hallo](../sql-database/sql-database-get-started-portal.md) zelfstudie.

  ![Azure SQL-Database maken](media/how-to-discover-classify-personal-data-azure/create-database.png)
- Een SQL-database kan ook worden gemaakt in Hallo [Azure Cloud Shell](https://azure.microsoft.com/features/cloud-shell/) CLI, een opdrachtregelprogramma op basis van een browser. Hallo-hulpprogramma is beschikbaar in hello Azure-portal en rechtstreeks van daaruit kan worden uitgevoerd. In deze zelfstudie maakt u Hallo hulpprogramma starten, scriptvariabelen definiëren, een resourcegroep en de logische server maken en een serverfirewallregel configureren. Vervolgens maakt u een database met voorbeeldgegevens. toolearn hoe toocreate uw database op deze manier gaat u naar Hallo [maken van één Azure SQL database met behulp van Azure CLI Hallo](../sql-database/sql-database-get-started-cli.md) zelfstudie.

  ![CLIT-zelfstudie](media/how-to-discover-classify-personal-data-azure/cli-tutorial.png)

>[!NOTE]
Azure CLI wordt doorgaans gebruikt door de Linux-beheerders en ontwikkelaars. Sommige gebruikers vinden het gemakkelijker en intuïtievere dan PowerShell, die is uw derde optie.

- Ten slotte kunt u een SQL-database met behulp van PowerShell, dit een hulpprogramma dat wordt gebruikt vanaf de opdrachtregel/script toocreate is maken en beheren van Azure en andere bronnen. In deze zelfstudie maakt u Hallo hulpprogramma starten, scriptvariabelen definiëren, een resourcegroep en de logische server maken en een serverfirewallregel configureren. Vervolgens maakt u een database met voorbeeldgegevens.

Hallo-zelfstudie vereist hello Azure PowerShell-moduleversie 4.0 of hoger. Voer Get-Module - ListAvailable AzureRM toofind uw versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u Installeer Azure PowerShell-module.

```PowerShell
New-AzureRmSQLDatabase -ResourceGroupName $resourcegroupname `
-ServerName $servername `
-DatabaseName $databasename `
-RequestedServiceObjectiveName "s0"
```

toolearn hoe toocreate uw database op deze manier gaat u naar Hallo [maken van één Azure SQL database met behulp van Powershell](../sql-database/sql-database-get-started-powershell.md) zelfstudie.

>[!Note]
Windows-beheerders hebben vaak toouse PowerShell, maar sommige van deze Azure CLI geven de voorkeur.

### <a name="how-do-i-search-for-personal-data-in-sql-database-in-hello-azure-portal"></a>Hoe kan ik zoeken voor persoonlijke gegevens in SQL-database in Azure-portal Hallo? **

U kunt hulpprogramma voor Hallo ingebouwde query-editor in Azure portal toosearch hello gebruiken voor persoonlijke gegevens. U Meld u bij toohello hulpprogramma met uw aanmelding voor SQL server-beheerder en het wachtwoord en voer vervolgens een query.

  ![sql via Hallo portal zoeken](media/how-to-discover-classify-personal-data-azure/search-sql-portal.png)

Stap 5 van Hallo zelfstudie ziet u een voorbeeldquery in Hallo editor Querydeelvenster, maar deze niet ligt de nadruk op persoonlijke of gevoelige gegevens (ook gegevens combineert uit twee tabellen en aliassen voor bronkolom Hallo maakt in Hallo-gegevensset wordt geretourneerd). Hallo volgende schermafbeelding ziet Hallo-query uit stap 5, evenals Hallo deelvenster met resultaten die wordt geretourneerd:

  ![queryeditor](media/how-to-discover-classify-personal-data-azure/query-editor.png)

Als uw database MyTable aangeroepen is, wordt een voorbeeldquery voor persoonlijke gegevens bevatten mogelijk naam, sofi-nummer en id-nummer en eruit als volgt:

"Selecteer naam, sofi-nummer, id-nummer van MijnTabel"

Zou Hallo-query uit te voeren en vervolgens ziet Hallo resulteert in een Hallo **resultaten** deelvenster.

Voor meer informatie over hoe tooquery een SQL-database in hello Azure-portal, gaat u naar Hallo [Query Hallo SQL-database](../sql-database/sql-database-get-started-portal.md) gedeelte van de zelfstudie Hallo.

### <a name="how-do-i-search-for-data-across-multiple-databases"></a>Hoe kan ik zoeken voor gegevens over meerdere databases?

Elastische SQL-query (preview) kunt u tooperform cross-database en meerdere databasequery's en retourneren een enkelvoudig resultaat wordt verkregen. Hallo [overzicht van de zelfstudie](../sql-database/sql-database-elastic-query-overview.md) bevat een gedetailleerde beschrijving van scenario's en wordt uitgelegd Hallo verschil tussen het partitioneren van de verticale en horizontale database. Horizontale partitioneren, heet 'sharding'.

  ![Verticale partities](media/how-to-discover-classify-personal-data-azure/vertical-partition.png)

  ![horizontale partitioneren](media/how-to-discover-classify-personal-data-azure/horizontal.png)

tooget gestart, gaat u naar Hallo [elastische query overzicht van Azure SQL Database (preview)](../sql-database/sql-database-elastic-query-overview.md) pagina.

#### <a name="power-query-for-importing-azure-hdinsight-hadoop-clusters-data-discovery-for-large-data-sets"></a>Power Query (voor het importeren van Azure HDInsight Hadoop-clusters): gegevens detectie voor grote gegevenssets

Hadoop is een open-source Apache opslag en verwerking service voor grote gegevenssets die worden geanalyseerd en opgeslagen in de Hadoop-clusters. [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) kunnen gebruikers toowork met Hadoop-clusters in Azure. Power Query is een Excel-invoegtoepassing die, onder andere helpt gebruikers gegevens uit verschillende bronnen detecteren.

Persoonlijke gegevens die zijn gekoppeld aan de Hadoop-clusters in Azure HDInsight worden geïmporteerde tooExcel met Power Query. Als Hallo gegevens zich bevinden in Excel kunt u een query tooidentify deze.

#### <a name="how-do-i-use-excel-power-query-tooimport-hadoop-clusters-in-azure-hdinsight-into-excel"></a>Hoe gebruik ik Power Query voor Excel tooimport Hadoop-clusters in Azure HDInsight in Excel

Een zelfstudie voor HDInsight begeleidt u door deze hele proces. Deze vereisten wordt uitgelegd en bevat een koppeling tooa [aan de slag met Azure HDInsight](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) zelfstudie. Instructies behandelen Excel 2016 evenals 2010 en 2013 (stappen zijn enigszins verschillen voor oudere versies van Excel Hallo). Als u geen Hallo Power Query voor Excel-invoegtoepassing, Hallo zelfstudie laat zien u hoe tooget deze. U Hallo zelfstudie beginnen in Excel en moet toohave een Azure Blob storage-account die is gekoppeld aan het cluster.

  ![De query in Excel](media/how-to-discover-classify-personal-data-azure/excel.png)

toolearn hoe toodo deze, gaat u naar Hallo [tooHadoop Excel verbinding maken met Power Query](../hdinsight/hdinsight-connect-excel-power-query.md) zelfstudie.

Bron: [tooHadoop Excel verbinden met Power Query](../hdinsight/hdinsight-connect-excel-power-query.md)

## <a name="azure-information-protection-personal-data-classification-for-documents-and-email"></a>Azure Information Protection: persoonsgegevens classificatie van documenten en e-mailadres

[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) kunt Azure-klanten labels tooclassify toepassen en beveiligen intern of extern gedeelde documenten en e-communicatie. Sommige van deze items kan de klant of werknemer persoonlijke gegevens bevatten. Regels en voorwaarden kunnen worden gedefinieerd automatisch of handmatig, door beheerders of gebruikers. Bijvoorbeeld, als een gebruiker een document met creditcardgegevens opslaat is, ziet hij of zij een label aanbeveling die is geconfigureerd door Hallo beheerder.

### <a name="how-do-i-try-it"></a>Hoe ik het proberen?

Als u toogive Azure Information Protection een try-toosee wilt als mogelijk een geschikt is voor uw organisatie, gaat u naar Hallo [Quick Start-zelfstudie](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial). Deze doorloopt u vijf eenvoudige stappen: van installatie tooconfiguring beleid tooseeing classificatie, labels en delen in actie: en minder dan een half uur duren.

### <a name="how-do-i-deploy-it"></a>Hoe kan ik het implementeren?

Als u toodeploy Azure Information Protection voor uw organisatie wilt, gaat u naar Hallo [implementatieschema voor classificatie, labels en beveiliging](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap).

### <a name="is-there-anything-else-i-should-know"></a>Is er iets anders die ik moet weten?

Voor aanvullende informatie waarmee u bedenken hoe tooset deze, gaat u naar Hallo [gereed, stel kunt beveiligen.](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
blogbericht. En controleer Hallo Leer meer koppelingen hieronder voor meer informatie over Azure Information Protection.

## <a name="azure-search-data-discovery-for-developer-apps"></a>Azure Search: detectie van gegevens voor ontwikkelaars apps

[Azure Search](https://azure.microsoft.com/services/search/) is een zoekopdracht cloudoplossing voor ontwikkelaars en biedt een uitgebreide gegevens zoekfunctie voor uw toepassingen. Azure Search kunt u toolocate gegevens over de gebruiker gedefinieerde indexen, afkomstig van Azure Cosmo DB, Azure SQL Database, Azure Blob Storage, Azure Table storage of aangepaste klant JSON-gegevens. U kunt ook Lucene-query's met hello Azure Search REST API toosearch voor persoonlijke gegevenstypen of persoonlijke gegevens van specifieke personen Hallo structuur. Functies omvatten zoeken in volledige tekst, vereenvoudigde querysyntaxis en Lucene-querysyntaxis. 

## <a name="how-do-i-use-sql-tooquery-data"></a>Hoe gebruik ik SQL tooquery gegevens?

toobegin met Hallo basisprincipes, gaat u naar Hallo [Azure CosmosD DB: hoe tooquery met behulp van SQL](../cosmos-db/tutorial-query-documentdb.md) zelfstudie. Hallo-zelfstudie biedt een voorbeelddocument en twee voorbeeld SQL-query's en resultaten.

Voor meer gedetailleerde informatie over het bouwen van de SQL-query's, gaat u naar [SQL-query's voor Azure Cosmos DB Document DB API.](../cosmos-db/documentdb-sql-query.md)

Als u nieuwe tooAzure Cosmos DB en zou zoals toolearn hoe toocreate een database, een verzameling toevoegen en het toevoegen van gegevens, gaat u naar Hallo [Azure Cosmos DB: een DocumentDB-API-web-app bouwen](../cosmos-db/create-documentdb-dotnet.md) Quick Start-zelfstudie. Als u wilt toodo dit op een andere taal dan .NET, zoals Java of Python, kiest uw voorkeurstaal u eenmaal toohello site.

## <a name="next-steps"></a>Volgende stappen

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)

[Wat is SQL Database?](../sql-database/sql-database-technical-overview.md)

[SQL Database Query-Editor in Azure-portal beschikbaar] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)

[Wat is Azure Information Protection?](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection)

[Wat is Azure Rights Management?](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

[Azure Information Protection: Ready, instellen, beveiligen!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
