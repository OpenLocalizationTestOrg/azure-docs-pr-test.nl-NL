---
title: aaaRestrict toegang met behulp van Shared Access Signatures - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Shared Access Signatures toorestrict HDInsight toegang krijgen tot toodata opgeslagen in Azure storage-blobs.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a>Azure Storage Shared Access Signatures toorestrict toegang toodata in HDInsight gebruiken

HDInsight heeft volledige toegang toodata in hello Azure Storage-accounts die zijn gekoppeld aan het Hallo-cluster. U kunt de handtekeningen voor gedeelde toegang op Hallo blob-container toorestrict toegang toohello gegevens. Bijvoorbeeld: tooprovide alleen-lezentoegang toohello gegevens. Shared Access Signatures (SAS) zijn een functie van Azure storage-accounts waarmee u toolimit toegang toodata. Bijvoorbeeld, het bieden van alleen-lezentoegang toodata.

> [!IMPORTANT]
> Voor een oplossing met behulp van Apache Zwerver, kunt u met HDInsight domein. Zie voor meer informatie, Hallo [HDInsight domein configureren](hdinsight-domain-joined-configure.md) document.

> [!WARNING]
> HDInsight moet hebben volledige toegang toohello standaard opslagruimte voor Hallo-cluster.

## <a name="requirements"></a>Vereisten

* Een Azure-abonnement
* C# of Python. C#-voorbeeldcode is opgegeven als een Visual Studio-oplossing.

  * Visual Studio moet versie 2013 of 2015 2017
  * Python moet 2.7 of hoger zijn

* Een Linux gebaseerde HDInsight-cluster of [Azure PowerShell] [ powershell] -als u een bestaand cluster op basis van Linux hebt, kunt u Ambari tooadd een Shared Access Signature toohello-cluster. Zo niet, kunt u gebruik van Azure PowerShell toocreate een cluster en het toevoegen van een Shared Access Signature tijdens het maken van het cluster.

    > [!IMPORTANT]
    > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* van de voorbeeldbestanden van Hallo [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature). Deze bibliotheek bevat de volgende items Hallo:

  * Een Visual Studio-project dat een storage-container, opgeslagen beleid en SAS voor gebruik met HDInsight maken kunt
  * Een pythonscript die een storage-container, opgeslagen beleid en SAS voor gebruik met HDInsight maken kunt
  * Een PowerShell-script dat van een HDInsight maken kan-cluster en configureert u het toouse Hallo SAS.

## <a name="shared-access-signatures"></a>Handtekeningen voor gedeelde toegang

Er zijn twee soorten handtekeningen voor gedeelde toegang:

* Ad hoc: Hallo starttijd, verlooptijd en machtigingen voor Hallo SAS zijn opgegeven op Hallo SAS-URI.

* Opgeslagen toegangsbeleid: een opgeslagen-beleid is gedefinieerd in een resourcecontainer, zoals een blob-container. Een beleid kan worden gebruikt toomanage beperkingen voor een of meer handtekeningen voor gedeelde toegang. Wanneer u een SAS aan een opgeslagen toegangsbeleid koppelt, Hallo SAS neemt over Hallo beperkingen - Hallo starttijd, verlooptijd en machtigingen - zijn opgegeven voor toegangsbeleid Hallo opgeslagen.

Hallo verschil tussen twee Hallo formulieren is belangrijk voor één key '-scenario: intrekken. Een SAS is een URL, zodat iedereen die Hallo SAS verkrijgt deze gebruiken kunt, ongeacht wie het aangevraagde toobegin met. Als een SAS openbaar wordt gepubliceerd, kan deze worden gebruikt door iedereen in Hallo wereld. Een SA's dat wordt gedistribueerd is geldig tot vier dingen gebeurt:

1. Hallo verlooptijd opgegeven op Hallo die SAS is bereikt.

2. Hallo verlooptijd opgegeven op Hallo opgeslagen toegangsbeleid waarnaar wordt verwezen door Hallo die SAS is bereikt. Hallo volgende scenario's ervoor zorgen dat het verlooptijdstip Hallo toobe bereikt:

    * Hallo tijdsinterval is verstreken.
    * Hallo opgeslagen toegangsbeleid is gewijzigde toohave een verlooptijd in de afgelopen Hallo. Wijzigen van het verlooptijdstip Hallo is eenrichtingssessie toorevoke Hallo SAS.

3. Hallo toegangsbeleid waarnaar wordt verwezen door Hallo die SAS wordt verwijderd, die een andere manier toorevoke Hallo SAS is opgeslagen. Als u opnieuw maken Hallo opgeslagen-beleid met dezelfde naam, SAS-tokens voor Hallo Hallo vorige beleid zijn geldig (als Hallo verlooptijd op Hallo SAS is niet verstreken). Als u van plan toorevoke Hallo SAS bent, zijn ervoor toouse een andere naam op als u het Hallo-beleid met een verlooptijd in toekomstige Hallo opnieuw maken.

4. Hallo accountsleutel die gebruikt toocreate Hallo SAS is wordt gegenereerd. Opnieuw genereren Hallo-sleutel zorgt ervoor dat alle toepassingen die gebruikmaken van de vorige sleutel toofail verificatie Hallo. Werk alle onderdelen toohello nieuwe sleutel.

> [!IMPORTANT]
> Een shared access signature-URI is gekoppeld aan Hallo account key gebruikte toocreate Hallo handtekening en Hallo opgeslagen toegangsbeleid dat is gekoppeld (indien aanwezig). Als er geen opgeslagen toegangsbeleid is opgegeven, is hello alleen manier toorevoke een shared access signature toochange hello accountsleutel.

Het is raadzaam om altijd opgeslagen toegangsbeleid te gebruiken. Als u opgeslagen beleid, kunt u handtekeningen intrekken of vervaldatum Hallo uitbreiden naar behoefte. Hallo stappen in dit document wordt opgeslagen toegang beleid toogenerate SAS gebruikt.

Zie voor meer informatie over handtekeningen voor gedeelde toegang [Understanding Hallo SAS-model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="create-a-stored-policy-and-sas-using-c"></a>Maak een opgeslagen beleid en de SAS met C\#

1. Hallo-oplossing in Visual Studio openen.

2. Klik in Solution Explorer met de rechtermuisknop op Hallo **SASToken** project en selecteer **eigenschappen**.

3. Selecteer **instellingen** en waarden voor de volgende vermeldingen Hallo toevoegen:

   * StorageConnectionString: Hallo verbinding tekenreeks voor Hallo storage-account dat u wilt dat toocreate een opgeslagen beleid en een SAS voor. Hallo-indeling moet `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` waar `myaccount` Hallo-naam van uw opslagaccount en `mykey` is Hallo-sleutel voor Hallo storage-account.

   * ContainerName: Hallo-container in Hallo storage-account die u wilt dat de toegang tot toorestrict.

   * SASPolicyName: Hallo naam toouse voor Hallo opgeslagen beleid toocreate.

   * FileToUpload: Hallo pad tooa bestand dat is geüpload toohello container.

4. Hallo-project uitvoeren. Informatie vergelijkbare toohello na de tekst wordt weergegeven zodra Hallo SAS is gegenereerd:

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Hallo SAS-beleid token, opslagaccountnaam en containernaam opslaan. Deze waarden worden gebruikt wanneer Hallo storage-account koppelen aan uw HDInsight-cluster.

### <a name="create-a-stored-policy-and-sas-using-python"></a>Maak een opgeslagen beleid en de SAS met behulp van Python

1. Open Hallo SASToken.py bestand en wijzig Hallo volgende waarden:

   * beleid\_naam: Hallo naam toouse voor Hallo beleid toocreate opgeslagen.

   * opslag\_account\_naam: Hallo-naam van uw opslagaccount.

   * opslag\_account\_sleutel: Hallo-sleutel voor Hallo storage-account.

   * opslag\_container\_naam: Hallo-container in Hallo storage-account die u wilt dat de toegang tot toorestrict.

   * voorbeeld\_bestand\_pad: Hallo pad tooa-bestand dat is geüpload toohello container.

2. Hallo-script uitvoeren. Hallo SAS-token vergelijkbare toohello tekst volgen wanneer Hallo-script is voltooid wordt weergegeven:

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Hallo SAS-beleid token, opslagaccountnaam en containernaam opslaan. Deze waarden worden gebruikt wanneer Hallo storage-account koppelen aan uw HDInsight-cluster.

## <a name="use-hello-sas-with-hdinsight"></a>Hallo SAS gebruiken met HDInsight

Wanneer u een HDInsight-cluster maakt, moet u een primaire opslagaccount opgeven en kunt u eventueel extra opslagaccounts opgeven. Beide methoden voor het toevoegen van opslag vereist volledige toegang toohello storage-accounts en containers die worden gebruikt.

toouse een Shared Access Signature toolimit toegang tooa container, Voeg een aangepaste vermelding toohello **core site** configuratie voor Hallo-cluster.

* Voor **Windows gebaseerde** of **op basis van Linux** HDInsight-clusters, kunt u Hallo-vermelding toevoegen tijdens het maken van het cluster met behulp van PowerShell.
* Voor **op basis van Linux** HDInsight-clusters Hallo configuratie na het maken van het cluster met Ambari wijzigen.

### <a name="create-a-cluster-that-uses-hello-sas"></a>Maken van een cluster dat gebruik maakt van Hallo SAS

Een voorbeeld van het maken van een HDInsight-cluster dat gebruik Hallo SAS is opgenomen in Hallo `CreateCluster` map van Hallo-opslagplaats. toouse ervan gebruik Hallo volgende stappen:

1. Open Hallo `CreateCluster\HDInsightSAS.ps1` bestand in een teksteditor en wijzig Hallo waarden aan begin van document Hallo Hallo te volgen.

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    Wijzig bijvoorbeeld `'mycluster'` toohello naam Hallo-cluster dat u wilt dat toocreate. Hallo SAS waarden moeten overeenkomen met waarden uit de vorige stappen Hallo Hallo biedt bij het maken van een opslagaccount en SAS-token.

    Zodra u Hallo waarden hebt gewijzigd, moet u Hallo bestand opslaan.

2. Open een nieuw Azure PowerShell-opdrachtprompt. Als u niet bekend met Azure PowerShell bent of niet hebt geïnstalleerd, raadpleegt u [installeren en configureren van Azure PowerShell][powershell].

1. Gebruik vanaf Hallo prompt Hallo opdracht tooauthenticate tooyour Azure-abonnement te volgen:

    ```powershell
    Login-AzureRmAccount
    ```

    Wanneer u wordt gevraagd, aanmelden met Hallo-account voor uw Azure-abonnement.

    Als uw account gekoppeld aan meerdere Azure-abonnementen is, moet u mogelijk toouse `Select-AzureRmSubscription` tooselect Hallo abonnement u toouse wenst.

4. Wijzig vanaf Hallo-prompt mappen toohello `CreateCluster` directory die Hallo HDInsightSAS.ps1 bestand bevat. Gebruik vervolgens de volgende opdrachtscript toorun Hallo Hallo

    ```powershell
    .\HDInsightSAS.ps1
    ```

    Als het Hallo-script wordt uitgevoerd, geregistreerd in het logboek uitvoer toohello PowerShell-prompt als het Hallo-resource groep en storage-accounts maakt. U bent na vragen aan gebruiker tooenter Hallo HTTP gebruiker voor Hallo HDInsight-cluster. Dit account is gebruikte toosecure HTTP/s toegang toohello cluster.

    Als u een cluster op basis van Linux maakt, wordt u gevraagd om een SSH-gebruikersnaam voor account en wachtwoord. Dit account is gebruikte tooremotely toohello cluster aanmelden.

   > [!IMPORTANT]
   > Als u wordt gevraagd om Hallo HTTP/s of SSH-gebruikersnaam en wachtwoord, moet u een wachtwoord dat voldoet aan de volgende criteria Hallo opgeven:
   >
   > * Ten minste 10 tekens lang moet zijn
   > * Moet ten minste één cijfer bevatten
   > * Moet ten minste één niet-alfanumeriek teken bevatten
   > * Moet ten minste één hoofdletter of kleine letter bevatten

Het duurt lang voordat deze toocomplete script meestal ongeveer 15 minuten. Wanneer het Hallo-script is voltooid zonder fouten, is Hallo-cluster gemaakt.

### <a name="use-hello-sas-with-an-existing-cluster"></a>Hallo SAS gebruiken met een bestaand cluster

Als u een bestaand cluster op basis van Linux hebt, kunt u Hallo SAS toohello toevoegen **core site** configuratie met behulp van Hallo stappen te volgen:

1. Open Hallo Ambari-webgebruikersinterface voor uw cluster. Hallo-adres voor deze pagina is https://YOURCLUSTERNAME.azurehdinsight.net. Wanneer u wordt gevraagd, worden geverifieerd toohello cluster met behulp van de naam van de serverbeheerder hello (admin) en het wachtwoord die u hebt gebruikt toen Hallo cluster maken.

2. Selecteer in het Hallo-zijde van Hallo Ambari-webgebruikersinterface links, **HDFS** en selecteer vervolgens Hallo **Configs** tabblad in het midden van de pagina Hallo Hallo.

3. Selecteer Hallo **Geavanceerd** tabblad en schuif totdat u Hallo **aangepaste core-site** sectie.

4. Vouw Hallo **aangepaste core-site** sectie vervolgens schuiven toohello einde en selecteer Hallo **eigenschap toevoegen...**  koppeling. Gebruik Hallo volgende waarden voor Hallo **sleutel** en **waarde** velden:

   * **Sleutel**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net
   * **Waarde**: Hallo SAS geretourneerd door Hallo C# of Python-toepassing die u eerder hebt uitgevoerd.

     Vervang **CONTAINERNAME** met Hallo containernaam die u gebruikt met Hallo C# of SAS-toepassing. Vervang **STORAGEACCOUNTNAME** met Hallo opslagaccountnaam die u hebt gebruikt.

5. Klik op Hallo **toevoegen** knop toosave deze sleutel en waarde en klik op Hallo **opslaan** knop toosave Hallo configuratiewijzigingen. Wanneer u wordt gevraagd, een beschrijving van Hallo wijzigen ('toe te voegen toegang tot de SAS-opslag' bijvoorbeeld) toevoegen en klik vervolgens op **opslaan**.

    Klik op **OK** wanneer Hallo wijzigingen zijn voltooid.

   > [!IMPORTANT]
   > U moet verschillende services opnieuw starten voordat Hallo wijziging van kracht.

6. In Hallo Ambari-webgebruikersinterface, selecteer **HDFS** in Hallo-lijst op Hallo links en selecteer vervolgens **start opnieuw alle** van Hallo **serviceacties** vervolgkeuzelijst op de juiste Hallo. Wanneer u wordt gevraagd, selecteert u **onderhoudsmodus inschakelen** en vervolgens selecteert __Conform alle opnieuw starten '.

    Herhaal dit proces voor MapReduce2 en YARN.

7. Zodra het Hallo-services opnieuw hebt opgestart, selecteren en uitschakelen van onderhoudsmodus van Hallo **serviceacties** vervolgkeuzelijst.

## <a name="test-restricted-access"></a>Testen met beperkte toegang

tooverify die hebt u beperkte toegang, gebruik Hallo volgende methoden:

* Voor **Windows gebaseerde** HDInsight-clusters, extern bureaublad tooconnect toohello cluster gebruiken. Zie voor meer informatie [tooHDInsight met RDP verbinding](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

    Eenmaal zijn verbonden, gebruikt u Hallo **Hadoop opdrachtregelprogramma** pictogram op Hallo bureaublad tooopen vanaf de opdrachtprompt.

* Voor **op basis van Linux** SSH tooconnect toohello cluster voor HDInsight-clusters gebruiken. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

Eenmaal zijn verbonden toohello cluster, gebruikt u Hallo stappen tooverify kunt u alleen lezen en de lijst met items op Hallo SAS storage-account te volgen:

1. toolist hello inhoud van de container hello, Hallo volgende opdracht uit Hallo prompt gebruiken: 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    Vervang **SASCONTAINER** met de naam van de Hallo van Hallo-container gemaakt voor Hallo SAS storage-account. Vervang **SASACCOUNTNAME** met de naam Hallo van Hallo storage-account gebruikt voor Hallo SAS.

    Hallo-lijst bevat Hallo bestand geüpload wanneer Hallo-container en SAS zijn gemaakt.

2. Gebruik Hallo volgende opdracht tooverify dat u inhoud Hallo van Hallo-bestand kan lezen. Vervang Hallo **SASCONTAINER** en **SASACCOUNTNAME** zoals in de vorige stap Hallo. Vervang **FILENAME** met de naam van Hallo-bestand weergegeven in de vorige opdracht Hallo Hallo:

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    Met deze opdracht worden Hallo inhoud van Hallo-bestand.

3. Hallo opdracht toodownload Hallo bestand toohello lokaal bestandssysteem volgende gebruiken:

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    Met deze opdracht downloads Hallo tooa lokale bestand met de naam **testbestand.txt**.

4. Gebruik Hallo volgende opdracht tooupload Hallo lokaal bestand tooa nieuw bestand met de naam **testupload.txt** op Hallo SAS-opslag:

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    U ontvangt een bericht vergelijkbaar toohello volgende tekst:

        put: java.io.IOException

    Deze fout treedt op omdat de opslaglocatie Hallo lezen + alleen lijst. Gebruik Hallo volgende opdracht tooput Hallo gegevens op Hallo standaard opslag voor Hallo-cluster kunnen geschreven worden:

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    Deze tijd Hallo-bewerking is voltooid.

## <a name="troubleshooting"></a>Problemen oplossen

### <a name="a-task-was-canceled"></a>Een taak is geannuleerd

**Symptomen**: bij het maken van een cluster met behulp van PowerShell-script hello, krijgt u Hallo volgende foutbericht weergegeven:

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

**Oorzaak**: deze fout kan optreden als u een wachtwoord voor Hallo beheerder/HTTP-gebruiker voor Hallo cluster of (voor op basis van Linux-clusters) Hallo SSH-gebruiker.

**Resolutie**: geen wachtwoord gebruiken dat voldoet aan de volgende criteria Hallo:

* Ten minste 10 tekens lang moet zijn
* Moet ten minste één cijfer bevatten
* Moet ten minste één niet-alfanumeriek teken bevatten
* Moet ten minste één hoofdletter of kleine letter bevatten

## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe tooadd opslag met beperkte toegang tooyour HDInsight-cluster, informatie over andere manieren toowork met gegevens op het cluster:

* [Hive gebruiken met HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met HDInsight](hdinsight-use-pig.md)
* [MapReduce gebruiken met HDInsight](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
