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
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="e59e4-103">HDInsight-clusters maken met Data Lake Store als standaard opslag met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="e59e4-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e59e4-104">Gebruik hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e59e4-104">Use hello Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="e59e4-105">Gebruik PowerShell (voor opslag van de standaard)</span><span class="sxs-lookup"><span data-stu-id="e59e4-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="e59e4-106">Gebruik PowerShell (voor extra opslagruimte)</span><span class="sxs-lookup"><span data-stu-id="e59e4-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="e59e4-107">Gebruik Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e59e4-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="e59e4-108">Meer informatie over hoe toouse Azure PowerShell tooconfigure Azure HDInsight-clusters met Azure Data Lake Store als standaard opslag.</span><span class="sxs-lookup"><span data-stu-id="e59e4-108">Learn how toouse Azure PowerShell tooconfigure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="e59e4-109">Zie voor instructies over het maken van een HDInsight-cluster met Data Lake Store als extra opslagruimte [een HDInsight-cluster maken met Data Lake Store als extra opslagruimte](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e59e4-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="e59e4-110">Hier volgen enkele belangrijke overwegingen voor het gebruik van HDInsight met Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="e59e4-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="e59e4-111">Hallo optie toocreate HDInsight-clusters met toegang tooData Lake Store als standaard opslag is beschikbaar voor HDInsight versie 3.5 en 3.6.</span><span class="sxs-lookup"><span data-stu-id="e59e4-111">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="e59e4-112">Hallo optie toocreate HDInsight-clusters met toegang tot tooData Lake Store omdat standaard opslag *niet beschikbaar* voor clusters van HDInsight Premium.</span><span class="sxs-lookup"><span data-stu-id="e59e4-112">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="e59e4-113">tooconfigure HDInsight toowork met Data Lake Store met behulp van PowerShell, volg Hallo-instructies in de volgende vijf secties Hallo.</span><span class="sxs-lookup"><span data-stu-id="e59e4-113">tooconfigure HDInsight toowork with Data Lake Store by using PowerShell, follow hello instructions in hello next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e59e4-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e59e4-114">Prerequisites</span></span>
<span data-ttu-id="e59e4-115">Voordat u deze zelfstudie begint, controleert u dat u voldoet aan de Hallo volgens de vereisten:</span><span class="sxs-lookup"><span data-stu-id="e59e4-115">Before you begin this tutorial, make sure that you meet hello following requirements:</span></span>

* <span data-ttu-id="e59e4-116">**Een Azure-abonnement**: Ga te[gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e59e4-116">**An Azure subscription**: Go too[Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e59e4-117">**Azure PowerShell 1.0 of hoger**: Zie [hoe tooinstall PowerShell en configureren](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e59e4-117">**Azure PowerShell 1.0 or greater**: See [How tooinstall and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="e59e4-118">**Windows Software Development Kit (SDK)**: tooinstall Windows SDK te gaan[downloadt en hulpprogramma's voor Windows 10](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="e59e4-118">**Windows Software Development Kit (SDK)**: tooinstall Windows SDK, go too[Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="e59e4-119">Hallo SDK is gebruikte toocreate een beveiligingscertificaat.</span><span class="sxs-lookup"><span data-stu-id="e59e4-119">hello SDK is used toocreate a security certificate.</span></span>
* <span data-ttu-id="e59e4-120">**Azure Active Directory-service-principal**: deze zelfstudie wordt beschreven hoe toocreate een service-principal in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e59e4-120">**Azure Active Directory service principal**: This tutorial describes how toocreate a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e59e4-121">Echter, een service-principal toocreate, moet u een Azure AD-beheerder.</span><span class="sxs-lookup"><span data-stu-id="e59e4-121">However, toocreate a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="e59e4-122">Als u een beheerder bent, kunt u deze vereiste overslaan en doorgaan met het Hallo-zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="e59e4-122">If you are an administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e59e4-123">U kunt een service principal maken alleen als u een Azure AD-beheerder.</span><span class="sxs-lookup"><span data-stu-id="e59e4-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="e59e4-124">Uw Azure AD-beheerder moet maken een service principal voordat u een HDInsight-cluster met Data Lake Store maken kunt.</span><span class="sxs-lookup"><span data-stu-id="e59e4-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="e59e4-125">Hallo service-principal moet worden gemaakt met een certificaat, zoals beschreven in [een service-principal maken met certificaat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="e59e4-125">hello service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="e59e4-126">Een Data Lake Store-account maken</span><span class="sxs-lookup"><span data-stu-id="e59e4-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="e59e4-127">een Data Lake Store-account toocreate Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="e59e4-127">toocreate a Data Lake Store account, do hello following:</span></span>

1. <span data-ttu-id="e59e4-128">Vanaf uw bureaublad, open een PowerShell-venster en Voer Hallo codefragmenten hieronder.</span><span class="sxs-lookup"><span data-stu-id="e59e4-128">From your desktop, open a PowerShell window, and then enter hello snippets below.</span></span> <span data-ttu-id="e59e4-129">Wanneer u bent na vragen aan gebruiker toosign in aanmelden als een van de Hallo abonnementbeheerders of eigenaars.</span><span class="sxs-lookup"><span data-stu-id="e59e4-129">When you are prompted toosign in, sign in as one of hello subscription administrators or owners.</span></span> 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="e59e4-130">Als u de registerbronprovider Hallo Data Lake Store en een foutbericht weergegeven dat vergelijkbaar te ontvangt`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, uw abonnement mogelijk geen goedgekeurde lijst voor Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e59e4-130">If you register hello Data Lake Store resource provider and receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="e59e4-131">tooenable uw Azure-abonnement voor de openbare preview Hallo Data Lake Store, volg de instructies in Hallo [aan de slag met Azure Data Lake Store met behulp van Azure-portal Hallo](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e59e4-131">tooenable your Azure subscription for hello Data Lake Store public preview, follow hello instructions in [Get started with Azure Data Lake Store by using hello Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="e59e4-132">Een Data Lake Store-account is gekoppeld aan een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e59e4-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="e59e4-133">Begint met het maken van een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e59e4-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="e59e4-134">Hier ziet u uitvoer als volgt:</span><span class="sxs-lookup"><span data-stu-id="e59e4-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="e59e4-135">Een Data Lake Store-account maken.</span><span class="sxs-lookup"><span data-stu-id="e59e4-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="e59e4-136">Hallo account naam die u opgeeft mag alleen kleine letters en cijfers bevatten.</span><span class="sxs-lookup"><span data-stu-id="e59e4-136">hello account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="e59e4-137">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="e59e4-137">You should see an output like hello following:</span></span>

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

4. <span data-ttu-id="e59e4-138">Data Lake Store als standaard opslag, moet u toospecify die een hoofdmap pad toowhich Hallo clusterspecifieke tijdens het maken van het cluster bestanden worden.</span><span class="sxs-lookup"><span data-stu-id="e59e4-138">Using Data Lake Store as default storage requires you toospecify a root path toowhich hello cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="e59e4-139">een hoofdpad toocreate **/clusters/hdiadlcluster** gebruiken in Hallo-fragment Hallo cmdlets volgen:</span><span class="sxs-lookup"><span data-stu-id="e59e4-139">toocreate a root path, which is **/clusters/hdiadlcluster** in hello  snippet, use hello following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="e59e4-140">Instellen van verificatie voor op rollen gebaseerde toegang tot tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="e59e4-140">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="e59e4-141">Elke Azure-abonnement is gekoppeld aan een Azure AD-entiteit.</span><span class="sxs-lookup"><span data-stu-id="e59e4-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="e59e4-142">Gebruikers en services dat abonnement toegang tot de resources met behulp van Azure-portal Hallo of hello Azure Resource Manager-API moeten eerst worden geverifieerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e59e4-142">Users and services that access subscription resources by using hello Azure portal or hello Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="e59e4-143">Toegang wordt verleend tooAzure abonnementen en services door toe te wijzen Hallo geschikte rol op een Azure-resource.</span><span class="sxs-lookup"><span data-stu-id="e59e4-143">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span> <span data-ttu-id="e59e4-144">Voor services identificeert een service-principal Hallo-service in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e59e4-144">For services, a service principal identifies hello service in Azure AD.</span></span>

<span data-ttu-id="e59e4-145">Deze sectie ziet u hoe een toepassing toogrant service, zoals HDInsight, toegang tooan Azure-resource (hello Data Lake Store-account dat u eerder hebt gemaakt).</span><span class="sxs-lookup"><span data-stu-id="e59e4-145">This section illustrates how toogrant an application service, such as HDInsight, access tooan Azure resource (hello Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="e59e4-146">Dit doet u door het maken van een service principal voor de toepassing hello en het toewijzen van rollen tooit via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e59e4-146">You do so by creating a service principal for hello application and assigning roles tooit via PowerShell.</span></span>

<span data-ttu-id="e59e4-147">Hallo-taken tooset van Active Directory-verificatie voor Azure Data Lake uitvoeren in de volgende twee secties Hallo.</span><span class="sxs-lookup"><span data-stu-id="e59e4-147">tooset up Active Directory authentication for Azure Data Lake, perform hello tasks in hello following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="e59e4-148">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="e59e4-148">Create a self-signed certificate</span></span>
<span data-ttu-id="e59e4-149">Zorg ervoor dat u hebt [Windows SDK](https://dev.windows.com/en-us/downloads) geïnstalleerd voordat u doorgaat met de Hallo in deze sectie stappen.</span><span class="sxs-lookup"><span data-stu-id="e59e4-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="e59e4-150">U moet hebben ook een directory hebt gemaakt, zoals *C:\mycertdir*, waarin u Hallo certificaat maken.</span><span class="sxs-lookup"><span data-stu-id="e59e4-150">You must have also created a directory, such as *C:\mycertdir*, where you create hello certificate.</span></span>

1. <span data-ttu-id="e59e4-151">Ga in Hallo PowerShell-venster toohello locatie waar u de Windows SDK geïnstalleerd (normaal gesproken *C:\Program Files (x86) \Windows Kits\10\bin\x86*) en gebruiken van Hallo [MakeCert] [ makecert] hulpprogramma toocreate een zelfondertekend certificaat en een persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="e59e4-151">From hello PowerShell window, go toohello location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="e59e4-152">Hallo volgende opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e59e4-152">Use hello following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="e59e4-153">U zult na vragen aan gebruiker tooenter Hallo wachtwoord voor persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="e59e4-153">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="e59e4-154">Nadat het Hallo-opdracht met succes is uitgevoerd, ziet u **CertFile.cer** en **mykey.pvk** in Hallo certificaat map die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e59e4-154">After hello command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in hello certificate directory that you specified.</span></span>
2. <span data-ttu-id="e59e4-155">Gebruik Hallo [Pvk2Pfx] [ pvk2pfx] hulpprogramma tooconvert Hallo PVK en de .cer-bestanden die MakeCert gemaakte tooa pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="e59e4-155">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="e59e4-156">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e59e4-156">Run hello following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="e59e4-157">Wanneer u wordt gevraagd, typt u Hallo wachtwoord voor persoonlijke sleutel die u eerder hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e59e4-157">When you are prompted, enter hello private key password that you specified earlier.</span></span> <span data-ttu-id="e59e4-158">waarde die u voor Hallo opgeeft Hallo **-po** parameter is Hallo wachtwoord dat is gekoppeld aan Hallo pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="e59e4-158">hello value you specify for hello **-po** parameter is hello password that's associated with hello .pfx file.</span></span> <span data-ttu-id="e59e4-159">Nadat het Hallo-opdracht is voltooid, moet u ook zien een **CertFile.pfx** in Hallo certificaat map die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e59e4-159">After hello command has been completed successfully, you should also see a **CertFile.pfx** in hello certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="e59e4-160">Een Azure AD maken en een service-principal</span><span class="sxs-lookup"><span data-stu-id="e59e4-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="e59e4-161">In deze sectie maakt een service-principal voor een Azure AD-toepassing, een rol toohello service-principal toewijzen en verifiëren als de service-principal Hallo door te geven van een certificaat.</span><span class="sxs-lookup"><span data-stu-id="e59e4-161">In this section, you create a service principal for an Azure AD application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="e59e4-162">toocreate een toepassing in Azure AD Hallo volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e59e4-162">toocreate an application in Azure AD, run hello following commands:</span></span>

1. <span data-ttu-id="e59e4-163">Hallo-cmdlets in de PowerShell-consolevenster Hallo na plakken.</span><span class="sxs-lookup"><span data-stu-id="e59e4-163">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="e59e4-164">Zorg ervoor dat u voor Hallo opgeeft Hallo de waarde **- weergavenaam** eigenschap uniek is.</span><span class="sxs-lookup"><span data-stu-id="e59e4-164">Make sure that hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="e59e4-165">waarden voor Hallo **- startpagina** en **- IdentiferUris** tijdelijke aanduiding voor waarden zijn en worden niet geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="e59e4-165">hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="e59e4-166">Een service-principal maken met behulp van Hallo toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="e59e4-166">Create a service principal by using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="e59e4-167">Verleen Hallo service principal toegang toohello Data Lake Store-hoofdmap en alle Hallo mappen in Hallo hoofdpad die u eerder hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e59e4-167">Grant hello service principal access toohello Data Lake Store root and all hello folders in hello root path that you specified earlier.</span></span> <span data-ttu-id="e59e4-168">Gebruik Hallo cmdlets volgen:</span><span class="sxs-lookup"><span data-stu-id="e59e4-168">Use hello following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a><span data-ttu-id="e59e4-169">Een HDInsight Linux-cluster maken met Data Lake Store als Hallo standaard opslag</span><span class="sxs-lookup"><span data-stu-id="e59e4-169">Create an HDInsight Linux cluster with Data Lake Store as hello default storage</span></span>

<span data-ttu-id="e59e4-170">In deze sectie maakt u een HDInsight Hadoop Linux-cluster met Data Lake Store als Hallo standaard opslag.</span><span class="sxs-lookup"><span data-stu-id="e59e4-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as hello default storage.</span></span> <span data-ttu-id="e59e4-171">Voor deze release Hallo HDInsight-cluster en Data Lake Store moet Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="e59e4-171">For this release, hello HDInsight cluster and Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="e59e4-172">Hallo abonnement tenant-ID ophalen en opslaan toouse later.</span><span class="sxs-lookup"><span data-stu-id="e59e4-172">Retrieve hello subscription tenant ID, and store it toouse later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="e59e4-173">Hallo HDInsight-cluster maken met behulp van Hallo cmdlets volgen:</span><span class="sxs-lookup"><span data-stu-id="e59e4-173">Create hello HDInsight cluster by using hello following cmdlets:</span></span>

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

    <span data-ttu-id="e59e4-174">Nadat het Hallo-cmdlet is voltooid, ziet u uitvoer met een lijst met Hallo clusterdetails.</span><span class="sxs-lookup"><span data-stu-id="e59e4-174">After hello cmdlet has been successfully completed, you should see an output that lists hello cluster details.</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a><span data-ttu-id="e59e4-175">Testtaken uitvoeren op Hallo HDInsight-cluster toouse Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e59e4-175">Run test jobs on hello HDInsight cluster toouse Data Lake Store</span></span>
<span data-ttu-id="e59e4-176">Nadat u een HDInsight-cluster hebt geconfigureerd, kunt u testtaken uitvoeren op het tooensure dat toegang Data Lake Store tot.</span><span class="sxs-lookup"><span data-stu-id="e59e4-176">After you have configured an HDInsight cluster, you can run test jobs on it tooensure that it can access Data Lake Store.</span></span> <span data-ttu-id="e59e4-177">toodo dus een voorbeeld Hive-taak toocreate een tabel uitvoeren die gebruikmaakt van voorbeeldgegevens Hallo die al beschikbaar is in Data Lake Store op  *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="e59e4-177">toodo so, run a sample Hive job toocreate a table that uses hello sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="e59e4-178">U maakt een verbinding Secure Shell (SSH) in Hallo HDInsight Linux-cluster dat u hebt gemaakt in deze sectie en voert u een voorbeeld Hive-query.</span><span class="sxs-lookup"><span data-stu-id="e59e4-178">In this section, you make a Secure Shell (SSH) connection into hello HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="e59e4-179">Als u een Windows-client toomake Hallo-cluster met een SSH-verbinding gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="e59e4-179">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="e59e4-180">Als u een Linux-client toomake Hallo-cluster met een SSH-verbinding gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e59e4-180">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="e59e4-181">Als u Hallo verbinding hebt gemaakt, start u met behulp van de volgende opdracht Hallo Hallo Hive-opdrachtregelinterface (CLI):</span><span class="sxs-lookup"><span data-stu-id="e59e4-181">After you have made hello connection, start hello Hive command-line interface (CLI) by using hello following command:</span></span>

        hive
2. <span data-ttu-id="e59e4-182">Gebruik Hallo CLI tooenter hello toocreate instructies een nieuwe tabel met de naam na **voertuigen** met behulp van de voorbeeldgegevens Hallo in Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="e59e4-182">Use hello CLI tooenter hello following statements toocreate a new table named **vehicles** by using hello sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="e59e4-183">U ziet Hallo query-uitvoer op Hallo SSH-console.</span><span class="sxs-lookup"><span data-stu-id="e59e4-183">You should see hello query output on hello SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e59e4-184">Hallo pad toohello voorbeeldgegevens in Hallo voorafgaand aan de opdracht CREATE TABLE is `adl:///example/data/`, waarbij `adl:///` basis Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="e59e4-184">hello path toohello sample data in hello preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is hello cluster root.</span></span> <span data-ttu-id="e59e4-185">Volgende Hallo voorbeeld van een basis-Hallo cluster die opgegeven in deze zelfstudie, Hallo-opdracht is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="e59e4-185">Following hello example of hello cluster root that's specified in this tutorial, hello command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="e59e4-186">Gebruik Hallo korter alternatief of Hallo volledige pad toohello cluster hoofdmap bieden.</span><span class="sxs-lookup"><span data-stu-id="e59e4-186">You can either use hello shorter alternative or provide hello complete path toohello cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="e59e4-187">Toegang tot Data Lake Store via de HDFS-opdrachten</span><span class="sxs-lookup"><span data-stu-id="e59e4-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="e59e4-188">Nadat u Hallo HDInsight cluster toouse Data Lake Store hebt geconfigureerd, kunt u Hadoop Distributed File System (HDFS) shell-opdrachten tooaccess Hallo store.</span><span class="sxs-lookup"><span data-stu-id="e59e4-188">After you have configured hello HDInsight cluster toouse Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands tooaccess hello store.</span></span>

<span data-ttu-id="e59e4-189">In deze sectie maakt u een SSH-verbinding in Hallo HDInsight Linux-cluster dat u hebt gemaakt en Voer Hallo HDFS-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="e59e4-189">In this section, you make an SSH connection into hello HDInsight Linux cluster that you created, and then you run hello HDFS commands.</span></span>

* <span data-ttu-id="e59e4-190">Als u een Windows-client toomake Hallo-cluster met een SSH-verbinding gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="e59e4-190">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="e59e4-191">Als u een Linux-client toomake Hallo-cluster met een SSH-verbinding gebruikt, raadpleegt u [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e59e4-191">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="e59e4-192">Nadat u Hallo verbinding hebt gemaakt, kunt u de Hallo-bestanden in Data Lake Store weergeven met behulp van de volgende opdracht voor HDFS file system Hallo.</span><span class="sxs-lookup"><span data-stu-id="e59e4-192">After you've made hello connection, list hello files in Data Lake Store by using hello following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="e59e4-193">U kunt ook Hallo `hdfs dfs -put` opdracht tooupload sommige bestanden tooData Lake Store en gebruik vervolgens `hdfs dfs -ls` tooverify of Hallo bestanden geüpload.</span><span class="sxs-lookup"><span data-stu-id="e59e4-193">You can also use hello `hdfs dfs -put` command tooupload some files tooData Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="e59e4-194">Zie ook</span><span class="sxs-lookup"><span data-stu-id="e59e4-194">See also</span></span>
* [<span data-ttu-id="e59e4-195">Azure-portal: Maak een HDInsight-cluster toouse Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e59e4-195">Azure portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
