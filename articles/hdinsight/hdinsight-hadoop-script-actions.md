---
title: Actie bij het ontwikkelen met HDInsight - Azure aaaScript | Microsoft Docs
description: "Meer informatie over hoe toocustomize Hadoop-clusters met scriptactie. Scriptactie mag gebruikte tooinstall aanvullende software die worden uitgevoerd op een Hadoop-cluster of toochange Hallo configuratie van toepassingen zijn geïnstalleerd op een cluster."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 4fc3a389df8a003f7129ab00b4cd9bc7ad81a419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a>Scripts voor HDInsight Windows gebaseerde clusters scriptactie ontwikkelen
Meer informatie over hoe toowrite scriptactie scripts voor HDInsight. Zie voor meer informatie over het gebruik van de scriptactie scripts [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md). Zie voor Hallo hetzelfde artikel is geschreven voor Linux gebaseerde HDInsight-clusters, [scriptactie ontwikkelen scripts voor HDInsight](hdinsight-hadoop-script-actions-linux.md).



> [!IMPORTANT]
> Hallo stappen in dit document alleen werk voor op Windows gebaseerde HDInsight-clusters. HDInsight is alleen beschikbaar in Windows voor versies lager is dan HDInsight 3.4. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie. Zie voor meer informatie over het gebruik van scriptacties met Linux gebaseerde clusters [Scriptactieontwikkeling met HDInsight (Linux)](hdinsight-hadoop-script-actions-linux.md).
>
>



Scriptactie mag gebruikte tooinstall aanvullende software die worden uitgevoerd op een Hadoop-cluster of toochange Hallo configuratie van toepassingen zijn geïnstalleerd op een cluster. Scriptacties zijn scripts die worden uitgevoerd op de clusterknooppunten Hallo bij HDInsight-clusters worden geïmplementeerd en ze worden uitgevoerd zodra de knooppunten in cluster Hallo HDInsight-configuratie voltooien. Een scriptactie wordt uitgevoerd onder system-account beheerdersbevoegdheden en biedt volledige toegangsrechten toohello clusterknooppunten. Elk cluster kan worden opgegeven met een lijst met script acties toobe uitgevoerd in Hallo volgorde waarin ze worden opgegeven.

> [!NOTE]
> Als u Hallo volgende foutbericht weergegeven ondervindt:
>
> System.Management.Automation.CommandNotFoundException; ExceptionMessage: Hallo term 'Opslaan HDIFile' wordt niet herkend als Hallo-naam van een cmdlet, functie, scriptbestand of programma. Controleer de spelling Hallo van Hallo-naam of als een pad opgenomen is, Verifieer dat Hallo pad juist is en probeer het opnieuw.
> Omdat u niet hebt opgenomen methoden hello wordt.  Zie [Help-methoden voor aangepaste scripts](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).
>
>

## <a name="sample-scripts"></a>Voorbeeldscripts
Hallo scriptactie is voor het maken van HDInsight-clusters op Windows-besturingssysteem, Azure PowerShell-script. Hallo is volgende script een voorbeeld voor het configureren van configuratiebestanden Hallo-site:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable tooconfigure $ConfigFileName because it is not part of hello HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

Hallo script neemt vier parameters, naam configuratiebestand hello, Hallo-eigenschap die u wilt dat toomodify, Hallo-waarde die u wilt tooset en een beschrijving. Bijvoorbeeld:

    hive-site.xml hive.metastore.client.socket.timeout 90

Deze parameters stelt Hallo hive.metastore.client.socket.timeout waarde too90 in bestand Hallo-hive-site.xml.  Hallo-standaardwaarde is 60 seconden.

Dit voorbeeldscript kan ook worden gevonden op [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).

HDInsight biedt verschillende scripts tooinstall extra onderdelen op HDInsight-clusters:

| Naam | Script |
| --- | --- |
| **Spark installeren** |https://hdiconfigactions.BLOB.Core.Windows.NET/sparkconfigactionv03/Spark-Installer-v03.ps1. Zie [installeert en gebruikt Spark in HDInsight-clusters][hdinsight-install-spark]. |
| **R installeren** |https://hdiconfigactions.BLOB.Core.Windows.NET/rconfigactionv02/r-Installer-v02.ps1. Zie [installeert en gebruikt R op HDInsight-clusters][hdinsight-r-scripts]. |
| **Solr installeren** |https://hdiconfigactions.BLOB.Core.Windows.NET/solrconfigactionv01/solr-Installer-v01.ps1. Zie [installeert en gebruikt Solr op HDInsight-clusters](hdinsight-hadoop-solr-install.md). |
| - **Giraph installeren** |https://hdiconfigactions.BLOB.Core.Windows.NET/giraphconfigactionv01/giraph-Installer-v01.ps1. Zie [installeert en gebruikt Giraph op HDInsight-clusters](hdinsight-hadoop-giraph-install.md). |

Scriptactie kan worden geïmplementeerd vanaf hello Azure-portal, Azure PowerShell of met behulp van Hallo HDInsight .NET SDK.  Zie voor meer informatie [aanpassen HDInsight-clusters met behulp van de scriptactie][hdinsight-cluster-customize].

> [!NOTE]
> Hallo-voorbeeldscripts werkt alleen met HDInsight-cluster versie 3.1 of hoger. Zie voor meer informatie over de versies van HDInsight-cluster, [versies van HDInsight-cluster](hdinsight-component-versioning.md).
>
>

## <a name="helper-methods-for-custom-scripts"></a>Help-methoden voor aangepaste scripts
Script actie Help-methoden zijn hulpprogramma's die u gebruiken kunt bij het schrijven van aangepaste scripts. Deze methoden zijn gedefinieerd in [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1), en kan worden opgenomen in uw scripts met Hallo voorbeeld te volgen:

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module toomake writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed tooload HDInsightUtilities module, exiting ...";
        exit;
    }

Hier volgen Hallo Help-methoden die worden geleverd door dit script:

| Help-methode | Beschrijving |
| --- | --- |
| **Opslaan HDIFile** |Download een bestand van Hallo opgegeven Uniform Resource Identifier (URI) tooa locatie op Hallo lokale schijf die is gekoppeld aan het cluster toegewezen toohello hello Azure VM-knooppunten. |
| **Vouw HDIZippedFile** |Een ZIP-bestand uitpakken. |
| **Aanroepen HDICmdScript** |Een script uitvoeren vanaf cmd.exe. |
| **Schrijven HDILog** |Uitvoer van Hallo aangepast script gebruikt voor de scriptactie van een schrijven. |
| **Get-Services** |Ophalen van een lijst met services die worden uitgevoerd op de machine Hallo waar Hallo script wordt uitgevoerd. |
| **Get-Service** |Met de Hallo specifieke servicenaam als invoer, krijgt u gedetailleerde informatie voor een specifieke service (servicenaam, proces-ID, status, enz.) op Hallo machine waar Hallo script wordt uitgevoerd. |
| **Get-HDIServices** |Haal een lijst van HDInsight-services die worden uitgevoerd op de computer Hallo waar Hallo script wordt uitgevoerd. |
| **Get-HDIService** |Met de Hallo specifieke HDInsight servicenaam als invoer, krijgt u gedetailleerde informatie voor een specifieke service (servicenaam, proces-ID, status, enz.) op Hallo machine waar Hallo script wordt uitgevoerd. |
| **Get-ServicesRunning** |Ophalen van een lijst met services die worden uitgevoerd op Hallo computer waar Hallo script wordt uitgevoerd. |
| **Get-ServiceRunning** |Controleer of een specifieke service (met de naam) wordt uitgevoerd op de computer Hallo waar Hallo script wordt uitgevoerd. |
| **Get-HDIServicesRunning** |Haal een lijst van HDInsight-services die worden uitgevoerd op de computer Hallo waar Hallo script wordt uitgevoerd. |
| **Get-HDIServiceRunning** |Controleer of een specifieke HDInsight-service (met de naam) wordt uitgevoerd op de computer Hallo waar Hallo script wordt uitgevoerd. |
| **Get-HDIHadoopVersion** |Hallo-versie van Hadoop geïnstalleerd op Hallo computer waar Hallo script wordt uitgevoerd krijgen. |
| **Test IsHDIHeadNode** |Controleer of Hallo computer waar Hallo script wordt uitgevoerd een hoofdknooppunt. |
| **Test IsActiveHDIHeadNode** |Controleer of Hallo computer waar Hallo script wordt uitgevoerd een actieve hoofdknooppunt is. |
| **Test IsHDIDataNode** |Controleer of Hallo computer waar Hallo script wordt uitgevoerd een gegevensknooppunt is. |
| **Bewerken HDIConfigFile** |Hallo config bestanden hive-site.xml, core site.xml, hdfs-site.xml, mapred site.xml of yarn-site.xml bewerken. |

## <a name="best-practices-for-script-development"></a>Aanbevolen procedures voor het ontwikkelen van scripts
Wanneer u een aangepast script voor een HDInsight-cluster ontwikkelt, zijn er enkele aanbevolen procedures tookeep rekening:

* Controle op Hallo Hadoop-versie

    Alleen HDInsight versie 3.1 (Hadoop 2.4) en hoger ondersteuning met scriptactie tooinstall aangepaste onderdelen op een cluster. In een script, moet u Hallo **Get-HDIHadoopVersion** helper methode toocheck hello Hadoop versie voordat u doorgaat met de andere taken uitvoeren in Hallo-script.
* Geef stabiel koppelingen tooscript resources

    Gebruikers Zorg ervoor dat alle Hallo scripts en andere artefacten in Hallo aanpassing van een cluster gebruikt beschikbaar tijdens de levensduur Hallo van Hallo cluster blijven en dat Hallo versies van deze bestanden niet voor de duur van Hallo wijzigen. Deze resources zijn vereist als Hallo teruggezet van knooppunten in cluster Hallo vereist is. Hallo aanbevolen procedure is toodownload en alles in een opslagaccount die gebruikersbesturingselementen Hallo gearchiveerd. Dit kan zijn standaardopslagaccount hello of een van de Hallo extra opslagaccounts op Hallo moment van implementatie voor een cluster met aangepaste opgegeven.
    Hallo Spark en R aangepast cluster voorbeelden opgegeven in de documentatie Hallo bijvoorbeeld we hebben aangebracht een lokale kopie van het Hallo-resources in dit opslagaccount: https://hdiconfigactions.blob.core.windows.net/.
* Zorg ervoor dat Hallo cluster aanpassing script idempotent

    U moet verwachten dat Hallo knooppunten van een HDInsight-cluster wordt teruggezet tijdens de levensduur van de Hallo-cluster. Hallo cluster aanpassing script wordt uitgevoerd wanneer de installatiekopie van een cluster wordt hersteld. Dit script moet worden ontworpen toobe idempotent in Hallo zin dat bij teruggezet, Hallo script moet ervoor zorgen dat cluster Hallo toohello die dezelfde staat waarin deze zich bevond vlak nadat de eerste keer wanneer Hallo-cluster in eerste instantie was voor Hallo uitvoerde Hallo script aangepaste wordt geretourneerd gemaakt. Bijvoorbeeld als een aangepast script een toepassing op D:\AppLocation geïnstalleerd op het eerst wordt uitgevoerd, wordt bij elke volgende uitvoeren, bij teruggezet, Hallo script moet controleren of de toepassing hello op Hallo D:\AppLocation locatie voordat u doorgaat met andere bestaat de stappen in Hallo-script.
* Aangepaste onderdelen installeren op Hallo optimale locatie

    Wanneer de clusterknooppunten worden teruggezet, kunnen Hallo C:\ resource station en D:\ systeemstation worden geformatteerd, Hallo verlies van gegevens en toepassingen die was geïnstalleerd op deze schijven. Dit kan ook gebeuren als een virtuele Azure-machine (VM)-knooppunt dat deel uitmaakt van Hallo cluster uitvalt en wordt vervangen door een nieuw knooppunt. U kunt onderdelen installeren op station D:\ Hallo of in Hallo C:\apps locatie op Hallo-cluster. Alle andere locaties op Hallo station C:\ zijn gereserveerd. Hallo-locatie waar toepassingen of -bibliotheken geïnstalleerd in Hallo cluster aanpassing script toobe zijn opgeven.
* Zorg ervoor dat hoge beschikbaarheid van Hallo cluster-architectuur

    HDInsight is een actief / passief-architectuur voor hoge beschikbaarheid, in welke één hoofdknooppunt is in de actieve modus (waarbij Hallo HDInsight services worden uitgevoerd) en Hallo andere hoofdknooppunt in standby-modus (in welke HDInsight services niet worden uitgevoerd). Hallo knooppunten overschakelen actieve en passieve modus als de HDInsight-services worden onderbroken. Als een scriptactie gebruikte tooinstall services op beide hoofdknooppunten voor hoge beschikbaarheid, houd er rekening mee dat Hallo HDInsight failover-mechanisme niet kunnen tooautomatically mislukken via deze services gebruiker geïnstalleerd. Gebruiker geïnstalleerd dus services op hoofdknooppunten HDInsight die verwachte toobe maximaal beschikbare moeten hebben hun eigen mechanisme voor failover als deze in de modus actief-passief of in de actieve-actieve modus.

    Een HDInsight-scriptactie-opdracht wordt uitgevoerd op beide hoofdknooppunten wanneer Hallo hoofdknooppunt rol is opgegeven als een waarde in Hallo *ClusterRoleCollection* parameter. Wanneer u een aangepast script ontwerpt, zorg er dus dat uw script hoogte van deze installatie is. U moet niet uitvoeren op problemen waar hello dezelfde services zijn geïnstalleerd en gestart op zowel de hoofdknooppunten Hallo en ze met elkaar concurreren. Let op dat gegevens niet verloren tijdens teruggezet, zodat software is geïnstalleerd via een scriptactie toobe robuuste toosuch gebeurtenissen heeft. Toepassingen moeten worden ontworpen toowork met maximaal beschikbare gegevens die wordt gedistribueerd over veel knooppunten. Houd er rekening mee dat wel 1/5 Hallo knooppunten in een cluster kunnen worden hersteld met een installatiekopie op Hallo hetzelfde moment.
* Hallo aangepaste onderdelen toouse Azure Blob-opslag configureren

    Hallo aangepaste onderdelen die u op de clusterknooppunten Hallo installeert wellicht een standaard configuratie toouse Hadoop Distributed File System (HDFS) opslag. In plaats daarvan moet u Hallo configuratie toouse Azure Blob-opslag wijzigen. Terugzetten van een cluster de installatiekopie, Hallo HDFS-bestandssysteem geformatteerd opgehaald en verliest u gegevens die is opgeslagen. Azure Blob storage in plaats daarvan zorgt ervoor dat uw gegevens worden bewaard.

## <a name="common-usage-patterns"></a>Algemene gebruikspatronen
Deze sectie bevat richtlijnen over het implementeren van een aantal Hallo algemene gebruikspatronen die u tegenkomen kunt tijdens het schrijven van uw eigen aangepaste scripts.

### <a name="configure-environment-variables"></a>Omgevingsvariabelen configureren
Vaak in script actie ontwikkeling, u denkt dat Hallo moet tooset omgevingsvariabelen. Een meest waarschijnlijke scenario is bijvoorbeeld: wanneer u een binair bestand vanaf een externe site downloaden op Hallo-cluster installeren en voeg Hallo-locatie van waar het geïnstalleerde tooyour 'PATH' omgevingsvariabele is. Hallo volgende codefragment ziet u hoe de omgevingsvariabelen tooset in Hallo aangepast script.

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

Deze instructie stelt de omgevingsvariabele Hallo **MDS_RUNNER_CUSTOM_CLUSTER** toohello waarde 'true' en ook sets Hallo bereik van deze variabele toobe alle computers. Soms is het belangrijk dat de omgevingsvariabelen worden ingesteld op Hallo geschikte bereik – computer of gebruiker. Raadpleeg [hier] [ 1] voor meer informatie over het instellen van omgevingsvariabelen.

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Toegang tot toolocations waar Hallo aangepaste scripts worden opgeslagen
Scripts die worden gebruikt toocustomize een cluster moet tooeither zich in Hallo storage-standaardaccount voor Hallo cluster of in een openbare alleen-lezen container op andere storage-account. Als uw script toegang heeft tot resources die zich ergens anders bevindt deze toobe in een openbaar toegankelijk moeten zijn (ten minste openbare alleen-lezen). Voor instantie mogelijk tooaccess een bestand en sla het Hallo SaveFile HDI-opdracht.

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

In dit voorbeeld moet u ervoor zorgen dat container Hallo 'somecontainer' in de storage-account 'somestorageaccount' openbaar toegankelijk is. Anders Hallo script genereert een uitzondering 'Niet gevonden' en mislukken.

### <a name="pass-parameters-toohello-add-azurermhdinsightscriptaction-cmdlet"></a>Parameters toohello toevoegen AzureRmHDInsightScriptAction cmdlet doorgeven
toopass meerdere parameters toohello toevoegen AzureRmHDInsightScriptAction cmdlet, moet u tooformat Hallo tekenreeks waarde toocontain alle parameters voor Hallo-script. Bijvoorbeeld:

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

of

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a>Uitzondering voor mislukte Clusterimplementatie
Als u wilt dat tooget nauwkeurig Hallo feit gemeld dat cluster aanpassing is niet gelukt zoals verwacht, maar belangrijke toothrow is een uitzondering maken van het cluster Hallo mislukken. U kan bijvoorbeeld tooprocess een bestand wilt als deze bestaat en verwerken Hallo foutaanvraag waar Hallo bestand niet bestaat. Dit zou ervoor dat Hallo script wordt probleemloos afgesloten en Hallo staat van Hallo cluster goed bekend is. Hallo volgende fragment geeft een voorbeeld van hoe tooachieve dit:

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

In dit fragment als Hallo-bestand niet bestaat, zou dit leiden tooa status Hallo script daadwerkelijk wordt afgesloten zonder problemen na het afdrukken van het foutbericht Hallo waarbij Hallo cluster actief is, ervan uitgaande dat deze ' ' voltooid cluster aanpassing is bereikt. Als u wilt dat toobe nauwkeurig Hallo feit gemeld dat cluster aanpassing in principe kan niet zoals verwacht vanwege een ontbrekend bestand, geschiktere toothrow is een uitzondering en Hallo cluster aanpassing stap mislukt. tooachieve dit moet u Hallo voorbeeld codefragment in plaats daarvan te volgen.

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a>Controlelijst voor het implementeren van een scriptactie
Hier volgen Hallo stappen werd bij het voorbereiden van toodeploy deze scripts:

1. Hallo-bestanden met aangepaste scripts op een locatie die toegankelijk is voor de clusterknooppunten Hallo tijdens de implementatie van Hallo plaatsen. Dit kan zijn Hallo standaard of extra opslagaccounts bij Hallo van implementatie van het cluster of een andere openbaar toegankelijke storage-container worden opgegeven.
2. Toevoegen van controles in scripts toomake zeker van te zijn dat ze idempotently, uitvoeren zodat Hallo script kan meerdere keren worden uitgevoerd op Hallo hetzelfde knooppunt.
3. Gebruik Hallo **Write-Output** Azure PowerShell-cmdlet tooprint tooSTDOUT, evenals STDERR. Gebruik geen **Write-Host**.
4. Gebruik een tijdelijke map, zoals $env: TEMP tookeep Hallo gedownloade bestand dat wordt gebruikt door Hallo scripts en vervolgens opschonen van nadat scripts hebt uitgevoerd.
5. Aangepaste software alleen op D:\ of C:\apps installeren. Andere locaties op Hallo station C: mag niet worden gebruikt als deze gereserveerd zijn. Houd er rekening mee dat bestanden op Hallo C:-schijf buiten de Hallo C:\apps map installeren leiden setup kopieerfouten tijdens reimages van Hallo-knooppunt tot kan.
6. In de gebeurtenis Hallo OS-niveau instellingen of configuratiebestanden voor Hadoop-service zijn gewijzigd, kunt u toorestart HDInsight services zodat ze kunnen alle instellingen OS-niveau, zoals Hallo omgevingsvariabelen ingesteld in Hallo scripts ophalen.

## <a name="debug-custom-scripts"></a>Fouten opsporen in aangepaste scripts
Hallo script foutenlogboeken zijn opgeslagen, samen met andere uitvoer, in Hallo Storage-standaardaccount die u hebt opgegeven voor de cluster Hallo bij het maken ervan. Hallo logboeken worden opgeslagen in een tabel met naam Hallo *u < \cluster-name-fragment >< \time-stamp > bestand*. Dit zijn de cumulatieve logboeken die records uit alle Hallo knooppunten hoofdknooppunt en worker-knooppunten, op welke Hallo script wordt uitgevoerd in de cluster Hallo hebben.
Een eenvoudige manier toocheck Hallo Logboeken is toouse HDInsight Tools voor Visual Studio. Zie voor het installeren van extra Hallo [aan de slag met Visual Studio Hadoop-hulpprogramma's voor HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)

**toocheck hello logboek met Visual Studio**

1. Open Visual Studio.
2. Klik op **weergave**, en klik vervolgens op **Server Explorer**.
3. Met de rechtermuisknop op de 'Azure', klikt u op verbinden te**Microsoft Azure-abonnementen**, en voer uw referenties.
4. Vouw **opslag**, vouw hello Azure storage-account gebruikt als het standaardbestandssysteem Hallo uit, vouw **tabellen**, en dubbelklik vervolgens op Hallo tabelnaam.

U kunt ook externe in Hallo cluster knooppunten toosee zowel STDOUT en STDERR voor aangepaste scripts. Hallo-logboeken op elk knooppunt zijn specifiek alleen toothat-knooppunt en vastgelegd in **C:\HDInsightLogs\DeploymentAgent.log**. Deze logboekbestanden Leg alle uitvoerwaarden van een aangepast script Hallo. Een voorbeeld logboek codefragment voor een Spark-scriptactie ziet er als volgt:

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


In dit logboek is duidelijk dat Hallo Spark scriptactie is uitgevoerd op virtuele machine met de naam HEADNODE0 Hallo en dat er geen uitzonderingen tijdens het Hallo uitvoeren veroorzaakt.

In het Hallo-gebeurtenis die een uitvoeringsfout optreedt, met een beschrijving van het Hallo-uitvoer ook deel uitmaakt van dit logboekbestand. Hallo informatie in deze logboeken zijn te helpen bij foutopsporing script problemen die zich kunnen voordoen.

## <a name="see-also"></a>Zie ook
* [HDInsight-clusters met behulp van de scriptactie aanpassen][hdinsight-cluster-customize]
* [Installeren en gebruiken van Spark in HDInsight-clusters][hdinsight-install-spark]
* [Installeren en gebruiken van R op HDInsight-clusters][hdinsight-r-scripts]
* [Installeren en gebruiken van Solr op HDInsight-clusters](hdinsight-hadoop-solr-install.md).
* [Installeren en gebruiken van Giraph op HDInsight-clusters](hdinsight-hadoop-giraph-install.md).

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
