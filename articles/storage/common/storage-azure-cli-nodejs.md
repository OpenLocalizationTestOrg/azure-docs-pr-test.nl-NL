---
title: aaaUsing hello Azure CLI 1.0 met Azure Storage | Microsoft Docs
description: Informatie over hoe toouse hello Azure-opdrachtregelinterface (Azure CLI) 1.0 met Azure Storage toocreate en storage-accounts beheren en werken met Azure BLOB's en bestanden. Hello Azure CLI is een hulpprogramma voor meerdere platforms
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 25e459403dde631741403c8722ed07beafac35c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a>Hallo 1.0 van Azure CLI gebruiken met Azure Storage

## <a name="overview"></a>Overzicht

Hello Azure CLI biedt een set van open-source platformoverschrijdende opdrachten voor het werken met hello Azure-Platform. Het biedt veel van dezelfde functionaliteit in Hallo gevonden Hallo [Azure-portal](https://portal.azure.com) ook zo uitgebreid data access-functionaliteit.

In deze handleiding wordt besproken hoe toouse [Azure-opdrachtregelinterface (Azure CLI)](../../cli-install-nodejs.md) tooperform tal van ontwikkeling en het beheer van taken met Azure Storage. Het is raadzaam dat u downloaden en installeren of upgraden van toohello nieuwste Azure CLI voordat u deze handleiding.

Deze handleiding wordt ervan uitgegaan dat u Hallo basisconcepten van Azure Storage begrijpt. Hallo handleiding biedt een aantal scripts toodemonstrate Hallo gebruik van hello Azure CLI met Azure Storage. Niet zeker tooupdate Hallo scriptvariabelen op basis van uw configuratie voordat elk script wordt uitgevoerd.

> [!NOTE]
> Hallo handleiding bevat hello Azure CLI opdracht en het script voorbeelden voor klassieke opslagaccounts. Zie [Using hello Azure CLI voor Mac, Linux en Windows met Azure Resource Management](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) voor Azure CLI-opdrachten voor Resource Manager-opslagaccounts.
>
>

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a>Aan de slag met Azure Storage en Azure CLI Hallo in vijf minuten
Deze handleiding gebruikt Ubuntu voor voorbeelden, maar andere platforms OS moeten op dezelfde manier worden uitgevoerd.

**Nieuwe tooAzure:** ophalen van een Microsoft Azure-abonnement en een Microsoft-account die is gekoppeld aan dat abonnement. Zie voor informatie over Azure-Aankoopopties, [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/), [kopen opties](https://azure.microsoft.com/pricing/purchase-options/), en [lid biedt](https://azure.microsoft.com/pricing/member-offers/) (voor leden van MSDN, Microsoft Partner Network BizSpark en andere Microsoft-programma's).

Zie [beheerdersrollen toewijzen in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) voor meer informatie over Azure-abonnementen.

**Na het maken van een Microsoft Azure-abonnement en -account:**

1. Download en installeer Azure CLI Hallo instructies te volgen die worden beschreven in Hallo [installeren hello Azure CLI](../../cli-install-nodejs.md).
2. Zodra hello Azure CLI is geïnstalleerd, kunt u zich kunt toouse hello azure opdracht vanaf de opdrachtregel-interface (Bash, Terminal-opdrachtprompt) tooaccess hello Azure CLI-opdrachten. Type Hallo _azure_ opdracht en u ziet Hallo na uitvoer.

    ![Azure opdrachtuitvoer](./media/storage-azure-cli/azure_command.png)   
3. Typ in het Hallo-opdrachtregelinterface `azure storage` toolist uit alle azure-opslag-opdrachten Hallo en krijgt u een eerste indruk Hallo functionaliteiten Hallo Azure CLI wordt verstrekt. U kunt de naam van de opdracht met typen **-h** parameter (bijvoorbeeld `azure storage share create -h`) toosee details van de opdrachtsyntaxis.
4. Nu geven we u een eenvoudig script waarin basic Azure CLI-opdrachten tooaccess Azure Storage. Hallo script eerst vragen u de twee variabelen tooset voor uw opslagaccount en de sleutel. Hallo-script wordt vervolgens een nieuwe container in deze nieuwe opslagaccount maken en uploaden van een bestaande installatiekopie-bestand (blob) toothat container. Nadat het Hallo-script geeft een lijst van alle blobs in de container, zal deze Hallo installatiekopie bestand toohello doelmap dat op de lokale computer Hallo bestaat downloaden.

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. Open uw voorkeur teksteditor (vim voor voorbeeld) in uw lokale computer. Typ Hallo hierboven script in een teksteditor.
6. U moet nu tooupdate Hallo scriptvariabelen op basis van uw configuratie-instellingen.

   * **< Storage_account_name >** Hallo naam die in het Hallo-script gebruiken of voer een nieuwe naam voor uw opslagaccount. **Belangrijk:** Hallo-naam van Hallo opslagaccount moet uniek zijn in Azure. Er moet een kleine letter, te!
   * **< storage_account_key >** Hallo toegangssleutel van uw opslagaccount.
   * **< Container_name >** Hallo naam die in het Hallo-script gebruiken of voer een nieuwe naam voor de container.
   * **< Image_to_upload >** Voer een pad tooa afbeelding op uw lokale computer, zoals: ' ~ / images/HelloWorld.png '.
   * **< Destination_folder >** Enter een pad tooa lokale directory toostore bestanden gedownload van Azure Storage, zoals: '~/downloadImages'.
7. Nadat u Hallo nodig variabelen in vim hebt bijgewerkt, drukt u op toetsencombinaties `ESC`, `:`, `wq!` toosave Hallo script.
8. toorun dit script gewoon type Hallo Scriptbestandsnaam in Hallo bash-console. Nadat u dit script wordt uitgevoerd, moet u een lokale doelmap met Hallo gedownload bestand hebben. Hallo volgende schermafbeelding ziet u een voorbeeld van uitvoer:

Nadat het Hallo-script wordt uitgevoerd, moet u een lokale doelmap met Hallo gedownload bestand hebben.

## <a name="manage-storage-accounts-with-hello-azure-cli"></a>Storage-accounts met hello Azure CLI beheren
### <a name="connect-tooyour-azure-subscription"></a>Verbinding maken met tooyour Azure-abonnement
Hoewel de meeste van Hallo opslag opdrachten zonder een Azure-abonnement werkt, wordt aangeraden u tooconnect tooyour abonnement hello Azure CLI. tooconfigure hello Azure CLI toowork bij uw abonnement, Hallo stappen in [tooan Azure-abonnement verbinden van hello Azure CLI](../../xplat-cli-connect.md).

### <a name="create-a-new-storage-account"></a>Een nieuw opslagaccount maken
toouse Azure-opslag, moet u een opslagaccount. Nadat u uw computer tooconnect tooyour-abonnement hebt geconfigureerd, kunt u een nieuwe Azure storage-account maken.

```azurecli
azure storage account create <account_name>
```

Hallo-naam van uw opslagaccount moet tussen 3 en 24 tekens lang zijn en alleen cijfers en kleine letters gebruiken.

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a>Een Azure storage-standaardaccount in omgevingsvariabelen instellen
U kunt meerdere opslagaccounts hebben in uw abonnement. U kunt kiezen één van beide en deze eigenschap instellen in Hallo omgevingsvariabelen voor alle Hallo-opslag-in Hallo dezelfde opdrachten sessie. Hiermee kunt u toorun hello Azure CLI opslag opdrachten zonder op te geven Hallo storage-account en expliciet sleutel.

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Verbindingsreeks maakt gebruik van een andere manier tooset storage-standaardaccount. Ten eerste Hallo-verbindingsreeks ophalen door de opdracht:

```azurecli
azure storage account connectionstring show <account_name>
```

Kopieer Hallo uitvoer verbindingsreeks en stel deze tooenvironment variabele:

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a>Maken en blobs beheren
Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS. Deze sectie wordt ervan uitgegaan dat u al bekend met concepten voor hello Azure Blob storage bent. Zie voor gedetailleerde informatie [aan de slag met Azure Blob storage met .NET](../blobs/storage-dotnet-how-to-use-blobs.md) en [concepten van Blob-Service](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="create-a-container"></a>Een container maken
Elke blob in Azure-opslag moet zich in een container. U kunt een persoonlijke container met Hallo maken `azure storage container create` opdracht:

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> Er zijn drie niveaus van anonieme toegang voor lezen: **uit**, **Blob**, en **Container**. tooprevent anonieme toegang tot tooblobs, setparameter Hallo machtiging te**uit**. Standaard Hallo nieuwe container privé is en toegankelijk zijn alleen voor de accounteigenaar Hallo. anonieme openbare tooallow lezen toegang tot tooblob bronnen, maar niet toocontainer metagegevens of toohello lijst met blobs in de container hello, stelt u Hallo machtiging parameter te**Blob**. volledige openbare tooallow lezen toegang tot tooblob bronnen, container metagegevens en Hallo lijst met blobs in de container hello, stelt u Hallo machtiging parameter te**Container**. Zie voor meer informatie [anonieme leestoegang toocontainers en blobs beheren](../blobs/storage-manage-access-to-resources.md).
>
>

### <a name="upload-a-blob-into-a-container"></a>Een blob uploaden naar een container
Azure Blob Storage ondersteunt blok-blobs en pagina-blobs. Zie voor meer informatie [blok-Blobs, toevoeg-Blobs en pagina-Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).

tooupload blobs in tooa container, kunt u Hallo `azure storage blob upload`. Standaard uploadt u deze opdracht Hallo lokale bestanden tooa blok-blob. Hallo-type toospecify voor Hallo blob, kunt u Hallo `--blobtype` parameter.

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a>Blobs downloaden uit een container
Hallo volgende voorbeeld laat zien hoe toodownload blobs uit een container.

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a>Blobs kopiëren
U kunt blobs binnen of tussen opslagaccounts en regio's asynchroon kopiëren.

Hallo volgende voorbeeld laat zien hoe toocopy blobs uit één opslag tooanother account. In dit voorbeeld maken we een container waarin blobs openbaar zijn, anoniem toegankelijk.

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

Dit voorbeeld voert een asynchrone kopie. U kunt Hallo status van elke kopieerbewerking bewaken door het uitvoeren van Hallo `azure storage blob copy show` bewerking.

Houd er rekening mee dat Hallo bron-URL opgegeven voor de kopieerbewerking Hallo moet openbaar toegankelijk, of een SAS (shared access signature)-token omvatten.

### <a name="delete-a-blob"></a>Een blob verwijderen
toodelete een blob Hallo onder opdracht gebruiken:

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a>Maken en beheren van bestandsshares
Azure File storage biedt gedeelde opslag voor toepassingen die gebruikmaken van Hallo standaard SMB-protocol. Microsoft Azure virtuele machines en cloud-services, evenals de on-premises toepassingen kunnen bestandsgegevens via gekoppelde shares delen. U kunt bestandsshares en bestandsgegevens via hello Azure CLI kunt beheren. Zie voor meer informatie over Azure File storage [aan de slag met Azure File storage in Windows](../storage-dotnet-how-to-use-files.md) of [hoe toouse Azure File storage met Linux](../storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Een bestandsshare maken
Een Azure-bestandsshare is een SMB-bestandsshare in Azure. Alle mappen en bestanden moeten worden gemaakt in een bestandsshare. Een account kan een onbeperkt aantal shares bevatten en een bestandsshare kan een onbeperkt aantal bestanden van toohello capaciteitslimiet van het opslagaccount Hallo opslaan. Hallo volgende voorbeeld wordt een bestandsshare met de naam **mijnshare**.

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a>Een map maken
Een directory biedt een optionele hiërarchische structuur voor een Azure-bestandsshare. Hallo volgende voorbeeld maakt u een map met de naam **myDir** in Hallo-bestandsshare.

```azurecli
azure storage directory create myshare myDir
```

Opmerking die directorypad kan bestaan uit meerdere niveaus *bijvoorbeeld*, **een / b**. Echter, moet u ervoor zorgen dat alle bovenliggende mappen bestaan. Bijvoorbeeld: voor pad **een / b**, moet u directory **een** vervolgens Maak eerst map **b**.

### <a name="upload-a-local-file-toodirectory"></a>De toodirectory van een lokaal bestand uploaden
Hallo volgende voorbeeld wordt een bestand geüpload vanuit **~/temp/samplefile.txt** toohello **myDir** directory. Hallo-bestandspad bewerken zodat deze tooa geldig bestand op uw lokale machine verwijst:

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

Let op: een bestand in de share Hallo kan up too1 TB groot zijn.

### <a name="list-hello-files-in-hello-share-root-or-directory"></a>Hallo-bestanden in basis Hallo-share of map weergeven
U kunt Hallo bestanden en submappen in de hoofdmap van een share of map met behulp van de volgende opdracht Hallo weergeven:

```azurecli
azure storage file list myshare myDir
```

Houd er rekening mee dat Hallo mapnaam is optioneel voor Hallo aanbieding bewerking. Als u dit weglaat, weergegeven Hallo Hallo inhoud van de hoofdmap Hallo van Hallo share.

### <a name="copy-files"></a>Bestanden kopiëren
Vanaf versie 0.9.8 van Azure CLI, kunt u een bestand tooanother, een bestand tooa blob of een blob tooa-bestand kopiëren. Hieronder ziet u hoe tooperform die deze kopiëren bewerkingen met behulp van de CLI-opdrachten. een nieuwe map toohello toocopy:

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

een map voor blob tooa toocopy:

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a>Volgende stappen

U vindt de Azure CLI 1.0-opdrachtregelprogramma voor het werken met opslagbronnen hier:

* [Azure CLI-opdrachten in de modus Resource Manager](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [Azure CLI-opdrachten in de Azure Service Management-modus](../../cli-install-nodejs.md)

U kunt ook graag tootry Hallo [Azure CLI 2.0](../storage-azure-cli.md), de volgende generatie CLI geschreven in Python, voor gebruik met Hallo Resource Manager-implementatiemodel.
