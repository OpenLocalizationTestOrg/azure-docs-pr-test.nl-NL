---
title: aaaGet de slag met R Server op een HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toocreate een Apache Spark in HDInsight-cluster met R Server en het verzenden van een R-script op Hallo-cluster.
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a>Aan de slag met R Server op HDInsight

HDInsight bevat een R Server optie toobe geïntegreerd in uw HDInsight-cluster. Deze optie kunt scripts R toouse Spark en MapReduce toorun gedistribueerd berekeningen. In dit document leert u hoe toocreate een R Server op HDInsight-cluster en klik vervolgens op uitvoeren een R-script dat wordt gedemonstreerd met behulp van Spark voor gedistribueerde R-berekeningen.


## <a name="prerequisites"></a>Vereisten

* **Een Azure-abonnement**: voordat u aan deze zelfstudie begint, moet u beschikken over een Azure-abonnement. Ga toohello artikel [gratis proefversie van Microsoft Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) voor meer informatie.
* **Een client Secure Shell (SSH)**: een SSH-client wordt gebruikt tooremotely verbinding toohello HDInsight-cluster en uitvoeren van opdrachten rechtstreeks op Hallo-cluster. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.
* **SSH-sleutels (optioneel)**: U kunt beveiligen Hallo SSH-account gebruikt tooconnect toohello cluster met een wachtwoord of een openbare sleutel. Met een wachtwoord is eenvoudiger en kunt u tooget gestart zonder toocreate een openbaar/persoonlijk sleutelpaar. Het gebruik van een sleutel is echter veiliger.

> [!NOTE]
> Hallo stappen in dit document wordt ervan uitgegaan dat u van een wachtwoord gebruikmaakt.


## <a name="automated-cluster-creation"></a>Automatisch een cluster maken

U kunt maken van HDInsight R Servers via Azure Resource Manager-sjablonen, Hallo SDK en ook PowerShell Hallo automatiseren.

* Zie een R Server met een Azure Resource Management-sjabloon toocreate [een R server HDInsight-cluster implementeren](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).
* Zie toocreate een R Server met behulp van de .NET SDK Hallo [maken op basis van Linux-clusters in HDInsight met behulp van Hallo .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* toodeploy R Server met behulp van powershell, Zie Hallo-artikel over [een R Server maken in HDInsight met PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a>Hallo-cluster met behulp van hello Azure-portal maken

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

2. Selecteer **NIEUW** -> **Intelligence en analyse**, -> **HDInsight**.

    ![Afbeelding van het maken van een nieuw cluster](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. In Hallo **snelle invoer** -ervaring, voer een naam voor de cluster Hallo in Hallo **clusternaam** veld. Als u meerdere Azure-abonnementen hebt, gebruikt u Hallo **abonnement** vermelding tooselect Hallo een gewenste toouse.

    ![Clusternaam en geselecteerde abonnementen](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. Selecteer **type Cluster** tooopen hello **clusterconfiguratie** blade. Op Hallo **clusterconfiguratie** blade Selecteer Hallo volgende opties:

    * **Clustertype**: R Server
    * **Versie**: Selecteer Hallo-versie van tooinstall R Server op Hallo-cluster. Hallo-versie die momenteel beschikbaar is ***R Server 9.1 (HDI 3.6)***. Releaseopmerkingen voor Hallo beschikbare versies van R Server beschikbaar zijn [hier](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).
    * **R Studio community edition voor op R Server**: deze browser gebaseerde IDE wordt standaard geïnstalleerd op Hallo edge-knooppunt. Als u liever toonot hebt geïnstalleerd en schakel het selectievakje Hallo. Als u ervoor kiest toohave deze geïnstalleerd, Hallo-URL voor het openen van Hallo RStudio Server-aanmelding is gevonden in een portaltoepassing blade voor uw cluster zodra deze gemaakt.
    * Andere opties van Hallo laten op het Hallo-standaardwaarden en hello gebruiken **Selecteer** knoptype toosave Hallo-cluster.

        ![Schermafbeelding van de blade Clustertype](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. Voer een **gebruikersnaam** en **wachtwoord** voor aanmelden bij het cluster in.

    Geef een **SSH-gebruikersnaam** op. SSH is gebruikte tooremotely verbinden toohello cluster via een **Secure Shell (SSH)** client. U kunt Hallo SSH-gebruiker opgeven in dit dialoogvenster of nadat het Hallo-cluster is gemaakt (in Hallo tabblad van de configuratie voor Hallo cluster). R Server geconfigureerde tooexpect is een **SSH-gebruikersnaam** van 'remoteuser'.  **Als u een andere gebruikersnaam gebruikt, moet u een extra stap uitvoeren nadat Hallo-cluster is gemaakt.**

    Laat de eigenschap Hallo selectievakje is ingeschakeld voor **gebruik hetzelfde wachtwoord als cluster aanmelding** toouse **wachtwoord** als het Hallo verificatie type tenzij u liever gebruik van een openbare sleutel.  U moet een openbaar/persoonlijk sleutelpaar tooaccess R Server op Hallo-cluster via een externe client als bijvoorbeeld RTVS, RStudio of een ander bureaublad IDE. Als u Hallo RStudio Server community edition installeert, moet u een SSH-wachtwoord toochoose.     

    toocreate en gebruik een openbaar/persoonlijk sleutelpaar, schakel het selectievakje **gebruik hetzelfde wachtwoord als cluster aanmelding** en selecteer vervolgens **openbare sleutel** en gaat u als volgt. Bij deze instructies wordt ervan uitgegaan dat u Cygwin SSH-keygen of iets gelijkwaardigs hebt geïnstalleerd.

    * Een openbaar/persoonlijk sleutelpaar genereren via de opdrachtprompt Hallo op uw laptop:

        ssh-keygen -t rsa -b 2048

    * Volg Hallo vragen tooname een sleutelbestand en voer vervolgens een wachtwoordzin voor extra beveiliging. Uw scherm ziet er ongeveer als Hallo installatiekopie te volgen:

        ![SSH-opdrachtregel in Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * Deze opdracht maakt u een bestand met een persoonlijke sleutel en een bestand met een openbare sleutel onder de naam < persoonlijke sleutel bestandsnaam > .pub hello, bijvoorbeeld furiosa en furiosa.pub.

        ![SSH-dir](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * Geef vervolgens Hallo bestand openbare sleutel (&#42;. pub) wanneer toewijzen HDI cluster referenties en ten slotte bevestigt de resourcegroep en de regio en selecteer **volgende**.

        ![Blade Referenties](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * Machtigingen op Hallo persoonlijke sleutelbestand op uw laptop wijzigen:

        chmod 600 <bestandsnaam-persoonlijke-sleutel>

   * Hallo persoonlijke sleutelbestand met SSH gebruiken voor externe aanmelding:

        ssh – i <bestandsnaam-persoonlijke-sleutel> remoteuser@<hostname public ip>

      Of als onderdeel Hallo definitie van uw Hadoop Spark compute-context voor R Server op Hallo-client. Zie Hallo **met behulp van Microsoft R Server als een Hadoop Client** subsectie [maken van een Compute-Context voor Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).

6. Hallo snelle invoer overgangen die u toohello **opslag** blade tooselect hello opslagaccount instellingen toobe gebruikt voor de primaire locatie Hallo Hallo HDFS bestandssysteem door Hallo cluster gebruikt. Selecteer een nieuw of een bestaand Azure Storage-account of een bestaand Data Lake Storage-account.

    - Als u een Azure Storage-account selecteert, een bestaand opslagaccount is geselecteerd door te kiezen **Selecteer een opslagaccount** en het Hallo relevante account selecteren. Een nieuwe account maken met Hallo **nieuw** koppeling in Hallo **Selecteer een opslagaccount** sectie.

      > [!NOTE]
      > Als u selecteert **nieuw** u moet een naam voor het nieuwe opslagaccount Hallo opgeven. Een groen vinkje weergegeven als de naam van de Hallo is geaccepteerd.

      Hallo **standaard Container** standaardwaarden toohello naam van Hallo-cluster. Laat deze standaardinstelling Hallo-waarde.

      Als u een nieuwe opslagoptie account hebt geselecteerd een prompt tooselect **locatie** is gegeven tooselect welke regio toocreate Hallo storage-account.  

         ![Blade Gegevensbron](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > Locatie van de HDInsight-cluster Hallo HALLO hallo locatie voor Hallo standaardgegevensbron selecteren ook worden ingesteld. Hallo-cluster en het standaard gegevensbron moet Hallo dezelfde regio.

    - Als u een bestaande Data Lake Store toouse wilt, selecteer Hallo ADLS storage account toouse en Hallo-cluster toevoegen *toevoegen* identiteit tooyour cluster tooallow toegang tot toohello store. Raadpleeg [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal) (HDInsight-cluster met Data Lake Store maken met behulp van Azure Portal) voor meer informatie over dit proces.

    Gebruik Hallo **Selecteer** knop toosave Hallo data source-configuratie.


7. Hallo **samenvatting** blade geeft toovalidate alle instellingen. Hier kunt u uw **clustergrootte** toomodify Hallo aantal servers in het cluster en geeft u ook een **acties Script** gewenste toorun. Tenzij u zeker weet dat u een groter cluster nodig hebt, laat u Hallo aantal worker-knooppunten op Hallo standaardwaarde van `4`. Hallo geschatte kosten van het Hallo-cluster wordt weergegeven in de blade Hallo.

    ![clusteroverzicht](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > Indien nodig, u kunt de grootte van uw cluster later via Hallo Portal (**Cluster** -> **instellingen** -> **Scale Cluster**) tooincrease of het aantal worker-knooppunten Hallo verkleinen.  Deze grootte is handig voor stationair omlaag Hallo cluster als deze niet in gebruik of voor het toevoegen van toomeet Hallo capaciteitsbehoeften van grote taken.
   >
   >

   Een aantal factoren tookeep rekening moet houden bij het formaat van uw cluster, Hallo gegevensknooppunten en Hallo edge-knooppunt zijn onder andere:  

   * Hallo-prestaties van gedistribueerde R Server analyses op Spark is evenredig toohello aantal worker-knooppunten wanneer Hallo gegevens groot is.  

   * Hallo-prestaties van R Server analyses is lineaire Hallo omvang van gegevens wordt geanalyseerd. Bijvoorbeeld:  

     * Voor kleine toomodest gegevens, prestaties, het wordt aanbevolen wanneer geanalyseerd in de context van een lokale compute op Hallo edge-knooppunt.  Voor meer informatie over het Hallo-scenario's waarin Hallo lokale en Spark contexten COMPUTE werken het beste, Compute context opties voor R Server ziet op HDInsight.<br>
     * Als u toohello edge-knooppunt aanmelden en uw R-script uitvoeren, wordt alle maar Hallo ScaleR rx-functies worden uitgevoerd <strong>lokaal</strong> op Hallo edge-knooppunt. Dus Hallo geheugen en het aantal kernen van Hallo edge-knooppunt dienovereenkomstig moet worden aangepast. Hallo geldt ook als u R Server op HDI als een externe compute-context van uw laptop.

     ![Blade Prijscategorieën voor knooppunten](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     Gebruik Hallo **Selecteer** knop toosave Hallo knooppunt configuratie prijzen.

   Er is ook een koppeling **Sjabloon en parameters downloaden**. Klik op deze koppeling toodisplay scripts die kunnen worden gebruikt tooautomate Hallo maken van een cluster met geselecteerde Hallo-configuratie. Deze scripts zijn ook beschikbaar is via Azure portal-ingang voor uw cluster Hallo zodra deze is gemaakt.

   > [!NOTE]
   > Het duurt enige tijd Hallo cluster toobe gemaakt, meestal ongeveer 20 minuten. Hallo-tegel op Hallo Startboard gebruiken of Hallo **meldingen** post op Hallo links van Hallo pagina toocheck op Hallo aanmaakproces.
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a>Verbinding maken met Server tooRStudio

Als u tooinclude RStudio Server community edition in de installatie hebt gekozen, kunt u Hallo RStudio aanmelding via twee verschillende methoden gebruiken.

1. Ga toohello na URL (waarbij **CLUSTERNAME** Hallo-naam van Hallo-cluster die u hebt gemaakt):

    https://**CLUSTERNAAM**.azurehdinsight.net/rstudio/

2. Hallo-vermelding voor uw cluster openen in hello Azure-portal, selecteer Hallo **R Server Dashboards** snelkoppeling en vervolgens te klikken op Hallo **R Studio Dashboard**:

     ![Toegang Hallo R studio dashboard](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Toegang Hallo R studio dashboard](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > Hallo-methode die wordt gebruikt, ongeacht de moet hello eerste keer dat u zich aanmeldt u tooauthenticate twee keer.  Geef op de eerste verificatie Hallo Hallo *cluster Admin userid* en *wachtwoord*. Geef op de tweede vraag hello, Hallo *SSH userid* en *wachtwoord*. Daaropvolgende logboek modules vereisen alleen Hallo *SSH-wachtwoord* en *userid*.

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a>Verbinding maken met toohello edge-knooppunt op R Server

Verbinding maken met een rondleiding Server edge-knooppunt van Hallo HDInsight-cluster via SSH met Hallo-opdracht:

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> U vindt Hallo `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` adres in hello Azure-portal door te selecteren van het cluster vervolgens **alle instellingen** -> **Apps** -> **RServer**. U ziet nu Hallo SSH Endpoint-informatie voor Hallo edge-knooppunt.
>
> ![Afbeelding van Hallo SSH-eindpunt voor Hallo edge-knooppunt](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

Als u een wachtwoord toosecure uw SSH gebruikersaccount gebruikt, bent u na vragen aan gebruiker tooenter deze. Als u een openbare sleutel gebruikt, hebt u mogelijk toouse hello `-i` parameter toospecify Hallo overeenkomende persoonlijke sleutel. Bijvoorbeeld:

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Zie voor meer informatie [tooHDInsight (Hadoop) via SSH verbinding](hdinsight-hadoop-linux-use-ssh-unix.md).

Eenmaal zijn verbonden, wordt u aankomt bij een prompt vergelijkbare toohello volgende:

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a>Meerdere gelijktijdige gebruikers inschakelen

U kunt meerdere gelijktijdige gebruikers inschakelen door het toevoegen van meer gebruikers voor Hallo edge-knooppunt op welke Hallo RStudio community-versie wordt uitgevoerd.

Wanneer u een HDInsight-cluster maakt, moet u twee gebruikers opgeven, te weten een HTTP-gebruiker en een SSH-gebruiker:

![Gelijktijdige gebruiker 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- **Gebruikersnaam voor aanmelding cluster**: een gebruiker met HTTP voor verificatie via Hallo HDInsight gateway die wordt gebruikt tooprotect hello HDInsight-clusters u hebt gemaakt. Deze gebruiker HTTP is gebruikte tooaccess hello Ambari UI, gebruikersinterface van YARN, evenals andere UI-onderdelen.
- **Secure Shell (SSH) gebruikersnaam**: een SSH gebruiker tooaccess Hallo-cluster via secure shell. Deze gebruiker is een gebruiker in Hallo Linux-systeem voor alle hoofdknooppunten hello, worker-knooppunten en knooppunten van de rand. Zo kunt u secure shell tooaccess Hallo knooppunten in een RAS-cluster.

Hallo R Studio Server Community-versie die wordt gebruikt in Hallo Microsoft R Server op HDInsight-cluster type accepteert alleen een Linux-gebruikersnaam en wachtwoord als een mechanisme voor aanmelding. Doorgegeven tokens worden niet ondersteund. Als u een nieuw cluster hebt gemaakt en toouse R Studio tooaccess wilt, moet u toolog in twee keer.

- Meldt u zich eerst bij het gebruik van de gebruikersreferenties Hallo HTTP via Hallo HDInsight-Gateway: 

    ![Gelijktijdige gebruiker 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- Gebruik vervolgens Hallo SSH gebruiker referenties toolog in tooRStudio:
  
    ![Gelijktijdige gebruiker 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

Op dit moment kan slechts één SSH gebruikersaccount worden gemaakt tijdens het inrichten van een HDInsight-cluster. Dus tooenable meerdere gebruikers tooaccess Microsoft R Server op een HDInsight-clusters, moeten we toocreate extra gebruikers in Hallo Linux-systeem.

Omdat RStudio Server-Community op Hallo van het cluster edge-knooppunt wordt uitgevoerd, zijn er verschillende volgende stappen uit:

1. Gebruik Hallo gemaakt SSH gebruiker toolog in toohello edge-knooppunt
2. Meer Linux-gebruikers toevoegen in Edge-knooppunt
3. Hallo gebruiker gemaakt RStudio Community-versie gebruiken

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a>Stap 1: Gebruik Hallo gemaakt SSH gebruiker toolog in toohello edge-knooppunt

Een SSH-hulpprogramma (zoals Putty) downloaden en gebruiken van Hallo bestaande SSH gebruiker toolog in. Volg de instructies Hallo in [tooHDInsight (Hadoop) via SSH verbinding](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess Hallo edge-knooppunt. Hallo edge-knooppuntadres voor R Server op HDInsight-cluster is: *clustername-ed-ssh.azurehdinsight.net*


### <a name="step-2-add-more-linux-users-in-edge-node"></a>Stap 2: meer Linux-gebruikers toevoegen in Edge-knooppunt

een gebruiker toohello edge-knooppunt tooadd Hallo opdrachten uitvoeren:

    sudo useradd yournewusername -m
    sudo passwd yourusername

U ziet de volgende items geretourneerd Hallo: 

![Gelijktijdige gebruiker 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

Als u wordt gevraagd ' huidige Kerberos-wachtwoord: ', drukt u op **Enter** tooignore deze. Hallo `-m` optie in `useradd` opdracht geeft aan dat hello wordt gemaakt een basismap voor Hallo-gebruiker vereist voor RStudio Community-versie is.


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a>Stap 3: Gebruik RStudio Community-versie met Hallo gebruiker gemaakt

Hallo gebruiker gemaakte toolog in tooRStudio gebruiken:

![Gelijktijdige gebruiker 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

Kennisgeving RStudio geeft aan dat u van de nieuwe gebruiker hello gebruikmaakt (hier bijvoorbeeld *sshuser6*) toolog in Hallo-cluster: 

![Gelijktijdige gebruiker 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

U kunt ook aanmelden met behulp van de oorspronkelijke referenties hello (dit is standaard *sshuser*) tegelijkertijd uit een ander browservenster.

U kunt een taak met scaleR-functies verzenden. Hier volgt een voorbeeld van Hallo-opdrachten gebruikt toorun een taak:

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


U ziet dat de Hallo taken die worden verzonden onder andere gebruikersnamen in de gebruikersinterface van YARN zijn:

![Gelijktijdige gebruiker 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

Opmerking ook die Hallo toegevoegde gebruikers hebben geen hoofdmap bevoegdheden in Linux-systeem, maar ze hebben Hallo dezelfde tooall Hallo bestanden in de Hallo externe HDFS en WASB opslag openen.


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a>Hallo R-console gebruiken

1. Gebruik van Hallo SSH-sessie, Hallo opdrachtconsole toostart Hallo R te volgen:  

        R

2. Hier ziet u uitvoer vergelijkbare toohello volgende:
    
    R versie 3.2.2 (2015-08-14)--'Fire veiligheid' Copyright (C) 2015 R Foundation Hallo voor statistische Computing Platform: x86_64-pc-linux-gnu (64-bits)

    R is gratis software en wordt geleverd ZONDER ENIGE GARANTIE.
    U staat op het Welkom tooredistribute dit onder bepaalde omstandigheden.
    Typ 'license()' of 'licence()' voor distributie-informatie.

    Ondersteuning van natuurlijke taal, maar uitgevoerd in een Engelse landinstelling

    R is een samenwerkingsproject met veel inzenders.
    Typ 'contributors()' voor meer informatie en 'citation()' op hoe toocite R of R-in publicaties pakketten.

    Typ 'demo()' voor sommige demo's, voor on line help ' help()' of 'help.start()' voor een HTML-browser interface toohelp.
    Typ 'q()' tooquit R.

    Microsoft R Server versie 8.0: een verbeterde distributie van R Microsoft-pakketten Copyright (C) 2016 Microsoft Corporation

    Typ 'readme()' voor de release-opmerkingen.
    >

3. Van Hallo `>` vragen, kunt u R-code invoeren. R server bevat pakketten waarmee u tooeasily communiceren met Hadoop en gedistribueerde berekeningen uitgevoerd. Gebruik bijvoorbeeld Hallo opdracht tooview Hallo hoofdmap van Hallo standaardbestandssysteem voor Hallo HDInsight-cluster te volgen:

    rxHadoopListFiles("/")

4. U kunt ook Hallo WASB stijl adressering.

    rxHadoopListFiles("wasb:///")


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a>R Server op HDI gebruiken vanaf een extern exemplaar van Microsoft R Server of Microsoft R Client

Het is mogelijk tooset up toegang toohello HDI Hadoop Spark compute context van een extern exemplaar van Microsoft R Server of Microsoft R Client uitgevoerd op een desktop of laptop. Zie **met behulp van Microsoft R Server als een Hadoop Client** subsectie in Hallo [maken van een Compute-Context voor Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md). toodo u moet dus toospecify Hallo opties te volgen bij het definiëren van Hallo RxSpark compute context op uw laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, en sshProfileScript. Bijvoorbeeld:


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a>Een compute-context gebruiken

Een compute-context kunt u toocontrol of berekening wordt lokaal uitgevoerd op de edge-knooppunt Hallo of verdeeld over knooppunten Hallo in Hallo HDInsight-cluster.

1. Gebruik van Hallo R-console (in een SSH-sessie) of RStudio Server Hallo code tooload bijvoorbeeld gegevens te volgen in de Hallo standaard opslag voor HDInsight:

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. Vervolgens laten we enkele info gegevens maken en twee gegevensbronnen definiëren, zodat we met Hallo gegevens werken.

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. We gaan een logistic regression via Hallo-gegevens met Hallo lokale compute context worden uitgevoerd.

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    Hier ziet u uitvoer die eindigt op regels vergelijkbare toohello te volgen:

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. Vervolgens gaat uitvoeren Hallo dezelfde logistic regression met Hallo Spark context. Hallo Spark context distribueert Hallo verwerking via alle Hallo worker-knooppunten in Hallo HDInsight-cluster.

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > U kunt ook MapReduce toodistribute berekening over clusterknooppunten. Zie [Opties voor compute-context voor R Server op HDInsight](hdinsight-hadoop-r-server-compute-contexts.md) voor meer informatie over compute-context.


## <a name="distribute-r-code-toomultiple-nodes"></a>R code toomultiple knooppunten distribueren

R server, u kunt eenvoudig bestaande R-code en deze op meerdere knooppunten in cluster Hallo uitvoeren met behulp van `rxExec`. Deze functie is handig bij het uitvoeren van een parameteropschoning of van simulaties. Hallo volgende code is een voorbeeld van hoe toouse `rxExec`:

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

Als u nog steeds Hallo Spark of MapReduce-context, deze opdracht retourneert Hallo nodename waarde voor de worker-knooppunten Hallo die code Hallo `(Sys.info()["nodename"])` op wordt uitgevoerd. Bijvoorbeeld: op een cluster met vier knooppunten verwacht tooreceive vergelijkbare toohello volgende uitvoer:

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a>Toegang tot gegevens in Hive en Parquet

Een functie die beschikbaar zijn in R Server 9.1 kunt directe toegang toodata in Hive en parketvloeren voor gebruik door ScaleR functies in Hallo Spark compute-context. Deze mogelijkheden zijn beschikbaar via de nieuwe ScaleR bron gegevensfuncties RxHiveData en RxParquetData genoemd die door het gebruik van Spark SQL tooload gegevens rechtstreeks in een Spark-DataFrame voor analyse door ScaleR werken.  

Sommige voorbeeldcode biedt Hallo na code bij het gebruik van nieuwe functies Hallo:

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


Zie voor meer informatie over het gebruik van deze nieuwe functies Hallo in de online help R Server door het gebruik van Hallo `?RxHivedata` en `?RxParquetData` opdrachten.  


## <a name="install-additional-r-packages-on-hello-edge-node"></a>Extra R-pakketten installeren op Hallo edge-knooppunt

Als u tooinstall extra R-pakketten op Hallo edge-knooppunt dat wilt, kunt u `install.packages()` rechtstreeks vanuit Hallo R-console wanneer verbonden toohello edge-knooppunt via SSH. Als u tooinstall R-pakketten op Hallo worker-knooppunten van het Hallo-cluster nodig hebt, moet u echter een scriptactie gebruiken.

Scriptacties zijn Bash-scripts die gebruikt toomake configuratie wijzigingen toohello HDInsight-cluster of tooinstall aanvullende software, zoals extra R-pakketten zijn. tooinstall extra pakketten met behulp van een scriptactie gebruik Hallo stappen te volgen:

> [!IMPORTANT]
> Met behulp van scriptacties tooinstall aanvullende R-pakketten kan alleen worden gebruikt nadat Hallo-cluster is gemaakt. Gebruik deze procedure niet tijdens het maken van het cluster, zoals het Hallo-script is afhankelijk van het R Server wordt volledig geïnstalleerd en geconfigureerd.
>
>

1. Van Hallo [Azure-portal](https://portal.azure.com), selecteer uw R Server op HDInsight-cluster.

2. Van Hallo **instellingen** blade Selecteer **scriptacties** en vervolgens **nieuwe indienen** toosubmit een nieuwe scriptactie.

   ![Afbeelding van de blade Scriptacties](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. Van Hallo **scriptactie indienen** blade bieden Hallo volgende informatie:

   * **Naam**: een beschrijvende naam tooidentify dit script

   * **Bash-script-URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`

   * **Head**: dit item moet zijn **uitgeschakeld**

   * **Worker**: dit item moet zijn **ingeschakeld**

   * **Edge nodes**: dit item moet zijn **uitgeschakeld**.

   * **Zookeeper**: dit item moet zijn **uitgeschakeld**

   * **Parameters**: Hallo R-pakketten toobe geïnstalleerd. Bijvoorbeeld: `bitops stringr arules`

   * **Deze scriptactie opnieuw laten uitvoeren...** : dit item moet zijn **ingeschakeld**  

   > [!NOTE]
   > 1. Standaard worden alle R-pakketten geïnstalleerd vanuit een momentopname van Hallo Microsoft MRAN opslagplaats consistent zijn met het Hallo-versie van het R-Server die is geïnstalleerd. Als u wilt dat tooinstall nieuwere versies van pakketten, is de risico's niet compatibel. Dit soort installeren is echter mogelijk door te geven `useCRAN` als Hallo eerste element van het pakket hello wilt weergeven, bijvoorbeeld `useCRAN bitops, stringr, arules`.  
   > 2. Voor sommige R-pakketten zijn aanvullende Linux-systeembibliotheken vereist. Voor het gemak hebben we Hallo afhankelijkheden die nodig is voor Hallo top 100 meest populaire R-pakketten vooraf geïnstalleerd. Echter als Hallo R pakketten die u installeert bibliotheken afgezien van deze vereist moet vervolgens u downloaden Hallo base script hier gebruikt en stappen tooinstall Hallo systeembibliotheken toevoegen. U moet vervolgens uploaden Hallo gewijzigd script tooa openbare blob-container in Azure-opslag en Hallo gewijzigd script tooinstall hello-pakketten gebruiken.
   >    Zie [Ontwikkeling van scriptacties](hdinsight-hadoop-script-actions-linux.md) voor meer informatie over het ontwikkelen van scriptacties.  
   >
   >

   ![Een scriptactie toevoegen](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. Selecteer **maken** toorun Hallo script. Zodra het Hallo-script is voltooid, zijn Hallo R-pakketten beschikbaar op alle worker-knooppunten.


## <a name="using-microsoft-r-server-operationalization"></a>Microsoft R Server-uitoefening gebruiken

Wanneer uw gegevens modelleren voltooid is, kunt u Hallo model toomake voorspellingen operationeel te maken. tooconfigure voor Microsoft R Server uitoefening, Voer Hallo stappen te volgen:

Eerst ssh in Hallo Edge-knooppunt. Bijvoorbeeld: 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Als u met ssh, map voor relevante Hallo-versie en sudo Hallo dotnet dll-bestand te wijzigen: 

- Voor Microsoft R Server 9.1:

    cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll

- Voor Microsoft R Server 9.0:

    cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll

tooconfigure Microsoft R Server uitoefening met een 1-box-configuratie Hallo te volgen:

1. 'R-Server voor uitoefening configureren' selecteren
2. Selecteer A. Alles-in-één (web- + rekenknooppunten)
3. Geef een wachtwoord voor Hallo **admin** gebruiker

![De optie Alles-in-één](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

Als optionele stap kunt u Diagnostische controles uitvoeren door als volgt een diagnostische test uit te voeren:

1. Selecteer 6. Diagnostische tests uitvoeren
2. Selecteer A. Configuratie testen
3. Voer als gebruikersnaam Beheerder in en geef het wachtwoord uit de voorgaande configuratiestap op
4. Algehele status bevestigen = geslaagd
5. Exit Hallo beheerder hulpprogramma
6. Sluit SSH

![De optie Diagnose voor](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
>**Lange vertragingen bij het gebruiken van webservice op Spark**
>
>Als u lange vertragingen optreden als een webservice tooconsume probeert met mrsdeploy functies in de context van een Spark compute gemaakt, moet u mogelijk tooadd sommige ontbrekende mappen. Hallo Spark toepassing behoort tooa gebruiker met de naam '*rserve2*' wanneer deze wordt aangeroepen vanuit mrsdeploy functies met een webservice. toowork dit probleem oplossen:

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


In deze fase is Hallo-configuratie voor uitoefening voltooid. Nu kunt u Hallo 'mrsdeploy' pakket op uw RClient tooconnect toohello uitoefening op de edge-knooppunt en gestart met de functies, zoals [uitvoering op afstand](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) en [webservices](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette). Afhankelijk van of het cluster is ingesteld op een virtueel netwerk of niet, moet u mogelijk tooset up poort doorsturen van tunneling via SSH-aanmelding. Hallo volgende secties wordt uitgelegd hoe tooset van deze tunnel.

### <a name="rserver-cluster-on-virtual-network"></a>RServer-cluster in een virtueel netwerk

Zorg ervoor dat u toestaat dat verkeer via poort 12800 toohello edge-knooppunt. Op die manier kunt u Hallo edge-knooppunt tooconnect toohello uitoefening functie.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


Als hello `remoteLogin()` kan geen verbinding toohello edge-knooppunt, maar kunt u SSH toohello edge-knooppunt, moet u tooverify of Hallo regel tooallow verkeer op poort 12800 goed of niet is ingesteld. Als u tooface Hallo probleem doorgaat, kunt u omzeilen het door het instellen van poort doorsturen van tunneling via SSH. Voor instructies raadpleegt u de volgende sectie Hallo.

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a>RServer-cluster is niet ingesteld in het virtuele netwerk

Als het cluster niet is ingesteld in het virtuele netwerk vnet of als u problemen ondervindt met de connectiviteit via dit netwerk, kunt u forward tunneling via SSH instellen voor de poort:

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

U kunt dit ook instellen op Putty.

![Putty SSH-verbinding](./media/hdinsight-hadoop-r-server-get-started/putty.png)

Nadat uw SSH-sessie actief is, doorgestuurd verkeer van uw machine poort 12800 Hallo toohello edge-knooppunt van poort 12800 via SSH-sessie. Zorg ervoor dat u `127.0.0.1:12800` gebruikt in de `remoteLogin()`-methode. Dit uitoefening toohello rand van het knooppunt via poort doorsturen zich aanmeldt.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a>Hoe Microsoft R Server uitoefening tooscale rekenknooppunten op HDInsight worker-knooppunten

### <a name="decommission-hello-worker-nodes"></a>Hallo worker-knooppunten uit bedrijf nemen

Microsoft R Server wordt momenteel niet beheerd via Yarn. Als Hallo worker-knooppunten niet buiten gebruik wordt gesteld, werkt Hallo Yarn Resource Manager niet zoals verwacht, omdat het niet op de hoogte van Hallo resources in beslag nemen Hallo-server. In de volgorde tooavoid deze situatie wordt aangeraden Hallo worker-knooppunten uit bedrijf nemen voordat u Hallo rekenknooppunten uitbreiden.

Stappen toodecommissioning worker-knooppunten:

* Aanmelden van het cluster tooHDI Ambari-console en klikt u op het tabblad 'hosts'
* Worker-knooppunten (toobe buiten gebruik gesteld) selecteren, klikt u op 'Acties' > 'Geselecteerd Hosts' > "Hosts" > Klik op 'ON onderhoudsmodus inschakelen'. We hebben bijvoorbeeld wn3 en wn4 toodecommission geselecteerd in Hallo installatiekopie te volgen.  

   ![worker-knooppunten uit bedrijf nemen](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* Selecteer **Acties** > **Geselecteerde hosts** > **Datanodes** > klik op **Uit bedrijf nemen**
* Selecteer **Acties** > **Geselecteerde hosts** > **NodeManagers** > klik op **Uit bedrijf nemen**
* Selecteer **Acties** > **Geselecteerde hosts** > **Datanodes** > klik op **Stoppen**
* Selecteer **Acties** > **Geselecteerde hosts** > **NodeManagers** > klik op **Stoppen**
* Selecteer **Acties** > **Geselecteerde hosts** > **Hosts** > klik op **Alle onderdelen stoppen**
* Hef de selectie Hallo worker-knooppunten en Hallo hoofdknooppunten selecteren
* Selecteer **Acties** > **Geselecteerde hosts** > **Hosts** > **Alle onderdelen opnieuw starten**

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a>Rekenknooppunten configureren op elk uit bedrijf genomen worker-knooppunt

1. SSH op elk uit bedrijf genomen werkknooppunt.
2. Voer het beheerprogramma uit met behulp van `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.
3. Voer '1' tooselect optie 'Configureren R Server voor uitoefening'.
4. Geef "c" tooselect optie 'C. Rekenknooppunt te selecteren. Hiermee configureert u Hallo-rekenknooppunt op hello werkrolknooppunt.
5. Exit Hallo beheerder hulpprogramma.

### <a name="add-compute-nodes-details-on-web-node"></a>Details van rekenknooppunten toevoegen op het webknooppunt

Zodra alle buiten gebruik gestelde worker-knooppunten zijn geconfigureerd toorun rekenknooppunt, keert u terug op Hallo edge-knooppunt en buiten gebruik gestelde worker-knooppunten IP-adressen in Hallo Microsoft web knooppunt op R Server de configuratie toevoegen:

* SSH in Hallo edge-knooppunt.
* Voer `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json` uit.
* Zoek naar de sectie 'URI' hello en werkrolknooppunt van IP- en poortgegevens toevoegen.

    ![opdrachtregel worker-knooppunten uit bedrijf nemen](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a>Problemen oplossen

Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.


## <a name="next-steps"></a>Volgende stappen

Nu moet u begrijpen hoe een nieuwe HDInsight-cluster met Hallo R Server en Hallo basisbeginselen van toocreate Hallo R-console van een SSH-sessie. Hallo volgende onderwerpen wordt uitgelegd andere manieren te beheren en werken met op HDInsight R Server:

* [RStudio Server tooHDInsight toevoegen (indien niet geïnstalleerd tijdens het maken van de cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opties voor compute-context voor R Server op HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)
* [Opties voor Azure-opslag voor R Server op HDInsight](hdinsight-hadoop-r-server-storage.md)
