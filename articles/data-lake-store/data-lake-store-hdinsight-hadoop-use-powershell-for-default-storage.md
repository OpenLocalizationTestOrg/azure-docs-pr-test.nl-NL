---
title: HDInsight-clusters maken met Data Lake Store als standaard opslag met behulp van PowerShell | Microsoft-Docs
description: Azure PowerShell gebruiken voor het maken en gebruiken van HDInsight-clusters met Azure Data Lake Store
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
ms.openlocfilehash: 77eb83b80312eca401e6f60d57ed6a5668ea442e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="a8e08-103">HDInsight-clusters maken met Data Lake Store als standaard opslag met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8e08-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a8e08-104">Azure Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="a8e08-104">Use the Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="a8e08-105">Gebruik PowerShell (voor opslag van de standaard)</span><span class="sxs-lookup"><span data-stu-id="a8e08-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="a8e08-106">Gebruik PowerShell (voor extra opslagruimte)</span><span class="sxs-lookup"><span data-stu-id="a8e08-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="a8e08-107">Gebruik Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8e08-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="a8e08-108">Informatie over het gebruik van Azure PowerShell voor Azure HDInsight-clusters met Azure Data Lake Store als standaard opslag configureren.</span><span class="sxs-lookup"><span data-stu-id="a8e08-108">Learn how to use Azure PowerShell to configure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="a8e08-109">Zie voor instructies over het maken van een HDInsight-cluster met Data Lake Store als extra opslagruimte [een HDInsight-cluster maken met Data Lake Store als extra opslagruimte](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a8e08-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="a8e08-110">Hier volgen enkele belangrijke overwegingen voor het gebruik van HDInsight met Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="a8e08-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="a8e08-111">De optie voor het maken van HDInsight-clusters met toegang tot Data Lake Store als standaard opslag is beschikbaar voor HDInsight versie 3.5 en 3.6.</span><span class="sxs-lookup"><span data-stu-id="a8e08-111">The option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="a8e08-112">De optie voor het maken van HDInsight-clusters met toegang naar Data Lake Store omdat standaard opslag *niet beschikbaar* voor clusters van HDInsight Premium.</span><span class="sxs-lookup"><span data-stu-id="a8e08-112">The option to create HDInsight clusters with access to Data Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="a8e08-113">Volg de instructies in de volgende vijf secties voor het configureren van HDInsight werken met Data Lake Store met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a8e08-113">To configure HDInsight to work with Data Lake Store by using PowerShell, follow the instructions in the next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8e08-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a8e08-114">Prerequisites</span></span>
<span data-ttu-id="a8e08-115">Voordat u deze zelfstudie begint, controleert u dat u voldoet aan de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="a8e08-115">Before you begin this tutorial, make sure that you meet the following requirements:</span></span>

* <span data-ttu-id="a8e08-116">**Een Azure-abonnement**: Ga naar [gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8e08-116">**An Azure subscription**: Go to [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a8e08-117">**Azure PowerShell 1.0 of hoger**: Zie [PowerShell installeren en configureren hoe](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a8e08-117">**Azure PowerShell 1.0 or greater**: See [How to install and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="a8e08-118">**Windows Software Development Kit (SDK)**: voor het installeren van Windows-SDK, gaat u naar [downloadt en hulpprogramma's voor Windows 10](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="a8e08-118">**Windows Software Development Kit (SDK)**: To install Windows SDK, go to [Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="a8e08-119">De SDK gebruikt voor het maken van een beveiligingscertificaat.</span><span class="sxs-lookup"><span data-stu-id="a8e08-119">The SDK is used to create a security certificate.</span></span>
* <span data-ttu-id="a8e08-120">**Azure Active Directory-service-principal**: in deze zelfstudie wordt beschreven hoe u een service-principal maken in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8e08-120">**Azure Active Directory service principal**: This tutorial describes how to create a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a8e08-121">Voor het maken van een service-principal, moet u echter een Azure AD-beheerder zijn.</span><span class="sxs-lookup"><span data-stu-id="a8e08-121">However, to create a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="a8e08-122">Als u een beheerder bent, kunt u deze vereiste overslaan en doorgaan met de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a8e08-122">If you are an administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="a8e08-123">U kunt een service principal maken alleen als u een Azure AD-beheerder.</span><span class="sxs-lookup"><span data-stu-id="a8e08-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="a8e08-124">Uw Azure AD-beheerder moet maken een service principal voordat u een HDInsight-cluster met Data Lake Store maken kunt.</span><span class="sxs-lookup"><span data-stu-id="a8e08-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="a8e08-125">De service-principal moet worden gemaakt met een certificaat, zoals beschreven in [een service-principal maken met certificaat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="a8e08-125">The service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="a8e08-126">Een Data Lake Store-account maken</span><span class="sxs-lookup"><span data-stu-id="a8e08-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="a8e08-127">Ga als volgt te werk als u wilt maken van een Data Lake Store-account:</span><span class="sxs-lookup"><span data-stu-id="a8e08-127">To create a Data Lake Store account, do the following:</span></span>

1. <span data-ttu-id="a8e08-128">Open een PowerShell-venster op het bureaublad en voer vervolgens de codefragmenten hieronder.</span><span class="sxs-lookup"><span data-stu-id="a8e08-128">From your desktop, open a PowerShell window, and then enter the snippets below.</span></span> <span data-ttu-id="a8e08-129">Wanneer u wordt gevraagd met aanmelden, meld u aan als een van de abonnementbeheerders of eigenaren.</span><span class="sxs-lookup"><span data-stu-id="a8e08-129">When you are prompted to sign in, sign in as one of the subscription administrators or owners.</span></span> 

        # Sign in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="a8e08-130">Als u de Data Lake Store-resourceprovider registreren en een foutbericht zoals ontvangt `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`, uw abonnement mogelijk geen goedgekeurde lijst voor Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a8e08-130">If you register the Data Lake Store resource provider and receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="a8e08-131">Volg de instructies in zodat uw Azure-abonnement voor de openbare preview van Data Lake Store [aan de slag met Azure Data Lake Store met behulp van de Azure-portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a8e08-131">To enable your Azure subscription for the Data Lake Store public preview, follow the instructions in [Get started with Azure Data Lake Store by using the Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="a8e08-132">Een Data Lake Store-account is gekoppeld aan een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a8e08-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="a8e08-133">Begint met het maken van een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a8e08-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="a8e08-134">Hier ziet u uitvoer als volgt:</span><span class="sxs-lookup"><span data-stu-id="a8e08-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="a8e08-135">Een Data Lake Store-account maken.</span><span class="sxs-lookup"><span data-stu-id="a8e08-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="a8e08-136">De accountnaam die u opgeeft moet alleen kleine letters en cijfers bevatten.</span><span class="sxs-lookup"><span data-stu-id="a8e08-136">The account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="a8e08-137">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a8e08-137">You should see an output like the following:</span></span>

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

4. <span data-ttu-id="a8e08-138">Data Lake Store als standaard opslag, moet u een basis-pad waaraan de cluster-specifieke bestanden tijdens maken van het cluster worden gekopieerd op te geven.</span><span class="sxs-lookup"><span data-stu-id="a8e08-138">Using Data Lake Store as default storage requires you to specify a root path to which the cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="a8e08-139">Maken van een hoofdpad **/clusters/hdiadlcluster** in het codefragment maakt gebruik van de volgende cmdlets:</span><span class="sxs-lookup"><span data-stu-id="a8e08-139">To create a root path, which is **/clusters/hdiadlcluster** in the  snippet, use the following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="a8e08-140">Verificatie voor op rollen gebaseerde toegang tot Data Lake Store instellen</span><span class="sxs-lookup"><span data-stu-id="a8e08-140">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="a8e08-141">Elke Azure-abonnement is gekoppeld aan een Azure AD-entiteit.</span><span class="sxs-lookup"><span data-stu-id="a8e08-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="a8e08-142">Gebruikers en services die toegang krijgen bronnen van abonnement tot met behulp van de Azure-portal of de Azure Resource Manager-API moeten eerst worden geverifieerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8e08-142">Users and services that access subscription resources by using the Azure portal or the Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="a8e08-143">Toegang te krijgen tot Azure-abonnementen en services door het toewijzen van de juiste rol op een Azure-resource.</span><span class="sxs-lookup"><span data-stu-id="a8e08-143">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span> <span data-ttu-id="a8e08-144">Voor services identificeert een service-principal de service in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8e08-144">For services, a service principal identifies the service in Azure AD.</span></span>

<span data-ttu-id="a8e08-145">Deze sectie ziet u het verlenen van een toepassingsservice, zoals HDInsight, toegang tot een Azure-resource (het Data Lake Store-account dat u eerder hebt gemaakt).</span><span class="sxs-lookup"><span data-stu-id="a8e08-145">This section illustrates how to grant an application service, such as HDInsight, access to an Azure resource (the Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="a8e08-146">Dit doet u door het maken van een service principal voor de toepassing en het toewijzen van rollen aan via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a8e08-146">You do so by creating a service principal for the application and assigning roles to it via PowerShell.</span></span>

<span data-ttu-id="a8e08-147">Als u Active Directory-verificatie voor Azure Data Lake instelt, moet u de taken uitvoert in de volgende twee secties.</span><span class="sxs-lookup"><span data-stu-id="a8e08-147">To set up Active Directory authentication for Azure Data Lake, perform the tasks in the following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="a8e08-148">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="a8e08-148">Create a self-signed certificate</span></span>
<span data-ttu-id="a8e08-149">Zorg ervoor dat u hebt [Windows SDK](https://dev.windows.com/en-us/downloads) geïnstalleerd voordat u doorgaat met de stappen in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="a8e08-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="a8e08-150">U moet hebben ook een directory hebt gemaakt, zoals *C:\mycertdir*, waarin u het certificaat maken.</span><span class="sxs-lookup"><span data-stu-id="a8e08-150">You must have also created a directory, such as *C:\mycertdir*, where you create the certificate.</span></span>

1. <span data-ttu-id="a8e08-151">Ga naar de locatie waar u de Windows SDK geïnstalleerd in het PowerShell-venster (meestal *C:\Program Files (x86) \Windows Kits\10\bin\x86*) en gebruiken de [MakeCert] [ makecert] hulpprogramma voor het maken van een zelfondertekend certificaat en een persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="a8e08-151">From the PowerShell window, go to the location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="a8e08-152">Gebruik de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="a8e08-152">Use the following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="a8e08-153">U wordt gevraagd om in te voeren van het wachtwoord van de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="a8e08-153">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="a8e08-154">Nadat u de opdracht met succes is uitgevoerd, ziet u **CertFile.cer** en **mykey.pvk** in de certificaat-map die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a8e08-154">After the command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in the certificate directory that you specified.</span></span>
2. <span data-ttu-id="a8e08-155">Gebruik de [Pvk2Pfx] [ pvk2pfx] hulpprogramma voor het converteren van de PVK en de .cer-bestanden die MakeCert gemaakt naar een pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="a8e08-155">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="a8e08-156">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="a8e08-156">Run the following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="a8e08-157">Wanneer u wordt gevraagd, typt u het wachtwoord voor persoonlijke sleutel die u eerder hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a8e08-157">When you are prompted, enter the private key password that you specified earlier.</span></span> <span data-ttu-id="a8e08-158">De waarde die u opgeeft voor de **-po** parameter is het wachtwoord dat is gekoppeld aan het .pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="a8e08-158">The value you specify for the **-po** parameter is the password that's associated with the .pfx file.</span></span> <span data-ttu-id="a8e08-159">Nadat de opdracht is voltooid, ook ziet u een **CertFile.pfx** in de certificaat-map die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a8e08-159">After the command has been completed successfully, you should also see a **CertFile.pfx** in the certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="a8e08-160">Een Azure AD maken en een service-principal</span><span class="sxs-lookup"><span data-stu-id="a8e08-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="a8e08-161">In deze sectie maakt een service-principal voor een Azure AD-toepassing, een rol toewijzen aan de service-principal en verifiëren als de service-principal door te geven van een certificaat.</span><span class="sxs-lookup"><span data-stu-id="a8e08-161">In this section, you create a service principal for an Azure AD application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="a8e08-162">Een toepassing maken in Azure AD, voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="a8e08-162">To create an application in Azure AD, run the following commands:</span></span>

1. <span data-ttu-id="a8e08-163">Plak de volgende cmdlets in het venster PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="a8e08-163">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="a8e08-164">Zorg ervoor dat de waarde die u opgeeft voor de **- weergavenaam** eigenschap uniek is.</span><span class="sxs-lookup"><span data-stu-id="a8e08-164">Make sure that the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="a8e08-165">De waarden voor **- startpagina** en **- IdentiferUris** tijdelijke aanduiding voor waarden zijn en worden niet geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="a8e08-165">The values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="a8e08-166">Een service-principal maken met behulp van de toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="a8e08-166">Create a service principal by using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="a8e08-167">De service principal toegang verlenen tot de Data Lake Store-hoofdmap en de mappen in het basis-pad dat u eerder hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a8e08-167">Grant the service principal access to the Data Lake Store root and all the folders in the root path that you specified earlier.</span></span> <span data-ttu-id="a8e08-168">Gebruik de volgende cmdlets:</span><span class="sxs-lookup"><span data-stu-id="a8e08-168">Use the following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-the-default-storage"></a><span data-ttu-id="a8e08-169">Een HDInsight Linux-cluster maken met Data Lake Store als de standaard-opslag</span><span class="sxs-lookup"><span data-stu-id="a8e08-169">Create an HDInsight Linux cluster with Data Lake Store as the default storage</span></span>

<span data-ttu-id="a8e08-170">In deze sectie maakt u een HDInsight Hadoop Linux-cluster met Data Lake Store als de standaard-opslag.</span><span class="sxs-lookup"><span data-stu-id="a8e08-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as the default storage.</span></span> <span data-ttu-id="a8e08-171">Voor deze release de HDInsight-cluster en Data Lake Store moeten op dezelfde locatie bevinden.</span><span class="sxs-lookup"><span data-stu-id="a8e08-171">For this release, the HDInsight cluster and Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="a8e08-172">De tenant-ID van het abonnement ophalen en opslaan voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="a8e08-172">Retrieve the subscription tenant ID, and store it to use later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="a8e08-173">Het HDInsight-cluster maken met behulp van de volgende cmdlets:</span><span class="sxs-lookup"><span data-stu-id="a8e08-173">Create the HDInsight cluster by using the following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
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

    <span data-ttu-id="a8e08-174">Nadat de cmdlet is voltooid, ziet u uitvoer die hiermee de clusterdetails worden.</span><span class="sxs-lookup"><span data-stu-id="a8e08-174">After the cmdlet has been successfully completed, you should see an output that lists the cluster details.</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-data-lake-store"></a><span data-ttu-id="a8e08-175">Testtaken uitvoeren op het HDInsight-cluster te gebruiken van Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a8e08-175">Run test jobs on the HDInsight cluster to use Data Lake Store</span></span>
<span data-ttu-id="a8e08-176">Nadat u een HDInsight-cluster hebt geconfigureerd, kunt u testtaken uitvoeren erop om ervoor te zorgen dat deze toegang heeft tot Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a8e08-176">After you have configured an HDInsight cluster, you can run test jobs on it to ensure that it can access Data Lake Store.</span></span> <span data-ttu-id="a8e08-177">Voer een voorbeeld Hive-taak voor het maken van een tabel die gebruikmaakt van de voorbeeldgegevens die al beschikbaar is in Data Lake Store op om dit te doen  *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="a8e08-177">To do so, run a sample Hive job to create a table that uses the sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="a8e08-178">U maakt een verbinding Secure Shell (SSH) in het cluster voor HDInsight Linux die u hebt gemaakt in deze sectie en voert u een voorbeeld Hive-query.</span><span class="sxs-lookup"><span data-stu-id="a8e08-178">In this section, you make a Secure Shell (SSH) connection into the HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="a8e08-179">Als u een Windows-client gebruikt een SSH-verbinding in het cluster te maken, Zie [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="a8e08-179">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="a8e08-180">Als u een Linux-client gebruikt een SSH-verbinding in het cluster te maken, Zie [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a8e08-180">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="a8e08-181">Als u de verbinding hebt gemaakt, start u de Hive-opdrachtregelinterface (CLI) met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a8e08-181">After you have made the connection, start the Hive command-line interface (CLI) by using the following command:</span></span>

        hive
2. <span data-ttu-id="a8e08-182">Gebruik de CLI voor het invoeren van de volgende instructies voor het maken van een nieuwe tabel met de naam **voertuigen** met behulp van de voorbeeldgegevens in Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="a8e08-182">Use the CLI to enter the following statements to create a new table named **vehicles** by using the sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="a8e08-183">U ziet de uitvoer van een query op de SSH-console.</span><span class="sxs-lookup"><span data-stu-id="a8e08-183">You should see the query output on the SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="a8e08-184">Het pad naar de voorbeeldgegevens in de voorgaande opdracht voor CREATE TABLE `adl:///example/data/`, waarbij `adl:///` is de hoofdmap van het cluster.</span><span class="sxs-lookup"><span data-stu-id="a8e08-184">The path to the sample data in the preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is the cluster root.</span></span> <span data-ttu-id="a8e08-185">Na het voorbeeld van de basis-cluster dat is opgegeven in deze zelfstudie is van de opdracht `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="a8e08-185">Following the example of the cluster root that's specified in this tutorial, the command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="a8e08-186">U kunt de verkorte gebruiken of geef het volledige pad naar de hoofdmap van het cluster.</span><span class="sxs-lookup"><span data-stu-id="a8e08-186">You can either use the shorter alternative or provide the complete path to the cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="a8e08-187">Toegang tot Data Lake Store via de HDFS-opdrachten</span><span class="sxs-lookup"><span data-stu-id="a8e08-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="a8e08-188">Nadat u het HDInsight-cluster voor het gebruik van Data Lake Store hebt geconfigureerd, kunt u de shell-opdrachten Hadoop Distributed File System (HDFS) toegang tot de store.</span><span class="sxs-lookup"><span data-stu-id="a8e08-188">After you have configured the HDInsight cluster to use Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands to access the store.</span></span>

<span data-ttu-id="a8e08-189">In deze sectie maakt u een SSH-verbinding in het cluster voor HDInsight Linux die u hebt gemaakt en voert u de HDFS-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="a8e08-189">In this section, you make an SSH connection into the HDInsight Linux cluster that you created, and then you run the HDFS commands.</span></span>

* <span data-ttu-id="a8e08-190">Als u een Windows-client gebruikt een SSH-verbinding in het cluster te maken, Zie [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="a8e08-190">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="a8e08-191">Als u een Linux-client gebruikt een SSH-verbinding in het cluster te maken, Zie [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a8e08-191">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="a8e08-192">Nadat u de verbinding hebt gemaakt, moet u de bestanden in Data Lake Store weergeven met behulp van de volgende opdracht voor het systeem HDFS-bestand.</span><span class="sxs-lookup"><span data-stu-id="a8e08-192">After you've made the connection, list the files in Data Lake Store by using the following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="a8e08-193">U kunt ook de `hdfs dfs -put` opdracht voor sommige bestanden uploaden naar Data Lake Store en vervolgens gebruik `hdfs dfs -ls` om te controleren of de bestanden zijn geüpload.</span><span class="sxs-lookup"><span data-stu-id="a8e08-193">You can also use the `hdfs dfs -put` command to upload some files to Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="a8e08-194">Zie ook</span><span class="sxs-lookup"><span data-stu-id="a8e08-194">See also</span></span>
* [<span data-ttu-id="a8e08-195">Azure-portal: een HDInsight-cluster voor het gebruik van Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a8e08-195">Azure portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
