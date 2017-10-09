---
title: aaaUse hello Python SDK tooget de slag met Azure Data Lake Store | Microsoft Docs
description: Meer informatie over hoe toouse Python SDK toowork met Data Lake Store-accounts en Hallo-bestandssysteem.
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 75f6de6f-6fd8-48f4-8707-cb27d22d27a6
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 7061fdf25ef607608bab618a20ddd3d6fc7af01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="ffd39-103">Aan de slag met Azure Data Lake Store met Python</span><span class="sxs-lookup"><span data-stu-id="ffd39-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ffd39-104">Portal</span><span class="sxs-lookup"><span data-stu-id="ffd39-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="ffd39-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffd39-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="ffd39-106">.NET-SDK</span><span class="sxs-lookup"><span data-stu-id="ffd39-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="ffd39-107">Java-SDK</span><span class="sxs-lookup"><span data-stu-id="ffd39-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="ffd39-108">REST API</span><span class="sxs-lookup"><span data-stu-id="ffd39-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="ffd39-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ffd39-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="ffd39-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="ffd39-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="ffd39-111">Python</span><span class="sxs-lookup"><span data-stu-id="ffd39-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="ffd39-112">Informatie over hoe toouse Hallo Python SDK voor Azure en Azure Data Lake Store tooperform basisbewerkingen, zoals maken van mappen, uploaden en downloaden van gegevensbestanden, enzovoort. Zie [Azure Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ffd39-112">Learn how toouse hello Python SDK for Azure and Azure Data Lake Store tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffd39-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ffd39-113">Prerequisites</span></span>

* <span data-ttu-id="ffd39-114">**Python**.</span><span class="sxs-lookup"><span data-stu-id="ffd39-114">**Python**.</span></span> <span data-ttu-id="ffd39-115">U kunt Python [hier](https://www.python.org/downloads/) downloaden.</span><span class="sxs-lookup"><span data-stu-id="ffd39-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="ffd39-116">In dit artikel wordt Python 3.5.2 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ffd39-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="ffd39-117">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ffd39-117">**An Azure subscription**.</span></span> <span data-ttu-id="ffd39-118">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ffd39-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="ffd39-119">**Een Azure Active Directory-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="ffd39-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="ffd39-120">U hello Azure AD-toepassing tooauthenticate Hallo Data Lake Store-toepassing gebruiken met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffd39-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="ffd39-121">Er zijn verschillende benaderingen tooauthenticate met Azure AD zijn **eindgebruiker verificatie** of **authentication service-naar-serviceconnector**.</span><span class="sxs-lookup"><span data-stu-id="ffd39-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="ffd39-122">Voor instructies en meer informatie over het tooauthenticate, Zie [eindgebruiker verificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [authentication Service-naar-serviceconnector](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="ffd39-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-hello-modules"></a><span data-ttu-id="ffd39-123">Hallo-modules installeren</span><span class="sxs-lookup"><span data-stu-id="ffd39-123">Install hello modules</span></span>

<span data-ttu-id="ffd39-124">toowork met Data Lake Store met behulp van Python, moet u drie tooinstall-modules.</span><span class="sxs-lookup"><span data-stu-id="ffd39-124">toowork with Data Lake Store using Python, you need tooinstall three modules.</span></span>

* <span data-ttu-id="ffd39-125">Hallo `azure-mgmt-resource` module.</span><span class="sxs-lookup"><span data-stu-id="ffd39-125">hello `azure-mgmt-resource` module.</span></span> <span data-ttu-id="ffd39-126">Deze bevat Azure-modules voor Active Directory enz.</span><span class="sxs-lookup"><span data-stu-id="ffd39-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="ffd39-127">Hallo `azure-mgmt-datalake-store` module.</span><span class="sxs-lookup"><span data-stu-id="ffd39-127">hello `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="ffd39-128">Dit omvat beheerbewerkingen voor hello Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="ffd39-128">This includes hello Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="ffd39-129">Zie [Naslaginformatie over Azure Data Lake Store-beheermodule](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html) voor meer informatie over deze module.</span><span class="sxs-lookup"><span data-stu-id="ffd39-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="ffd39-130">Hallo `azure-datalake-store` module.</span><span class="sxs-lookup"><span data-stu-id="ffd39-130">hello `azure-datalake-store` module.</span></span> <span data-ttu-id="ffd39-131">Dit omvat bestandssysteembewerkingen van hello Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ffd39-131">This includes hello Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="ffd39-132">Zie [Naslaginformatie over Azure Data Lake Store-bestandssysteemmodule](http://azure-datalake-store.readthedocs.io/en/latest/) voor meer informatie over deze module.</span><span class="sxs-lookup"><span data-stu-id="ffd39-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="ffd39-133">Gebruik Hallo opdrachten tooinstall Hallo modules te volgen.</span><span class="sxs-lookup"><span data-stu-id="ffd39-133">Use hello following commands tooinstall hello modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="ffd39-134">Een nieuwe Python-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="ffd39-134">Create a new Python application</span></span>

1. <span data-ttu-id="ffd39-135">In Hallo IDE van uw keuze, bijvoorbeeld een nieuwe Python-toepassing maken **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="ffd39-135">In hello IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="ffd39-136">Hallo volgende regels tooimport Hallo vereist modules toevoegen</span><span class="sxs-lookup"><span data-stu-id="ffd39-136">Add hello following lines tooimport hello required modules</span></span>

    ```
    ## Use this only for Azure AD service-to-service authentication
    from azure.common.credentials import ServicePrincipalCredentials

    ## Use this only for Azure AD end-user authentication
    from azure.common.credentials import UserPassCredentials

    ## Use this only for Azure AD multi-factor authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Store account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Store filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, getpass, pprint, uuid, time
    ```

3. <span data-ttu-id="ffd39-137">Sla de wijzigingen toomysample.py.</span><span class="sxs-lookup"><span data-stu-id="ffd39-137">Save changes toomysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="ffd39-138">Authentication</span><span class="sxs-lookup"><span data-stu-id="ffd39-138">Authentication</span></span>

<span data-ttu-id="ffd39-139">In deze sectie bespreken we Hallo verschillende manieren tooauthenticate met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffd39-139">In this section, we talk about hello different ways tooauthenticate with Azure AD.</span></span> <span data-ttu-id="ffd39-140">Hallo opties zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="ffd39-140">hello options available are:</span></span>

* <span data-ttu-id="ffd39-141">Verificatie van de eindgebruiker</span><span class="sxs-lookup"><span data-stu-id="ffd39-141">End-user authentication</span></span>
* <span data-ttu-id="ffd39-142">Verificatie van service-tot-service</span><span class="sxs-lookup"><span data-stu-id="ffd39-142">Service-to-service authentication</span></span>
* <span data-ttu-id="ffd39-143">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ffd39-143">Multi-factor authentication</span></span>

<span data-ttu-id="ffd39-144">U moet deze verificatieopties gebruiken voor zowel accountbeheer- als bestandssysteembeheermodules.</span><span class="sxs-lookup"><span data-stu-id="ffd39-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="ffd39-145">Verificatie van de eindgebruiker voor accountbeheer</span><span class="sxs-lookup"><span data-stu-id="ffd39-145">End-user authentication for account management</span></span>

<span data-ttu-id="ffd39-146">Gebruik deze tooauthenticate met Azure AD voor accountbeheerbewerkingen (maken/verwijderen Data Lake Store-account, enz.).</span><span class="sxs-lookup"><span data-stu-id="ffd39-146">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="ffd39-147">U moet een gebruikersnaam en wachtwoord voor een Azure AD-gebruiker opgeven.</span><span class="sxs-lookup"><span data-stu-id="ffd39-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="ffd39-148">Houd er rekening mee dat Hallo-gebruiker moet niet worden geconfigureerd voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="ffd39-148">Note that hello user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="ffd39-149">Verificatie van de eindgebruiker voor bestandssysteembewerkingen</span><span class="sxs-lookup"><span data-stu-id="ffd39-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="ffd39-150">Gebruik deze tooauthenticate met Azure AD voor bestandssysteembewerkingen (maken map, uploadbestand, enz.).</span><span class="sxs-lookup"><span data-stu-id="ffd39-150">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="ffd39-151">Gebruik dit met een bestaande **native clienttoepassing** van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffd39-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="ffd39-152">Hello Azure AD-gebruiker die u referenties opgeven die moet niet worden geconfigureerd voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="ffd39-152">hello Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="ffd39-153">Service-naar-serviceverificatie met clientgeheim voor accountbeheer</span><span class="sxs-lookup"><span data-stu-id="ffd39-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="ffd39-154">Gebruik deze tooauthenticate met Azure AD voor accountbeheerbewerkingen (maken/verwijderen Data Lake Store-account, enz.).</span><span class="sxs-lookup"><span data-stu-id="ffd39-154">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="ffd39-155">Hallo volgende codefragment kan worden gebruikt tooauthenticate uw toepassing niet-interactief, met behulp van het clientgeheim Hallo voor een toepassing / service-principal.</span><span class="sxs-lookup"><span data-stu-id="ffd39-155">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="ffd39-156">Gebruik dit met een bestaande Azure AD-toepassing voor webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="ffd39-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="ffd39-157">Service-naar-serviceverificatie met clientgeheim voor bestandssysteembewerkingen</span><span class="sxs-lookup"><span data-stu-id="ffd39-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="ffd39-158">Gebruik deze tooauthenticate met Azure AD voor bestandssysteembewerkingen (maken map, uploadbestand, enz.).</span><span class="sxs-lookup"><span data-stu-id="ffd39-158">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="ffd39-159">Hallo volgende codefragment kan worden gebruikt tooauthenticate uw toepassing niet-interactief, met behulp van het clientgeheim Hallo voor een toepassing / service-principal.</span><span class="sxs-lookup"><span data-stu-id="ffd39-159">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="ffd39-160">Gebruik dit met een bestaande Azure AD-toepassing voor webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="ffd39-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="ffd39-161">Multi-Factor Authentication voor accountbeheer</span><span class="sxs-lookup"><span data-stu-id="ffd39-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="ffd39-162">Gebruik deze tooauthenticate met Azure AD voor accountbeheerbewerkingen (maken/verwijderen Data Lake Store-account, enz.).</span><span class="sxs-lookup"><span data-stu-id="ffd39-162">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="ffd39-163">Hallo volgende fragment mag tooauthenticate uw toepassing met multi-factor authentication gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ffd39-163">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="ffd39-164">Gebruik dit met een bestaande Azure AD-toepassing voor webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="ffd39-164">Use this with an existing Azure AD "Web App" application.</span></span>

    authority_host_url = "https://login.microsoftonline.com"
    tenant = "FILL-IN-HERE"
    authority_url = authority_host_url + '/' + tenant
    client_id = 'FILL-IN-HERE'
    redirect = 'urn:ietf:wg:oauth:2.0:oob'
    RESOURCE = 'https://management.core.windows.net/'
    
    context = adal.AuthenticationContext(authority_url)
    code = context.acquire_user_code(RESOURCE, client_id)
    print(code['message'])
    mgmt_token = context.acquire_token_with_device_code(RESOURCE, code, client_id)
    credentials = AADTokenCredentials(mgmt_token, client_id)

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="ffd39-165">Multi-Factor Authentication voor bestandssysteembeheer</span><span class="sxs-lookup"><span data-stu-id="ffd39-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="ffd39-166">Gebruik deze tooauthenticate met Azure AD voor bestandssysteembewerkingen (maken map, uploadbestand, enz.).</span><span class="sxs-lookup"><span data-stu-id="ffd39-166">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="ffd39-167">Hallo volgende fragment mag tooauthenticate uw toepassing met multi-factor authentication gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ffd39-167">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="ffd39-168">Gebruik dit met een bestaande Azure AD-toepassing voor webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="ffd39-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="ffd39-169">Een Azure-resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="ffd39-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="ffd39-170">Hallo code codefragment toocreate een Azure-resourcegroep volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ffd39-170">Use hello following code snippet toocreate an Azure Resource Group:</span></span>

    ## Declare variables
    subscriptionId= 'FILL-IN-HERE'
    resourceGroup = 'FILL-IN-HERE'
    location = 'eastus2'
    
    ## Create management client object
    resourceClient = ResourceManagementClient(
        credentials,
        subscriptionId
    )
    
    ## Create an Azure Resource Group
    resourceClient.resource_groups.create_or_update(
        resourceGroup,
        ResourceGroup(
            location=location
        )
    )

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="ffd39-171">Clients en een Data Lake Store-account maken</span><span class="sxs-lookup"><span data-stu-id="ffd39-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="ffd39-172">Hallo codefragment eerst na maakt Hallo Data Lake Store-account client.</span><span class="sxs-lookup"><span data-stu-id="ffd39-172">hello following snippet first creates hello Data Lake Store account client.</span></span> <span data-ttu-id="ffd39-173">Hallo client object toocreate een Data Lake Store-account wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ffd39-173">It uses hello client object toocreate a Data Lake Store account.</span></span> <span data-ttu-id="ffd39-174">Ten slotte maakt Hallo-codefragment een client-object van het bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="ffd39-174">Finally, hello snippet creates a filesystem client object.</span></span>

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'

    ## Create management client object
    adlsAcctClient = DataLakeStoreAccountManagementClient(credentials, subscriptionId)

    ## Create a Data Lake Store account
    adlsAcctResult = adlsAcctClient.account.create(
        resourceGroup,
        adlsAccountName,
        DataLakeStoreAccount(
            location=location
        )
    ).wait()

    ## Create a filesystem client object
    adlsFileSystemClient = core.AzureDLFileSystem(token, store_name=adlsAccountName)

## <a name="list-hello-data-lake-store-accounts"></a><span data-ttu-id="ffd39-175">Lijst Hallo Data Lake Store-accounts</span><span class="sxs-lookup"><span data-stu-id="ffd39-175">List hello Data Lake Store accounts</span></span>

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="ffd39-176">Een map maken</span><span class="sxs-lookup"><span data-stu-id="ffd39-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="ffd39-177">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="ffd39-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="ffd39-178">Bestand downloaden</span><span class="sxs-lookup"><span data-stu-id="ffd39-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="ffd39-179">Een map verwijderen</span><span class="sxs-lookup"><span data-stu-id="ffd39-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="ffd39-180">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ffd39-180">See also</span></span>

- [<span data-ttu-id="ffd39-181">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="ffd39-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="ffd39-182">Azure Data Lake Analytics gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ffd39-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="ffd39-183">Azure HDInsight gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ffd39-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="ffd39-184">Naslaginformatie over Data Lake Store .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ffd39-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="ffd39-185">Naslaginformatie over Data Lake Store REST</span><span class="sxs-lookup"><span data-stu-id="ffd39-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
