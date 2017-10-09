---
title: aaaMigrate uit HDInsight op basis van Windows tooLinux gebaseerde HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toomigrate van een HDInsight op basis van Windows cluster-tooa Linux gebaseerde HDInsight-cluster.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: ff35be59-bae3-42fd-9edc-77f0041bab93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 7e5e536e8672d7e7c3086c6860cec062d05eda65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-a-windows-based-hdinsight-cluster-tooa-linux-based-cluster"></a>Migreren van een HDInsight op basis van Windows cluster tooa op basis van Linux cluster

Dit document bevat informatie over Hallo verschillen tussen HDInsight op Windows- en Linux- en aanwijzingen over hoe toomigrate bestaande werkbelastingen tooa op basis van Linux-cluster.

Hoewel HDInsight op basis van Windows een eenvoudige manier toouse Hadoop in de cloud hello biedt, moet u mogelijk toomigrate tooa op basis van Linux-cluster. Bijvoorbeeld: tootake profiteren van Linux-gebaseerde hulpprogramma's en -technologieën die nodig voor uw oplossing zijn. Groot aantal dingen in Hadoop-ecosysteem Hallo op Linux gebaseerde systemen zijn ontwikkeld en mogelijk niet beschikbaar voor gebruik met HDInsight op basis van Windows. Bovendien veel boeken, video's en andere trainingsmateriaal wordt ervan uitgegaan dat u van een Linux-systeem gebruikmaakt bij het werken met Hadoop.

> [!NOTE]
> HDInsight-clusters gebruiken op lange termijn Ubuntu-ondersteuning (TNS) als besturingssysteem Hallo voor Hallo knooppunten in cluster Hallo. Zie voor informatie over het Hallo-versie van Ubuntu beschikbaar met HDInsight, samen met andere versiegegevens onderdeel, [HDInsight onderdeel versies](hdinsight-component-versioning.md).

## <a name="migration-tasks"></a>Migratietaken

Hallo algemene werkstroom voor de migratie is als volgt.

![Werkstroomdiagram van migratie](./media/hdinsight-migrate-from-windows-to-linux/workflow.png)

1. Elke sectie van dit document toounderstand wijzigingen die nodig zijn bij het migreren van uw bestaande werkstroom, taken, enz. tooa op basis van Linux cluster lezen.

2. Een cluster op basis van Linux maken als een test/quality assurance-omgeving. Zie voor meer informatie over het maken van een cluster op basis van Linux [clusters in HDInsight op basis van Linux maken](hdinsight-hadoop-provision-linux-clusters.md).

3. Kopie bestaande taken, de gegevensbronnen en de sinks toohello nieuwe omgeving.

4. Validatie toomake ervoor dat uw taken werken zoals verwacht op het nieuwe cluster Hallo testen uitvoeren.

Zodra u hebt gecontroleerd dat alles werkt zoals verwacht, plant u uitvaltijd voor Hallo-migratie. Tijdens deze uitvaltijd uit Hallo van de volgende activiteiten:

1. Back-up die lokaal zijn opgeslagen op de clusterknooppunten Hallo tijdelijke gegevens. Bijvoorbeeld, als u gegevens hebt opgeslagen rechtstreeks op een hoofdknooppunt.

2. Hallo op basis van Windows cluster verwijderen.

3. Maak een cluster op basis van Linux met behulp van dezelfde standaard gegevensopslag die op basis van Windows-cluster gebruikt Hallo Hallo. Hallo-cluster op basis van Linux kunt blijven werken met uw bestaande productiegegevens.

4. Importeer tijdelijke gegevens die u een back-up.

5. Start taken/doorgaan met het verwerken met behulp van het nieuwe cluster Hallo.

### <a name="copy-data-toohello-test-environment"></a>Kopiëren van gegevens toohello-testomgeving

Er zijn veel manieren toocopy Hallo gegevens en taken, Hallo eenvoudigste methoden toodirectly verplaatsen bestanden tooa testcluster echter Hallo twee besproken in deze sectie zijn.

#### <a name="hdfs-copy"></a>HDFS kopiëren

Volgende stappen toocopy gegevens uit Hallo cluster toohello test productiecluster hello gebruiken. Deze stappen wordt gebruik Hallo `hdfs dfs` hulpprogramma dat wordt meegeleverd met HDInsight.

1. Hallo storage-account en het standaard container informatie vinden voor het bestaande cluster. Hallo volgt PowerShell tooretrieve deze informatie wordt gebruikt:

    ```powershell
    $clusterName="Your existing HDInsight cluster name"
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    write-host "Storage account name: $clusterInfo.DefaultStorageAccount.split('.')[0]"
    write-host "Default container: $clusterInfo.DefaultStorageContainer"
    ```

2. een testomgeving toocreate stappen Hallo in Hallo maken Linux gebaseerde clusters in HDInsight-document. Stoppen voordat u Hallo-cluster maakt en selecteert u in plaats daarvan **optionele configuratie**.

3. Selecteer in de blade Hallo optionele configuratie **gekoppelde Storage-Accounts**.

4. Selecteer **opslag van een sleutel**, en wanneer u wordt gevraagd, selecteert u Hallo storage-account die is geretourneerd door Hallo PowerShell-script in stap 1. Klik op **Selecteer** op elk blade. Maak ten slotte Hallo-cluster.

5. Zodra het Hallo-cluster is gemaakt, verbinding maken met behulp van tooit **SSH.** Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

6. Gebruik van SSH-sessie hello, Hallo volgende opdrachtbestanden toocopy uit Hallo gekoppelde storage-account toohello nieuwe storage-standaardaccount. CONTAINER vervangen door Hallo container informatie geretourneerd door PowerShell. Vervang __ACCOUNT__ met Hallo-accountnaam. Hallo pad toodata vervangen door Hallo pad tooa-gegevensbestand.

    ```bash
    hdfs dfs -cp wasb://CONTAINER@ACCOUNT.blob.core.windows.net/path/to/old/data /path/to/new/location
    ```

    > [!NOTE]
    > Als het Hallo-mapstructuur die Hallo gegevens bevat, bestaat niet op Hallo testomgeving, kunt u met behulp van de volgende opdracht Hallo maken:

    ```bash
    hdfs dfs -mkdir -p /new/path/to/create
    ```

    Hallo `-p` schakelt u de Hallo maken van alle mappen in Hallo-pad.

#### <a name="direct-copy-between-blobs-in-azure-storage"></a>Directe kopiëren tussen blobs in Azure Storage

U kunt ook toouse hello `Start-AzureStorageBlobCopy` Azure PowerShell-cmdlet toocopy BLOB's tussen opslagaccounts buiten HDInsight. Zie voor meer informatie Hallo hoe toomanage Azure Blobs sectie van Azure PowerShell gebruiken met Azure Storage.

## <a name="client-side-technologies"></a>Client-side '-technologieën

Client-side '-technologieën zoals [Azure PowerShell-cmdlets](/powershell/azureps-cmdlets-docs), [Azure CLI](../cli-install-nodejs.md), of Hallo [.NET SDK voor Hadoop](https://hadoopsdk.codeplex.com/) toowork op basis van Linux-clusters worden voortgezet. Deze technologieën zijn afhankelijk van REST API's die zijn dezelfde Hallo beide typen OS-cluster.

## <a name="server-side-technologies"></a>Server-side technologieën

Hallo volgende tabel biedt richtlijnen voor migratie specifiek voor Windows zijn server-side-onderdelen.

| Als u van deze technologie gebruikmaakt... | Deze actie duren... |
| --- | --- |
| **PowerShell** (serverzijde scripts, met inbegrip van scriptacties gebruikt tijdens het maken van het cluster) |Herschrijf als Bash-scripts. Zie voor scriptacties, [HDInsight op basis van Linux aanpassen met scriptacties](hdinsight-hadoop-customize-cluster-linux.md) en [Scriptactieontwikkeling voor HDInsight op basis van Linux](hdinsight-hadoop-script-actions-linux.md). |
| **Azure CLI** (serverzijde scripts) |Hello Azure CLI is beschikbaar op Linux, is niet afkomstig vooraf worden geïnstalleerd op HDInsight-cluster hoofdknooppunten Hallo. Zie voor meer informatie over het installeren van hello Azure CLI [aan de slag met Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli). |
| **.NET-onderdelen** |.NET wordt ondersteund op Linux gebaseerde HDInsight via [Mono](https://mono-project.com). Zie voor meer informatie [oplossingen migreren .NET HDInsight op basis van tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md). |
| **Win32-onderdelen of andere alleen Windows technologie** |Richtlijnen, is afhankelijk van Hallo-onderdeel of technologie. Hebt u mogelijk kunnen toofind een versie die compatibel is met Linux of of u kunt mogelijk toofind een alternatieve oplossing herschrijven van dit onderdeel. |

> [!IMPORTANT]
> Hallo HDInsight management SDK is niet volledig compatibel is met Mono. Deze mag niet worden gebruikt als onderdeel van de oplossingen geïmplementeerd toohello HDInsight-cluster op dit moment.

## <a name="cluster-creation"></a>Maken van het cluster

Deze sectie bevat informatie over de verschillen in het maken van het cluster.

### <a name="ssh-user"></a>SSH gebruiker

Linux gebaseerde HDInsight-clusters gebruiken Hallo **Secure Shell (SSH)** protocol tooprovide RAS toohello clusterknooppunten. In tegenstelling tot extern bureaublad voor Windows gebaseerde clusters bieden meeste SSH-clients geen een grafische gebruikersinterface. SSH-clients bieden in plaats daarvan een opdrachtregel waarmee u toorun opdrachten op Hallo-cluster. Sommige clients (zoals [MobaXterm](http://mobaxterm.mobatek.net/)) bieden een browser grafische file system in toevoeging tooa extern vanaf de opdrachtregel.

Tijdens het maken, moet u een SSH-gebruiker en een opgeven een **wachtwoord** of **openbare-sleutelcertificaat** voor verificatie.

Wordt u aangeraden openbare-sleutelcertificaat, omdat het is veiliger dan een wachtwoord te gebruiken. Verificatie via certificaat werkt door een ondertekende openbaar/persoonlijk sleutelpaar genereren en vervolgens de openbare sleutel Hallo bieden bij het Hallo-cluster maken. Wanneer u verbinding maakt met behulp van SSH toohello-server, biedt Hallo persoonlijke sleutel op Hallo client verificatie voor Hallo-verbinding.

Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

### <a name="cluster-customization"></a>Aanpassing van het cluster

**Acties script** gebruikt met clusters op basis van Linux in Bash-scripts moeten worden geschreven. Terwijl scriptacties kan worden gebruikt tijdens het maken van het cluster voor Linux gebaseerde clusters die ze kunnen ook gebruikte tooperform aanpassing worden nadat een cluster actief is en die wordt uitgevoerd. Zie voor meer informatie [HDInsight op basis van Linux aanpassen met scriptacties](hdinsight-hadoop-customize-cluster-linux.md) en [Scriptactieontwikkeling voor HDInsight op basis van Linux](hdinsight-hadoop-script-actions-linux.md).

Een andere aanpassing-functie is **bootstrap**. Voor Windows-clusters is deze functie kunt u toospecify Hallo locatie van aanvullende bibliotheken voor gebruik met Hive. Na het maken van het cluster deze bibliotheken zijn automatisch beschikbaar voor gebruik met Hive-query's zonder Hallo nodig toouse `ADD JAR`.

Hallo Bootstrap functie voor op basis van Linux-clusters biedt deze functionaliteit niet. Gebruik in plaats daarvan scriptactie gedocumenteerd in [toevoegen Hive-bibliotheken tijdens het maken van het cluster](hdinsight-hadoop-add-hive-libraries.md).

### <a name="virtual-networks"></a>Virtuele netwerken

HDInsight op basis van Windows-clusters alleen werken met klassieke virtuele netwerken, terwijl Linux gebaseerde HDInsight-clusters Resource Manager virtuele netwerken vereisen. Als u resources hebt een klassiek virtueel netwerk die Hallo Linux-HDInsight-cluster moet verbinding maken met, Zie [verbinding maken met een klassiek virtueel netwerk tooa Resource Manager virtueel netwerk](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

Zie voor meer informatie over de configuratievereisten voor het gebruik van Azure Virtual Networks met HDInsight, [mogelijkheden uitbreiden HDInsight met behulp van een virtueel netwerk](hdinsight-extend-hadoop-virtual-network.md).

## <a name="management-and-monitoring"></a>Beheer en controle

Veel van Hallo web UI die u in combinatie met HDInsight op basis van Windows zoals Taakgeschiedenis of de gebruikersinterface van Yarn gebruikt zijn beschikbaar via Ambari. Bovendien biedt Hallo Ambari Hive-weergave een manier toorun Hive-query's via uw webbrowser. Hallo Ambari-Webgebruikersinterface is beschikbaar op Linux gebaseerde clusters op https://CLUSTERNAME.azurehdinsight.net.

Zie voor meer informatie over het werken met Ambari Hallo documenten te volgen:

* [Ambari Web](hdinsight-hadoop-manage-ambari.md)
* [Ambari REST-API](hdinsight-hadoop-manage-ambari-rest-api.md)

### <a name="ambari-alerts"></a>Ambari-waarschuwingen

Ambari is een waarschuwing systeem waarmee u mogelijke problemen met het Hallo-cluster. Waarschuwingen worden weergegeven als rood of geel vermeldingen in Hallo Ambari-Webgebruikersinterface, maar u ze ook via Hallo REST-API ophalen kunt.

> [!IMPORTANT]
> Ambari waarschuwingen geven aan dat er *mogelijk* is er een probleem niet dat er *is* een probleem. Bijvoorbeeld, verschijnt een waarschuwing dat HiveServer2 kan niet worden geopend, zelfs als u toegang hebt tot het normaal.
>
> Veel waarschuwingen worden geïmplementeerd als op interval gebaseerde query uitgevoerd naar een service en een reactie binnen een specifiek tijdsbestek verwachten. Dus Hallo waarschuwing niet noodzakelijkerwijs dat Hallo-service niet actief is, alleen dat niet het retourneren van resultaten binnen het tijdsbestek Hallo verwacht.

U moet evalueren of een waarschuwing heeft gedurende lange tijd is optreedt of problemen van gebruikers die zijn gerapporteerd weerspiegelt voordat deze actie te ondernemen.

## <a name="file-system-locations"></a>De locaties van systeem

Hallo Linux cluster bestandssysteem worden anders dan Windows gebaseerde HDInsight-clusters verspreid. Hallo volgende tabel toofind gebruikte bestanden gebruiken.

| Ik moet toofind... | Deze bevindt zich... |
| --- | --- |
| Configuratie |`/etc`. Bijvoorbeeld: `/etc/hadoop/conf/core-site.xml` |
| Logboekbestanden |`/var/logs` |
| Hortonworks Data Platform HDP) |`/usr/hdp`. Er zijn twee directory's die u hier, een Hallo huidige HDP versie en `current`. Hallo `current` map symbolische koppelingen toofiles en mappen die zich in Hallo versie nummer map bevat. Hallo `current` directory is opgegeven als een handige manier toegang krijgen tot HDP bestanden sinds Hallo versie verandert als Hallo HDP versie is bijgewerkt. |
| hadoop-streaming.jar |`/usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar` |

Als u Hallo-naam van bestand Hallo weet, kunt u in het algemeen Hallo volgende opdracht uit een SSH-sessie toofind Hallo-bestandspad gebruiken:

    find / -name FILENAME 2>/dev/null

U kunt ook jokertekens gebruiken met Hallo-bestandsnaam. Bijvoorbeeld, `find / -name *streaming*.jar 2>/dev/null` retourneert Hallo pad tooany jar-bestanden met Hallo woord streaming als onderdeel van het Hallo-bestandsnaam.

## <a name="hive-pig-and-mapreduce"></a>Hive, Pig en MapReduce

Pig en MapReduce-belastingen lijken op Linux gebaseerde clusters. Linux gebaseerde HDInsight-clusters kunnen echter worden gemaakt met een nieuwere versie van Hadoop Hive en Pig. Deze verschillen tussen versies kunnen leiden tot wijzigingen in hoe uw bestaande oplossingen-functie. Zie voor meer informatie over Hallo versies van onderdelen in HDInsight [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md).

Linux gebaseerde HDInsight biedt geen functionaliteit voor extern bureaublad. In plaats daarvan kunt u SSH tooremotely toohello van head clusterknooppunten verbinden. Zie voor meer informatie Hallo documenten te volgen:

* [Hive gebruiken met SSH](hdinsight-hadoop-use-hive-ssh.md)
* [Pig gebruiken met SSH](hdinsight-hadoop-use-pig-ssh.md)
* [U MapReduce gebruikt met SSH](hdinsight-hadoop-use-mapreduce-ssh.md)

### <a name="hive"></a>Hive

> [!IMPORTANT]
> Als u een externe Hive-metastore gebruikt, moet u back-up Hallo metastore voordat u deze gebruikt met HDInsight op basis van Linux. HDInsight op basis van Linux is beschikbaar met nieuwere versies van Hive, die mogelijk incompatibel met metastores gemaakt met eerdere versies.

Hallo volgende diagram biedt richtlijnen voor het migreren van uw Hive-werkbelastingen.

| Op Windows gebaseerde ik gebruik... | Op Linux gebaseerde... |
| --- | --- |
| **Hive-Editor** |[Weergave in de Ambari hive](hdinsight-hadoop-use-hive-ambari-view.md) |
| `set hive.execution.engine=tez;`tooenable Tez |Tez is Hallo standaard engine voor het uitvoeren voor op basis van Linux-clusters, zodat Hallo instellen instructie is niet meer nodig. |
| C# gebruiker gedefinieerde functies | Zie voor informatie over het valideren van C#-onderdelen met HDInsight op basis van Linux, [oplossingen migreren .NET HDInsight op basis van tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD-bestanden of scripts op Hallo-server als onderdeel van een Hive-taak wordt aangeroepen |Bash-scripts gebruiken |
| `hive`de opdracht van een extern bureaublad |Gebruik [Beeline](hdinsight-hadoop-use-hive-beeline.md) of [Hive van een SSH-sessie](hdinsight-hadoop-use-hive-ssh.md) |

### <a name="pig"></a>Pig

| Op Windows gebaseerde ik gebruik... | Op Linux gebaseerde... |
| --- | --- |
| C# gebruiker gedefinieerde functies | Zie voor informatie over het valideren van C#-onderdelen met HDInsight op basis van Linux, [oplossingen migreren .NET HDInsight op basis van tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD-bestanden of scripts op Hallo-server als onderdeel van een Pig-taak wordt aangeroepen |Bash-scripts gebruiken |

### <a name="mapreduce"></a>MapReduce

| Op Windows gebaseerde ik gebruik... | Op Linux gebaseerde... |
| --- | --- |
| C# toewijzen en reducer-onderdelen | Zie voor informatie over het valideren van C#-onderdelen met HDInsight op basis van Linux, [oplossingen migreren .NET HDInsight op basis van tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD-bestanden of scripts op Hallo-server als onderdeel van een Hive-taak wordt aangeroepen |Bash-scripts gebruiken |

## <a name="oozie"></a>Oozie

> [!IMPORTANT]
> Als u een externe Oozie-metastore gebruikt, moet u back-up Hallo metastore voordat u deze gebruikt met HDInsight op basis van Linux. HDInsight op basis van Linux is beschikbaar met nieuwere versies van Oozie, die mogelijk incompatibel met metastores gemaakt met eerdere versies.

Oozie werkstromen shell acties voor toestaan. Shell-acties Hallo standaardshell voor Hallo besturingssysteem toorun opdrachtregelopdrachten gebruiken. Als u Oozie-werkstromen die afhankelijk van Windows-shell Hallo zijn hebt, moet u Hallo werkstromen toorely op Hallo Linux shell-omgeving (Bash) herschrijven. Zie voor meer informatie over het gebruik van de shell-acties met Oozie [Oozie actie shelluitbreiding](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html).

Als u Oozie-werkstromen die afhankelijk van C#-toepassingen die wordt opgeroepen via de shell acties zijn hebt, moet u deze toepassingen in een omgeving met Linux valideren. Zie voor meer informatie [oplossingen migreren .NET HDInsight op basis van tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="storm"></a>Storm

| Op Windows gebaseerde ik gebruik... | Op Linux gebaseerde... |
| --- | --- |
| Storm-Dashboard |Hallo Storm-Dashboard is niet beschikbaar. Zie [implementeren en beheren van Storm-topologieën op Linux gebaseerde HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md) voor topologieën met manieren toosubmit |
| Storm-gebruikersinterface |Hallo Storm-gebruikersinterface is beschikbaar op https://CLUSTERNAME.azurehdinsight.NET/stormui |
| Visual Studio toocreate, implementeren en beheren van C# of hybride topologieën |Visual Studio kunt gebruikte toocreate worden, implementeren en beheren van C# (SCP.NET) of hybride topologieën op Linux gebaseerde Storm op HDInsight-clusters die zijn gemaakt na 28-10-2016. |

## <a name="hbase"></a>HBase

Op Linux gebaseerde clusters Hallo znode bovenliggende voor HBase is `/hbase-unsecure`. Stel deze waarde in de configuratie Hallo voor Java-clienttoepassingen die gebruikmaken van systeemeigen HBase Java-API.

Zie [een HBase op basis van Java-toepassing bouwt](hdinsight-hbase-build-java-maven.md) voor een voorbeeld van de client die deze waarde wordt ingesteld.

## <a name="spark"></a>Spark

Spark-clusters zijn beschikbaar op Windows-clusters tijdens de preview. Spark GA is alleen beschikbaar bij op basis van Linux-clusters. Er is geen migratiepad van een op basis van Windows Spark preview cluster tooa release op basis van Linux Spark-cluster.

## <a name="known-issues"></a>Bekende problemen

### <a name="azure-data-factory-custom-net-activities"></a>Azure Data Factory aangepaste .NET-activiteiten

Azure Data Factory aangepaste .NET-activiteiten worden momenteel niet ondersteund op Linux gebaseerde HDInsight-clusters. In plaats daarvan moet u een van de Hallo methoden tooimplement aangepaste activiteiten volgen als onderdeel van uw ADF-pijplijn.

* .NET-activiteiten niet uitvoeren op Azure Batch-pool. Zie Hallo gebruik Azure Batch gekoppelde service sectie [aangepaste activiteiten gebruiken in een Azure Data Factory-pijplijn](../data-factory/data-factory-use-custom-activities.md)
* Hallo-activiteit als een MapReduce-activiteit worden geïmplementeerd. Zie voor meer informatie [MapReduce-programma's uit Data Factory aanroepen](../data-factory/data-factory-map-reduce.md).

### <a name="line-endings"></a>Regeleinden

In het algemeen gebruik regeleinden op Windows-systemen bij van CRLF, op basis van Linux-systemen LF gebruiken. Als u produceren, of van plan, gegevens met regeleinden CRLF bent, moet u mogelijk toomodify Hallo producenten en consumenten toowork met Hallo LF regel eindigt.

Bijvoorbeeld, retourneert met behulp van Azure PowerShell tooquery HDInsight op een cluster met Windows-gegevens met CRLF. Hallo retourneert dezelfde query met een cluster op basis van Linux LF. U moet toosee testen als Hallo regel beëindigen zorgt ervoor een probleem met uw solutuion voordat u migreert dat tooa op basis van Linux-cluster.

Als u scripts die rechtstreeks op Hallo Linux-clusterknooppunten worden uitgevoerd hebt, moet u altijd LF gebruiken als Hallo regel beëindigen. Als u CRLF gebruikt, kunt u misschien fouten ziet wanneer Hallo scripts uitgevoerd op een cluster op basis van Linux.

Als u Hallo scripts bevatten geen tekenreeksen met ingesloten CR tekens weet, kunt u met een van de volgende methoden Hallo Hallo-regeleinden voor wijziging bulksgewijs:

* **Voordat u uploadt toohello cluster**: gebruik Hallo volgende PowerShell-instructies toochange Hallo-regeleinden uit CRLF tooLF voordat u uploadt Hallo script toohello cluster.

    ```powershell
    $original_file ='c:\path\to\script.py'
    $text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
    [IO.File]::WriteAllText($original_file, $text)
    ```

* **Na het uploaden van toohello cluster**: gebruik Hallo volgende opdracht uit vanaf een SSH-sessie toohello cluster op basis van Linux toomodify Hallo script.

    ```bash
    hdfs dfs -get wasb:///path/to/script.py oldscript.py
    tr -d '\r' < oldscript.py > script.py
    hdfs dfs -put -f script.py wasb:///path/to/script.py
    ```

## <a name="next-steps"></a>Volgende stappen

* [Meer informatie over hoe toocreate Linux gebaseerde HDInsight-clusters](hdinsight-hadoop-provision-linux-clusters.md)
* [SSH tooconnect tooHDInsight gebruiken](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Beheer op basis van Linux clusters met Ambari](hdinsight-hadoop-manage-ambari.md)
