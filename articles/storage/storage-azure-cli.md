---
title: aaaUsing hello Azure CLI 2.0 met Azure Storage | Microsoft Docs
description: Informatie over hoe toouse hello Azure-opdrachtregelinterface (Azure CLI) 2.0 met Azure Storage toocreate en storage-accounts beheren en werken met Azure BLOB's en bestanden. Hello Azure CLI 2.0 is een cross-platform-hulpprogramma dat is geschreven in Python.
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 38402373dcd87f1ef05471a02353c77d58f1a9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a>Hello Azure CLI 2.0 gebruiken met Azure Storage

Hallo open-source platformoverschrijdende Azure CLI 2.0 biedt een reeks opdrachten voor het werken met hello Azure-platform. Het biedt veel van dezelfde functionaliteit in Hallo gevonden Hallo [Azure-portal](https://portal.azure.com), met inbegrip van toegang tot uitgebreide gegevens.

In deze handleiding wordt uitgelegd hoe u dat toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform verschillende taken die werken met resources in uw Azure Storage-account. U wordt aangeraden dat u downloaden en installeren of upgraden van de meest recente versie toohello Hallo CLI 2.0 voordat u deze handleiding.

Hallo-voorbeelden in Hallo handleiding wordt ervan uitgegaan Hallo gebruik van Hallo Bash-shell op Ubuntu, maar andere platforms op dezelfde manier moeten uitvoeren. 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a>Vereisten
Deze handleiding wordt ervan uitgegaan dat u Hallo basisconcepten van Azure Storage begrijpt. Ook wordt ervan uitgegaan dat u kunnen toosatisfy Hallo-account maken vereisten die bent hieronder zijn opgegeven voor Azure en Hallo Storage-service.

### <a name="accounts"></a>Accounts
* **Azure-account**: als u nog een Azure-abonnement hebt [maken van een gratis Azure-account](https://azure.microsoft.com/free/).
* **Opslagaccount**: zie [Een opslagaccount maken](../storage/storage-create-storage-account.md#create-a-storage-account) in [Over Azure-opslagaccounts](../storage/storage-create-storage-account.md).

### <a name="install-hello-azure-cli-20"></a>Hello Azure CLI 2.0 installeren

Download en installeer hello Azure CLI 2.0 door Hallo aanwijzingen [2.0 voor Azure CLI installeren](/cli/azure/install-az-cli2).

> [!TIP]
> Als u problemen met de installatie Hallo ondervindt, bekijk Hallo [installatie probleemoplossing](/cli/azure/install-az-cli2#installation-troubleshooting) sectie van Hallo artikel en Hallo [installeren probleemoplossing](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) handleiding op GitHub.
>

## <a name="working-with-hello-cli"></a>Werken met Hallo CLI

Zodra u Hallo CLI hebt geïnstalleerd, kunt u Hallo `az` opdracht in de opdrachtregelinterface (Bash, Terminal, opdrachtprompt) tooaccess hello Azure CLI-opdrachten. Type Hallo `az` toosee opdracht een volledige lijst met base Hallo-opdrachten (Hallo volgende voorbeelduitvoer afgekapt):

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

In de opdrachtregelinterface Hallo-opdracht uitvoeren `az storage --help` toolist hello `storage` opdracht subgroepen. Hallo beschrijvingen van Hallo subgroepen bieden een overzicht van Hallo functionaliteit hello die Azure CLI wordt verstrekt voor het werken met uw opslagresources.

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a>Verbinding maken met de Hallo CLI tooyour Azure-abonnement

toowork met Hallo resources in uw Azure-abonnement, moet u zich eerst in tooyour Azure-account met `az login`. Er zijn verschillende manieren die kunt u zich aanmeldt:

* **Interactieve aanmelding**:`az login`
* **Meld u aan met de gebruikersnaam en wachtwoord**:`az login -u johndoe@contoso.com -p VerySecret`
  * Dit werkt niet met Microsoft-accounts of -mailaccounts die gebruikmaken van multi-factor authentication-server.
* **Meld u aan met een service-principal**:`az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`

## <a name="azure-cli-20-sample-script"></a>Azure CLI 2.0-voorbeeldscript

Vervolgens werkt we met een kleine shellscript dat een paar eenvoudige Azure CLI 2.0 opdrachten toointeract met een Azure Storage-resources problemen. Hallo script eerst maakt een nieuwe container in uw opslagaccount en vervolgens een bestaand bestand (als een blob) toothat container uploadt. Deze vervolgens een lijst met alle blobs in Hallo-container en ten slotte downloadt Hallo tooa bestemming op uw lokale computer die u opgeeft.

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

**Configureren en het Hallo-script uitvoeren**

1. Uw favoriete teksteditor openen en vervolgens kopieert en plakt Hallo vóór het script in Hallo-editor.

2. Werk van het script Hallo variabelen tooreflect vervolgens uw configuratie-instellingen. Vervang Hallo waarden zoals opgegeven te volgen:

   * **\<storage_account_name\>**  Hallo-naam van uw opslagaccount.
   * **\<storage_account_key\>**  Hallo primaire of secundaire toegangssleutel voor uw opslagaccount.
   * **\<container_name\>**  naam van een nieuwe container toocreate, zoals "azure-cli-voorbeeld-container" Hallo.
   * **\<blob_name\>**  een naam voor de bestemmings-blob Hallo in Hallo-container.
   * **\<file_to_upload\>**  Hallo pad toosmall bestand op uw lokale computer, zoals ' ~ / images/HelloWorld.png '.
   * **\<destination_file\>**  Hallo bestemmingspad, zoals ' ~ / downloadedImage.png '.

3. Nadat u de benodigde variabelen Hallo hebt bijgewerkt, Hallo script opslaat en sluit de editor af. Hallo volgende stappen wordt ervan uitgegaan dat u hebt uw script genoemd **my_storage_sample.sh**.

4. U markeert Hallo script als uitvoerbare, indien nodig:`chmod +x my_storage_sample.sh`

5. Hallo-script uitvoeren. Bijvoorbeeld in Bash:`./my_storage_sample.sh`

U moet uitvoer vergelijkbare toohello volgende Zie en Hallo  **\<destination_file\>**  u hebt opgegeven in Hallo script moet worden weergegeven op de lokale computer.

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> Hallo voorgaande uitvoer is in **tabel** indeling. U kunt opgeven dat indeling toouse uitvoer door te geven Hallo `--output` argument in de CLI-opdrachten of stel deze globaal met `az configure`.
>

## <a name="manage-storage-accounts"></a>Opslagaccounts beheren

### <a name="create-a-new-storage-account"></a>Een nieuw opslagaccount maken
toouse Azure Storage, moet u een opslagaccount. U kunt een nieuw Azure-opslagaccount maken nadat u uw computer te hebt geconfigureerd[tooyour abonnement verbinding](#connect-to-your-azure-subscription).

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* `--location`[Vereist]: locatie. Bijvoorbeeld "VS-West'.
* `--name`[Vereist]: Hallo opslagaccountnaam. Hallo-naam moet 3 too24 tekens bestaan en gebruik alleen kleine letters alfanumerieke tekens.
* `--resource-group`[Vereist]: naam van resourcegroep.
* `--sku`[Vereist]: Hallo opslagaccount SKU. Toegestane waarden:
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a>Azure storage-standaardaccount omgevingsvariabelen worden ingesteld
U kunt meerdere opslagaccounts in uw Azure-abonnement hebben. tooselect één van deze opdrachten toouse voor alle daaropvolgende opslag, kunt u deze omgevingsvariabelen instellen:

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Er is een andere manier tooset storage-standaardaccount met behulp van een verbindingsreeks. De verbindingsreeks Hallo Hello eerst ophalen `show-connection-string` opdracht:

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

Vervolgens kopiëren Hallo verbindingsreeks uitvoer en stelt u Hallo `AZURE_STORAGE_CONNECTION_STRING` omgevingsvariabele (mogelijk moet u het Hallo-verbindingsreeks tooenclose aanhalingstekens):

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> Alle voorbeelden in Hallo volgende secties in dit artikel wordt ervan uitgegaan dat u hebt ingesteld dat Hallo `AZURE_STORAGE_ACCOUNT` en `AZURE_STORAGE_ACCESS_KEY` omgevingsvariabelen.
>

## <a name="create-and-manage-blobs"></a>Maken en blobs beheren
Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS. Deze sectie wordt ervan uitgegaan dat u al bekend met concepten voor Azure Blob-opslag bent. Zie voor gedetailleerde informatie [aan de slag met Azure Blob storage met .NET](storage-dotnet-how-to-use-blobs.md) en [concepten van Blob-Service](/rest/api/storageservices/blob-service-concepts).

### <a name="create-a-container"></a>Een container maken
Elke blob in Azure-opslag moet zich in een container. U kunt een container maken met behulp van Hallo `az storage container create` opdracht:

```azurecli
az storage container create --name <container_name>
```

U kunt een van drie niveaus van leestoegang voor een nieuwe container instellen door te geven Hallo optionele `--public-access` argument:

* `off`(standaard): gegevens van de Container is eigenaar van de persoonlijke toohello-account.
* `blob`: Openbare leestoegang voor blobs.
* `container`: Toegang tot de volledige container toohello openbare lees- en lijst.

Zie voor meer informatie [anonieme leestoegang toocontainers en blobs beheren](storage-manage-access-to-resources.md).

### <a name="upload-a-blob-tooa-container"></a>Een blob-container tooa uploaden
Azure Blob storage ondersteunt blok, toevoegen en pagina-blobs. Het uploaden van blobs tooa container via Hallo `blob upload` opdracht:

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 Standaard Hallo `blob upload` opdracht uploadt *.vhd bestanden toopage blobs of anderszins blok-blobs. toospecify een ander type wanneer u een blob uploaden, kunt u Hallo `--type` argument--toegestane waarden zijn `append`, `block`, en `page`.

 Zie voor meer informatie over Hallo andere blob-typen [blok-Blobs, toevoeg-Blobs en pagina-Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).


### <a name="download-a-blob-from-a-container"></a>Een blob downloaden uit een container
In dit voorbeeld laat zien hoe toodownload een blob uit een container:

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a>Lijst Hallo blobs in een container

Hallo blobs in een container met Hallo lijst [lijst met blob storage az](/cli/azure/storage/blob#list) opdracht.

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a>Blobs kopiëren
U kunt blobs binnen of tussen opslagaccounts en regio's asynchroon kopiëren.

Hallo volgende voorbeeld laat zien hoe toocopy blobs uit één opslag tooanother account. We eerst een container maken in Hallo bron storage-account, openbare leestoegang voor de blobs opgeven. Vervolgens uploaden we een bestandscontainer toohello en ten slotte kopie Hallo blob uit die container naar een container in Hallo doelopslagaccount.

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

Hallo doelcontainer moet Hallo hierboven voorbeeld, al aanwezig in Hallo doelopslagaccount voor Hallo kopie bewerking toosucceed. Bovendien Hallo bron-blob opgegeven in Hallo `--source-uri` argument moet een shared access signature (SAS)-token Neem of openbaar toegankelijk zijn, zoals in dit voorbeeld.

### <a name="delete-a-blob"></a>Een blob verwijderen
een blob toodelete gebruiken Hallo `blob delete` opdracht:

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a>Maken en beheren van bestandsshares
Azure File storage biedt gedeelde opslag voor toepassingen met behulp van Hallo Server Message Block (SMB)-protocol. Microsoft Azure virtuele machines en cloud-services, evenals de on-premises toepassingen kunnen bestandsgegevens via gekoppelde shares delen. U kunt bestandsshares en bestandsgegevens via hello Azure CLI kunt beheren. Zie voor meer informatie over Azure File storage [aan de slag met Azure File storage in Windows](storage-dotnet-how-to-use-files.md) of [hoe toouse Azure File storage met Linux](storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Een bestandsshare maken
Een Azure-bestandsshare is een SMB-bestandsshare in Azure. Alle mappen en bestanden moeten worden gemaakt in een bestandsshare. Een account kan een onbeperkt aantal shares bevatten en een bestandsshare kan een onbeperkt aantal bestanden van toohello capaciteitslimiet van het opslagaccount Hallo opslaan. Hallo volgende voorbeeld wordt een bestandsshare met de naam **mijnshare**.

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a>Een map maken
Een directory biedt een hiërarchische structuur in een Azure-bestandsshare. Hallo volgende voorbeeld maakt u een map met de naam **myDir** in Hallo-bestandsshare.

```azurecli
az storage directory create --name myDir --share-name myshare
```

Een pad kan bijvoorbeeld meerdere niveaus bevatten **dir1/dir2**. Echter, moet u ervoor zorgen dat alle bovenliggende mappen bestaan voordat u een submap maakt. Bijvoorbeeld: voor pad **dir1/dir2**, moet u eerst directory maken **dir1**, maak vervolgens de directory **dir2**.

### <a name="upload-a-local-file-tooa-share"></a>Uploaden van een lokale tooa bestandsshare
Hallo volgende voorbeeld wordt een bestand geüpload vanuit **~/temp/samplefile.txt** tooroot Hallo **mijnshare** bestandsshare. Hallo `--source` geeft Hallo bestaande lokale bestand tooupload argument.

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

Net als bij het maken van de directory, kunt u een mappad binnen Hallo share tooupload Hallo bestand tooan bestaande map in Hallo share opgeven:

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

Een bestand in de share Hallo kan up too1 TB groot zijn.

### <a name="list-hello-files-in-a-share"></a>Hallo-bestanden weergeven in een share
U kunt bestanden en mappen in een share weergeven met behulp van Hallo `az storage file list` opdracht:

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a>Bestanden kopiëren      
U kunt een bestand tooanother, een bestand tooa blob of een blob tooa-bestand kopiëren. Bijvoorbeeld, een map in een andere share tooa toocopy:        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a>Volgende stappen
Hier volgen enkele aanvullende resources voor meer informatie over het werken met hello Azure CLI 2.0.

* [Aan de slag met Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Azure CLI 2.0-opdrachtenreferentie](/cli/azure)
* [Azure CLI 2.0 op GitHub](https://github.com/Azure/azure-cli)
