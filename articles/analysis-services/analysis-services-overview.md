---
title: aaaWhat Azure Analysis Services is | Microsoft Docs
description: Grote afbeelding Hallo van Analysis Services in Azure worden opgehaald.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 83d7a29c-57ae-4aa0-8327-72dd8f00247d
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: 48830a86f47a8ddc7770e6c44dd56c29927fe582
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-analysis-services"></a>Wat is Azure Analysis Services?
![Azure Analysis Services](./media/analysis-services-overview/aas-overview-aas-icon.png)

Azure Analysis Services biedt bedrijfsniveau gegevens modelleren in Hallo cloud. Het is een volledig beheerd Platform as a Service (PaaS), geïntegreerd met de Azure Data Platform-services. 

Met Analysis Services kunt u gegevens uit meerdere bronnen verfijnen en combineren, metrische gegevens definiëren, en de gegevens beveiligen in één vertrouwd semantisch gegevensmodel. Hallo-gegevensmodel biedt een manier gemakkelijker en sneller voor uw gebruikers toobrowse enorme hoeveelheden gegevens met clienttoepassingen zoals Power BI, Excel, Reporting Services van derden en aangepaste apps.

![Gegevensbronnen](./media/analysis-services-overview/aas-overview-data-sources.png)

Bekijk [in deze video](https://sec.ch9.ms/ch9/d6dd/a1cda46b-ef03-4cea-8f11-68da23c5d6dd/AzureASoverview_high.mp4) toolearn hoe Azure Analysis Services in Microsoft past de algemene BI-mogelijkheden en hoe u kunt profiteren van uw data-modellen in de cloud Hallo ophalen.

## <a name="built-on-sql-server-analysis-services"></a>Gebaseerd op SQL Server Analysis Services
Azure Analysis Services is compatibel met veel geweldige functies die al deel uitmaken van SQL Server Analysis Services Enterprise Edition. Azure Analysis Services biedt ondersteuning voor tabelmodellen op Hallo 1200 en 1400 [compatibiliteitsniveaus](analysis-services-compat-level.md). Partities, beveiliging op rijniveau, bidirectionele relaties en vertalingen worden allemaal ondersteund. De in-memory en DirectQuery-modi staan garant voor razendsnelle query's in omvangrijke en complexe gegevenssets.

De tabellaire modellen kunnen snel worden ontwikkeld en zijn in hoge mate aanpasbaar. Voor ontwikkelaars omvatten modellen in tabelvorm Hallo in tabelvorm Object Model (aangepaste) toodescribe modelobjecten. AANGEPASTE in JSON is zichtbaar via Hallo [Tabellaire Model Scripting Language (TMSL)](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference) en Hallo AMO databasebeheersysteem via Hallo [Microsoft.AnalysisServices.Tabular](https://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) naamruimte.

## <a name="better-with-azure"></a>Beter met Azure
Azure Analysis Services kan worden geïntegreerd met vele Azure-services zodat u toobuild geavanceerde analytics-oplossingen. Integratie met [Azure Active Directory](../active-directory/active-directory-whatis.md) biedt veilige toegang op basis van rollen tooyour essentiële gegevens. Integreren met [Azure Data Factory](../data-factory/data-factory-introduction.md) pijplijnen door te nemen van een activiteit waarmee gegevens worden in Hallo model geladen. [Azure Automation](../automation/automation-intro.md) en [Azure Functions](../azure-functions/functions-overview.md) kunnen worden gebruikt voor de eenvoudige indeling van modellen met behulp van aangepaste code.

## <a name="get-up-and-running-quickly"></a>Snel aan de slag
In Azure Portal kunt u binnen enkele minuten [een server maken](analysis-services-create-server.md). En met behulp van Azure Resource Manager-[sjablonen](../azure-resource-manager/resource-manager-create-first-template.md) en PowerShell kunt u servers inrichten aan de hand van een declaratieve sjabloon. Met één enkele sjabloon kunt u meerdere services implementeren, samen met andere Azure-onderdelen, zoals opslagaccounts en Azure Functions. 

Nadat u een server hebt gemaakt, kunt u rechtstreeks in Azure Portal een tabellair model maken. Nieuwe hello (preview) [designer webfunctie](analysis-services-create-model-portal.md), u kunt verbinding maken met tooan Azure SQL Database, Azure SQL Data Warehouse-gegevensbron, of een Power BI Desktop pbix-bestand importeren. Relaties tussen tabellen worden automatisch gemaakt en kunt u eenheden maken of bewerken van Hallo model.bim bestand in json-indeling rechts van uw browser.

## <a name="scale-tooyour-needs"></a>Schaal tooyour behoeften
Azure Analysis Services is beschikbaar in de servicelagen Developer, Basic en Standard. Binnen elke laag variëren plankosten volgens tooprocessing voeding, QPUs en geheugen grootte. Wanneer u een server maakt, selecteert u binnen een servicelaag een abonnement. U kunt abonnementen wijzigen van of upgrade tooa hogere lagen, maar u kunt niet downgraden van een hogere laag tooa lagere lagen omlaag binnen Hallo dezelfde laag.

U kunt uw server omhoog of omlaag schalen en zelfs onderbreken. Gebruik hello Azure-portal of hebt u volledige controle op het moment met behulp van PowerShell. U betaalt alleen voor wat u gebruikt. toolearn meer informatie over Hallo verschillende planningen en lagen en gebruik Hallo Rekenmachine toodetermine Hallo juiste prijsstelling, Zie [prijzen van Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="keep-your-data-close"></a>Gegevens in de buurt houden
Azure Analysis Services-servers kunnen worden gemaakt in de volgende Hallo [Azure-regio's](https://azure.microsoft.com/regions/):

| Noord- en Zuid-Amerika | Europa | Azië en Stille Oceaan |
|----------|--------|--------------|
|  Brazilië - zuid<br> Canada - midden<br> VS - oost 2<br> Noord-centraal VS<br> Zuid-centraal VS<br> West-centraal VS<br> VS - west | Noord-Europa<br> Verenigd Koninkrijk Zuid<br> West-Europa |   Australië - zuidoost<br> Japan - oost<br> Zuidoost-Azië<br> West-India  |

Nieuwe regio's worden alle Hallo tijd toegevoegd zodat deze lijst is mogelijk onvolledig. U kiest uw locatie tijdens het maken van uw server in Azure Portal of met behulp van een Azure Resource Manager-sjabloon. Hallo tooget optimaal, kies een locatie dichtstbijzijnde uw grootste gebruikersgroep. Een [hoge beschikbaarheid](analysis-services-bcdr.md) garandeert u door uw modellen op redundante servers in meerdere regio's te implementeren.

## <a name="migrate-your-existing-tabular-models"></a>Bestaande tabellaire modellen migreren
Als u oplossingen voor bestaande on-premises SQL Server Analysis Services-model al hebt, kunt u tooAzure Analysis Services zonder aanzienlijke wijzigingen migreren. toomigrate, kunt u SSDT toodeploy uw model tooyour-server. In SSMS kunt u ook Back-up maken en terugzetten gebruiken, evenals TMSL.

Als u de on-premises gegevensbronnen hebt, u moet tooinstall en configureer een [On-premises gegevensgateway](analysis-services-gateway.md). Als u functies en leden van een rol al geconfigureerd hebt, uw rollen migreren, maar u leden van een rol tooreadd met behulp van SSMS of PowerShell.

## <a name="connect-toopopular-data-sources"></a>Verbinding maken met gegevensbronnen toopopular
Azure Analysis Services ondersteunt [toodata bronnen](analysis-services-datasource.md) on-premises in uw organisatie en in de cloud Hallo. Combineer gegevens uit zowel on-premises als in de cloud opgeslagen gegevensbronnen voor een hybride oplossing. 

Nieuwe modellen in tabelvorm 1400 gebruik Hallo moderne gegevens ophalen-functie in SSDT, op basis van de formule querytaal Hallo M. Gegevens ophalen u hebt meer gegevenstransformatie en mashup-onderdelen en Hallo mogelijkheid toocreate en bewerken van uw eigen geavanceerde M formule language-query's. U kunt een tabellair model met compatibiliteitsniveau 1400 bijvoorbeeld baseren op gegevensbestanden in Azure Blob Storage.

## <a name="use-hello-tools-you-already-know"></a>Hallo-hulpprogramma's die u al weet gebruiken

![Tools voor BI-ontwikkelaars](./media/analysis-services-overview/aas-overview-dev-tools.png)

#### <a name="sql-server-data-tools-ssdt-for-visual-studio"></a>SQL Server Data Tools (SSDT) voor Visual Studio
Ontwikkelen en implementeren van modellen Hello gratis [SQL Server Data Tools (SSDT) voor Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx). SSDT bevat Analysis Services-projectsjablonen waarmee u snel aan de slag kunt gaan. SSDT bevat nu Hallo moderne gegevens ophalen datasource query en mashup functionaliteit voor modellen in tabelvorm 1400. Als u bekend met ophalen van gegevens in Power BI Desktop- en Excel 2016 bent, weet u al hoe eenvoudig is toocreate aangepast maximaal data source-query's.

#### <a name="sql-server-management-studio"></a>SQL Server Management Studio
Servers en modeldatabases beheert u met behulp van [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Servers in de cloud Hallo tooyour koppelen. TMSL scripts rechts uitvoeren vanuit Hallo XMLA-query-venster en taken automatiseren met behulp van TMSL scripts. Omdat er in hoog tempo nieuwe functies en mogelijkheden worden toegevoegd, wordt SSMS maandelijks bijgewerkt.

#### <a name="powershell"></a>PowerShell
Beheertaken voor server resource zoals het maken van servers, onderbreken of hervatten van serverbewerkingen of wijzigen van Hallo serviceniveau (laag) Azure Resource Manager (AzureRM)-cmdlets gebruiken. Andere taken voor het beheren van databases zoals het toevoegen of verwijderen van leden van een rol verwerken of het uitvoeren van scripts TMSL cmdlets in Hallo SqlServer module gebruiken. Zowel AzureRM en SQL Server-modules zijn beschikbaar in Hallo [PowerShell gallery](https://www.powershellgallery.com/).


## <a name="your-data-is-secure"></a>Gegevens zijn beveiligd
![Gegevensvisualisaties](./media/analysis-services-overview/aas-overview-secure.png)

#### <a name="authentication"></a>Authentication
Gebruikersverificatie voor Azure Analysis services wordt afgehandeld door [Azure Active Directory (AAD)](../active-directory/active-directory-whatis.md). Bij een poging toolog in tooan Azure Analysis Services-database, gebruikers werken met een identiteit van de organisatie-account met toegang toohello database probeert ze tooaccess. Deze gebruikers-id's moeten lid zijn van Hallo standaard Azure Active Directory voor Hallo abonnement waarin hello Azure Analysis Services-server zich bevindt. toolearn meer, Zie [verificatie en gebruikersmachtigingen](analysis-services-manage-users.md).

#### <a name="data-security"></a>Gegevensbeveiliging
Azure Analysis Services maakt gebruik van Azure Blob storage toopersist opslag en metagegevens voor Analysis Services-databases. Gegevensbestanden in Blob worden versleuteld met behulp van Azure Blob Server Side Encryption (SSE). Wanneer de Direct Query-modus wordt gebruikt, worden alleen metagegevens opgeslagen. de werkelijke gegevens Hallo is toegankelijk vanuit Hallo-gegevensbron op het moment dat de query.

#### <a name="on-premises-data-sources"></a>On-premises gegevensbronnen
Veilige toegang toodata tijdelijk on-premises in uw organisatie wordt bereikt door het installeren en configureren van een [On-premises gegevensgateway](analysis-services-gateway.md). Gateways bieden toegang toodata voor zowel de directe Query als de modi in het geheugen. Wanneer een Azure Analysis Services-model verbinding tooan on-premises gegevensbron maakt, wordt een query gemaakt samen met de Hallo versleuteld referenties voor Hallo on-premises gegevensbron. gateway-cloudservice Hallo Hallo query analyseert en pushes Hallo aanvraag tooan Azure Service Bus. Hallo lokale gateway hello Azure Service Bus voor aanvragen in behandeling worden opgevraagd. Hallo gateway vervolgens Hallo query opgehaald, ontsleutelt Hallo referenties en verbindt toohello gegevensbron voor uitvoering. Hallo resultaten worden vervolgens verzonden vanuit de gegevensbron hello, back-toohello gateway en klik vervolgens op toohello Azure Analysis Services-database.

Azure Analysis Services wordt beheerst door Hallo [Microsoft Online servicevoorwaarden](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) en Hallo [privacyverklaring van Microsoft Online Services](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).
toolearn meer informatie over Azure-beveiliging, Zie Hallo [Microsoft Trust Center](https://www.microsoft.com/trustcenter/Security/AzureSecurity).

## <a name="supports-hello-latest-client-tools"></a>Hallo nieuwste clienthulpprogramma's ondersteunt
![Gegevensvisualisaties](./media/analysis-services-overview/aas-overview-clients.png)

Moderne hulpprogramma's voor het verkennen en visualiseren van gegevens, zoals Power BI, Excel en hulpprogramma's van derden, bieden gebruikers interactieve en visueel aantrekkelijke inzichten in de gegevens van uw model.

Clients gebruiken MSOLAP AMO of ADOMD [clientbibliotheken](analysis-services-data-providers.md) tooconnect tooAnalysis Services-servers. In Microsoft-clienttoepassingen als Power BI Desktop en Excel zijn alle drie deze clientbibliotheken geïnstalleerd. Maar houd er rekening mee, afhankelijk van het Hallo-versie of -frequentie van updates, clientbibliotheken mogelijk niet de nieuwste versies Hallo vereist door Azure Analysis Services. Hallo geldt toocustom toepassingen of andere interfaces zoals AsCmd, aangepaste, ADOMD.NET. Deze toepassingen moeten normaal Hallo tapewisselaars handmatig te installeren als onderdeel van een pakket.


## <a name="get-help"></a>Help opvragen

#### <a name="documentation"></a>Documentatie
Azure Analysis Services is eenvoudig tooset up en toomanage. U vindt alle Hallo info u toocreate nodig hebt en beheren van uw server-services. Bij het maken van een model toodeploy tooyour beheerserver, heeft deze dezelfde veel Hallo omdat dit voor het maken van een gegevensmodel dat u implementeert tooan lokale server. Er is een uitgebreide bibliotheek met overzichtsinformatie, procedures, zelfstudies en naslagartikelen beschikbaar op [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services).

#### <a name="videos"></a>Video's
Bekijk nuttige video's over [Azure Analysis Services op Channel 9](https://channel9.msdn.com/series/Azure-Analysis-Services).

#### <a name="blogs"></a>Blogs
Er veranderen nog veel dingen. U krijgt altijd de meest recente informatie op Hallo Hallo [Analysis Services-teamblog](https://blogs.msdn.microsoft.com/analysisservices/) en [Azure blog](https://azure.microsoft.com/blog/).

#### <a name="community"></a>Community
Analysis Services heeft een zeer actieve gebruikerscommunity. Deelnemen aan Hallo conversatie op [Azure Analysis Services-forum](https://aka.ms/azureanalysisservicesforum).

## <a name="feedback"></a>Feedback
Hebt u suggesties of functieverzoeken? Zich ervoor tooleave hierop een toelichting op [Azure Analysis Services Feedback](https://aka.ms/azureanalysisservicesfeedback).

Hebt u suggesties over Hallo documentatie? U kunt opmerkingen Livefyre Hallo onder aan elk artikel toevoegen.

## <a name="next-steps"></a>Volgende stappen
Nu u meer informatie over Azure Analysis Services, is het tijd tooget gestart. Meer informatie over hoe te[maken van een server](analysis-services-create-server.md) in Azure. Wanneer de server klaar is, is doorlopen Hallo [Adventure Works zelfstudie](tutorials/aas-adventure-works-tutorial.md) toolearn hoe toocreate een volledig functionele model in tabelvorm en deze tooyour server implementeren.
