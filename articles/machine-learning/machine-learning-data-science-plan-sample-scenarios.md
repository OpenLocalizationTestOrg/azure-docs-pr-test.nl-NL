---
title: geavanceerde scenario's met gegevensanalyses voor Azure Machine Learning aaaIdentify | Microsoft Docs
description: Selecteer Hallo juiste scenario's voor geavanceerde predictive analytics Hello Team gegevens wetenschap proces doen.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a>Scenario's voor geavanceerde analyses in Azure Machine Learning
In dit artikel bevat een overzicht van Hallo verschillende gegevensbronnen voorbeeld en doel-scenario's die kunnen worden verwerkt door Hallo [Team gegevens wetenschap proces (TDSP)](data-science-process-overview.md). Hallo TDSP biedt een systematische aanpak voor teams toocollaborate op intelligente toepassingen bouwen. Hallo-scenario's die hier wordt gepresenteerd illustreren beschikbare opties in Hallo gegevensverwerking werkstroom die afhankelijk van Hallo gegevenskenmerken, bronlocaties en doel-opslagplaatsen in Azure zijn.

Hallo **beslissingsstructuur** voor Hallo voorbeeldscenario's die geschikt is voor uw gegevens en doel selecteren in de laatste sectie hello wordt weergegeven.

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

Elk van de volgende secties Hallo geeft een voorbeeldscenario. Voor elk scenario, een mogelijke gegevenswetenschap of geavanceerde analyses stroom en de ondersteunende Azure-resources die worden vermeld.

> [!NOTE]
> **Voor alle Hallo volgen scenario's, moet u:**
> <br/>
> 
> * [Een opslagaccount maken](../storage/common/storage-create-storage-account.md)
>   <br/>
> * [Een Azure Machine Learning-werkruimte maken](machine-learning-create-workspace.md)
> 
> 

## <a name="smalllocal"></a>Scenario \#1: kleine toomedium in tabelvorm gegevensset in een lokale bestanden
![Kleine toomedium lokale bestanden][1]

#### <a name="additional-azure-resources-none"></a>Extra Azure-resources: geen
1. Meld u aan toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
2. Upload een dataset.
3. Maak een Azure Machine Learning-experiment stroom beginnen met geüploade gegevensset (s).

## <a name="smalllocalprocess"></a>Scenario \#2: kleine toomedium gegevensset van lokale bestanden die moeten worden verwerkt
![Kleine toomedium lokale bestanden met de verwerking][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Extra Azure-resources: Azure virtuele Machine (IPython Notebook server)
1. Maak een virtuele Machine van Azure IPython Notebook uitgevoerd.
2. Het uploaden van gegevens tooan Azure storage-container.
3. Vooraf verwerken en de gegevens in IPython laptop, toegang tot gegevens uit Azure storage-container opschonen.
4. Transformeer gegevens toocleaned, tabelvorm.
5. Getransformeerde gegevens opslaan in Azure blobs.
6. Meld u aan toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
7. Hallo-gegevens lezen uit Azure blobs Hallo met [importgegevens] [ import-data] module.
8. Maak een Azure Machine Learning-experiment stroom vanaf opgenomen gegevensset (s).

## <a name="largelocal"></a>Scenario \#3: grote gegevensset van lokale bestanden, die gericht is op Azure Blobs
![Grote lokale bestanden][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Extra Azure-resources: Azure virtuele Machine (IPython Notebook server)
1. Maak een virtuele Machine van Azure IPython Notebook uitgevoerd.
2. Het uploaden van gegevens tooan Azure storage-container.
3. Vooraf verwerken en de gegevens in IPython laptop, toegang tot gegevens uit Azure blobs opschonen.
4. Transformeer gegevens toocleaned, tabelvorm, indien nodig.
5. Gegevens verkennen en functies maken indien nodig.
6. Een voorbeeld van kleine tot middelgrote gegevens extraheren.
7. Hallo door actieve gegevens opslaan in Azure blobs.
8. Meld u aan toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
9. Hallo-gegevens lezen uit Azure blobs Hallo met [importgegevens] [ import-data] module.
10. Azure Machine Learning-experiment stroom vanaf opgenomen kolomovereenkomst bouwen.

## <a name="smalllocaltodb"></a>Scenario \#4: klein toomedium gegevensset van lokale bestanden, die gericht is op SQL Server in een virtuele Machine van Azure
![Kleine toomedium lokale bestanden tooSQL DB in Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Extra Azure-resources: Azure virtuele Machine (SQL Server / IPython Notebook server)
1. Maak een virtuele Machine van Azure SQL-Server + IPython Notebook uitgevoerd.
2. Het uploaden van gegevens tooan Azure storage-container.
3. Vooraf verwerken en de gegevens in Azure storage-container met IPython Notebook opschonen.
4. Transformeer gegevens toocleaned, tabelvorm, indien nodig.
5. Gegevens tooVM lokale bestanden op te slaan (IPython Notebook wordt uitgevoerd op virtuele machine, lokale stations verwijzen tooVM stations).
6. Laden van gegevens tooSQL Server-database op een Azure VM.
   
   Optie \#1: met SQL Server Management Studio.
   
   * Aanmelding tooSQL Server VM
   * Voer SQL Server Management Studio.
   * Database- en doel-tabellen maken.
   * Gebruik een van de Hallo bulksgewijs wordt methoden tooload Hallo gegevens importeren uit VM-lokale bestanden.
   
   Optie \#2: met behulp van IPython Notebook – niet aanbevolen voor middelgrote en grote gegevenssets
   
   <!-- -->    
   * Gebruik ODBC connection string tooaccess SQL Server op virtuele machine.
   * Database- en doel-tabellen maken.
   * Gebruik een van de Hallo bulksgewijs wordt methoden tooload Hallo gegevens importeren uit VM-lokale bestanden.
7. Gegevens verkennen, functies maken indien nodig. Houd er rekening mee Hallo functies hoeft geen toobe gematerialiseerd in Hallo databasetabellen. Alleen Houd er rekening mee Hallo nodig query toocreate ze.
8. Bepaal op een steekproefomvang gegevens als nodig is en/of gewenst.
9. Meld u aan toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
10. Lees Hallo gegevens rechtstreeks van Hallo SQL Server met behulp van Hallo [importgegevens] [ import-data] module. Plakken Hallo nodig query die velden, pakt functies maakt en voorbeelden van gegevens, indien nodig rechtstreeks in Hallo [importgegevens] [ import-data] query.
11. Azure Machine Learning-experiment stroom vanaf opgenomen kolomovereenkomst bouwen.

## <a name="largelocaltodb"></a>Scenario \#5: grote gegevensset in een lokale bestanden doel-SQL-Server in Azure VM
![Grote lokale bestanden tooSQL DB in Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Extra Azure-resources: Azure virtuele Machine (SQL Server / IPython Notebook server)
1. Een Azure-virtuele Machine met SQL Server en IPython Notebook server maken.
2. Het uploaden van gegevens tooan Azure storage-container.
3. (Optioneel) Vooraf verwerken en gegevens opgeschoond.
   
   a.  Vooraf verwerken en de gegevens in IPython laptop, toegang tot gegevens uit Azure opschonen
   
       blobs.
   
   b.  Transformeer gegevens toocleaned, tabelvorm, indien nodig.
   
   c.  Gegevens tooVM lokale bestanden op te slaan (IPython Notebook wordt uitgevoerd op virtuele machine, lokale stations verwijzen tooVM stations).
4. Laden van gegevens tooSQL Server-database op een Azure VM.
   
   a.  Aanmelding tooSQL Server-VM.
   
   b.  Als gegevens niet al opgeslagen, downloaden van gegevensbestanden van Azure
   
       storage container toolocal-VM folder.
   
   c.  Voer SQL Server Management Studio.
   
   d.  Database- en doel-tabellen maken.
   
   e.  Gebruik een van de Hallo bulksgewijs methoden tooload Hallo gegevens importeren.
   
   f.  Als tabelsamenvoegingen vereist zijn, maakt u indexen tooexpedite joins.
   
   > [!NOTE]
   > Voor sneller laden van grote hoeveelheden gegevens grootten verdient het aanbeveling gepartitioneerde tabellen te maken en importeren Hallo gegevens parallel bulksgewijs. Zie voor meer informatie [parallelle gegevensimport tooSQL gepartitioneerde tabellen](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Gegevens verkennen, functies maken indien nodig. Houd er rekening mee Hallo functies hoeft geen toobe gematerialiseerd in Hallo databasetabellen. Alleen Houd er rekening mee Hallo nodig query toocreate ze.
6. Bepaal op een steekproefomvang gegevens als nodig is en/of gewenst.
7. Meld u aan toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
8. Lees Hallo gegevens rechtstreeks van Hallo SQL Server met behulp van Hallo [importgegevens] [ import-data] module. Plakken Hallo nodig query die velden, pakt functies maakt en voorbeelden van gegevens, indien nodig rechtstreeks in Hallo [importgegevens] [ import-data] query.
9. Eenvoudige Azure Machine Learning-experiment stroom beginnen met geüploade gegevensset

## <a name="largedbtodb"></a>Scenario \#6: grote gegevensset in een SQL Server-database on-premises, die gericht is op SQL Server in een virtuele Machine van Azure
![Grote SQL DB on-premises tooSQL DB in Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Extra Azure-resources: Azure virtuele Machine (SQL Server / IPython Notebook server)
1. Een Azure-virtuele Machine met SQL Server en IPython Notebook server maken.
2. Gebruik een van de gegevens Hallo wordt methoden tooexport Hallo gegevens exporteren uit SQL Server toodump-bestanden.
   
   > [!NOTE]
   > Als u toomove alle gegevens van Hallo on-premises database, een alternatieve (sneller) methode toomove Hallo volledige database toothe SQL Server-exemplaar in Azure besluit. Hallo stappen tooexport gegevens overslaan, database en de belasting/importeren gegevens toohello doeldatabase maken en volg Hallo alternatieve methode.
   > 
   > 
3. Upload dump bestanden tooAzure storage-container.
4. Laden Hallo gegevens tooa SQL Server-database op een virtuele Machine van Azure wordt uitgevoerd.
   
   a.  Aanmelding toohello SQL Server-VM.
   
   b.  Downloaden van gegevensbestanden uit een Azure storage-container toohello lokale VM-map.
   
   c.  Voer SQL Server Management Studio.
   
   d.  Database- en doel-tabellen maken.
   
   e.  Gebruik een van de Hallo bulksgewijs methoden tooload Hallo gegevens importeren.
   
   f.  Als tabelsamenvoegingen vereist zijn, maakt u indexen tooexpedite joins.
   
   > [!NOTE]
   > Maken voor sneller laden van grote hoeveelheden gegevens grootten gepartitioneerde tabellen en toobulk importeren Hallo gegevens parallel. Zie voor meer informatie [parallelle gegevensimport tooSQL gepartitioneerde tabellen](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Gegevens verkennen, functies maken indien nodig. Houd er rekening mee Hallo functies hoeft geen toobe gematerialiseerd in Hallo databasetabellen. Alleen Houd er rekening mee Hallo nodig query toocreate ze.
6. Bepaal op een steekproefomvang gegevens als nodig is en/of gewenst.
7. Meld u aan toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
8. Lees Hallo gegevens rechtstreeks van Hallo SQL Server met behulp van Hallo [importgegevens] [ import-data] module. Plakken Hallo nodig query die velden, pakt functies maakt en voorbeelden van gegevens, indien nodig rechtstreeks in Hallo [importgegevens] [ import-data] query.
9. Eenvoudige Azure Machine Learning-experiment stroom met geüploade gegevensset wordt gestart.

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a>Alternatieve methode toocopy volledige database van een lokale SQL Server tooAzure SQL-Database
![Loskoppelen van de lokale database en koppelt u tooSQL DB in Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Extra Azure-resources: Azure virtuele Machine (SQL Server / IPython Notebook server)
tooreplicate hello volledige SQL Server-database in uw SQL Server VM u moet een database kopiëren vanaf één locatie of de server tooanother, ervan uitgaande dat die database Hallo tijdelijk offline kan worden uitgevoerd. Dit doet u in Hallo SQL Server Management Studio Object Explorer of Hallo gelijkwaardige Transact-SQL-opdrachten te gebruiken.

1. Hallo-database op de bronlocatie Hallo loskoppelen. Zie voor meer informatie [loskoppelen van een database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).
2. In Windows Verkenner of Windows-opdrachtprompt venster losgekoppeld kopie Hallo databasebestand of bestanden en logboekbestand of bestanden toohello doellocatie op Hallo van SQL Server VM in Azure.
3. Hallo gekopieerd bestanden toohello doel SQL Server-exemplaar koppelen. Zie voor meer informatie [om een Database koppelen](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).

[Verplaatsen van een Database met loskoppelen en koppelt (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)

## <a name="largedbtohive"></a>Scenario \#7: Big data in lokale bestanden doel Hive-database in Azure HDInsight Hadoop-clusters
![BIG data in lokale doel Hive][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a>Extra Azure-resources: Azure HDInsight Hadoop-Cluster en Azure virtuele Machine (IPython Notebook server)
1. Maak een Azure virtuele Machine waarop IPython Notebook server wordt uitgevoerd.
2. Maak een Azure HDInsight Hadoop-cluster.
3. (Optioneel) Vooraf verwerken en gegevens opgeschoond.
   
   a.  Vooraf verwerken en de gegevens in IPython laptop, toegang tot gegevens uit Azure opschonen
   
       blobs.
   
   b.  Transformeer gegevens toocleaned, tabelvorm, indien nodig.
   
   c.  Gegevens tooVM lokale bestanden op te slaan (IPython Notebook wordt uitgevoerd op virtuele machine, lokale stations verwijzen tooVM stations).
4. Het uploaden van gegevens toohello standaardcontainer van Hallo Hadoop-cluster in Hallo stap 2 hebt geselecteerd.
5. Laden van gegevens tooHive database in Azure HDInsight Hadoop-cluster.
   
   a.  Meld u bij het hoofdknooppunt van het Hadoop-cluster Hallo toohello
   
   b.  Open Hallo Hadoop-opdrachtregel.
   
   c.  Voer Hallo Hive-hoofdmap door opdracht `cd %hive_home%\bin` in Hadoop vanaf de opdrachtregel.
   
   d.  Voer Hallo Hive-query's toocreate database en tabellen en laden van gegevens uit blob storage-tooHive tabellen.
   
   > [!NOTE]
   > Als Hallo gegevens groot is, kunnen gebruikers Hallo Hive-tabel met partities maken. Vervolgens kunnen gebruikers gebruiken een `for` lus in Hallo Hadoop vanaf de opdrachtregel op Hallo hoofdknooppunt tooload gegevens in Hallo Hive-tabel is gepartitioneerd door partitie.
   > 
   > 
6. Gegevens verkennen en functies maken indien nodig in de Hadoop-opdrachtregel. Houd er rekening mee Hallo functies hoeft geen toobe gematerialiseerd in Hallo databasetabellen. Alleen Houd er rekening mee Hallo nodig query toocreate ze.
   
   a.  Meld u bij het hoofdknooppunt van het Hadoop-cluster Hallo toohello
   
   b.  Open Hallo Hadoop-opdrachtregel.
   
   c.  Voer Hallo Hive-hoofdmap door opdracht `cd %hive_home%\bin` in Hadoop vanaf de opdrachtregel.
   
   d.  Hallo Hive-query's in de Hadoop-opdrachtregel uitvoeren op Hallo hoofdknooppunt Hallo Hadoop-cluster tooexplore Hallo gegevens en onderdelen naar behoefte maken.
7. Indien nodig en/of gewenst, steekproef Hallo gegevens toofit in Azure Machine Learning Studio.
8. Meld u aan toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
9. Hallo-gegevens lezen rechtstreeks vanuit Hallo `Hive Queries` met Hallo [importgegevens] [ import-data] module. Plakken Hallo nodig query die velden, pakt functies maakt en voorbeelden van gegevens, indien nodig rechtstreeks in Hallo [importgegevens] [ import-data] query.
10. Eenvoudige Azure Machine Learning-experiment stroom met geüploade gegevensset wordt gestart.

## <a name="decisiontree"></a>Beslissingsstructuur voor de selectie van scenario
- - -
Hallo volgende diagram ziet u Hallo scenario's die hierboven worden beschreven en Hallo Advanced Analytics-proces en de technologie hebt gekozen waarmee u tooeach Hallo gespecificeerde scenario's. Denk eraan dat gegevensverwerking, exploratie functie-engineering en steekproeven kunnen duren plaats in een of meer methode/omgeving--op Hallo bron, tussenliggende, en/of doel omgevingen: en iteratief naar behoefte kunt doorgaan. Hallo diagram alleen fungeert als een illustratie van enkele mogelijke stromen en biedt geen een uitputtende opsomming.

![Voorbeeldscenario DS proces scenario 's][8]

### <a name="advanced-analytics-in-action-examples"></a>Geavanceerde analyses in actie voorbeelden
Voor end-to-end Azure Machine Learning-scenario's die gebruikmaken van met Hallo Advanced Analytics-proces en de technologie met behulp van openbare gegevenssets, Zie:

* [Procedure voor het wetenschappelijke gegevens in een team in actie: met behulp van SQL Server](machine-learning-data-science-process-sql-walkthrough.md).
* [Procedure voor het wetenschappelijke gegevens in een team in actie: met behulp van HDInsight Hadoop-clusters](machine-learning-data-science-process-hive-walkthrough.md).

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
