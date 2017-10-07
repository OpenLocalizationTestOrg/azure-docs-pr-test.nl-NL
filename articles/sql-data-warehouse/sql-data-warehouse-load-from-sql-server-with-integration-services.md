---
title: aaaLoad gegevens uit SQL Server in Azure SQL Data Warehouse (SSIS) | Microsoft Docs
description: Ziet u hoe toocreate SQL Server Integration Services (SSIS) toomove pakketgegevens uit een scala aan gegevensbronnen tooSQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: bb28a08807a5b07832b85f2f074c2acf912c1dc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a>Laden van gegevens uit SQL Server in Azure SQL Data Warehouse (SSIS)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

SQL Server Integration Services (SSIS) tooload pakketgegevens van SQL Server maken in Azure SQL Data Warehouse. U kunt eventueel herstructureren, transformeren en opschonen Hallo gegevens als het Hallo SSIS-gegevensstroom passeert.

In deze zelfstudie leert u het volgende:

* Maak een nieuwe Integration Services-project in Visual Studio.
* Verbinding maken met toodata bronnen, met inbegrip van SQL Server (als een bron) en SQL Data Warehouse (als doel).
* Ontwerp een SSIS-pakket dat gegevens worden geladen van bron Hallo in Hallo bestemming.
* Hallo SSIS tooload Hallo Pakketgegevens worden uitgevoerd.

Deze zelfstudie gebruikt SQL Server als Hallo-gegevensbron. SQL Server kan on-premises of in Azure een virtuele machine worden uitgevoerd.

## <a name="basic-concepts"></a>Basisconcepten
Hallo-pakket is Hallo werkeenheid in SSIS. Verwante pakketten worden gegroepeerd in projecten. U maken projecten en ontwerp pakketten in Visual Studio met SQL Server Data Tools. Hallo-ontwerp proces is een visual proces waarin u slepen en neerzetten van onderdelen van Hallo werkset toohello ontwerpoppervlak ze verbinding maken en hun eigenschappen instellen. Nadat u het pakket, kunt u eventueel implementeren tooSQL Server voor uitgebreide beheer, bewaking en beveiliging.

## <a name="options-for-loading-data-with-ssis"></a>Opties voor het laden van gegevens met SSIS
SQL Server Integration Services (SSIS) is een flexibele set hulpprogramma's waarmee een groot aantal opties voor verbinding met en gegevens in SQL Data Warehouse te laden.

1. Gebruik een ADO NET bestemming tooconnect tooSQL Data Warehouse. Deze zelfstudie wordt een ADO NET doel omdat het minste aantal configuratieopties Hallo heeft.
2. Gebruik een OLE DB-bestemming tooconnect tooSQL Data Warehouse. Deze optie kan enigszins betere prestaties dan Hallo ADO NET bestemming bieden.
3. Hello Azure Blob uploaden taak toostage Hallo gegevens in Azure Blob Storage gebruiken. Gebruik vervolgens Hallo SQL uitvoeren van SSIS taak toolaunch een Polybase-script dat Hallo gegevens in SQL Data Warehouse laadt. Deze optie biedt de beste prestaties Hallo van Hallo drie opties die hier worden vermeld. tooget hello Azure Blob uploaden taak downloaden Hallo [Microsoft SQL Server 2016 Integration Services Feature Pack voor Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]. toolearn meer informatie over Polybase, Zie [PolyBase-handleiding][PolyBase Guide].

## <a name="before-you-start"></a>Voordat u begint
toostep voor deze zelfstudie hebt u nodig:

1. **SQL Server integratieservices (SSIS)**. SSIS is een onderdeel van SQL Server en een evaluatieversie of een gelicentieerde versie van SQL Server vereist. Zie voor een evaluatieversie van SQL Server 2016 Preview tooget [SQL Server-evaluaties][SQL Server Evaluations].
2. **Visual Studio**. tooget Hallo gratis Visual Studio Community Edition, Zie [Visual Studio Community][Visual Studio Community].
3. **SQL Server Data Tools voor Visual Studio (SSDT)**. tooget SQL Server Data Tools voor Visual Studio, Zie [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].
4. **Voorbeeldgegevens**. Deze zelfstudie wordt opgeslagen in SQL Server in de AdventureWorks voorbeelddatabase Hallo het Hallo bron gegevens toobe geladen in SQL Data Warehouse voorbeeldgegevens. Zie tooget Hallo AdventureWorks-voorbeelddatabase [AdventureWorks 2014 voorbeeld Databases][AdventureWorks 2014 Sample Databases].
5. **Een SQL Data Warehouse-database en machtigingen**. Deze zelfstudie verbindt tooa SQL Data Warehouse-exemplaar en gegevens worden geladen in de App. U hebt een tabel en tooload data toohave machtigingen toocreate.
6. **Een firewallregel**. U hebt toocreate een firewallregel op SQL Data Warehouse met Hallo IP-adres van uw lokale computer voordat u gegevens toohello SQL Data Warehouse kunt uploaden.

## <a name="step-1-create-a-new-integration-services-project"></a>Stap 1: Maak een nieuw project voor de Integration Services
1. Visual Studio starten.
2. Op Hallo **bestand** selecteert u **nieuw | Project**.
3. Navigeer toohello **geïnstalleerde | Sjablonen | Business Intelligence | Integratieservices** projecttypen.
4. Selecteer **Integration Services-Project**. Waarden opgeven voor **naam** en **locatie**, en selecteer vervolgens **OK**.

Visual Studio wordt geopend en wordt een nieuw project voor de Integration Services (SSIS) gemaakt. Visual Studio wordt geopend Hallo ontwerpfunctie voor Hallo één nieuwe SSIS-pakket (Package.dtsx) in Hallo-project. U ziet Hallo schermgebieden te volgen:

* Aan de linkerkant Hallo Hallo **werkset** van SSIS-onderdelen.
* Hallo ontwerpoppervlak met meerdere tabbladen in het Hallo-midden. Doorgaans gebruikt u ten minste Hallo **controlestroom** en Hallo **gegevensstroom** tabbladen.
* Op de juiste hello, Hallo **Solution Explorer** en Hallo **eigenschappen** deelvensters.
  
    ![][01]

## <a name="step-2-create-hello-basic-data-flow"></a>Stap 2: Basic Hallo-gegevensstroom maken
1. Sleep een taak gegevens stromen van Hallo werkset toohello midden van het ontwerpoppervlak hello (op Hallo **controlestroom** tabblad).
   
    ![][02]
2. Dubbelklik op Hallo gegevens stromen tooswitch toohello gegevensstroom tabblad taak.
3. Hallo lijst van de andere bronnen in Hallo werkset, Sleep een ADO.NET bron toohello-ontwerpoppervlak. Met de Hallo bron-adapter is nog steeds is geselecteerd, ook de naam ervan wijzigen**SQL Server-bron** in Hallo **eigenschappen** deelvenster.
4. Sleep een ADO.NET bestemming toohello ontwerpoppervlak onder Hallo ADO.NET-bron van Hallo andere bestemmingen lijst in Hallo werkset. Met de Hallo-doeladapter nog steeds is geselecteerd, ook de naam ervan wijzigen**SQL DW bestemming** in Hallo **eigenschappen** deelvenster.
   
    ![][09]

## <a name="step-3-configure-hello-source-adapter"></a>Stap 3: Configureer Hallo bron adapter
1. Dubbelklik op Hallo bron adapter tooopen hello **ADO.NET bron Editor**.
   
    ![][03]
2. Op Hallo **Verbindingsbeheer** tabblad Hallo **ADO.NET bron Editor**, klikt u op Hallo **nieuw** knop volgende toohello **ADO.NET Verbindingsbeheer**lijst tooopen hello **ADO.NET Verbindingsbeheer configureren** dialoogvenster en te maken van de verbindingsinstellingen voor Hallo SQL Server-database waarin gegevens voor deze zelfstudie worden geladen.
   
    ![][04]
3. In Hallo **ADO.NET Verbindingsbeheer configureren** dialoogvenster vak, klikt u op Hallo **nieuw** knop tooopen hello **Verbindingsbeheer** dialoogvenster vak en maak een nieuwe verbinding.
   
    ![][05]
4. In Hallo **Verbindingsbeheer** dialoogvenster vak, de volgende dingen Hallo.
   
   1. Voor **Provider**, selecteer Hallo SqlClient-gegevensprovider.
   2. Voor **servernaam**, Voer Hallo SQL Server-naam.
   3. In Hallo **toohello server aanmelden** sectie Selecteer of typ de verificatiegegevens.
   4. In Hallo **Connect tooa database** sectie, selecteert u Hallo AdventureWorks-voorbeelddatabase.
   5. Klik op **verbinding testen**.
      
       ![][06]
   6. Klik in het dialoogvenster Hallo Hallo resultaten van de verbindingstest Hallo rapporten, **OK** tooreturn toohello **Verbindingsbeheer** in het dialoogvenster.
   7. In Hallo **Connection Manager** in het dialoogvenster, klikt u op **OK** tooreturn toohello **ADO.NET Verbindingsbeheer configureren** in het dialoogvenster.
5. In Hallo **ADO.NET Verbindingsbeheer configureren** in het dialoogvenster, klikt u op **OK** tooreturn toohello **ADO.NET gegevensbron bewerken**.
6. In Hallo **ADO.NET bron Editor**, in Hallo **naam van Hallo tabel of weergave Hallo** lijst, selecteer Hallo **Sales.SalesOrderDetail** tabel.
   
    ![][07]
7. Klik op **Preview** toosee eerste 200 rijen met gegevens in de brontabel Hallo in Hallo Hallo **Preview queryresultaten** in het dialoogvenster.
   
    ![][08]
8. In Hallo **Preview queryresultaten** in het dialoogvenster klikt u op **sluiten** tooreturn toohello **ADO.NET bron Editor**.
9. In Hallo **ADO.NET bron Editor**, klikt u op **OK** toofinish configureren Hallo-gegevensbron.

## <a name="step-4-connect-hello-source-adapter-toohello-destination-adapter"></a>Stap 4: Verbinding maken met de Hallo bron adapter toohello-doeladapter
1. Selecteer de bron-adapter Hallo op Hallo ontwerpoppervlak.
2. Selecteer Hallo blauwe pijl die uitgebreider is dan uit de bron-adapter Hallo en sleep deze toohello bestemming editor totdat deze wordt uitgelijnd naar de juiste plaats.
   
    ![][10]
   
    Een aantal andere onderdelen van Hallo SSIS-werkset Between Hallo bron en Hallo bestemming toorestructure, transformatie gebruiken in een typische SSIS-pakketten en gegevens verwijderen als het Hallo SSIS-gegevensstroom passeert. tookeep in dit voorbeeld zo eenvoudig mogelijk we verbinden Hallo bron rechtstreeks toohello doel.

## <a name="step-5-configure-hello-destination-adapter"></a>Stap 5: Hallo-doeladapter configureren
1. Dubbelklik op Hallo bestemming adapter tooopen hello **ADO.NET bestemming Editor**.
   
    ![][11]
2. Op Hallo **Verbindingsbeheer** tabblad Hallo **ADO.NET bestemming Editor**, klikt u op Hallo **nieuw** knop volgende toohello **Verbindingsbeheer**lijst tooopen hello **ADO.NET Verbindingsbeheer configureren** dialoogvenster en te maken van de verbindingsinstellingen voor hello Azure SQL Data Warehouse-database waarin gegevens voor deze zelfstudie worden geladen.
3. In Hallo **ADO.NET Verbindingsbeheer configureren** dialoogvenster vak, klikt u op Hallo **nieuw** knop tooopen hello **Verbindingsbeheer** dialoogvenster vak en maak een nieuwe verbinding.
4. In Hallo **Verbindingsbeheer** dialoogvenster vak, de volgende dingen Hallo.
   1. Voor **Provider**, selecteer Hallo SqlClient-gegevensprovider.
   2. Voor **servernaam**, Hallo SQL Data Warehouse naam invoeren.
   3. In Hallo **toohello server aanmelden** sectie **Gebruik SQL Server-verificatie** en voer de verificatiegegevens.
   4. In Hallo **Connect tooa database** sectie, selecteer een bestaande SQL Data Warehouse-database.
   5. Klik op **verbinding testen**.
   6. Klik in het dialoogvenster Hallo Hallo resultaten van de verbindingstest Hallo rapporten, **OK** tooreturn toohello **Verbindingsbeheer** in het dialoogvenster.
   7. In Hallo **Connection Manager** in het dialoogvenster, klikt u op **OK** tooreturn toohello **ADO.NET Verbindingsbeheer configureren** in het dialoogvenster.
5. In Hallo **ADO.NET Verbindingsbeheer configureren** in het dialoogvenster, klikt u op **OK** tooreturn toohello **ADO.NET bestemming Editor**.
6. In Hallo **ADO.NET bestemming Editor**, klikt u op **nieuw** volgende toohello **gebruik van een tabel of weergave** lijst tooopen hello **Create Table** in het dialoogvenster een nieuwe bestemming tabel met een kolomlijst die overeenkomt met de brontabel Hallo toocreate.
   
    ![][12a]
7. In Hallo **Create Table** dialoogvenster vak, de volgende dingen Hallo.
   
   1. Hallo-naam van de doeltabel Hallo ook wijzigen**verkooporderdetail**.
   2. Hallo verwijderen **rowguid** kolom. Hallo **uniqueidentifier** gegevenstype wordt niet ondersteund in SQL Data Warehouse.
   3. Wijzig het gegevenstype Hallo Hallo **LineTotal** kolom te**geld**. Hallo **decimale** gegevenstype wordt niet ondersteund in SQL Data Warehouse. Zie voor informatie over de ondersteunde gegevenstypen [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].
      
       ![][12b]
   4. Klik op **OK** toocreate Hallo tabel en keer terug toohello **ADO.NET bestemming Editor**.
8. In Hallo **ADO.NET bestemming Editor**, selecteer Hallo **toewijzingen** tabblad toosee toocolumns in Hallo doel hoe kolommen in bron Hallo zijn toegewezen.
   
    ![][13]
9. Klik op **OK** toofinish configureren Hallo-gegevensbron.

## <a name="step-6-run-hello-package-tooload-hello-data"></a>Stap 6: Tooload Hallo-Hallo pakketgegevens uitvoeren
Voer Hallo-pakket door te klikken op Hallo **Start** knop op Hallo werkbalk of door een hello te selecteren **uitvoeren** opties op Hallo **Debug** menu.

Als het pakket Hallo begint toorun, ziet u gele draaiende wheels tooindicate activiteit, evenals het aantal rijen verwerkt tot nu toe Hallo.

![][14]

Wanneer het Hallo-pakket is voltooid, u groen vinkje tooindicate geslaagd Zie evenals Hallo totale aantal rijen met gegevens die worden geladen vanuit Hallo bron toohello doel.

![][15]

Gefeliciteerd. U hebt de gegevens van SQL Server Integration Services tooload is gebruikt in Azure SQL Data Warehouse.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over Hallo SSIS-gegevensstroom. Begin hier: [gegevensstroom][Data Flow].
* Meer informatie over hoe toodebug en uw recht pakketten in de ontwerpomgeving Hallo oplossen. Begin hier: [hulpprogramma's voor het oplossen van problemen voor de ontwikkeling van pakket][Troubleshooting Tools for Package Development].
* Meer informatie over hoe toodeploy uw SSIS-projecten en pakketten tooIntegration Services-Server of tooanother opslaglocatie. Begin hier: [van implementatieprojecten en pakketten][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
