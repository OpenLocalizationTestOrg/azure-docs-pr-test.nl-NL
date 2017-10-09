---
title: aaaIntroduction tooData Factory, een gegevensservice integratie | Microsoft Docs
description: 'Leer wat een Data Factory is: een cloudgebaseerde gegevensintegratieservice waarmee de verplaatsing en transformatie van gegevens wordt beheerd en geautomatiseerd.'
keywords: gegevensintegratie, cloudgegevensintegratie, wat is Azure Data Factory
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: cec68cb5-ca0d-473b-8ae8-35de949a009e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 4cc30515315efc938951057743ff8eb3701214ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-data-factory"></a>Inleiding tooAzure Data Factory 
## <a name="what-is-azure-data-factory"></a>Wat is Azure Data Factory?
In Hallo wereld van big data, hoe wordt bestaande gegevens gebruikt in bedrijf? Is het mogelijk tooenrich gegevens gegenereerd in de cloud Hallo referentiegegevens van on-premises gegevensbronnen of andere verschillende gegevensbronnen met? Een bedrijf games verzamelt bijvoorbeeld veel logboeken die wordt geproduceerd door games in Hallo cloud. Deze tooanalyze wil deze logboeken toogain inzichten in toocustomer voorkeuren, demografische gegevens, gebruik gedrag enzovoort tooidentify Upsell en cross-verkopen verkoopkansen, nieuwe functies toodrive zakelijke groei dwingende ontwikkelen en bieden een betere ervaring toocustomers. 

tooanalyze deze logboeken, Hallo bedrijf moet toouse Hallo referentiegegevens zoals klantgegevens, game informatie campagne marketinggegevens die zich in een on-premises gegevensopslag. Hallo bedrijf wil daarom tooingest logboekgegevens van gegevensarchief Hallo-cloud- en referentiegegevens van Hallo on-premises gegevensopslag. Vervolgens proces Hallo gegevens met behulp van Hadoop in Hallo cloud (Azure HDInsight) en publiceren van Hallo resultaat opslaan van gegevens in een cloud datawarehouse zoals Azure SQL Data Warehouse of een on-premises gegevens zoals SQL Server. Dit wil deze werkstroom toorun wekelijks eenmaal. 

Wat u nodig hebt, is een platform waarmee Hallo bedrijf toocreate een werkstroom die u kunt gegevens uit zowel on-premises en gegevensarchieven cloud, en transformeren of proces opnemen met behulp van bestaande compute services zoals Hadoop en Hallo resultaten tooan lokale publiceren of gegevensopslag voor BI toepassingen tooconsume cloud. 

![Overzicht van Data Factory](media/data-factory-introduction/what-is-azure-data-factory.png) 

Azure Data Factory is Hallo platform voor dit soort scenario's. Het is een **gegevens cloud-gebaseerde integration-service waarmee u toocreate gegevensgestuurde werkstromen in Hallo cloud voor organiseren en te automatiseren verplaatsing van gegevens en gegevenstransformatie**. Met behulp van Azure Data Factory, kunt u maken en plannen van gegevensgestuurde werkstromen (pijplijnen genoemd) die kan worden voor het opnemen van gegevens uit verschillende gegevensarchieven transformatie/proces Hallo gegevens met behulp van compute services zoals Azure HDInsight Hadoop, Spark, Azure Data Lake Analyse en Azure Machine Learning en publiceren van gegevens toodata zoals Azure SQL Data Warehouse voor business intelligence (BI) toepassingen tooconsume slaat uitvoer.  

Het is eerder een EL-platform (Extract-and-Load) en vervolgens een TL-platform (Transform-and-Load) dan een traditioneel ETL-platform (Extract-Transform-and-Load). Hallo-transformaties die worden uitgevoerd worden tootransform/proces gegevens met behulp van compute services in plaats van tooperform transformaties zoals Hallo die voor het toevoegen van afgeleide kolommen, tellen van het aantal rijen, voor het sorteren van gegevens, enzovoort. 

In Azure Data Factory Hallo-gegevens die wordt gebruikt en die wordt geproduceerd door werkstromen is momenteel **tijd gesegmenteerd gegevens** (elk uur, dagelijks, wekelijks, enz.). Een pijplijn kan bijvoorbeeld één keer per dag invoergegevens lezen, gegevens verwerken en uitvoer produceren. U kunt er ook voor kiezen om een werkstroom slechts één keer uit te voeren.  
  

## <a name="how-does-it-work"></a>Hoe werkt het? 
Hallo pijplijnen (gegevensgestuurde werkstromen) in Azure Data Factory wordt normaal gesproken uitvoert Hallo drie stappen te volgen:

![Drie fasen van Azure Data Factory](media/data-factory-introduction/three-information-production-stages.png)

### <a name="connect-and-collect"></a>Verbinding maken en verzamelen
Ondernemingen hebben verschillende typen gegevens, opgeslagen op verschillende bronnen. Hallo eerste stap bij het bouwen van een productiesysteem tooconnect tooall Hallo vereist gegevensbronnen en verwerken, zoals SaaS-services, bestand shares, FTP, webservices en verplaatsen Hallo gegevens nodig tooa centrale locatie voor verdere verwerking.

Ondernemingen moeten zonder Data Factory bouwen van aangepaste gegevens gegevensverplaatsing onderdelen of schrijven van aangepaste services toointegrate deze gegevensbronnen en de verwerking. Het is duur en moeilijk toointegrate en onderhouden van dergelijke systemen en vaak ontbreekt Hallo enterprise hoogwaardige bewaking en waarschuwingen en Hallo-besturingselementen die worden geboden door een volledig beheerde service.

U kunt met Data Factory gebruiken Hallo Kopieeractiviteit in een data pipeline toomove gegevens uit zowel on-premises en cloud winkels tooa centralisering gegevens brongegevensarchief in Hallo cloud voor verdere analyse. Bijvoorbeeld, kunt u de gegevens in een Azure Data Lake Store en transformatie hello later verzamelen met behulp van een Azure Data Lake Analytics compute-service. Of u kunt gegevens verzamelen in Azure Blob Storage en later transformeren met behulp van een Hadoop-cluster van Azure HDInsight.

### <a name="transform-and-enrich"></a>Transformeren en verrijken
Nadat de gegevens in een gecentraliseerde gegevensopslag in Hallo cloud aanwezig is, wilt u Hallo verzamelde gegevens toobe omgezet met behulp van compute services zoals HDInsight Hadoop, Spark, Data Lake Analytics en Machine Learning of verwerkt. Wilt u tooreliably produceren getransformeerd gegevens op een bruikbaar en gecontroleerde planning toofeed-productieomgevingen met vertrouwde gegevens. 

### <a name="publish"></a>Publiceren 
Leveren getransformeerde gegevens uit de cloud Hallo tooon lokale bronnen, zoals SQL Server of behouden blijft in uw cloud opslag bronnen voor verbruik door business intelligence (BI) en hulpprogramma's voor webanalyse en andere toepassingen.

## <a name="key-components"></a>Belangrijkste onderdelen
Een Azure-abonnement kan een of meer Azure Data Factory-exemplaren (oftewel 'data factory's') hebben. Azure Data Factory bestaat uit vier belangrijke onderdelen die samenwerken tooprovide Hallo platform waarop u gegevensgestuurde werkstromen met stappen toomove en transformatie gegevens kunt samenstellen. 

### <a name="pipeline"></a>Pijplijn
Een data factory kan één of meer pijplijnen hebben. Een pijplijn is een groep activiteiten. Hallo-activiteiten in een pijplijn worden samen een taak uitvoeren. Een pijplijn kan bijvoorbeeld een groep activiteiten die gegevens uit een Azure-blob opgenomen bevatten en voer vervolgens een Hive-query op een HDInsight-cluster toopartition Hallo gegevens. Hallo voordeel hiervan is dat pijplijn Hallo kunt u toomanage Hallo activiteiten als een set in plaats van elk afzonderlijk. U kunt bijvoorbeeld implementeren en onafhankelijk Hallo pipeline, in plaats van Hallo-activiteiten plannen. 

### <a name="activity"></a>Activiteit
Een pijplijn kan één of meer activiteiten bevatten. Hallo acties tooperform definiëren activiteiten voor uw gegevens. U kunt bijvoorbeeld toocopy activiteitsgegevens van een kopie van één data store tooanother gegevensarchief. U kunt op dezelfde manier een Hive-activiteit die wordt uitgevoerd een Hive-query op een Azure HDInsight-cluster tootransform gebruiken of uw gegevens analyseren. Data Factory ondersteunt twee soorten activiteiten: activiteiten voor gegevensverplaatsing en activiteiten voor gegevenstransformatie.

### <a name="data-movement-activities"></a>Activiteiten voor gegevensverplaatsing
Kopieeractiviteit in Data Factory kopieert gegevens van een gegevensarchief bron data store tooa sink. Data Factory ondersteunt Hallo gegevensarchieven te volgen. Gegevens van elke bron kan worden geschreven als tooany sink. Hoe klikt u op een data store toolearn toocopy gegevens tooand van dat archief.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie.

### <a name="data-transformation-activities"></a>Activiteiten voor gegevenstransformatie
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Zie het artikel [Activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) voor meer informatie.

### <a name="custom-net-activities"></a>Aangepaste .NET-activiteiten
Als u moet toomove gegevens naar/van een gegevensarchief die Kopieeractiviteit niet ondersteunen, of gegevens met behulp van uw eigen logica transformeren, maken een **aangepaste .NET-activiteit**. Zie [Aangepaste activiteiten gebruiken in een Azure Data Factory-pijplijn](data-factory-use-custom-activities.md) voor meer informatie over het maken en gebruiken van een aangepaste activiteit.

### <a name="datasets"></a>Gegevenssets
Voor een activiteit zijn nul of meer gegevenssets nodig als invoer en één of meer gegevenssets als uitvoer. Gegevenssets vertegenwoordigen gegevensstructuren binnen Hallo gegevensarchieven die of gewoon Hallo referentiegegevens gewenste toouse in uw activiteiten als invoer of uitvoer van gegevenspunt. Een Azure Blob-gegevensset bevat bijvoorbeeld Hallo blob-container en map in hello Azure Blob Storage uit welke Hallo pijplijn Hallo gegevens moet lezen. Of een Azure SQL-tabel gegevensset geeft Hallo tabel toowhich Hallo uitvoergegevens worden geschreven door Hallo-activiteit. 

### <a name="linked-services"></a>Gekoppelde services
Gekoppelde services zijn veel zoals verbindingsreeksen die Hallo verbindingsinformatie die nodig is voor Data Factory tooconnect tooexternal bronnen definiëren. Beschouw deze manier: een gekoppelde service definieert Hallo verbinding toohello gegevensbron en een gegevensset Hallo-structuur van Hallo gegevens vertegenwoordigt. Een gekoppelde Azure Storage-service geeft bijvoorbeeld verbinding tekenreeks tooconnect toohello Azure Storage-account. En een Azure Blob-gegevensset geeft Hallo blob-container en de Hallo map Hallo gegevens bevat.   

Gekoppelde services worden voor twee doeleinden gebruikt in een Data Factory:

* toorepresent een **gegevensarchief** inclusief, maar niet beperkt tot een lokale SQL Server, Oracle-database, bestandsshare of een Azure Blob Storage-account. Zie Hallo [activiteiten voor gegevensverplaatsing](#data-movement-activities) sectie voor een lijst van ondersteunde gegevensarchieven.
* toorepresent een **compute resource** die Hallo uitvoering van een activiteit kan hosten. Hallo activiteit Hdinsightahive wordt bijvoorbeeld uitgevoerd op een HDInsight Hadoop-cluster. Zie de sectie [Activiteiten voor gegevenstransformatie](#data-transformation-activities) voor een lijst met ondersteunde rekenomgevingen.

### <a name="relationship-between-data-factory-entities"></a>Relatie tussen Data Factory-entiteiten
![Diagram: Data Factory, een service voor gegevensintegratie in de cloud - belangrijkste concepten](./media/data-factory-introduction/data-integration-service-key-concepts.png)
**Afbeelding 2.** Relaties tussen de gegevensset, de activiteit, de pijplijn en de gekoppelde service

## <a name="supported-regions"></a>Ondersteunde regio’s
Op dit moment kunt u data factory maken in Hallo **VS-West**, **VS-Oost**, en **Noord-Europa** regio's. Echter een gegevensfactory kan toegang tot gegevensarchieven en compute services in andere Azure-regio's toomove gegevens tussen gegevensarchieven of compute-procesgegevens met behulp van services.

Azure Data Factory zelf slaat geen gegevens op. Hiermee kunt u gegevensgestuurde werkstromen tooorchestrate verplaatsing van gegevens tussen maken [ondersteunde gegevensarchieven](#data-movement-activities) en het verwerken van gegevens met [compute-services](#data-transformation-activities) in andere regio's of in een on-premises -omgeving. U kunt er ook te[bewaken en beheren van werkstromen](data-factory-monitor-manage-pipelines.md) met zowel programmatische als gebruikersinterfacemechanismen.

Hoewel Data Factory is alleen beschikbaar in **VS-West**, **VS-Oost**, en **Noord-Europa** regio's, Hallo-service dat Hallo gegevensverplaatsing in Data Factory is beschikbaar [globaal](data-factory-data-movement-activities.md#global) in meerdere regio's. Als een gegevensarchief zich achter een firewall, en vervolgens een [Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) geïnstalleerd in uw on-premises omgeving verplaatst Hallo gegevens in plaats daarvan.

Voorbeeld: uw berekeningsomgevingen, zoals een Azure HDInsight-cluster en Azure Machine Learning, worden uitgevoerd in de regio West-Europa. U kunt maken en gebruiken van een Azure Data Factory-exemplaar in Noord-Europa en tooschedule taken in uw berekeningsomgevingen in West-Europa gebruiken. Het duurt enkele milliseconden voor de Data Factory tootrigger Hallo taak van uw omgeving compute maar Hallo tijd voor het Hallo-taak uitvoeren op uw computeromgeving worden niet gewijzigd.

## <a name="get-started-with-creating-a-pipeline"></a>Aan de slag met het maken van een pijplijn
U kunt een van deze hulpprogramma's of API's toocreate gegevenspijplijnen in Azure Data Factory: 

- Azure Portal
- Visual Studio
- PowerShell
- .NET API
- REST API
- Azure Resource Manager-sjabloon. 

toolearn hoe toobuild data Factory met gegevens pijplijnen, volg de stapsgewijze instructies in de volgende zelfstudies Hallo:

| Zelfstudie | Beschrijving |
| --- | --- |
| [Gegevens verplaatsen tussen twee cloudlocaties voor gegevensopslag](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) |In deze zelfstudie maakt u een gegevensfactory maken met een pipeline die **gegevens verplaatst** uit Blob storage tooSQL database. |
| [Gegevens transformeren met een Hadoop-cluster](data-factory-build-your-first-pipeline.md) |In deze zelfstudie bouwt u uw eerste Azure-gegevensfactory met een gegevenspijplijn die **gegevens verwerkt** door Hive-script uit te voeren op een Azure HDInsight-cluster (Hadoop). |
| [Gegevens verplaatsen tussen een on-premises gegevensopslag en een gegevensarchief in de cloud met behulp van Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) |In deze zelfstudie maakt u een gegevensfactory bouwen met een pipeline die **gegevens verplaatst** van een **lokale** SQL Server-database tooan Azure-blob. Als onderdeel van het Hallo-scenario, installeren en configureren Hallo Data Management Gateway op uw computer. |
