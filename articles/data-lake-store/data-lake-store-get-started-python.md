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
# <a name="get-started-with-azure-data-lake-store-using-python"></a>Aan de slag met Azure Data Lake Store met Python

> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET-SDK](data-lake-store-get-started-net-sdk.md)
> * [Java-SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Informatie over hoe toouse Hallo Python SDK voor Azure en Azure Data Lake Store tooperform basisbewerkingen, zoals maken van mappen, uploaden en downloaden van gegevensbestanden, enzovoort. Zie [Azure Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake.

## <a name="prerequisites"></a>Vereisten

* **Python**. U kunt Python [hier](https://www.python.org/downloads/) downloaden. In dit artikel wordt Python 3.5.2 gebruikt.

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).

* **Een Azure Active Directory-toepassing maken**. U hello Azure AD-toepassing tooauthenticate Hallo Data Lake Store-toepassing gebruiken met Azure AD. Er zijn verschillende benaderingen tooauthenticate met Azure AD zijn **eindgebruiker verificatie** of **authentication service-naar-serviceconnector**. Voor instructies en meer informatie over het tooauthenticate, Zie [eindgebruiker verificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [authentication Service-naar-serviceconnector](data-lake-store-authenticate-using-active-directory.md).

## <a name="install-hello-modules"></a>Hallo-modules installeren

toowork met Data Lake Store met behulp van Python, moet u drie tooinstall-modules.

* Hallo `azure-mgmt-resource` module. Deze bevat Azure-modules voor Active Directory enz.
* Hallo `azure-mgmt-datalake-store` module. Dit omvat beheerbewerkingen voor hello Azure Data Lake Store-account. Zie [Naslaginformatie over Azure Data Lake Store-beheermodule](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html) voor meer informatie over deze module.
* Hallo `azure-datalake-store` module. Dit omvat bestandssysteembewerkingen van hello Azure Data Lake Store. Zie [Naslaginformatie over Azure Data Lake Store-bestandssysteemmodule](http://azure-datalake-store.readthedocs.io/en/latest/) voor meer informatie over deze module.

Gebruik Hallo opdrachten tooinstall Hallo modules te volgen.

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a>Een nieuwe Python-toepassing maken

1. In Hallo IDE van uw keuze, bijvoorbeeld een nieuwe Python-toepassing maken **mysample.py**.

2. Hallo volgende regels tooimport Hallo vereist modules toevoegen

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

3. Sla de wijzigingen toomysample.py.

## <a name="authentication"></a>Authentication

In deze sectie bespreken we Hallo verschillende manieren tooauthenticate met Azure AD. Hallo opties zijn beschikbaar:

* Verificatie van de eindgebruiker
* Verificatie van service-tot-service
* Multi-Factor Authentication

U moet deze verificatieopties gebruiken voor zowel accountbeheer- als bestandssysteembeheermodules.

### <a name="end-user-authentication-for-account-management"></a>Verificatie van de eindgebruiker voor accountbeheer

Gebruik deze tooauthenticate met Azure AD voor accountbeheerbewerkingen (maken/verwijderen Data Lake Store-account, enz.). U moet een gebruikersnaam en wachtwoord voor een Azure AD-gebruiker opgeven. Houd er rekening mee dat Hallo-gebruiker moet niet worden geconfigureerd voor multi-factor authentication.

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a>Verificatie van de eindgebruiker voor bestandssysteembewerkingen

Gebruik deze tooauthenticate met Azure AD voor bestandssysteembewerkingen (maken map, uploadbestand, enz.). Gebruik dit met een bestaande **native clienttoepassing** van Azure AD. Hello Azure AD-gebruiker die u referenties opgeven die moet niet worden geconfigureerd voor multi-factor authentication.

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a>Service-naar-serviceverificatie met clientgeheim voor accountbeheer

Gebruik deze tooauthenticate met Azure AD voor accountbeheerbewerkingen (maken/verwijderen Data Lake Store-account, enz.). Hallo volgende codefragment kan worden gebruikt tooauthenticate uw toepassing niet-interactief, met behulp van het clientgeheim Hallo voor een toepassing / service-principal. Gebruik dit met een bestaande Azure AD-toepassing voor webtoepassingen.

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a>Service-naar-serviceverificatie met clientgeheim voor bestandssysteembewerkingen

Gebruik deze tooauthenticate met Azure AD voor bestandssysteembewerkingen (maken map, uploadbestand, enz.). Hallo volgende codefragment kan worden gebruikt tooauthenticate uw toepassing niet-interactief, met behulp van het clientgeheim Hallo voor een toepassing / service-principal. Gebruik dit met een bestaande Azure AD-toepassing voor webtoepassingen.

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a>Multi-Factor Authentication voor accountbeheer

Gebruik deze tooauthenticate met Azure AD voor accountbeheerbewerkingen (maken/verwijderen Data Lake Store-account, enz.). Hallo volgende fragment mag tooauthenticate uw toepassing met multi-factor authentication gebruikt. Gebruik dit met een bestaande Azure AD-toepassing voor webtoepassingen.

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

### <a name="multi-factor-authentication-for-filesystem-management"></a>Multi-Factor Authentication voor bestandssysteembeheer

Gebruik deze tooauthenticate met Azure AD voor bestandssysteembewerkingen (maken map, uploadbestand, enz.). Hallo volgende fragment mag tooauthenticate uw toepassing met multi-factor authentication gebruikt. Gebruik dit met een bestaande Azure AD-toepassing voor webtoepassingen.

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a>Een Azure-resourcegroep maken

Hallo code codefragment toocreate een Azure-resourcegroep volgende gebruiken:

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

## <a name="create-clients-and-data-lake-store-account"></a>Clients en een Data Lake Store-account maken

Hallo codefragment eerst na maakt Hallo Data Lake Store-account client. Hallo client object toocreate een Data Lake Store-account wordt gebruikt. Ten slotte maakt Hallo-codefragment een client-object van het bestandssysteem.

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

## <a name="list-hello-data-lake-store-accounts"></a>Lijst Hallo Data Lake Store-accounts

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a>Een map maken

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a>Bestand uploaden


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a>Bestand downloaden

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a>Een map verwijderen

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a>Zie ook

- [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)
- [Azure Data Lake Analytics gebruiken met Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [Azure HDInsight gebruiken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
- [Naslaginformatie over Data Lake Store .NET SDK](https://msdn.microsoft.com/library/mt581387.aspx)
- [Naslaginformatie over Data Lake Store REST](https://msdn.microsoft.com/library/mt693424.aspx)
