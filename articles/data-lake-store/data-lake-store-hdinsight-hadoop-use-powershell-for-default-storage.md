---
title: aaaCreate HDInsight-clusters met Data Lake Store als standaard opslag met behulp van PowerShell | Microsoft-Docs
description: Gebruik Azure PowerShell toocreate en HDInsight-clusters gebruiken met Azure Data Lake Store
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a>HDInsight-clusters maken met Data Lake Store als standaard opslag met behulp van PowerShell
> [!div class="op_single_selector"]
> * [Gebruik hello Azure-portal](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Gebruik PowerShell (voor opslag van de standaard)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Gebruik PowerShell (voor extra opslagruimte)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Gebruik Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

Meer informatie over hoe toouse Azure PowerShell tooconfigure Azure HDInsight-clusters met Azure Data Lake Store als standaard opslag. Zie voor instructies over het maken van een HDInsight-cluster met Data Lake Store als extra opslagruimte [een HDInsight-cluster maken met Data Lake Store als extra opslagruimte](data-lake-store-hdinsight-hadoop-use-powershell.md).

Hier volgen enkele belangrijke overwegingen voor het gebruik van HDInsight met Data Lake Store:

* Hallo optie toocreate HDInsight-clusters met toegang tooData Lake Store als standaard opslag is beschikbaar voor HDInsight versie 3.5 en 3.6.

* Hallo optie toocreate HDInsight-clusters met toegang tot tooData Lake Store omdat standaard opslag *niet beschikbaar* voor clusters van HDInsight Premium.

tooconfigure HDInsight toowork met Data Lake Store met behulp van PowerShell, volg Hallo-instructies in de volgende vijf secties Hallo.

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, controleert u dat u voldoet aan de Hallo volgens de vereisten:

* **Een Azure-abonnement**: Ga te[gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 of hoger**: Zie [hoe tooinstall PowerShell en configureren](/powershell/azure/overview).
* **Windows Software Development Kit (SDK)**: tooinstall Windows SDK te gaan[downloadt en hulpprogramma's voor Windows 10](https://dev.windows.com/en-us/downloads). Hallo SDK is gebruikte toocreate een beveiligingscertificaat.
* **Azure Active Directory-service-principal**: deze zelfstudie wordt beschreven hoe toocreate een service-principal in Azure Active Directory (Azure AD). Echter, een service-principal toocreate, moet u een Azure AD-beheerder. Als u een beheerder bent, kunt u deze vereiste overslaan en doorgaan met het Hallo-zelfstudie.

    >[!NOTE]
    >U kunt een service principal maken alleen als u een Azure AD-beheerder. Uw Azure AD-beheerder moet maken een service principal voordat u een HDInsight-cluster met Data Lake Store maken kunt. Hallo service-principal moet worden gemaakt met een certificaat, zoals beschreven in [een service-principal maken met certificaat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).
    >

## <a name="create-a-data-lake-store-account"></a>Een Data Lake Store-account maken
een Data Lake Store-account toocreate Hallo te volgen:

1. Vanaf uw bureaublad, open een PowerShell-venster en Voer Hallo codefragmenten hieronder. Wanneer u bent na vragen aan gebruiker toosign in aanmelden als een van de Hallo abonnementbeheerders of eigenaars. 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > Als u de registerbronprovider Hallo Data Lake Store en een foutbericht weergegeven dat vergelijkbaar te ontvangt`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, uw abonnement mogelijk geen goedgekeurde lijst voor Data Lake Store. tooenable uw Azure-abonnement voor de openbare preview Hallo Data Lake Store, volg de instructies in Hallo [aan de slag met Azure Data Lake Store met behulp van Azure-portal Hallo](data-lake-store-get-started-portal.md).
    >

2. Een Data Lake Store-account is gekoppeld aan een Azure-resourcegroep. Begint met het maken van een resourcegroep.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Hier ziet u uitvoer als volgt:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Een Data Lake Store-account maken. Hallo account naam die u opgeeft mag alleen kleine letters en cijfers bevatten.

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

4. Data Lake Store als standaard opslag, moet u toospecify die een hoofdmap pad toowhich Hallo clusterspecifieke tijdens het maken van het cluster bestanden worden. een hoofdpad toocreate **/clusters/hdiadlcluster** gebruiken in Hallo-fragment Hallo cmdlets volgen:

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Instellen van verificatie voor op rollen gebaseerde toegang tot tooData Lake Store
Elke Azure-abonnement is gekoppeld aan een Azure AD-entiteit. Gebruikers en services dat abonnement toegang tot de resources met behulp van Azure-portal Hallo of hello Azure Resource Manager-API moeten eerst worden geverifieerd met Azure AD. Toegang wordt verleend tooAzure abonnementen en services door toe te wijzen Hallo geschikte rol op een Azure-resource. Voor services identificeert een service-principal Hallo-service in Azure AD.

Deze sectie ziet u hoe een toepassing toogrant service, zoals HDInsight, toegang tooan Azure-resource (hello Data Lake Store-account dat u eerder hebt gemaakt). Dit doet u door het maken van een service principal voor de toepassing hello en het toewijzen van rollen tooit via PowerShell.

Hallo-taken tooset van Active Directory-verificatie voor Azure Data Lake uitvoeren in de volgende twee secties Hallo.

### <a name="create-a-self-signed-certificate"></a>Een zelfondertekend certificaat maken
Zorg ervoor dat u hebt [Windows SDK](https://dev.windows.com/en-us/downloads) geïnstalleerd voordat u doorgaat met de Hallo in deze sectie stappen. U moet hebben ook een directory hebt gemaakt, zoals *C:\mycertdir*, waarin u Hallo certificaat maken.

1. Ga in Hallo PowerShell-venster toohello locatie waar u de Windows SDK geïnstalleerd (normaal gesproken *C:\Program Files (x86) \Windows Kits\10\bin\x86*) en gebruiken van Hallo [MakeCert] [ makecert] hulpprogramma toocreate een zelfondertekend certificaat en een persoonlijke sleutel. Hallo volgende opdrachten gebruiken:

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    U zult na vragen aan gebruiker tooenter Hallo wachtwoord voor persoonlijke sleutel. Nadat het Hallo-opdracht met succes is uitgevoerd, ziet u **CertFile.cer** en **mykey.pvk** in Hallo certificaat map die u hebt opgegeven.
2. Gebruik Hallo [Pvk2Pfx] [ pvk2pfx] hulpprogramma tooconvert Hallo PVK en de .cer-bestanden die MakeCert gemaakte tooa pfx-bestand. Hallo volgende opdracht uitvoeren:

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    Wanneer u wordt gevraagd, typt u Hallo wachtwoord voor persoonlijke sleutel die u eerder hebt opgegeven. waarde die u voor Hallo opgeeft Hallo **-po** parameter is Hallo wachtwoord dat is gekoppeld aan Hallo pfx-bestand. Nadat het Hallo-opdracht is voltooid, moet u ook zien een **CertFile.pfx** in Hallo certificaat map die u hebt opgegeven.

### <a name="create-an-azure-ad-and-a-service-principal"></a>Een Azure AD maken en een service-principal
In deze sectie maakt een service-principal voor een Azure AD-toepassing, een rol toohello service-principal toewijzen en verifiëren als de service-principal Hallo door te geven van een certificaat. toocreate een toepassing in Azure AD Hallo volgende opdrachten uitvoeren:

1. Hallo-cmdlets in de PowerShell-consolevenster Hallo na plakken. Zorg ervoor dat u voor Hallo opgeeft Hallo de waarde **- weergavenaam** eigenschap uniek is. waarden voor Hallo **- startpagina** en **- IdentiferUris** tijdelijke aanduiding voor waarden zijn en worden niet geverifieerd.

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
2. Een service-principal maken met behulp van Hallo toepassings-ID.

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Verleen Hallo service principal toegang toohello Data Lake Store-hoofdmap en alle Hallo mappen in Hallo hoofdpad die u eerder hebt opgegeven. Gebruik Hallo cmdlets volgen:

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a>Een HDInsight Linux-cluster maken met Data Lake Store als Hallo standaard opslag

In deze sectie maakt u een HDInsight Hadoop Linux-cluster met Data Lake Store als Hallo standaard opslag. Voor deze release Hallo HDInsight-cluster en Data Lake Store moet Hallo dezelfde locatie.

1. Hallo abonnement tenant-ID ophalen en opslaan toouse later.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. Hallo HDInsight-cluster maken met behulp van Hallo cmdlets volgen:

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    Nadat het Hallo-cmdlet is voltooid, ziet u uitvoer met een lijst met Hallo clusterdetails.

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a>Testtaken uitvoeren op Hallo HDInsight-cluster toouse Data Lake Store
Nadat u een HDInsight-cluster hebt geconfigureerd, kunt u testtaken uitvoeren op het tooensure dat toegang Data Lake Store tot. toodo dus een voorbeeld Hive-taak toocreate een tabel uitvoeren die gebruikmaakt van voorbeeldgegevens Hallo die al beschikbaar is in Data Lake Store op  *<cluster root>/example/data/sample.log*.

U maakt een verbinding Secure Shell (SSH) in Hallo HDInsight Linux-cluster dat u hebt gemaakt in deze sectie en voert u een voorbeeld Hive-query.

* Als u een Windows-client toomake Hallo-cluster met een SSH-verbinding gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Als u een Linux-client toomake Hallo-cluster met een SSH-verbinding gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

1. Als u Hallo verbinding hebt gemaakt, start u met behulp van de volgende opdracht Hallo Hallo Hive-opdrachtregelinterface (CLI):

        hive
2. Gebruik Hallo CLI tooenter hello toocreate instructies een nieuwe tabel met de naam na **voertuigen** met behulp van de voorbeeldgegevens Hallo in Data Lake Store:

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    U ziet Hallo query-uitvoer op Hallo SSH-console.

    >[!NOTE]
    >Hallo pad toohello voorbeeldgegevens in Hallo voorafgaand aan de opdracht CREATE TABLE is `adl:///example/data/`, waarbij `adl:///` basis Hallo-cluster. Volgende Hallo voorbeeld van een basis-Hallo cluster die opgegeven in deze zelfstudie, Hallo-opdracht is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`. Gebruik Hallo korter alternatief of Hallo volledige pad toohello cluster hoofdmap bieden.
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a>Toegang tot Data Lake Store via de HDFS-opdrachten
Nadat u Hallo HDInsight cluster toouse Data Lake Store hebt geconfigureerd, kunt u Hadoop Distributed File System (HDFS) shell-opdrachten tooaccess Hallo store.

In deze sectie maakt u een SSH-verbinding in Hallo HDInsight Linux-cluster dat u hebt gemaakt en Voer Hallo HDFS-opdrachten.

* Als u een Windows-client toomake Hallo-cluster met een SSH-verbinding gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Als u een Linux-client toomake Hallo-cluster met een SSH-verbinding gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

Nadat u Hallo verbinding hebt gemaakt, kunt u de Hallo-bestanden in Data Lake Store weergeven met behulp van de volgende opdracht voor HDFS file system Hallo.

    hdfs dfs -ls adl:///

U kunt ook Hallo `hdfs dfs -put` opdracht tooupload sommige bestanden tooData Lake Store en gebruik vervolgens `hdfs dfs -ls` tooverify of Hallo bestanden geüpload.

## <a name="see-also"></a>Zie ook
* [Azure-portal: Maak een HDInsight-cluster toouse Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
