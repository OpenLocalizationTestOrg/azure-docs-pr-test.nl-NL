---
<span data-ttu-id="3f7f6-101">titel: aaa "PowerShell: Azure HDInsight-cluster met Data Lake Store als extra opslag | Microsoft Docs' services: data lake store, hdinsight documentationcenter: '' auteur: nitinme manager: jhubbard-editor: cgronlun</span><span class="sxs-lookup"><span data-stu-id="3f7f6-101">title: aaa"PowerShell: Azure HDInsight cluster with Data Lake Store as add-on storage | Microsoft Docs" services: data-lake-store,hdinsight documentationcenter: '' author: nitinme manager: jhubbard editor: cgronlun</span></span>

<span data-ttu-id="3f7f6-102">MS.AssetID: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: gegevensarchief-lake ms.devlang: na ms.topic: artikel ms.tgt_pltfrm: n.v.t. ms.workload: big data ms.date: 08-06/2017 ms.author: nitinme</span><span class="sxs-lookup"><span data-stu-id="3f7f6-102">ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: data-lake-store ms.devlang: na ms.topic: article ms.tgt_pltfrm: na ms.workload: big-data ms.date: 06/08/2017 ms.author: nitinme</span></span>

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="3f7f6-103">Azure PowerShell toocreate een HDInsight-cluster gebruiken met Data Lake Store (als extra opslag)</span><span class="sxs-lookup"><span data-stu-id="3f7f6-103">Use Azure PowerShell toocreate an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3f7f6-104">Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="3f7f6-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="3f7f6-105">Met behulp van PowerShell (voor opslag van de standaard)</span><span class="sxs-lookup"><span data-stu-id="3f7f6-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="3f7f6-106">Met behulp van PowerShell (voor extra opslagruimte)</span><span class="sxs-lookup"><span data-stu-id="3f7f6-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="3f7f6-107">Resource Manager gebruiken</span><span class="sxs-lookup"><span data-stu-id="3f7f6-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="3f7f6-108">Meer informatie over hoe toouse Azure PowerShell tooconfigure een HDInsight-cluster met Azure Data Lake Store **als extra opslagruimte**.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="3f7f6-109">Zie voor instructies over hoe toocreate een HDInsight-cluster met Azure Data Lake Store als standaard opslag, [een HDInsight-cluster maken met Data Lake Store als standaard opslag](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span><span class="sxs-lookup"><span data-stu-id="3f7f6-109">For instructions on how toocreate an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3f7f6-110">Als u toouse Azure Data Lake Store als extra opslag voor HDInsight-cluster gaat, wordt aangeraden dat u dit doen terwijl u Hallo-cluster maakt, zoals beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-110">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="3f7f6-111">Het toevoegen van Azure Data Lake Store als extra opslagruimte tooan is bestaand HDInsight-cluster een ingewikkeld proces en foutgevoelige tooerrors.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-111">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

<span data-ttu-id="3f7f6-112">Voor ondersteunde clustertypen, kan Data Lake Store worden gebruikt als een standaard-opslag- of aanvullende storage-account.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-112">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="3f7f6-113">Wanneer Data Lake Store als extra opslagruimte wordt gebruikt, Hallo storage-standaardaccount voor Hallo clusters is nog steeds Azure Storage-Blobs (WASB) en Hallo cluster-gerelateerde bestanden (zoals Logboeken, enzovoort) worden nog steeds geschreven toohello standaard opslag tijdens het Hallo-gegevens die u hebt gewenste tooprocess kunnen worden opgeslagen in een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-113">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="3f7f6-114">Met behulp van Data Lake Store als extra storage-account heeft geen gevolgen voor prestaties of de Hallo mogelijkheid tooread schrijftijd toohello opslag van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-114">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="3f7f6-115">Met behulp van Data Lake Store voor opslag van HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="3f7f6-115">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="3f7f6-116">Hier volgen enkele belangrijke overwegingen voor het gebruik van HDInsight met Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="3f7f6-116">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="3f7f6-117">Optie toocreate HDInsight-clusters met toegang tooData Lake Store als extra opslag is beschikbaar voor HDInsight versie 3.2, 3.4, 3.5 en 3.6.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-117">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="3f7f6-118">Configureren van HDInsight omvat toowork met Data Lake Store met behulp van PowerShell Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3f7f6-118">Configuring HDInsight toowork with Data Lake Store using PowerShell involves hello following steps:</span></span>

* <span data-ttu-id="3f7f6-119">Maken van een Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3f7f6-119">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="3f7f6-120">Instellen van verificatie voor op rollen gebaseerde toegang tot tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="3f7f6-120">Set up authentication for role-based access tooData Lake Store</span></span>
* <span data-ttu-id="3f7f6-121">HDInsight-cluster maken met verificatie tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="3f7f6-121">Create HDInsight cluster with authentication tooData Lake Store</span></span>
* <span data-ttu-id="3f7f6-122">Een testtaak op Hallo cluster uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3f7f6-122">Run a test job on hello cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f7f6-123">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3f7f6-123">Prerequisites</span></span>
<span data-ttu-id="3f7f6-124">Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="3f7f6-124">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="3f7f6-125">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-125">**An Azure subscription**.</span></span> <span data-ttu-id="3f7f6-126">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3f7f6-126">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3f7f6-127">**Azure PowerShell 1.0 of hoger**.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-127">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="3f7f6-128">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3f7f6-128">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="3f7f6-129">**Windows-SDK**.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-129">**Windows SDK**.</span></span> <span data-ttu-id="3f7f6-130">Kunt u het installeren van [hier](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="3f7f6-130">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="3f7f6-131">U gebruikt deze toocreate een beveiligingscertificaat.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-131">You use this toocreate a security certificate.</span></span>
* <span data-ttu-id="3f7f6-132">**Azure Active Directory Service-Principal**.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-132">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="3f7f6-133">Stappen in deze zelfstudie bieden instructies over het toocreate een service-principal in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-133">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="3f7f6-134">U moet echter een Azure AD-beheerder toobe kunnen toocreate een service-principal.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-134">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="3f7f6-135">Als u een Azure AD-beheerder bent, kunt u deze vereiste overslaan en doorgaan met het Hallo-zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-135">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="3f7f6-136">**Als u niet een Azure AD-beheerder**, u zich niet kunnen tooperform Hallo stappen vereist toocreate een service-principal.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-136">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="3f7f6-137">In dat geval moet uw Azure AD-beheerder eerst een service-principal maken voordat u een HDInsight-cluster met Data Lake Store maken kunt.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-137">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="3f7f6-138">Bovendien Hallo service-principal moet worden gemaakt met een certificaat, zoals beschreven op [een service-principal maken met certificaat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="3f7f6-138">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="3f7f6-139">Maken van een Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3f7f6-139">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="3f7f6-140">Volg deze stappen toocreate een Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-140">Follow these steps toocreate a Data Lake Store.</span></span>

1. <span data-ttu-id="3f7f6-141">Op het bureaublad een nieuw Azure PowerShell-venster openen en voer de volgende codefragment Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-141">From your desktop, open a new Azure PowerShell window, and enter hello following snippet.</span></span> <span data-ttu-id="3f7f6-142">Wanneer de vraag toolog, zorg ervoor dat u zich aanmelden als een beheerder/eigenaar Hallo abonnement:</span><span class="sxs-lookup"><span data-stu-id="3f7f6-142">When prompted toolog in, make sure you log in as one of hello subscription administrator/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="3f7f6-143">Als u een foutbericht weergegeven dat vergelijkbaar te ontvangt`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` bij het registreren van Hallo Data Lake Store-resourceprovider, is het mogelijk dat uw abonnement niet goedgekeurde lijst voor Azure Data Lake Store is.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-143">If you receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` when registering hello Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="3f7f6-144">Zorg ervoor dat u uw Azure-abonnement voor de openbare preview van Data Lake Store inschakelen door het volgende [instructies](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3f7f6-144">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="3f7f6-145">Een Azure Data Lake Store-account is gekoppeld aan een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-145">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="3f7f6-146">Maak daarom eerst een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-146">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="3f7f6-147">Hier ziet u uitvoer als volgt:</span><span class="sxs-lookup"><span data-stu-id="3f7f6-147">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="3f7f6-148">Maak een Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-148">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="3f7f6-149">Hallo account naam die u opgeeft moet alleen kleine letters en cijfers bevatten.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-149">hello account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="3f7f6-150">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="3f7f6-150">You should see an output like hello following:</span></span>

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

5. <span data-ttu-id="3f7f6-151">Sommige sample data tooAzure Data Lake uploaden.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-151">Upload some sample data tooAzure Data Lake.</span></span> <span data-ttu-id="3f7f6-152">We gebruiken deze verderop in dit artikel tooverify dat Hallo gegevens toegankelijk vanuit een HDInsight-cluster is.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-152">We'll use this later in this article tooverify that hello data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="3f7f6-153">Als u een aantal gegevens voorbeeld tooupload zoekt, kunt u krijgen Hallo **Ambulance Data** map uit Hallo [Azure Data Lake Git-opslagplaats](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="3f7f6-153">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="3f7f6-154">Instellen van verificatie voor op rollen gebaseerde toegang tot tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="3f7f6-154">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="3f7f6-155">Elke Azure-abonnement is gekoppeld aan een Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-155">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="3f7f6-156">Gebruikers en services die toegang tot bronnen van het Hallo-abonnement met Hallo klassieke Azure-Portal of Azure Resource Manager-API moeten eerst worden geverifieerd met die Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-156">Users and services that access resources of hello subscription using hello Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="3f7f6-157">Toegang wordt verleend tooAzure abonnementen en services door toe te wijzen Hallo geschikte rol op een Azure-resource.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-157">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span>  <span data-ttu-id="3f7f6-158">Voor services identificeert een service-principal Hallo-service in hello Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="3f7f6-158">For services, a service principal identifies hello service in hello Azure Active Directory (AAD).</span></span> <span data-ttu-id="3f7f6-159">Deze sectie wordt beschreven hoe een toepassing toogrant service, zoals HDInsight, toegang tooan Azure-resource (hello Azure Data Lake Store-account die u eerder hebt gemaakt) door het maken van een service-principal voor de toepassing hello en toewijzen van rollen toothat via Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-159">This section illustrates how toogrant an application service, like HDInsight, access tooan Azure resource (hello Azure Data Lake Store account you created earlier) by creating a service principal for hello application and assigning roles toothat via Azure PowerShell.</span></span>

<span data-ttu-id="3f7f6-160">tooset van Active Directory-verificatie voor Azure Data Lake moet u Hallo volgende taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-160">tooset up Active Directory authentication for Azure Data Lake, you must perform hello following tasks.</span></span>

* <span data-ttu-id="3f7f6-161">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="3f7f6-161">Create a self-signed certificate</span></span>
* <span data-ttu-id="3f7f6-162">Een toepassing in Azure Active Directory en een Service-Principal maken</span><span class="sxs-lookup"><span data-stu-id="3f7f6-162">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="3f7f6-163">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="3f7f6-163">Create a self-signed certificate</span></span>
<span data-ttu-id="3f7f6-164">Zorg ervoor dat u hebt [Windows SDK](https://dev.windows.com/en-us/downloads) geïnstalleerd voordat u doorgaat met de Hallo in deze sectie stappen.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-164">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="3f7f6-165">U moet hebben ook een directory hebt gemaakt, zoals **C:\mycertdir**, waar Hallo certificaat wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-165">You must have also created a directory, such as **C:\mycertdir**, where hello certificate will be created.</span></span>

1. <span data-ttu-id="3f7f6-166">Ga vanuit de PowerShell-venster Hallo toohello locatie waar u de Windows SDK geïnstalleerd (meestal `C:\Program Files (x86)\Windows Kits\10\bin\x86` en gebruik Hallo [MakeCert] [ makecert] hulpprogramma toocreate een zelfondertekend certificaat en een persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-166">From hello PowerShell window, navigate toohello location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="3f7f6-167">Hallo volgende opdrachten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-167">Use hello following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="3f7f6-168">U zult na vragen aan gebruiker tooenter Hallo wachtwoord voor persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-168">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="3f7f6-169">Nadat het Hallo-opdracht met succes wordt uitgevoerd, ziet u een **CertFile.cer** en **mykey.pvk** in Hallo certificaat directory die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-169">After hello command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in hello certificate directory you specified.</span></span>
2. <span data-ttu-id="3f7f6-170">Gebruik Hallo [Pvk2Pfx] [ pvk2pfx] hulpprogramma tooconvert Hallo PVK en de .cer-bestanden die MakeCert gemaakte tooa pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-170">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="3f7f6-171">Hallo volgende opdracht worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-171">Run hello following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="3f7f6-172">Als u wordt gevraagd Hallo persoonlijke wachtwoord invoeren u eerder hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-172">When prompted enter hello private key password you specified earlier.</span></span> <span data-ttu-id="3f7f6-173">waarde die u voor Hallo opgeeft Hallo **-po** parameter is Hallo wachtwoord dat is gekoppeld aan Hallo pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-173">hello value you specify for hello **-po** parameter is hello password that is associated with hello .pfx file.</span></span> <span data-ttu-id="3f7f6-174">Nadat het Hallo-opdracht is voltooid, ziet u ook een CertFile.pfx in Hallo certificaat directory die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-174">After hello command successfully completes, you should also see a CertFile.pfx in hello certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="3f7f6-175">Een Azure Active Directory en een service-principal maken</span><span class="sxs-lookup"><span data-stu-id="3f7f6-175">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="3f7f6-176">In deze sectie Hallo stappen toocreate een service-principal uitvoeren voor een Azure Active Directory-toepassing, een functie toohello service-principal toewijzen en verifiëren als de service-principal Hallo door te geven van een certificaat.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-176">In this section, you perform hello steps toocreate a service principal for an Azure Active Directory application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="3f7f6-177">Hallo opdrachten toocreate na een toepassing in Azure Active Directory uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-177">Run hello following commands toocreate an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="3f7f6-178">Hallo-cmdlets in de PowerShell-consolevenster Hallo na plakken.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-178">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="3f7f6-179">Zorg ervoor Hallo-waarde die u voor Hallo opgeeft **- weergavenaam** eigenschap uniek is.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-179">Make sure hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="3f7f6-180">Bovendien Hallo waarden voor **- startpagina** en **- IdentiferUris** tijdelijke aanduiding voor waarden zijn en worden niet geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-180">Also, hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="3f7f6-181">Maken van een service-principal met behulp van Hallo toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-181">Create a service principal using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="3f7f6-182">Hallo-principal toegang toohello Data Lake Store-map en het Hallo-bestand dat u vanuit Hallo HDInsight-cluster wordt openen verlenen.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-182">Grant hello service principal access toohello Data Lake Store folder and hello file that you will access from hello HDInsight cluster.</span></span> <span data-ttu-id="3f7f6-183">Hallo codefragment hieronder biedt toegang tot toohello hoofdmap Hallo Data Lake Store-account (waar u gekopieerd Hallo voorbeeldgegevensbestand) en Hallo bestand zelf.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-183">hello snippet below provides access toohello root of hello Data Lake Store account (where you copied hello sample data file), and hello file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="3f7f6-184">Een HDInsight Linux-cluster maken met Data Lake Store als extra opslagruimte</span><span class="sxs-lookup"><span data-stu-id="3f7f6-184">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="3f7f6-185">In deze sectie maken we een HDInsight Hadoop Linux-cluster met Data Lake Store als extra opslagruimte.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-185">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="3f7f6-186">Voor deze release Hallo HDInsight-cluster en Hallo Data Lake Store moeten zich op Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-186">For this release, hello HDInsight cluster and hello Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="3f7f6-187">Beginnen met het ophalen van Hallo abonnement tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-187">Start with retrieving hello subscription tenant ID.</span></span> <span data-ttu-id="3f7f6-188">U moet die later.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-188">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="3f7f6-189">Voor deze release kan voor Hadoop-cluster Data Lake Store alleen worden gebruikt als extra opslag voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-189">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for hello cluster.</span></span> <span data-ttu-id="3f7f6-190">Hallo standaard opslag worden nog steeds hello Azure storage-blobs (WASB).</span><span class="sxs-lookup"><span data-stu-id="3f7f6-190">hello default storage will still be hello Azure storage blobs (WASB).</span></span> <span data-ttu-id="3f7f6-191">Dus eerst maakt u Hallo storage-account en opslag containers vereist voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-191">So, we'll first create hello storage account and storage containers required for hello cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="3f7f6-192">Hallo HDInsight-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-192">Create hello HDInsight cluster.</span></span> <span data-ttu-id="3f7f6-193">Gebruik hello cmdlets volgen.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-193">Use hello following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="3f7f6-194">Nadat het Hallo-cmdlet is voltooid, ziet u uitvoer Hallo clusterdetails van de aanbieding.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-194">After hello cmdlet successfully completes, you should see an output listing hello cluster details.</span></span>


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="3f7f6-195">Testtaken uitvoeren op Hallo HDInsight-cluster toouse Hallo Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3f7f6-195">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="3f7f6-196">Nadat u een HDInsight-cluster hebt geconfigureerd, kunt u uitvoeren testtaken op Hallo cluster tootest die Hallo HDInsight cluster toegang heeft tot Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-196">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="3f7f6-197">toodo dus voeren we een voorbeeld Hive-taak die u een tabel met voorbeeldgegevens Hallo maakt dat u hebt geüpload eerdere tooyour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-197">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="3f7f6-198">In deze sectie kunt u SSH in HDInsight Linux cluster u gemaakt en vervolgens een Hive-voorbeeldquery uitvoert Hallo Hallo gaat.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-198">In this section you will SSH into hello HDInsight Linux cluster you created and run hello a sample Hive query.</span></span>

* <span data-ttu-id="3f7f6-199">Als u een Windows client-tooSSH in Hallo cluster gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="3f7f6-199">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="3f7f6-200">Als u een Linux-client tooSSH in Hallo cluster gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="3f7f6-200">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="3f7f6-201">Eenmaal zijn verbonden, start u Hallo CLI Hive via Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3f7f6-201">Once connected, start hello Hive CLI by using hello following command:</span></span>

        hive
2. <span data-ttu-id="3f7f6-202">Gebruik Hallo CLI Hallo na toocreate instructies een nieuwe tabel met de naam te geven **voertuigen** met behulp van de voorbeeldgegevens Hallo in Hallo Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="3f7f6-202">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="3f7f6-203">U ziet een uitvoer vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="3f7f6-203">You should see an output similar toohello following:</span></span>

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

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="3f7f6-204">Toegang tot Data Lake Store met HDFS-opdrachten</span><span class="sxs-lookup"><span data-stu-id="3f7f6-204">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="3f7f6-205">Wanneer u Hallo HDInsight cluster toouse Data Lake Store hebt geconfigureerd, kunt u Hallo HDFS shell-opdrachten tooaccess Hallo store.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-205">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="3f7f6-206">In deze sectie wordt u SSH in Hallo HDInsight Linux cluster u gemaakt en Hallo HDFS-opdrachten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-206">In this section you will SSH into hello HDInsight Linux cluster you created and run hello HDFS commands.</span></span>

* <span data-ttu-id="3f7f6-207">Als u een Windows client-tooSSH in Hallo cluster gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="3f7f6-207">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="3f7f6-208">Als u een Linux-client tooSSH in Hallo cluster gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="3f7f6-208">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="3f7f6-209">Eenmaal zijn verbonden, gebruik Hallo HDFS bestandssysteem toolist Hallo opdrachtbestanden in Hallo Data Lake Store te volgen.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-209">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="3f7f6-210">Hallo-bestand dat u hebt geüpload eerdere toohello Data Lake Store moet u deze lijst.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-210">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="3f7f6-211">U kunt ook Hallo `hdfs dfs -put` opdracht tooupload sommige bestanden toohello Data Lake Store en gebruik vervolgens `hdfs dfs -ls` tooverify of Hallo bestanden geüpload.</span><span class="sxs-lookup"><span data-stu-id="3f7f6-211">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="3f7f6-212">Zie ook</span><span class="sxs-lookup"><span data-stu-id="3f7f6-212">See Also</span></span>
* [<span data-ttu-id="3f7f6-213">Portal: Maak een HDInsight-cluster toouse Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3f7f6-213">Portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
