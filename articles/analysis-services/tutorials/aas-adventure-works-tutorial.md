---
title: aaa "Azure analyseservices Adventure Works-zelfstudie | Microsoft Docs'
description: Introduceert Hallo Adventure Works zelfstudie voor Azure Analysis Services
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a>Azure Analysis Services - Adventure Works-zelfstudie

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Deze zelfstudie bevat de uitkomsten over het toocreate en implementeren van een model in tabelvorm op Hallo 1400 compatibiliteitsniveau via [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

Als u nieuwe tooAnalysis Services en in tabelvorm modellering, het voltooien van deze zelfstudie is de snelste manier toolearn Hallo hoe toocreate en implementeren van een model in tabelvorm basic. Zodra u Hallo vereisten hebt in-place kost tussen twee toothree uren toocomplete.  
  
## <a name="what-you-learn"></a>Wat u leert   
  
-   Hoe een nieuw model in tabelvorm toocreate projecteren op Hallo **1400 compatibiliteitsniveau** in SSDT.
  
-   Hoe tooimport gegevens uit een relationele database in een model in tabelvorm-project.  
  
-   Hoe toocreate en beheren van relaties tussen tabellen in het Hallo-model.  
  
-   Hoe toocreate berekende kolommen, metingen en Key Performance Indicators die gebruikers helpen bij het analyseren van essentiële zakelijke metrische gegevens.  
  
-   Hoe toocreate en beheren van perspectieven en hiërarchieën die gebruikers gemakkelijker helpen modelgegevens bladeren door bedrijven en toepassingsspecifieke standpunten te geven.  
  
-   Hoe toocreate partities die verdelen tabelgegevens in kleinere logische delen die onafhankelijk van andere partities kunnen worden verwerkt.  
  
-   Hoe model toosecure objecten en gegevens door rollen te maken met leden van de gebruiker.  
  
-   Hoe een model in tabelvorm tooan toodeploy **Azure Analysis Services** server of een on-premises SQL Server 2017 Analysis Services-server.  
  
## <a name="prerequisites"></a>Vereisten  
toocomplete deze zelfstudie hebt u nodig:  
  
-   Een Azure Analysis Services of SQL Server 2017 Analysis Services-toodeploy uw model exemplaar. Meld u aan voor een gratis [proefversie van Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) en [maak een server](../analysis-services-create-server.md). U kunt zich ook registreren voor [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp) en dit product downloaden. 

-   Een SQL Server Data Warehouse of Azure SQL Data Warehouse met Hallo [AdventureWorksDW2014 voorbeelddatabase](http://go.microsoft.com/fwlink/?LinkID=335807). Deze database bevat Hallo gegevens nodig toocomplete in deze zelfstudie. Download [gratis edities van SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads). U kunt zich ook aanmelden voor een gratis [proefversie van Azure SQL Database](https://azure.microsoft.com/services/sql-database/). 

    **Belangrijk:** als u de voorbeelddatabase Hallo op een lokale SQL Server installeren en implementeren van uw model tooan Azure Analysis Services-server een [On-premises gegevensgateway](../analysis-services-gateway.md) is vereist.

-   meest recente versie van Hallo [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

-   meest recente versie van Hallo [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   Een clienttoepassing zoals [Power BI Desktop](https://powerbi.microsoft.com/desktop/) of Excel. 

## <a name="scenario"></a>Scenario  
Deze zelfstudie is gebaseerd op Adventure Works Cycles, een fictief bedrijf. Adventure Works is een grote, meertalige productiebedrijf die u maakt en distribueert fietsen, onderdelen en accessoires toocommercial markten in Noord-Amerika, Europa en Azië. Hallo bedrijf veiligheidsmaatregelen 500 werknemers. Bovendien maakt Adventure Works gebruik van verschillende regionale verkoopteams op de verschillende markten. Uw project is een model in tabelvorm voor verkoop en marketing-gebruikers tooanalyze Internet verkoopgegevens in de database AdventureWorksDW hello toocreate.  
  
toocomplete hello zelfstudie, moet u verschillende uitkomsten voltooien. In elke les moet u enkele taken uitvoeren. Het voltooien van elke taak in de volgorde is nodig voor het voltooien van Hallo les. Het is mogelijk dat een bepaalde les verschillende taken bevat die een vergelijkbare uitkomst opleveren, maar waarvoor dan net iets andere stappen worden gebruikt. Deze methode ziet er vaak is meer dan één manier toocomplete een taak en toochallenge die u met behulp van de vaardigheden die u hebt geleerd in vorige les en taken.  
  
Hallo-doel van Hallo uitkomsten is tooguide u door het ontwerpen van een model in tabelvorm basic met behulp van veel van Hallo functies in SSDT opgenomen. Omdat elke les op de vorige les hello voortbouwt, moet u Hallo uitkomsten in volgorde uitvoeren.
  
Deze zelfstudie biedt uitkomsten over het beheren van een server in Azure portal voor het beheren van een server of database met behulp van SSMS of met behulp van een client geen toepassingsgegevens toobrowse model. 


## <a name="lessons"></a>Lessen  
Deze zelfstudie bevat Hallo uitkomsten te volgen:  
  
|Les|Geschatte tijd toocomplete|  
|----------|------------------------------|  
|[1 - Een nieuw project voor een tabellair model maken](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|10 minuten|  
|[2 - Gegevens ophalen](../tutorials/aas-lesson-2-get-data.md)|10 minuten|  
|[3: Als gegevenstabel markeren](../tutorials/aas-lesson-3-mark-as-date-table.md)|3 minuten|  
|[4: Relaties maken](../tutorials/aas-lesson-4-create-relationships.md)|10 minuten|  
|[5 - Berekende kolommen maken](../tutorials/aas-lesson-5-create-calculated-columns.md)|15 minuten|
|[6 - Metingen maken](../tutorials/aas-lesson-6-create-measures.md)|30 minuten|  
|[7 - Key Performance Indicators (KPI) maken](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|15 minuten|  
|[8 - Perspectieven maken](../tutorials/aas-lesson-8-create-perspectives.md)|5 minuten|  
|[9 - Hiërarchieën maken](../tutorials/aas-lesson-9-create-hierarchies.md)|20 minuten|  
|[10 - Partities maken](../tutorials/aas-lesson-10-create-partitions.md)|15 minuten|  
|[11 - Rollen maken](../tutorials/aas-lesson-11-create-roles.md)|15 minuten|  
|[12: Analyseren in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md)|5 minuten| 
|[13 - Implementeren](../tutorials/aas-lesson-13-deploy.md)|5 minuten|  
  
## <a name="supplemental-lessons"></a>Aanvullende lessen  
Deze uitkomsten zijn niet vereist toocomplete Hallo zelfstudie, maar kunnen nuttig zijn in een beter begrip geavanceerde model in tabelvorm ontwerpfuncties zijn.  
  
|Les|Geschatte tijd toocomplete|  
|----------|------------------------------|  
|[Detailrijen](../tutorials/aas-supplemental-lesson-detail-rows.md)|10 minuten|
|[Dynamische beveiliging](../tutorials/aas-supplemental-lesson-dynamic-security.md)|30 minuten|
|[Onregelmatige hiërarchieën](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|20 minuten| 

  
## <a name="next-steps"></a>Volgende stappen  
tooget gestart, Zie [les 1: Maak een nieuw Tabellair Model-Project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

