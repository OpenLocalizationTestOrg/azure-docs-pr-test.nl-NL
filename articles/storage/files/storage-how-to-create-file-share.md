---
title: aaaHow toocreate een Azure-bestandsshare | Microsoft Docs
description: Hoe toocreate een Azure-bestandsshare in Azure File storage met hello Azure-portal, PowerShell en hello Azure CLI.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 816694e411a993dae881816fc62173e2b7afe990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a>Een bestandsshare maken in Azure File Storage
U kunt Azure bestandsshares maken met [Azure-portal](https://portal.azure.com/), Azure PowerShell-cmdlets Storage hello, Hallo clientbibliotheken van Azure Storage of Hallo REST-API van Azure Storage. In deze zelfstudie leert u het:
* [Hoe toocreate een Azure-bestand delen met behulp van hello Azure-portal](#Create file share through hello Portal)
* [Hoe toocreate een Azure-bestandsshare met behulp van Powershell](#Create file share using PowerShell)
* [Hoe toocreate een Azure-bestandsshare met CLI](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a>Vereisten
toocreate een Azure-bestandsshare, kunt u een opslagaccount dat al bestaat, of [maken van een nieuwe Azure-opslagaccount](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json). een bestandsshare in Azure met PowerShell toocreate, moet u Hallo accountsleutel en de naam van uw opslagaccount... U moet de sleutel Opslagaccount als u van plan toouse Powershell of CLI bent.

## <a name="create-file-share-through-hello-portal"></a>Bestandsshare via Hallo Portal maken
1. **Blade-Account in Azure Portal gaat tooStorage**:    
    ![Blade Opslagaccount](./media/storage-how-to-create-file-share/create-file-share-portal1.png)

2. **Klik op de knop Bestandsshare toevoegen**:    
    ![Klik op Hallo file share knop toevoegen](./media/storage-how-to-create-file-share/create-file-share-portal2.png)

3. **Geef de naam en een quotum op. Het quotum heeft momenteel een maximum van 5 TB**:    
    ![Geef een naam en een gewenste quotum voor de nieuwe bestandsshare Hallo](./media/storage-how-to-create-file-share/create-file-share-portal3.png)

4. **Bekijk uw nieuwe bestandsshare**: ![Bekijk uw nieuwe bestandsshare](./media/storage-how-to-create-file-share/create-file-share-portal4.png)

5. **Upload een bestand**: ![Upload een bestand](./media/storage-how-to-create-file-share/create-file-share-portal5.png)

6. **Blader naar de bestandsshare en beheer uw mappen en bestanden**: ![Blader naar de bestandsshare](./media/storage-how-to-create-file-share/create-file-share-portal6.png)


## <a name="create-file-share-through-powershell"></a>Een bestandsshare via de PowerShell maken
tooprepare toouse PowerShell, download en installeer hello Azure PowerShell-cmdlets. Zie [hoe tooinstall en configureren van Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) installeren voor Hallo installatiepunt en de installatie-instructies.

> [!Note]  
> Het verdient aanbeveling dat u downloaden en installeren of upgraden van de meest recente Azure PowerShell-module toohello.

1. **Een context maken voor uw opslagaccount en de sleutel** Hallo context Hallo naam en het account opslagaccountsleutel ingekapseld. Voor instructies voor het kopiëren van de accountsleutel uit [Azure Portal](https://portal.azure.com/) raadpleegt u [Opslagtoegangssleutels bekijken en kopiëren](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. **Maak een nieuwe bestandsshare**:    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> Hallo-naam van de bestandsshare moet alleen kleine letters bevatten. Zie [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Shares, mappen, bestanden en metagegevens een naam geven en hiernaar verwijzen) voor meer informatie over de naamgeving van bestandsshares en bestanden.

## <a name="create-file-share-through-command-line-interface-cli"></a>Een bestandsshare via de opdrachtregelinterface (CLI) maken
1. **tooprepare toouse een opdrachtregelinterface (CLI), download en installeer hello Azure CLI.**  
    Zie [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) (Azure CLI 2.0 installeren) en [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) (Aan de slag met Azure CLI 2.0).

2. **Maak een verbinding tekenreeks toohello opslagaccount waar u toocreate Hallo share.**  
    Vervang ```<storage-account>``` en ```<resource_group>``` met uw account en de bron opslaggroep in Hallo voorbeeld te volgen.

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. **Bestandsshare maken**
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a>Volgende stappen
* [Bestandsshare verbinden en koppelen - Windows](storage-how-to-use-files-windows.md)
* [Bestandsshare verbinden en koppelen - Linux](../storage-how-to-use-files-linux.md)
* [Bestandsshare verbinden en koppelen - Mac OS](storage-how-to-use-files-mac.md)

Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.

* [Veelgestelde vragen](../storage-files-faq.md)
* [Problemen oplossen in Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Problemen oplossen in Linux](storage-troubleshoot-linux-file-connection-problems.md)   