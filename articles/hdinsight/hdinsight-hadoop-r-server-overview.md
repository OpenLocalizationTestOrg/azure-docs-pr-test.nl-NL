---
title: aaaIntroduction rondleiding Server op Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse R Server op HDInsight-toepassingen toocreate voor big data-analyse.
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6dc21bf5-4429-435f-a0fb-eea856e0ea96
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: daf7b70a15748d66510a04da370f39c5f26eb4ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#<a name="introduction-toor-server-and-open-source-r-capabilities-on-hdinsight"></a>Inleiding rondleiding Server en open-source R mogelijkheden in HDInsight

Microsoft R Server is beschikbaar als een Implementatieoptie wanneer u een HDInsight-clusters in Azure maken. Deze nieuwe mogelijkheid biedt gegevenswetenschappers en statistici R programmeurs met toegang op aanvraag tooscalable, gedistribueerde methoden van analyses in HDInsight.

Clusters kunnen worden aangepast op de juiste wijze toohello projecten en taken bij de hand en vervolgens verwijderd wanneer ze niet meer nodig zijn. Omdat ze onderdeel van Azure HDInsight zijn, wordt deze clusters worden geleverd met ondersteuning op bedrijfsniveau 24/7, een SLA van 99,9% beschikbaarheid en Hallo mogelijkheid toointegrate met andere onderdelen in hello Azure-ecosysteem.

Op HDInsight R Server biedt de nieuwste mogelijkheden voor analyses op basis van R Hallo op gegevenssets van vrijwel elke grootte, geladen tooeither Azure Blob of Data Lake storage. Aangezien R Server is gebouwd op open-source R, Hallo R gebaseerde toepassingen die u bouwt gebruik kunnen maken van Hallo 8000 + open-source R-pakketten. Hallo-routines in ScaleR, van Microsoft big analytics gegevenspakket opgenomen met R Server, zijn ook beschikbaar.

Hallo edge-knooppunt van een cluster biedt een handige locatie tooconnect toohello cluster en toorun uw R-scripts. Met een edge-knooppunt hebt u Hallo optie actief Hallo geparallelliseerde gedistribueerd functies van ScaleR over Hallo kernen van Hallo edge-knooppunt server. U kunt ook uitvoeren ze via Hallo knooppunten van het Hallo-cluster met behulp van ScaleR verminderen van Hadoop-kaart of Spark compute-contexten.

Hallo modellen of voorspellingen waarmee het resultaat van de analyses kan worden gedownload voor gebruik van lokale. Ze kunnen ook worden geoperationaliseerd elders in Azure, met name via [Azure Machine Learning Studio](http://studio.azureml.net) [webservice](../machine-learning/machine-learning-publish-a-machine-learning-web-service.md).

## <a name="get-started-with-r-on-hdinsight"></a>Aan de slag met R in HDInsight
tooinclude R Server in een HDInsight-cluster, moet u de Hallo clustertype R Server selecteren bij het maken van een HDInsight-cluster met behulp van hello Azure-portal. Hallo type R Server-cluster bevat R Server op Hallo gegevensknooppunten van het Hallo-cluster en op een edge-knooppunt dat als een zone landingspagina voor analyses op basis van een R Server fungeert. Zie [aan de slag met op HDInsight R Server](hdinsight-hadoop-r-server-get-started.md) voor een overzicht over hoe toocreate Hallo cluster.

## <a name="learn-about-data-storage-options"></a>Meer informatie over opties voor opslag van gegevens
Standaard opslag voor Hallo HDFS-bestandssysteem van het HDInsight-clusters kan worden gekoppeld aan een Azure Storage-account of een Azure Data Lake store. Deze koppeling zorgt ervoor dat de gegevens worden geüpload toohello clusteropslag tijdens de analyse persistent is gemaakt. Er zijn verschillende hulpmiddelen voor het verwerken van Hallo gegevensoverdracht toohello opslagoptie die u, inclusief Hallo op basis van de portal uploaden faciliteit van Hallo storage-account en Hallo selecteert [AzCopy](../storage/common/storage-use-azcopy.md) hulpprogramma.

U hebt de optie Hallo toegang tooadditional Blob en Data lake winkels toe te voegen tijdens het Hallo-cluster inrichtingsproces ongeacht Hallo primaire opslagoptie in gebruik. Zie [aan de slag met op HDInsight R Server](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-get-started) voor informatie over het toevoegen van toegangsaccounts tooadditional. Zie de aanvullende Hallo [Azure Storage-opties voor R Server op HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-storage) artikel toolearn meer over het gebruik van meerdere opslagaccounts.

U kunt ook [Azure Files](../storage/files/storage-how-to-use-files-linux.md) als een opslagoptie voor gebruik op Hallo edge-knooppunt. Azure Files kunt u toomount een bestandsshare die is gemaakt in Azure Storage toohello Linux-bestandssysteem. Zie voor meer informatie over deze opties voor het opslaan van gegevens voor R Server op HDInsight-cluster [Azure Storage-opties voor clusters op HDInsight R Server](hdinsight-hadoop-r-server-storage.md).

## <a name="access-r-server-on-hello-cluster"></a>Toegang R Server op Hallo-cluster
U kunt de Server op Hallo edge-knooppunt met een browser, mits u tooinclude RStudio Server hebt gekozen tijdens het inrichtingsproces Hallo rondleiding verbinden. Als u niet hebt geïnstalleerd het bij het inrichten van Hallo-cluster, kunt u deze later toevoegen. Zie voor meer informatie over het installeren van RStudio Server nadat een cluster is gemaakt, [RStudio-Server installeren op HDInsight-clusters](hdinsight-hadoop-r-server-install-r-studio.md). U kunt ook toohello R Server verbinden via SSH/PuTTY tooaccess Hallo R-console. 

## <a name="develop-and-run-r-scripts"></a>Ontwikkelen en uitvoeren van scripts R
Hallo R scripts u maken en uitvoeren, kunnen u elk Hallo 8000 + open-source R-pakketten in toevoeging toohello geparallelliseerde en routines die beschikbaar zijn in Hallo ScaleR bibliotheek gedistribueerd. In het algemeen een script dat wordt uitgevoerd met R Server op Hallo edge-knooppunt uitgevoerd binnen Hallo R-interpreter op dat knooppunt. Hallo-uitzonderingen zijn die stappen die nodig toocall een ScaleR-functie met een compute-context die tooHadoop kaart verkleinen (RxHadoopMR) of Spark (RxSpark) is ingesteld. Hallo-functie wordt in dit geval wordt uitgevoerd in een gedistribueerde manier over die (taak) gegevensknooppunten Hallo cluster die gekoppeld aan Hallo gegevens waarnaar wordt verwezen zijn. Zie voor meer informatie over opties voor verschillende rekenscenario context Hallo [Compute context opties voor R Server op HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).

## <a name="operationalize-a-model"></a>Mogelijk een model maken
Wanneer uw gegevens modelleren voltooid is, kunt u Hallo model toomake voorspellingen voor nieuwe gegevens vanuit Azure en on-premises operationeel te maken. Dit proces staat bekend als het score berekenen. Score berekenen kan worden gedaan in HDInsight, Azure Machine Learning of on-premises.

### <a name="score-in-hdinsight"></a>Score in HDInsight
tooscore in HDInsight, een R-functie die uw model toomake voorspellingen voor een nieuw gegevensbestand dat u tooyour storage-account hebt geladen aanroept schrijven. Sla Hallo voorspellingen back toohello storage-account. U kunt Hallo routinematige op aanvraag uitvoeren op Hallo edge-knooppunt van het cluster of met behulp van een geplande taak.  

### <a name="score-in-azure-machine-learning-aml"></a>Score in Azure Machine Learning eigen (AML)
met behulp van een webservice AML, gebruik Hallo tooscore open Azure Machine Learning-R-bronpakket bekend als [AzureML](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) toopublish uw model als een Azure-web-service. Dit pakket is voor het gemak vooraf geïnstalleerd zijn op Hallo edge-knooppunt. Vervolgens Hallo faciliteiten in Machine Learning toocreate een gebruikersinterface voor de webservice hello gebruiken en vervolgens om aan te roepen Hallo-webservice die nodig zijn voor score berekenen.

Als u deze optie kiest, moet u tooconvert ScaleR model objecten tooequivalent open source-modelobjecten voor gebruik met Hallo-webservice. Gebruik ScaleR afdwingen functies, zoals `as.randomForest()` voor ensemble-modellen, voor deze conversie.

### <a name="score-on-premises"></a>Score lokale
tooscore on-premises na het maken van uw model serialiseren Hallo-model in R, download, deserialiseren deze, en vervolgens worden gebruikt voor score berekenen voor nieuwe gegevens. U kunt met behulp van de eerder beschreven in Hallo-benadering beoordeling van nieuwe gegevens [scores in HDInsight](#scoring-in-hdinsight) of met behulp van [DeployR](https://deployr.revolutionanalytics.com/).

## <a name="maintain-hello-cluster"></a>Hallo cluster onderhouden
### <a name="install-and-maintain-r-packages"></a>Installeren en onderhouden van R-pakketten
Hallo R-pakketten die u gebruikt de meeste zijn vereist op de edge-knooppunt Hallo sinds het meeste werk uw R-scripts uitvoeren er. tooinstall aanvullende R-pakketten op Hallo edge-knooppunt, kunt u Hallo gebruikelijke `install.packages()` methode in R.

Als u alleen routines uit Hallo ScaleR bibliotheek over Hallo-cluster, hoeft meestal niet tooinstall extra R-pakketten op Hallo gegevensknooppunten. U moet echter extra pakketten toosupport Hallo gebruik van **rxExec** of **RxDataStep** op Hallo gegevensknooppunten kan worden uitgevoerd.

In dergelijke gevallen kan extra hello-pakketten worden geïnstalleerd met een scriptactie nadat u Hallo cluster hebt gemaakt. Zie voor meer informatie [maken van een HDInsight-cluster met R Server](hdinsight-hadoop-r-server-get-started.md).   

### <a name="change-hadoop-map-reduce-memory-settings"></a>Hadoop-kaart verminderen geheugeninstellingen wijzigen
Een cluster kan worden gewijzigd toochange Hallo hoeveelheid geheugen die beschikbaar rondleiding Server tijdens het uitvoeren van een taak kaart verminderen. een cluster toomodify gebruiken Hallo Apache Ambari gebruikersinterface die beschikbaar is via hello Azure portalblade voor uw cluster. Zie voor instructies over hoe tooaccess Ambari UI Hallo voor uw cluster [beheren HDInsight-clusters met Ambari-Webgebruikersinterface Hallo](hdinsight-hadoop-manage-ambari.md).

Het is ook mogelijk toochange Hallo hoeveelheid geheugen die beschikbaar rondleiding Server met behulp van Hadoop-switches in Hallo aanroep te**RxHadoopMR** als volgt:

    hadoopSwitches = "-libjars /etc/hadoop/conf -Dmapred.job.map.memory.mb=6656"  

### <a name="scale-your-cluster"></a>Een cluster schalen
Een bestaand cluster kan worden geschaald omhoog of omlaag via Hallo-portal. Door te schalen, krijgt u Hallo extra capaciteit die u voor grotere verwerkingstaken wellicht of u kunt schalen weer een cluster als deze niet actief is. Voor instructies over het tooscale een cluster, Zie [HDInsight-clusters beheren](hdinsight-administer-use-portal-linux.md).

### <a name="maintain-hello-system"></a>Hallo systeem onderhouden
Onderhoud tooapply OS patches en andere updates wordt uitgevoerd op Hallo onderliggende virtuele Linux-machines in een HDInsight-cluster buiten kantooruren. Onderhoud wordt gewoonlijk gedaan om 3:30 uur (gebaseerd op Hallo lokale tijd voor Hallo VM) elke maandag en donderdag. Updates worden zodanig dat ze geen invloed heeft op meer dan een kwartaal van Hallo cluster tegelijkertijd uitgevoerd.  

Aangezien Hallo hoofdknooppunten redundant zijn en niet alle gegevensknooppunten zijn beïnvloed, vertragen alle taken die worden uitgevoerd tijdens deze periode. Ze moeten echter nog steeds toocompletion, uitgevoerd. Alle aangepaste software- of lokale gegevens die u hebt blijft behouden over deze gebeurtenissen onderhoud tenzij er een onherstelbare fout optreedt waarvoor cluster opnieuw opbouwen.

## <a name="learn-about-ide-options-for-r-server-on-an-hdinsight-cluster"></a>Meer informatie over IDE-opties voor R Server op een HDInsight-cluster
Hallo Linux edge-knooppunt van een HDInsight-cluster is Hallo aanvoer zone voor op basis van het R-analyse. Bieden een standaardoptie voor het installeren van de community-versie Hallo van recente versies van HDInsight [RStudio Server](https://www.rstudio.com/products/rstudio-server/) op Hallo edge-knooppunt als een browser gebaseerde IDE. Gebruik van RStudio Server als een IDE voor Hallo ontwikkeling en uitvoering van scripts R aanzienlijk meer productief zijn dan het gebruik van alleen Hallo R-console. Als u niet tooadd RStudio Server hebt gekozen bij Hallo cluster maakt, maar tooadd wilt dat deze later vervolgens ziet [R Studio-Server installeren op een HDInsight-clusters](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-install-r-studio). +

Een andere optie voor volledige IDE tooinstall is een bureaublad IDE en gebruik ze tooaccess Hallo cluster door gebruik te maken van een externe Map verminderen of Spark compute context. Opties zijn onder andere Microsoft [R-Tools voor Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx) (RTVS) RStudio, en Walware's op basis van Eclipse [StatET](http://www.walware.de/goto/statet).

Ten slotte kunt u Hallo R Server-console op de edge-knooppunt Hallo openen door te typen **R** op Hallo Linux-opdrachtregel na verbinding maakt via SSH of PuTY. Wanneer u de interface van de console hello, handige toorun is een teksteditor voor het ontwikkelen van R-script in een ander venster en knippen en secties van het script in Hallo R console plakken als nodig is.

## <a name="learn-about-pricing"></a>Meer informatie over prijzen
Hallo kosten die gekoppeld aan een HDInsight zijn-cluster met R Server zijn op dezelfde manier gestructureerd toohello kosten voor Hallo HDInsight-clusters. Ze zijn gebaseerd op Hallo grootte van virtuele machines via het Hallo-naam, gegevens en edge-knooppunten, met Hallo toevoeging van een opwaartse core uur onderliggende hello. Zie voor meer informatie over prijzen voor HDInsight en Hallo beschikbaarheid van een gratis proefversie van 30 dagen [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over hoe toouse R Server met HDInsight-clusters, Zie Hallo volgende onderwerpen:

* [Aan de slag met op HDInsight R Server](hdinsight-hadoop-r-server-get-started.md)
* [RStudio Server tooHDInsight toevoegen (indien niet geïnstalleerd tijdens het maken van de cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opties voor compute-context voor R Server op HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)
* [Opties voor Azure-opslag voor R Server op HDInsight](hdinsight-hadoop-r-server-storage.md)
