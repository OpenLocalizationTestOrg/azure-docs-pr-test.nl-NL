---
title: een Windows-PC met Hadoop op HDInsight - Azure aaaUse | Microsoft Docs
description: Werken vanuit een Windows-PC in Hadoop op HDInsight. Query-clusters met PowerShell, Visual Studio- en Linux-hulpprogramma's en beheren. Ontwikkel big data-oplossingen met .NET.
services: hdinsight
keywords: hadoop op windows, hadoop voor windows
author: cjgronlund
manager: jhubbard
ms.author: cgronlun
ms.date: 05/17/2017
ms.topic: article
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 7c93f16e93349c0b8fb1abd55320c2c172b93aa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="work-in-hello-hadoop-ecosystem-on-hdinsight-from-a-windows-pc"></a>Hallo onderhanden werk Hadoop-ecosysteem in HDInsight via een Windows-PC

Meer informatie over de ontwikkeling en opties voor op Windows-PC Hallo voor het werken met Hallo Hadoop-ecosysteem in HDInsight. 

HDInsight is gebaseerd op Apache Hadoop en Hadoop-onderdelen, open source-technologieën die zijn ontwikkeld op Linux. Hallo Ubuntu Linux-distributie HDInsight versie 3.4 en hogere gebruikt als Hallo OS onderliggende voor Hallo-cluster. U kunt echter werken met HDInsight vanuit een Windows-client of een Windows-ontwikkelomgeving.

## <a name="use-powershell-for-deployment-and-management-tasks"></a>PowerShell gebruiken voor implementatie en beheer van taken
Azure PowerShell is een scriptomgeving toocontrol gebruik en implementatie en beheer van taken in HDInsight via Windows automatiseren.

Voorbeelden van taken die u met PowerShell uitvoeren kunt:

* [Maken van clusters met behulp van PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Uitvoeren van Hive-query's met behulp van PowerShell](hdinsight-hadoop-use-hive-powershell.md)
* [Clusters met PowerShell beheren](hdinsight-administer-use-powershell.md)

Volg de stappen te[Azure Powershell installeren en configureren](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooget Hallo meest recente versie. Als u scripts die toobe gewijzigd toouse Hallo nieuwe cmdlets voor Azure Resource Manager hebt moeten, raadpleegt u [tooAzure ontwikkeling Resource Manager gebaseerde hulpprogramma's voor HDInsight-clusters migreren](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="utilities-you-can-run-in-a-browser"></a>Hulpprogramma's die u kunt uitvoeren in een browser
Hallo hebben volgende hulpprogramma's een webgebruikersinterface die in een browser wordt uitgevoerd:
* **[Azure Cloud-Shell (preview)](https://docs.microsoft.com/azure/cloud-shell/quickstart)**  is een interactieve, opdrachtregel-shell die wordt uitgevoerd in uw browser en Hallo vanuit Azure-portal.
* **[Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md)**  is een beheer en controle hulpprogramma is beschikbaar in hello Azure-portal mag gebruikte toomanage verschillende soorten taken, zoals:
    * [Ambari Hello REST-API gebruiken](hdinsight-hadoop-manage-ambari-rest-api.md)
    * [Weergave in de Ambari hive](hdinsight-hadoop-use-hive-ambari-view.md)
    * [Tez-weergave in de Ambari](hdinsight-debug-ambari-tez-view.md)

## <a name="data-lake-hadoop-tools-for-visual-studio"></a>(Hadoop) van Data Lake Tools voor Visual Studio
Data Lake Tools voor Visual Studio toodeploy gebruiken en beheren van Storm-topologieën. Data Lake Tools installeert ook Hallo SCP.NET SDK, waarmee u toodevelop C# Storm-topologieën met Visual Studio.

Voordat u verdergaat toohello volgen voorbeelden, [installeren en probeer het Data Lake Tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md). 

Voorbeelden van taken die u met Visual Studio en Data Lake Tools voor Visual Studio doen kunt:
* [Implementeren en beheren van Storm-topologieën vanuit Visual Studio](hdinsight-storm-deploy-monitor-topology-linux.md)
* [C#-topologieën ontwikkelen voor Storm met Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md). Hallo bits voorbeeld sjablonen bevatten voor Storm-topologieën kunt u toodatabases, zoals Azure Cosmos DB en SQL-Database.

## <a name="visual-studio-and-hello-net-sdk"></a>Visual Studio en Hallo .NET SDK 

U kunt Visual Studio gebruiken met Hallo .NET SDK toomanage clusters en big data-toepassingen te ontwikkelen. U kunt andere IDE Hallo taken te volgen, maar voorbeelden worden weergegeven in Visual Studio.

Voorbeelden van taken die u met Hallo .NET SDK in Visual Studio doen kunt:
* [Clusters maken en gebruiken in HDInsight vanuit een .NET Framework-toepassing](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* [Uitvoeren van Hive-query's met behulp van Hallo .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [C# gebruiker gedefinieerde functies gebruiken met Hive en Pig streaming op Hadoop](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

> TIP als u .NET-oplossingen met HDInsight clusters op basis van Windows uitvoert, is het een goed moment tooplan een migratie tooLinux gebaseerde clusters. Zie voor meer informatie [migreren .NET-oplossing voor HDInsight op basis van Windows HDInsight op basis van tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="intellij-idea-and-eclipse-ide-for-spark-clusters"></a>Intellij IDEA en Eclipse IDE voor Spark-clusters
Beide [Intellij IDEA](https://www.jetbrains.com/idea/download) en Hallo [Eclipse IDE](https://www.eclipse.org/downloads/) kan worden gebruikt voor:
* Ontwikkelen en het verzenden van een Scala Spark-toepassing op een HDInsight Spark-cluster.
* Toegang tot bronnen van Spark-cluster.
* Ontwikkelen en een Scala Spark-toepassing lokaal uitvoeren.

Deze artikelen laten zien hoe: 
* Intellij IDEA: [maken Spark scala-toepassingen met behulp van hello Azure Toolkit voor Intellij-invoegtoepassing en Hallo Scala SDK.](hdinsight-apache-spark-intellij-tool-plugin.md)
* Eclipse IDE- of IDE Scala voor Eclipse: [maken Spark scala-toepassingen en hello Azure Toolkit voor Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) 


## <a name="notebooks-on-spark-for-data-scientists"></a>Notitieblokken op Spark voor gegevenswetenschappers 
Apache Spark-clusters in HDInsight omvat Zeppelin-notebooks en kernels die kunnen worden gebruikt met Jupyter-notebooks. 

* [Meer informatie over hoe toouse kernels op Spark-clusters met Jupyter-notebooks tootest Spark scala-toepassingen](hdinsight-apache-spark-zeppelin-notebook.md)
* [Meer informatie over hoe toouse Zeppelin-notebooks op Spark-clusters toorun Spark taken](hdinsight-apache-spark-jupyter-notebook-kernels.md) 


## <a name="run-linux-based-tools-and-technologies-on-windows"></a>Linux-gebaseerde hulpprogramma's en -technologieën in Windows worden uitgevoerd

Als u een situatie waarin moet u een hulpprogramma of de technologie die alleen beschikbaar op Linux tegenkomt, overweeg Hallo volgende opties:

* **Bash (bèta) op Windows 10** biedt een Linux-subsysteem in Windows. Bash kunt u toodirectly Linux-hulpprogramma's uitgevoerd zonder dat de toomaintain een speciale Linux-installatie. [Installeren en uitvoeren van Hallo Bash beta op Windows 10](https://msdn.microsoft.com/commandline/wsl/install_guide)
* **Docker voor Windows** toegang biedt toomany Linux-gebaseerde hulpprogramma's en rechtstreeks vanuit Windows kan worden uitgevoerd. U kunt bijvoorbeeld Docker toorun hello Beeline client gebruiken voor Hive rechtstreeks vanuit Windows. U kunt ook met Docker toorun een lokale Jupyter-notebook en tooSpark op HDInsight op afstand verbinding te maken. [Aan de slag met Docker voor Windows](https://docs.docker.com/docker-for-windows/)
* **[MobaXTerm](http://mobaxterm.mobatek.net/)**  kunt u toographically bladeren Hallo cluster-bestandssysteem via een SSH-verbinding.

## <a name="next-steps"></a>Volgende stappen
Als u nieuwe tooworking in op basis van Linux-clusters, Zie Hallo Volg artikelen:
* [Hadoop, Kafka, Spark of andere clusters instellen](hdinsight-hadoop-provision-linux-clusters.md)
* [Tips voor het HDInsight-clusters op Linux](hdinsight-hadoop-linux-information.md)