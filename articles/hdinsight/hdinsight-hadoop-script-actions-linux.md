---
title: ontwikkeling van een actie met HDInsight op basis van Linux - Azure aaaScript | Microsoft Docs
description: "Meer informatie over hoe toouse Bash scripts toocustomize Linux gebaseerde HDInsight-clusters. Hallo script actie functie van HDInsight kunt u toorun scripts tijdens of na het maken van het cluster. Scripts kunnen worden gebruikt toochange cluster configuratie-instellingen of andere software geïnstalleerd."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a>Scripts actie te ontwikkelen met HDInsight

Meer informatie over hoe toocustomize uw HDInsight-cluster met Bash scripts. Scriptacties zijn een manier toocustomize HDInsight tijdens of na het maken van het cluster.

> [!IMPORTANT]
> Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="what-are-script-actions"></a>Wat zijn scriptacties

Scriptacties Bash-scripts die Azure wordt uitgevoerd op Hallo cluster knooppunten toomake-configuratiewijzigingen zijn of software installeren. Een scriptactie wordt uitgevoerd als basis- en biedt volledige toegang rechten toohello clusterknooppunten.

Scriptacties kunnen worden toegepast met de volgende methoden Hallo:

| Gebruik deze methode tooapply een script... | Tijdens het cluster maken... | Op een cluster uitgevoerd... |
| --- |:---:|:---:|
| Azure Portal |✓ |✓ |
| Azure PowerShell |✓ |✓ |
| Azure CLI |&nbsp; |✓ |
| HDInsight .NET-SDK |✓ |✓ |
| Azure Resource Manager-sjabloon |✓ |&nbsp; |

Zie voor meer informatie over het gebruik van deze methoden tooapply scriptacties [aanpassen HDInsight-clusters met behulp van scriptacties](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="bestPracticeScripting"></a>Aanbevolen procedures voor het ontwikkelen van scripts

Wanneer u een aangepast script voor een HDInsight-cluster ontwikkelt, zijn er enkele aanbevolen procedures tookeep rekening:

* [Doelversie Hallo Hadoop](#bPS1)
* [Doel Hallo versie van het besturingssysteem](#bps10)
* [Geef stabiel koppelingen tooscript resources](#bPS2)
* [Vooraf gecompileerde resources gebruiken](#bPS4)
* [Zorg ervoor dat Hallo cluster aanpassing script idempotent](#bPS3)
* [Zorg ervoor dat hoge beschikbaarheid van Hallo cluster-architectuur](#bPS5)
* [Hallo aangepaste onderdelen toouse Azure Blob-opslag configureren](#bPS6)
* [Schrijven van gegevens tooSTDOUT en STDERR](#bPS7)
* [ASCII-bestanden opslaan met regeleinden LF](#bps8)
* [Probeer het opnieuw logica toorecover van tijdelijke fouten gebruiken](#bps9)

> [!IMPORTANT]
> Scriptacties moeten worden voltooid binnen 60 minuten of Hallo mislukt. Tijdens het inrichten van knooppunt voert Hallo script tegelijk met andere processen installatie en configuratie. Concurrentie voor resources, zoals CPU-tijd of netwerk bandbreedte mogelijk Hallo script tootake langer toofinish dan in uw ontwikkelomgeving.

### <a name="bPS1"></a>Doelversie Hallo Hadoop

Verschillende versies van HDInsight hebben verschillende versies van Hadoop-services en -onderdelen geïnstalleerd. Als uw script een specifieke versie van een service of het onderdeel verwacht, moet u alleen Hallo script gebruiken met Hallo-versie van HDInsight die Hallo vereiste onderdelen. Vindt u informatie over het onderdeel-versies die zijn opgenomen in HDInsight met behulp van Hallo [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md) document.

### <a name="bps10"></a>Hallo OS doelversie

Linux gebaseerde HDInsight is gebaseerd op Hallo Ubuntu Linux-distributie. Verschillende versies van HDInsight, is afhankelijk van verschillende versies van Ubuntu, die de werking van uw script kunnen wijzigen. Bijvoorbeeld, HDInsight 3,4 en eerder zijn gebaseerd op Ubuntu-versies die Upstart gebruiken. Versie 3.5 is gebaseerd op Ubuntu 16.04 dat gebruikmaakt van Systemd. Systemd en Upstart zijn afhankelijk van andere opdrachten, zodat uw script toowork met beide moet worden geschreven.

HDInsight 3.4 en 3.5 nog een belangrijk verschil is dat `JAVA_HOME` tooJava 8 nu verwijst.

U kunt Hallo OS-versie controleren met behulp van `lsb_release`. Hallo volgende code laat zien hoe toodetermine als hello script wordt uitgevoerd op Ubuntu 14 of 16:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

U vindt de volledige Hallo-script dat deze fragmenten op https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh bevat.

Zie voor Hallo-versie van Ubuntu die wordt gebruikt door HDInsight hello [HDInsight componentversie](hdinsight-component-versioning.md) document.

toounderstand hello verschillen tussen Systemd en Upstart, Zie [Systemd voor Upstart gebruikers](https://wiki.ubuntu.com/SystemdForUpstartUsers).

### <a name="bPS2"></a>Geef stabiel koppelingen tooscript resources

Hallo moeten-script en de bijbehorende resources blijven beschikbaar tijdens de levensduur Hallo van Hallo-cluster. Deze resources zijn vereist als er nieuwe knooppunten toohello cluster worden toegevoegd tijdens het schalen van bewerkingen.

Hallo aanbevolen procedure is toodownload en archiveren alles in een Azure Storage-account voor uw abonnement.

> [!IMPORTANT]
> Hallo storage-account gebruikt moet Hallo storage-standaardaccount voor Hallo cluster of een openbare, alleen-lezen container op andere storage-account.

Bijvoorbeeld, Hallo voorbeelden geleverd door Microsoft worden opgeslagen in Hallo [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage-account. Dit is een openbaar, alleen-lezen container onderhouden door Hallo HDInsight-team.

### <a name="bPS4"></a>Vooraf gecompileerde resources gebruiken

tooreduce Hallo tijd het duurt toorun Hallo script, te voorkomen dat de bewerkingen die bronnen van broncode compileren. Bijvoorbeeld, vooraf gecompileerd bronnen en op te slaan in een blob van Azure Storage-account in Hallo hetzelfde Datacenter als HDInsight.

### <a name="bPS3"></a>Zorg ervoor dat Hallo cluster aanpassing script idempotent

Scripts moet idempotent. Als geeft Hallo script meerdere keren wordt uitgevoerd, moet retourneren Hallo cluster toohello gelijk elke keer status.

Bijvoorbeeld dat een script dat wordt gewijzigd van configuratiebestanden geen dubbele vermeldingen moet toevoegen als meerdere keren uitgevoerd.

### <a name="bPS5"></a>Zorg ervoor dat hoge beschikbaarheid van Hallo cluster-architectuur

Linux gebaseerde HDInsight-clusters bieden twee hoofdknooppunten die actief zijn binnen Hallo-cluster, en scriptacties uitgevoerd op beide knooppunten. Als Hallo-onderdelen die u installeert slechts één hoofdknooppunt verwacht, Installeer geen Hallo-onderdelen op beide hoofdknooppunten.

> [!IMPORTANT]
> Services die worden geleverd als onderdeel van HDInsight zijn ontworpen toofail over tussen de twee hoofdknooppunten Hallo indien nodig. Deze functionaliteit is niet uitgebreid toocustom onderdelen zijn geïnstalleerd via scriptacties. Als u hoge beschikbaarheid voor aangepaste onderdelen nodig hebt, moet u uw eigen mechanisme failover implementeren.

### <a name="bPS6"></a>Hallo aangepaste onderdelen toouse Azure Blob-opslag configureren

Onderdelen die u op Hallo cluster installeert wellicht een standaardconfiguratie waarmee Hadoop Distributed File System (HDFS) opslag gebruikt. HDInsight gebruikt Azure Storage of de Data Lake Store als Hallo standaard opslag. Beide bieden een HDFS-compatibel bestandssysteem dat gegevens behouden blijft zelfs als het Hallo-cluster is verwijderd. Mogelijk moet u tooconfigure onderdelen die u installeert toouse WASB of ADL in plaats van HDFS.

Voor de meeste bewerkingen hoeft u geen toospecify Hallo-bestandssysteem. Hallo volgende wordt bijvoorbeeld Hallo giraph examples.jar-bestand van Hallo lokale systeem toocluster bestandsopslag gekopieerd:

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

In dit voorbeeld Hallo `hdfs` opdracht transparant Hallo standaard clusteropslag gebruikt. Voor bepaalde bewerkingen moet u toospecify Hallo URI. Bijvoorbeeld: `adl:///example/jars` voor Data Lake Store of `wasb:///example/jars` voor Azure Storage.

### <a name="bPS7"></a>Schrijven van gegevens tooSTDOUT en STDERR

HDInsight uitvoer van het script dat is geschreven tooSTDOUT en STDERR registreert. U kunt deze gegevens door middel van Hallo Ambari-webgebruikersinterface weergeven.

> [!NOTE]
> Ambari is alleen beschikbaar als het Hallo-cluster is gemaakt. Als u een scriptactie tijdens het maken van het cluster en mislukt het maken, Zie sectie troubleshooting Hallo [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) voor andere manieren van de toegang tot geregistreerde gegevens.

De meeste hulpprogramma's en installatiepakketten schrijven al informatie tooSTDOUT en STDERR, maar u aanvullende logboekregistratie tooadd kunt. toosend tekst tooSTDOUT, gebruik `echo`. Bijvoorbeeld:

```bash
echo "Getting ready tooinstall Foo"
```

Standaard `echo` verzendt Hallo tooSTDOUT tekenreeks. toodirect het tooSTDERR, Voeg `>&2` voordat `echo`. Bijvoorbeeld:

```bash
>&2 echo "An error occurred installing Foo"
```

Dit leidt informatie tooSTDOUT tooSTDERR (2) in plaats daarvan wordt geschreven. Zie voor meer informatie over i/o-omleiding [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).

Zie voor meer informatie over het weergeven van informatie die wordt geregistreerd door scriptacties [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)

### <a name="bps8"></a>ASCII-bestanden opslaan met regeleinden LF

Bash-scripts moeten worden opgeslagen als ASCII-indeling met regels die door LF is beëindigd. Bestanden die worden opgeslagen als UTF-8 of CRLF gebruiken als Hallo regel beëindigen kunnen mislukken met de volgende fout Hallo:

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <a name="bps9"></a>Probeer het opnieuw logica toorecover van tijdelijke fouten gebruiken

Bij het downloaden van bestanden met apt get- of andere acties die verzenden van gegevens over pakketten installeren Hallo van internet, Hallo-actie kan mislukken omdat tootransient netwerkfouten. Bijvoorbeeld, Hallo externe resource die u communiceert mogelijk Hallo-proces mislukt over tooa back-knooppunt.

toomake uw robuuste tootransient scriptfouten u Pogingslogica kunt implementeren. Hallo volgen functie laat zien hoe tooimplement Pogingslogica. Het opnieuw probeert Hallo bewerking driemaal voordat deze is mislukt.

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

Hallo volgende voorbeelden laten zien hoe toouse deze functie.

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <a name="helpermethods"></a>Help-methoden voor aangepaste scripts

Script actie Help-methoden zijn hulpprogramma's die u gebruiken kunt bij het schrijven van aangepaste scripts. Deze methoden zijn opgenomen in de[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script. Gebruik Hallo toodownload te volgen en ze als onderdeel van uw script gebruiken:

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

Hallo helpers beschikbaar voor gebruik in uw script te volgen:

| Gebruik helper | Beschrijving |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |Een bestand wordt gedownload van Hallo URI toohello opgegeven bronbestandspad. Standaard wordt er een bestaand bestand niet overschreven. |
| `untar_file TARFILE DESTDIR` |Extraheert een tar-bestand (met behulp van `-xf`) toohello doelmap. |
| `test_is_headnode` |Indien uitgevoerd op een cluster hoofdknooppunt, return 1; anders wordt 0. |
| `test_is_datanode` |Als het huidige knooppunt Hallo gegevensknooppunt (worker) is, retourneert een 1; anders wordt 0. |
| `test_is_first_datanode` |Als het huidige knooppunt Hallo Hallo eerste gegevens (worker) knooppunt (benoemde workernode0) retourneren een 1; anders wordt 0. |
| `get_headnodes` |Hallo volledig gekwalificeerde domeinnaam van Hallo headnodes in Hallo cluster retourneren. De namen zijn gescheiden door komma's. Een lege tekenreeks geretourneerd bij fout. |
| `get_primary_headnode` |Hallo volledig gekwalificeerde domeinnaam van de primaire headnode Hallo opgehaald. Een lege tekenreeks geretourneerd bij fout. |
| `get_secondary_headnode` |Hallo volledig gekwalificeerde domeinnaam van de secundaire headnode Hallo opgehaald. Een lege tekenreeks geretourneerd bij fout. |
| `get_primary_headnode_number` |Hallo numeriek achtervoegsel van primaire headnode Hallo opgehaald. Een lege tekenreeks geretourneerd bij fout. |
| `get_secondary_headnode_number` |Hallo numeriek achtervoegsel van de secundaire headnode Hallo opgehaald. Een lege tekenreeks geretourneerd bij fout. |

## <a name="commonusage"></a>Algemene gebruikspatronen

Deze sectie bevat richtlijnen over het implementeren van een aantal Hallo algemene gebruikspatronen die u tegenkomen kunt tijdens het schrijven van uw eigen aangepaste scripts.

### <a name="passing-parameters-tooa-script"></a>Parameters doorgeven tooa script

In sommige gevallen kan het script parameters vereist. Bijvoorbeeld, moet u mogelijk Hallo beheerderswachtwoord voor Hallo cluster bij gebruik van Hallo Ambari REST-API.

Toohello script doorgegeven parameters worden aangeduid als *positieparameters*, en te worden toegewezen`$1` voor de eerste parameter Hallo `$2` voor Hallo tweede en dus eenmalige aanmelding. `$0`bevat de naam Hallo van Hallo script zelf.

Toohello script als parameters doorgegeven waarden moeten tussen enkele aanhalingstekens ('). Hiermee zorgt u ervoor dat Hallo doorgegeven waarde wordt behandeld als een letterlijke waarde.

### <a name="setting-environment-variables"></a>Omgevingsvariabelen instellen

Instellen van een omgevingsvariabele wordt uitgevoerd door de volgende instructie Hallo:

    VARIABLENAME=value

Waarbij VARIABELENAAM Hallo-naam van Hallo variabele is. tooaccess Hallo-variabele, gebruik `$VARIABLENAME`. Bijvoorbeeld tooassign een waarde die door een positionele parameter als een omgevingsvariabele met de naam wachtwoord, gebruikt u Hallo-instructie:

    PASSWORD=$1

Daaropvolgende toegang toohello informatie kunt vervolgens `$PASSWORD`.

Omgevingsvariabelen ingesteld binnen Hallo script bestaan alleen binnen bereik Hallo van Hallo-script. In sommige gevallen moet u tooadd hele systeem omgevingsvariabelen die blijft van kracht nadat Hallo-script is voltooid. het hele systeem omgevingsvariabelen tooadd, Hallo variabele te toevoegen`/etc/environment`. Hallo-instructie wordt bijvoorbeeld toegevoegd `HADOOP_CONF_DIR`:

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Toegang tot toolocations waar Hallo aangepaste scripts worden opgeslagen

Scripts die worden gebruikt toocustomize een cluster moet toobe opgeslagen in een van de volgende locaties Hallo:

* Een __Azure Storage-account__ dat is gekoppeld aan het Hallo-cluster.

* Een __extra opslagaccount__ die zijn gekoppeld aan het Hallo-cluster.

* Een __openbaar leesbaar URI__. Bijvoorbeeld, een URL toodata opgeslagen op OneDrive, Dropbox of andere hostingservice bestand.

* Een __Azure Data Lake Store-account__ dat is gekoppeld aan Hallo HDInsight-cluster. Zie voor meer informatie over het gebruik van Azure Data Lake Store met HDInsight [een HDInsight-cluster maken met Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    > [!NOTE]
    > Hallo service principal HDInsight maakt gebruik van tooaccess Data Lake Store moet leestoegang toohello script hebben.

Resources die worden gebruikt door Hallo script moeten ook openbaar beschikbaar zijn.

Hallo-bestanden opslaan in een Azure Storage-account of een Azure Data Lake Store biedt snel toegang, als beide binnen hello Azure-netwerk.

> [!NOTE]
> Hallo URI-indeling gebruikt tooreference Hallo script is afhankelijk van Hallo-service wordt gebruikt. Gebruik voor storage-accounts die zijn gekoppeld aan de HDInsight-cluster Hallo `wasb://` of `wasbs://`. Gebruik voor openbaar leesbaar URI `http://` of `https://`. Gebruik voor Data Lake Store `adl://`.

### <a name="checking-hello-operating-system-version"></a>Hallo-besturingssysteemversie controleren

Verschillende versies van HDInsight, is afhankelijk van specifieke versies van Ubuntu. Mogelijk zijn er verschillen tussen versies van het besturingssysteem die u in uw script controleren moet. U moet mogelijk een binair bestand dat is gebonden toohello versie van Ubuntu tooinstall.

toocheck hello OS-versie, gebruik `lsb_release`. Bijvoorbeeld toont Hallo volgende script hoe tooreference een specifieke tar-bestand, afhankelijk van de versie van het besturingssysteem Hallo:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <a name="deployScript"></a>Controlelijst voor het implementeren van een scriptactie

Hier volgen Hallo stappen werd bij het voorbereiden van toodeploy deze scripts:

* Hallo-bestanden met aangepaste scripts op een locatie die toegankelijk is voor de clusterknooppunten Hallo tijdens de implementatie van Hallo plaatsen. Bijvoorbeeld, Hallo standaard opslag voor Hallo-cluster. Bestanden kunnen ook worden opgeslagen in openbaar leesbaar hosting-services.
* Controleer of Hallo script impotent. Hierdoor kunnen de Hallo script toobe uitgevoerd meerdere keren op Hallo hetzelfde knooppunt.
* Gebruik een tijdelijk bestand directory map tookeep Hallo gedownloade bestanden gebruikt door Hallo scripts en vervolgens opschonen van nadat scripts hebt uitgevoerd.
* Als de OS-niveau instellingen of configuratiebestanden voor Hadoop-service zijn gewijzigd, kunt u toorestart HDInsight services.

## <a name="runScriptAction"></a>Hoe een scriptactie toorun

U kunt script acties toocustomize HDInsight-clusters met behulp van de volgende methoden hello gebruiken:

* Azure Portal
* Azure PowerShell
* Azure Resource Manager-sjablonen
* Hello HDInsight .NET SDK.

Zie voor meer informatie over het gebruik van elke methode [hoe toouse actie script](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="sampleScripts"></a>Aangepast script-voorbeelden

Microsoft biedt voorbeeldscripts tooinstall onderdelen op een HDInsight-cluster. Zie de volgende koppelingen voor meer voorbeeld scriptacties Hallo.

* [Installeren en gebruiken van Hue op HDInsight-clusters](hdinsight-hadoop-hue-linux.md)
* [Installeren en gebruiken van Solr op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md)
* [Installeren en gebruiken van Giraph op HDInsight-clusters](hdinsight-hadoop-giraph-install-linux.md)
* [Installeren of upgraden van Mono op HDInsight-clusters](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a>Problemen oplossen

Hallo volgen fouten die optreden kunnen wanneer met behulp van scripts die u hebt ontwikkeld:

**Fout**: `$'\r': command not found`. Soms gevolgd door `syntax error: unexpected end of file`.

*Oorzaak*: deze fout wordt veroorzaakt wanneer Hallo regels in een script met CRLF eindigen. UNIX-systemen verwacht alleen LF als Hallo regel beëindigen.

Dit probleem treedt meestal wanneer het Hallo-script is gemaakt op een Windows-omgeving CRLF is een algemene regel die eindigt voor veel teksteditors op Windows.

*Resolutie*: als het is een optie in een teksteditor, selecteert u Unix-indeling of LF voor Hallo regel beëindigen. U kunt ook de volgende opdrachten op een Unix-systeem toochange Hallo CRLF tooan LF Hallo:

> [!NOTE]
> Hallo zijn volgende opdrachten grofweg gelijk Hallo CRLF regel uitgangen tooLF moet worden gewijzigd. Selecteer een op basis van Hallo hulpprogramma's beschikbaar zijn op uw systeem.

| Opdracht | Opmerkingen |
| --- | --- |
| `unix2dos -b INFILE` |het oorspronkelijke bestand Hallo back-up met een. De extensie BAK |
| `tr -d '\r' < INFILE > OUTFILE` |UITVOERBESTAND bevat een versie met alleen LF uitgangen |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | Hallo-bestand wijzigt rechtstreeks |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |UITVOERBESTAND bevat een versie met alleen LF uitgangen. |

**Fout**: `line 1: #!/usr/bin/env: No such file or directory`.

*Oorzaak*: deze fout treedt op wanneer hello script is opgeslagen als UTF-8 met een Byte Order Mark (BOM).

*Resolutie*: opgeslagen Hallo-bestand als ASCII of als UTF-8 zonder een stuklijst. U kunt ook de opdracht volgen op een Linux- of Unix-systeem toocreate een bestand zonder Hallo BOM Hallo:

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

Vervang `INFILE` met Hallo-bestand waarin Hallo stuklijst. `OUTFILE`moet u een nieuwe bestandsnaam die Hallo script zonder Hallo BOM bevat.

## <a name="seeAlso"></a>Volgende stappen

* Meer informatie over hoe te[aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md)
* Gebruik Hallo [HDInsight .NET SDK-naslaginformatie](https://msdn.microsoft.com/library/mt271028.aspx) toolearn meer over het maken van .NET-toepassingen die HDInsight beheren
* Gebruik Hallo [HDInsight REST-API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn hoe toouse REST tooperform acties op HDInsight-clusters.
