---
titel: aaa "PowerShell: Azure HDInsight-cluster met Data Lake Store als extra opslag | Microsoft Docs' services: data lake store, hdinsight documentationcenter: '' auteur: nitinme manager: jhubbard-editor: cgronlun

MS.AssetID: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: gegevensarchief-lake ms.devlang: na ms.topic: artikel ms.tgt_pltfrm: n.v.t. ms.workload: big data ms.date: 08-06/2017 ms.author: nitinme

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a>Azure PowerShell toocreate een HDInsight-cluster gebruiken met Data Lake Store (als extra opslag)
> [!div class="op_single_selector"]
> * [Portal gebruiken](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Met behulp van PowerShell (voor opslag van de standaard)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Met behulp van PowerShell (voor extra opslagruimte)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Resource Manager gebruiken](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Meer informatie over hoe toouse Azure PowerShell tooconfigure een HDInsight-cluster met Azure Data Lake Store **als extra opslagruimte**. Zie voor instructies over hoe toocreate een HDInsight-cluster met Azure Data Lake Store als standaard opslag, [een HDInsight-cluster maken met Data Lake Store als standaard opslag](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).

> [!NOTE]
> Als u toouse Azure Data Lake Store als extra opslag voor HDInsight-cluster gaat, wordt aangeraden dat u dit doen terwijl u Hallo-cluster maakt, zoals beschreven in dit artikel. Het toevoegen van Azure Data Lake Store als extra opslagruimte tooan is bestaand HDInsight-cluster een ingewikkeld proces en foutgevoelige tooerrors.
>

Voor ondersteunde clustertypen, kan Data Lake Store worden gebruikt als een standaard-opslag- of aanvullende storage-account. Wanneer Data Lake Store als extra opslagruimte wordt gebruikt, Hallo storage-standaardaccount voor Hallo clusters is nog steeds Azure Storage-Blobs (WASB) en Hallo cluster-gerelateerde bestanden (zoals Logboeken, enzovoort) worden nog steeds geschreven toohello standaard opslag tijdens het Hallo-gegevens die u hebt gewenste tooprocess kunnen worden opgeslagen in een Data Lake Store-account. Met behulp van Data Lake Store als extra storage-account heeft geen gevolgen voor prestaties of de Hallo mogelijkheid tooread schrijftijd toohello opslag van Hallo-cluster.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>Met behulp van Data Lake Store voor opslag van HDInsight-cluster

Hier volgen enkele belangrijke overwegingen voor het gebruik van HDInsight met Data Lake Store:

* Optie toocreate HDInsight-clusters met toegang tooData Lake Store als extra opslag is beschikbaar voor HDInsight versie 3.2, 3.4, 3.5 en 3.6.

Configureren van HDInsight omvat toowork met Data Lake Store met behulp van PowerShell Hallo stappen te volgen:

* Maken van een Azure Data Lake Store
* Instellen van verificatie voor op rollen gebaseerde toegang tot tooData Lake Store
* HDInsight-cluster maken met verificatie tooData Lake Store
* Een testtaak op Hallo cluster uitvoeren

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 of hoger**. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).
* **Windows-SDK**. Kunt u het installeren van [hier](https://dev.windows.com/en-us/downloads). U gebruikt deze toocreate een beveiligingscertificaat.
* **Azure Active Directory Service-Principal**. Stappen in deze zelfstudie bieden instructies over het toocreate een service-principal in Azure AD. U moet echter een Azure AD-beheerder toobe kunnen toocreate een service-principal. Als u een Azure AD-beheerder bent, kunt u deze vereiste overslaan en doorgaan met het Hallo-zelfstudie.

    **Als u niet een Azure AD-beheerder**, u zich niet kunnen tooperform Hallo stappen vereist toocreate een service-principal. In dat geval moet uw Azure AD-beheerder eerst een service-principal maken voordat u een HDInsight-cluster met Data Lake Store maken kunt. Bovendien Hallo service-principal moet worden gemaakt met een certificaat, zoals beschreven op [een service-principal maken met certificaat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-azure-data-lake-store"></a>Maken van een Azure Data Lake Store
Volg deze stappen toocreate een Data Lake Store.

1. Op het bureaublad een nieuw Azure PowerShell-venster openen en voer de volgende codefragment Hallo. Wanneer de vraag toolog, zorg ervoor dat u zich aanmelden als een beheerder/eigenaar Hallo abonnement:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > Als u een foutbericht weergegeven dat vergelijkbaar te ontvangt`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` bij het registreren van Hallo Data Lake Store-resourceprovider, is het mogelijk dat uw abonnement niet goedgekeurde lijst voor Azure Data Lake Store is. Zorg ervoor dat u uw Azure-abonnement voor de openbare preview van Data Lake Store inschakelen door het volgende [instructies](data-lake-store-get-started-portal.md).
   >
   >
2. Een Azure Data Lake Store-account is gekoppeld aan een Azure-resourcegroep. Maak daarom eerst een Azure-resourcegroep.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Hier ziet u uitvoer als volgt:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Maak een Azure Data Lake Store-account. Hallo account naam die u opgeeft moet alleen kleine letters en cijfers bevatten.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    Hier ziet u uitvoer Hallo volgende:

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. Sommige sample data tooAzure Data Lake uploaden. We gebruiken deze verderop in dit artikel tooverify dat Hallo gegevens toegankelijk vanuit een HDInsight-cluster is. Als u een aantal gegevens voorbeeld tooupload zoekt, kunt u krijgen Hallo **Ambulance Data** map uit Hallo [Azure Data Lake Git-opslagplaats](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Instellen van verificatie voor op rollen gebaseerde toegang tot tooData Lake Store
Elke Azure-abonnement is gekoppeld aan een Azure Active Directory. Gebruikers en services die toegang tot bronnen van het Hallo-abonnement met Hallo klassieke Azure-Portal of Azure Resource Manager-API moeten eerst worden geverifieerd met die Azure Active Directory. Toegang wordt verleend tooAzure abonnementen en services door toe te wijzen Hallo geschikte rol op een Azure-resource.  Voor services identificeert een service-principal Hallo-service in hello Azure Active Directory (AAD). Deze sectie wordt beschreven hoe een toepassing toogrant service, zoals HDInsight, toegang tooan Azure-resource (hello Azure Data Lake Store-account die u eerder hebt gemaakt) door het maken van een service-principal voor de toepassing hello en toewijzen van rollen toothat via Azure PowerShell.

tooset van Active Directory-verificatie voor Azure Data Lake moet u Hallo volgende taken uitvoeren.

* Een zelfondertekend certificaat maken
* Een toepassing in Azure Active Directory en een Service-Principal maken

### <a name="create-a-self-signed-certificate"></a>Een zelfondertekend certificaat maken
Zorg ervoor dat u hebt [Windows SDK](https://dev.windows.com/en-us/downloads) geïnstalleerd voordat u doorgaat met de Hallo in deze sectie stappen. U moet hebben ook een directory hebt gemaakt, zoals **C:\mycertdir**, waar Hallo certificaat wordt gemaakt.

1. Ga vanuit de PowerShell-venster Hallo toohello locatie waar u de Windows SDK geïnstalleerd (meestal `C:\Program Files (x86)\Windows Kits\10\bin\x86` en gebruik Hallo [MakeCert] [ makecert] hulpprogramma toocreate een zelfondertekend certificaat en een persoonlijke sleutel. Hallo volgende opdrachten gebruiken.

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    U zult na vragen aan gebruiker tooenter Hallo wachtwoord voor persoonlijke sleutel. Nadat het Hallo-opdracht met succes wordt uitgevoerd, ziet u een **CertFile.cer** en **mykey.pvk** in Hallo certificaat directory die u hebt opgegeven.
2. Gebruik Hallo [Pvk2Pfx] [ pvk2pfx] hulpprogramma tooconvert Hallo PVK en de .cer-bestanden die MakeCert gemaakte tooa pfx-bestand. Hallo volgende opdracht worden uitgevoerd.

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    Als u wordt gevraagd Hallo persoonlijke wachtwoord invoeren u eerder hebt opgegeven. waarde die u voor Hallo opgeeft Hallo **-po** parameter is Hallo wachtwoord dat is gekoppeld aan Hallo pfx-bestand. Nadat het Hallo-opdracht is voltooid, ziet u ook een CertFile.pfx in Hallo certificaat directory die u hebt opgegeven.

### <a name="create-an-azure-active-directory-and-a-service-principal"></a>Een Azure Active Directory en een service-principal maken
In deze sectie Hallo stappen toocreate een service-principal uitvoeren voor een Azure Active Directory-toepassing, een functie toohello service-principal toewijzen en verifiëren als de service-principal Hallo door te geven van een certificaat. Hallo opdrachten toocreate na een toepassing in Azure Active Directory uitgevoerd.

1. Hallo-cmdlets in de PowerShell-consolevenster Hallo na plakken. Zorg ervoor Hallo-waarde die u voor Hallo opgeeft **- weergavenaam** eigenschap uniek is. Bovendien Hallo waarden voor **- startpagina** en **- IdentiferUris** tijdelijke aanduiding voor waarden zijn en worden niet geverifieerd.

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. Maken van een service-principal met behulp van Hallo toepassings-ID.

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Hallo-principal toegang toohello Data Lake Store-map en het Hallo-bestand dat u vanuit Hallo HDInsight-cluster wordt openen verlenen. Hallo codefragment hieronder biedt toegang tot toohello hoofdmap Hallo Data Lake Store-account (waar u gekopieerd Hallo voorbeeldgegevensbestand) en Hallo bestand zelf.

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a>Een HDInsight Linux-cluster maken met Data Lake Store als extra opslagruimte

In deze sectie maken we een HDInsight Hadoop Linux-cluster met Data Lake Store als extra opslagruimte. Voor deze release Hallo HDInsight-cluster en Hallo Data Lake Store moeten zich op Hallo dezelfde locatie.

1. Beginnen met het ophalen van Hallo abonnement tenant-ID. U moet die later.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. Voor deze release kan voor Hadoop-cluster Data Lake Store alleen worden gebruikt als extra opslag voor Hallo-cluster. Hallo standaard opslag worden nog steeds hello Azure storage-blobs (WASB). Dus eerst maakt u Hallo storage-account en opslag containers vereist voor Hallo-cluster.

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. Hallo HDInsight-cluster maken. Gebruik hello cmdlets volgen.

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    Nadat het Hallo-cmdlet is voltooid, ziet u uitvoer Hallo clusterdetails van de aanbieding.


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Testtaken uitvoeren op Hallo HDInsight-cluster toouse Hallo Data Lake Store
Nadat u een HDInsight-cluster hebt geconfigureerd, kunt u uitvoeren testtaken op Hallo cluster tootest die Hallo HDInsight cluster toegang heeft tot Data Lake Store. toodo dus voeren we een voorbeeld Hive-taak die u een tabel met voorbeeldgegevens Hallo maakt dat u hebt geüpload eerdere tooyour Data Lake Store.

In deze sectie kunt u SSH in HDInsight Linux cluster u gemaakt en vervolgens een Hive-voorbeeldquery uitvoert Hallo Hallo gaat.

* Als u een Windows client-tooSSH in Hallo cluster gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Als u een Linux-client tooSSH in Hallo cluster gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

1. Eenmaal zijn verbonden, start u Hallo CLI Hive via Hallo volgende opdracht:

        hive
2. Gebruik Hallo CLI Hallo na toocreate instructies een nieuwe tabel met de naam te geven **voertuigen** met behulp van de voorbeeldgegevens Hallo in Hallo Data Lake Store:

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    U ziet een uitvoer vergelijkbare toohello volgende:

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a>Toegang tot Data Lake Store met HDFS-opdrachten
Wanneer u Hallo HDInsight cluster toouse Data Lake Store hebt geconfigureerd, kunt u Hallo HDFS shell-opdrachten tooaccess Hallo store.

In deze sectie wordt u SSH in Hallo HDInsight Linux cluster u gemaakt en Hallo HDFS-opdrachten uitvoeren.

* Als u een Windows client-tooSSH in Hallo cluster gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Als u een Linux-client tooSSH in Hallo cluster gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

Eenmaal zijn verbonden, gebruik Hallo HDFS bestandssysteem toolist Hallo opdrachtbestanden in Hallo Data Lake Store te volgen.

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

Hallo-bestand dat u hebt geüpload eerdere toohello Data Lake Store moet u deze lijst.

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

U kunt ook Hallo `hdfs dfs -put` opdracht tooupload sommige bestanden toohello Data Lake Store en gebruik vervolgens `hdfs dfs -ls` tooverify of Hallo bestanden geüpload.

## <a name="see-also"></a>Zie ook
* [Portal: Maak een HDInsight-cluster toouse Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
