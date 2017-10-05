---
title: 'PowerShell: Azure HDInsight-cluster met Data Lake Store als extra opslag | Microsoft Docs'
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/08/2017
ms.author: nitinme
ms.openlocfilehash: 7a7069adab5742a9dae2833c13a1db57337a41a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-create-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="ac86c-102">Azure PowerShell gebruiken voor het maken van een HDInsight-cluster met Data Lake Store (als extra opslag)</span><span class="sxs-lookup"><span data-stu-id="ac86c-102">Use Azure PowerShell to create an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac86c-103">Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="ac86c-103">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="ac86c-104">Met behulp van PowerShell (voor opslag van de standaard)</span><span class="sxs-lookup"><span data-stu-id="ac86c-104">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="ac86c-105">Met behulp van PowerShell (voor extra opslagruimte)</span><span class="sxs-lookup"><span data-stu-id="ac86c-105">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="ac86c-106">Resource Manager gebruiken</span><span class="sxs-lookup"><span data-stu-id="ac86c-106">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="ac86c-107">Informatie over het gebruik van Azure PowerShell voor het configureren van een HDInsight-cluster met Azure Data Lake Store **als extra opslagruimte**.</span><span class="sxs-lookup"><span data-stu-id="ac86c-107">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="ac86c-108">Zie voor instructies over het maken van een HDInsight-cluster met Azure Data Lake Store als standaard opslag [een HDInsight-cluster maken met Data Lake Store als standaard opslag](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span><span class="sxs-lookup"><span data-stu-id="ac86c-108">For instructions on how to create an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ac86c-109">Als u Azure Data Lake Store als extra opslag voor HDInsight-cluster wilt gebruiken, is het raadzaam dat te doen terwijl u het cluster maakt zoals beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="ac86c-109">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span></span> <span data-ttu-id="ac86c-110">Azure Data Lake Store als extra opslagruimte toevoegen aan een bestaand HDInsight-cluster is een ingewikkeld proces en gevoelig voor fouten.</span><span class="sxs-lookup"><span data-stu-id="ac86c-110">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is a complicated process and prone to errors.</span></span>
>

<span data-ttu-id="ac86c-111">Voor ondersteunde clustertypen, kan Data Lake Store worden gebruikt als een standaard-opslag- of aanvullende storage-account.</span><span class="sxs-lookup"><span data-stu-id="ac86c-111">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="ac86c-112">Wanneer Data Lake Store als extra opslagruimte wordt gebruikt, is het standaardopslagaccount voor de clusters nog steeds Azure Storage-Blobs (WASB) en de cluster-gerelateerde bestanden (zoals Logboeken, enz.) worden nog steeds naar de standaard-opslag geschreven terwijl de gegevens die u wilt laten verwerken, kunnen worden opgeslagen in een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="ac86c-112">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="ac86c-113">Met behulp van Data Lake Store als extra storage-account heeft geen gevolgen voor prestaties of de mogelijkheid om te lezen/schrijven naar de opslag van het cluster.</span><span class="sxs-lookup"><span data-stu-id="ac86c-113">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="ac86c-114">Met behulp van Data Lake Store voor opslag van HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="ac86c-114">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="ac86c-115">Hier volgen enkele belangrijke overwegingen voor het gebruik van HDInsight met Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="ac86c-115">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="ac86c-116">De optie voor het maken van HDInsight-clusters met toegang tot Data Lake Store als extra opslag beschikbaar voor HDInsight versie 3.2, 3.4 3.5 en 3.6.</span><span class="sxs-lookup"><span data-stu-id="ac86c-116">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="ac86c-117">HDInsight werken met Data Lake Store configureren omvat met behulp van PowerShell de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="ac86c-117">Configuring HDInsight to work with Data Lake Store using PowerShell involves the following steps:</span></span>

* <span data-ttu-id="ac86c-118">Maken van een Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ac86c-118">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="ac86c-119">Verificatie voor op rollen gebaseerde toegang tot Data Lake Store instellen</span><span class="sxs-lookup"><span data-stu-id="ac86c-119">Set up authentication for role-based access to Data Lake Store</span></span>
* <span data-ttu-id="ac86c-120">HDInsight-cluster maken met Data Lake Store-verificatie</span><span class="sxs-lookup"><span data-stu-id="ac86c-120">Create HDInsight cluster with authentication to Data Lake Store</span></span>
* <span data-ttu-id="ac86c-121">Een testtaak voor uitvoeren op het cluster</span><span class="sxs-lookup"><span data-stu-id="ac86c-121">Run a test job on the cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac86c-122">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ac86c-122">Prerequisites</span></span>
<span data-ttu-id="ac86c-123">Voordat u met deze zelfstudie begint, moet u het volgende hebben of hebben gedaan:</span><span class="sxs-lookup"><span data-stu-id="ac86c-123">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="ac86c-124">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ac86c-124">**An Azure subscription**.</span></span> <span data-ttu-id="ac86c-125">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ac86c-125">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ac86c-126">**Azure PowerShell 1.0 of hoger**.</span><span class="sxs-lookup"><span data-stu-id="ac86c-126">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="ac86c-127">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ac86c-127">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="ac86c-128">**Windows-SDK**.</span><span class="sxs-lookup"><span data-stu-id="ac86c-128">**Windows SDK**.</span></span> <span data-ttu-id="ac86c-129">Kunt u het installeren van [hier](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="ac86c-129">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="ac86c-130">Hiermee u maakt een beveiligingscertificaat.</span><span class="sxs-lookup"><span data-stu-id="ac86c-130">You use this to create a security certificate.</span></span>
* <span data-ttu-id="ac86c-131">**Azure Active Directory Service-Principal**.</span><span class="sxs-lookup"><span data-stu-id="ac86c-131">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="ac86c-132">De stappen in deze zelfstudie bevatten instructies voor het maken van een service-principal in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac86c-132">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="ac86c-133">U moet echter een Azure AD-beheerder om te kunnen maken van een service-principal.</span><span class="sxs-lookup"><span data-stu-id="ac86c-133">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="ac86c-134">Als u een Azure AD-beheerder bent, kunt u deze vereiste overslaan en doorgaan met de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ac86c-134">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="ac86c-135">**Als u niet een Azure AD-beheerder**, u kan niet worden de stappen die zijn vereist voor het maken van een service-principal uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ac86c-135">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="ac86c-136">In dat geval moet uw Azure AD-beheerder eerst een service-principal maken voordat u een HDInsight-cluster met Data Lake Store maken kunt.</span><span class="sxs-lookup"><span data-stu-id="ac86c-136">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="ac86c-137">Ook de service-principal moet worden gemaakt met een certificaat, zoals beschreven op [een service-principal maken met certificaat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="ac86c-137">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="ac86c-138">Maken van een Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ac86c-138">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="ac86c-139">Volg deze stappen voor het maken van een Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ac86c-139">Follow these steps to create a Data Lake Store.</span></span>

1. <span data-ttu-id="ac86c-140">Een nieuw Azure PowerShell-venster openen vanaf het bureaublad en voer het volgende fragment.</span><span class="sxs-lookup"><span data-stu-id="ac86c-140">From your desktop, open a new Azure PowerShell window, and enter the following snippet.</span></span> <span data-ttu-id="ac86c-141">Als u wordt gevraagd om aan te melden, zorg er dan voor dat u zich aanmelden als een beheerder/eigenaar van het abonnement:</span><span class="sxs-lookup"><span data-stu-id="ac86c-141">When prompted to log in, make sure you log in as one of the subscription administrator/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="ac86c-142">Als u een foutmelding die vergelijkbaar is met `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` bij het registreren van de resourceprovider Data Lake Store is het mogelijk dat uw abonnement niet goedgekeurde lijst voor Azure Data Lake Store is.</span><span class="sxs-lookup"><span data-stu-id="ac86c-142">If you receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` when registering the Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="ac86c-143">Zorg ervoor dat u uw Azure-abonnement voor de openbare preview van Data Lake Store inschakelen door het volgende [instructies](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ac86c-143">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="ac86c-144">Een Azure Data Lake Store-account is gekoppeld aan een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ac86c-144">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="ac86c-145">Maak daarom eerst een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ac86c-145">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="ac86c-146">Hier ziet u uitvoer als volgt:</span><span class="sxs-lookup"><span data-stu-id="ac86c-146">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="ac86c-147">Maak een Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="ac86c-147">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="ac86c-148">De accountnaam die u opgeeft voor het mag alleen kleine letters en cijfers bevatten.</span><span class="sxs-lookup"><span data-stu-id="ac86c-148">The account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="ac86c-149">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="ac86c-149">You should see an output like the following:</span></span>

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

5. <span data-ttu-id="ac86c-150">Voorbeeldgegevens uploadt naar Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ac86c-150">Upload some sample data to Azure Data Lake.</span></span> <span data-ttu-id="ac86c-151">We gebruiken deze verderop in dit artikel om te controleren of de gegevens toegankelijk is vanaf een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ac86c-151">We'll use this later in this article to verify that the data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="ac86c-152">Als u nog geen voorbeeldgegevens hebt om te uploaden, kunt u de map **Ambulance Data** uit de [Azure Data Lake Git-opslagplaats](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ac86c-152">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path to data>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="ac86c-153">Verificatie voor op rollen gebaseerde toegang tot Data Lake Store instellen</span><span class="sxs-lookup"><span data-stu-id="ac86c-153">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="ac86c-154">Elke Azure-abonnement is gekoppeld aan een Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ac86c-154">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="ac86c-155">Gebruikers en services die toegang tot bronnen van het abonnement met de klassieke Azure-Portal of Azure Resource Manager-API moeten eerst worden geverifieerd met die Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ac86c-155">Users and services that access resources of the subscription using the Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="ac86c-156">Toegang te krijgen tot Azure-abonnementen en services door het toewijzen van de juiste rol op een Azure-resource.</span><span class="sxs-lookup"><span data-stu-id="ac86c-156">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span>  <span data-ttu-id="ac86c-157">Voor services identificeert een service-principal in de Azure Active Directory (AAD) van de service.</span><span class="sxs-lookup"><span data-stu-id="ac86c-157">For services, a service principal identifies the service in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="ac86c-158">Deze sectie ziet u hoe u een toepassingsservice,, zoals HDInsight, toegang tot een Azure-resource (de Azure Data Lake Store-account u eerder hebt gemaakt) verlenen door het maken van een service-principal voor de toepassing en rollen toewijzen aan die via Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac86c-158">This section illustrates how to grant an application service, like HDInsight, access to an Azure resource (the Azure Data Lake Store account you created earlier) by creating a service principal for the application and assigning roles to that via Azure PowerShell.</span></span>

<span data-ttu-id="ac86c-159">Als u Active Directory-verificatie voor Azure Data Lake instelt, moet u de volgende taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ac86c-159">To set up Active Directory authentication for Azure Data Lake, you must perform the following tasks.</span></span>

* <span data-ttu-id="ac86c-160">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="ac86c-160">Create a self-signed certificate</span></span>
* <span data-ttu-id="ac86c-161">Een toepassing in Azure Active Directory en een Service-Principal maken</span><span class="sxs-lookup"><span data-stu-id="ac86c-161">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="ac86c-162">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="ac86c-162">Create a self-signed certificate</span></span>
<span data-ttu-id="ac86c-163">Zorg ervoor dat u hebt [Windows SDK](https://dev.windows.com/en-us/downloads) geïnstalleerd voordat u doorgaat met de stappen in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="ac86c-163">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="ac86c-164">U moet hebben ook een directory hebt gemaakt, zoals **C:\mycertdir**, waar het certificaat wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ac86c-164">You must have also created a directory, such as **C:\mycertdir**, where the certificate will be created.</span></span>

1. <span data-ttu-id="ac86c-165">Ga naar de locatie waar u de Windows SDK geïnstalleerd vanuit het PowerShell-venster (meestal `C:\Program Files (x86)\Windows Kits\10\bin\x86` en gebruik de [MakeCert] [ makecert] hulpprogramma om een zelfondertekend certificaat en een persoonlijke sleutel te maken.</span><span class="sxs-lookup"><span data-stu-id="ac86c-165">From the PowerShell window, navigate to the location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="ac86c-166">Gebruik de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="ac86c-166">Use the following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="ac86c-167">U wordt gevraagd om in te voeren van het wachtwoord van de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="ac86c-167">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="ac86c-168">Nadat u de opdracht met succes wordt uitgevoerd, ziet u een **CertFile.cer** en **mykey.pvk** in de opgegeven map voor het certificaat.</span><span class="sxs-lookup"><span data-stu-id="ac86c-168">After the command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in the certificate directory you specified.</span></span>
2. <span data-ttu-id="ac86c-169">Gebruik de [Pvk2Pfx] [ pvk2pfx] hulpprogramma voor het converteren van de PVK en de .cer-bestanden die MakeCert gemaakt naar een pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="ac86c-169">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="ac86c-170">Voer de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="ac86c-170">Run the following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="ac86c-171">Als u wordt gevraagd het wachtwoord voor persoonlijke invoeren u eerder hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ac86c-171">When prompted enter the private key password you specified earlier.</span></span> <span data-ttu-id="ac86c-172">De waarde die u opgeeft voor de **-po** parameter is het wachtwoord dat is gekoppeld aan het .pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="ac86c-172">The value you specify for the **-po** parameter is the password that is associated with the .pfx file.</span></span> <span data-ttu-id="ac86c-173">Nadat u de opdracht is voltooid, ziet u ook een CertFile.pfx in de opgegeven map voor het certificaat.</span><span class="sxs-lookup"><span data-stu-id="ac86c-173">After the command successfully completes, you should also see a CertFile.pfx in the certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="ac86c-174">Een Azure Active Directory en een service-principal maken</span><span class="sxs-lookup"><span data-stu-id="ac86c-174">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="ac86c-175">In deze sectie voert u de stappen voor het maken van een service principal voor een Azure Active Directory-toepassing, een rol toewijzen aan de service-principal en verifiëren als de service-principal door te geven van een certificaat.</span><span class="sxs-lookup"><span data-stu-id="ac86c-175">In this section, you perform the steps to create a service principal for an Azure Active Directory application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="ac86c-176">Voer de volgende opdrachten om te maken van een toepassing in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ac86c-176">Run the following commands to create an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="ac86c-177">Plak de volgende cmdlets in het venster PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="ac86c-177">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="ac86c-178">Zorg ervoor dat de waarde die u opgeeft voor de **- weergavenaam** eigenschap uniek is.</span><span class="sxs-lookup"><span data-stu-id="ac86c-178">Make sure the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="ac86c-179">Ook kunnen de waarden voor **- startpagina** en **- IdentiferUris** tijdelijke aanduiding voor waarden zijn en worden niet geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="ac86c-179">Also, the values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter the password" # This is the password you specified for the .pfx file

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
2. <span data-ttu-id="ac86c-180">Maken van een service-principal met behulp van de toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="ac86c-180">Create a service principal using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="ac86c-181">De service principal toegang verlenen tot de Data Lake Store-map en het bestand dat u toegang hebben tot van het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ac86c-181">Grant the service principal access to the Data Lake Store folder and the file that you will access from the HDInsight cluster.</span></span> <span data-ttu-id="ac86c-182">Het onderstaande codefragment biedt toegang tot de hoofdmap van het Data Lake Store-account (waarin het voorbeeldgegevensbestand), en het bestand zelf.</span><span class="sxs-lookup"><span data-stu-id="ac86c-182">The snippet below provides access to the root of the Data Lake Store account (where you copied the sample data file), and the file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="ac86c-183">Een HDInsight Linux-cluster maken met Data Lake Store als extra opslagruimte</span><span class="sxs-lookup"><span data-stu-id="ac86c-183">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="ac86c-184">In deze sectie maken we een HDInsight Hadoop Linux-cluster met Data Lake Store als extra opslagruimte.</span><span class="sxs-lookup"><span data-stu-id="ac86c-184">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="ac86c-185">Voor deze versie van het HDInsight-cluster en de Data Lake Store moeten op dezelfde locatie bevinden.</span><span class="sxs-lookup"><span data-stu-id="ac86c-185">For this release, the HDInsight cluster and the Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="ac86c-186">Beginnen met het ophalen van de tenant abonnements-ID.</span><span class="sxs-lookup"><span data-stu-id="ac86c-186">Start with retrieving the subscription tenant ID.</span></span> <span data-ttu-id="ac86c-187">U moet die later.</span><span class="sxs-lookup"><span data-stu-id="ac86c-187">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="ac86c-188">Voor deze release kan voor Hadoop-cluster Data Lake Store alleen worden gebruikt als extra opslag voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="ac86c-188">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for the cluster.</span></span> <span data-ttu-id="ac86c-189">De standaard opslag worden nog steeds de blobs in Azure storage (WASB).</span><span class="sxs-lookup"><span data-stu-id="ac86c-189">The default storage will still be the Azure storage blobs (WASB).</span></span> <span data-ttu-id="ac86c-190">Dus eerst maakt u de storage-account en storage-containers die zijn vereist voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="ac86c-190">So, we'll first create the storage account and storage containers required for the cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="ac86c-191">Het HDInsight-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="ac86c-191">Create the HDInsight cluster.</span></span> <span data-ttu-id="ac86c-192">De volgende cmdlets gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ac86c-192">Use the following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have the same name for the cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="ac86c-193">Nadat de cmdlet is voltooid, ziet u uitvoer de clusterdetails van de aanbieding.</span><span class="sxs-lookup"><span data-stu-id="ac86c-193">After the cmdlet successfully completes, you should see an output listing the cluster details.</span></span>


## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="ac86c-194">Testtaken uitvoeren op het HDInsight-cluster te gebruiken van de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ac86c-194">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="ac86c-195">Nadat u een HDInsight-cluster hebt geconfigureerd, kunt u testtaken uitvoeren op het cluster om te testen of de HDInsight-cluster toegang Data Lake Store tot.</span><span class="sxs-lookup"><span data-stu-id="ac86c-195">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="ac86c-196">Om dit te doen, voeren we een voorbeeld Hive-taak die u maakt een tabel met de voorbeeldgegevens die u eerder hebt geüpload naar uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ac86c-196">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="ac86c-197">In deze sectie wordt u SSH in het cluster voor HDInsight Linux u gemaakt en voer de een Hive-voorbeeldquery.</span><span class="sxs-lookup"><span data-stu-id="ac86c-197">In this section you will SSH into the HDInsight Linux cluster you created and run the a sample Hive query.</span></span>

* <span data-ttu-id="ac86c-198">Als u een Windows-client voor SSH in het cluster gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ac86c-198">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="ac86c-199">Als u een Linux-client voor SSH in het cluster gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="ac86c-199">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="ac86c-200">Eenmaal zijn verbonden, start u de CLI Hive met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ac86c-200">Once connected, start the Hive CLI by using the following command:</span></span>

        hive
2. <span data-ttu-id="ac86c-201">De volgende instructies om een nieuwe tabel met de naam te maken met behulp van de CLI Voer **voertuigen** met behulp van de voorbeeldgegevens in de Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="ac86c-201">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="ac86c-202">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="ac86c-202">You should see an output similar to the following:</span></span>

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

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="ac86c-203">Toegang tot Data Lake Store met HDFS-opdrachten</span><span class="sxs-lookup"><span data-stu-id="ac86c-203">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="ac86c-204">Wanneer u het HDInsight-cluster voor het gebruik van Data Lake Store hebt geconfigureerd, kunt u de HDFS-shell-opdrachten voor toegang tot de store.</span><span class="sxs-lookup"><span data-stu-id="ac86c-204">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="ac86c-205">In deze sectie kunt u SSH gaat in het cluster voor HDInsight Linux u gemaakt en voer de HDFS-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="ac86c-205">In this section you will SSH into the HDInsight Linux cluster you created and run the HDFS commands.</span></span>

* <span data-ttu-id="ac86c-206">Als u een Windows-client voor SSH in het cluster gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ac86c-206">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="ac86c-207">Als u een Linux-client voor SSH in het cluster gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="ac86c-207">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="ac86c-208">Eenmaal zijn verbonden, gebruikt u de volgende opdracht uit HDFS-bestandssysteem voor het weergeven van de bestanden in de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ac86c-208">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="ac86c-209">Dit moet het bestand dat u eerder hebt geüpload naar de Data Lake Store weergeven.</span><span class="sxs-lookup"><span data-stu-id="ac86c-209">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="ac86c-210">U kunt ook de `hdfs dfs -put` opdracht voor sommige bestanden uploaden naar Data Lake Store en vervolgens gebruik `hdfs dfs -ls` om te controleren of de bestanden zijn geüpload.</span><span class="sxs-lookup"><span data-stu-id="ac86c-210">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="ac86c-211">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ac86c-211">See Also</span></span>
* [<span data-ttu-id="ac86c-212">Portal: Maak een HDInsight-cluster voor het gebruik van Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ac86c-212">Portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
